# TDD-RIPER5 Integration Design Document

## 背景和问题陈述

### 核心问题
当前 RIPER5 的 Ω₄ Exec Agent 执行结果不稳定，主要问题：
- **一次性实现幻想**：复杂功能很难"exactly"实现
- **缺乏验证循环**：没有测试反馈机制，不知道对错  
- **错误级联**：一个错误导致整个流程中断
- **质量漂移**：没有重构阶段，代码质量持续衰减

### 解决思路
将TDD的Red-Green-Refactor精髓融入RIPER5，用RGR迭代循环替换线性执行，通过QA/DE角色协作提升执行稳定性。

## 设计原则和约束

### 确定的设计原则
1. **失败即终止**：QA/DE返回结果=成功，出现异常=终止程序，不做复杂回滚
2. **单线程执行**：串行RGR循环，需要并行处理另开CC终端
3. **全面RGR化**：AI参与的任务都要流程验证，能测试的都测试
4. **不考虑兼容**：直接升级现有系统，专注核心价值
5. **质量优先**：用执行时间换取质量，避免后期返工

### 范式保持
- 保持RIPER5的符号化简洁性
- 维持σ₁-σ₆内存协议体系
- 保留严格的模式转换控制

## 总体架构设计

### 核心改造：Ω₄ → Ω₄ᵀ

```
原来的Ω₄: 线性执行清单 → 经常失败
改造后的Ω₄ᵀ: FOREACH σ₂.tdd_cycles[i] { ℜ→ℜᴳ→ℜᶠ }
```

### 状态流转
```
Ω₁→Ω₂→Ω₃→Ω₄ᵀ[ℜ→ℜᴳ→ℜᶠ]*→Ω₅
其中: Ω₄ᵀ[ℜ→ℜᴳ→ℜᶠ]* = 多个TDD循环的迭代
```

### 角色重新定义
```
Agent-TDD-QA ↔ Ω₄ᴿ + Ω₄ᶠᵗᵉˢᵗ (RED相位 + 测试重构)
Agent-TDD-DE ↔ Ω₄ᴳ + Ω₄ᶠⁱᵐᵖˡ (GREEN相位 + 实现重构)  
Agent-Plan   ↔ Ω₃ (增强：生成TDD cycles而非线性清单)
```

## 符号化协议设计

### 核心符号扩展
```
# 新增符号
Ω₄ᵀ: TDD-Enhanced Execution Mode
ℜ→ℜᴳ→ℜᶠ: Complete TDD cycle (Red→Green→Refactor)
QA∨DE: Role alternation within Ω₄ᵀ
⟲[method]: Cycle iteration for specific method

# 子相位符号
Ω₄ᴿ: RED phase (QA writes failing tests)  
Ω₄ᴳ: GREEN phase (DE minimal implementation)
Ω₄ᶠᵗᵉˢᵗ: Refactor phase for test code
Ω₄ᶠⁱᵐᵖˡ: Refactor phase for implementation code
```

### 执行流程符号化
```
Ω₄ᵀ.cycle_execution:
FOREACH σ₂.tdd_cycles[i]:
  ├─ UPDATE σ₄.STATE(current_cycle=i, phase="red")
  ├─ ℜ: QA∨Agent(σ₂.tdd_cycles[i], σ₄.context)
  ├─ UPDATE σ₄.STATE(phase="green")
  ├─ ℜᴳ: DE∨Agent(σ₂.tdd_cycles[i], σ₄.context) 
  ├─ UPDATE σ₄.STATE(phase="refactor")
  ├─ ℜᶠ: {
  │   ├─ QA∨Ω₄ᶠᵗᵉˢᵗ(current_cycle, Ψ_quality_rules)
  │   ├─ DE∨Ω₄ᶠⁱᵐᵖˡ(current_cycle, Ψ_quality_rules)  
  │   └─ 协作∨✓(test_suite + code_review)
  │   }
  └─ UPDATE σ₅.progress[i] = ✓
```

## 三个关键组件设计

### 1. Plan Agent (Ω₃) 增强

**核心转变**：从线性checklist → 循环式TDD规划

```
# 原来的Ω₃输出
σ₂.implementation_plan = [
  □ 1. /path/file.ext: function()
  □ 2. /path/other.ext: class  
]

# TDD增强后的Ω₃输出  
σ₂.tdd_cycles = [
  Phase0: 创建最小接口定义
  □ TDD₁: Interface.MethodA() → ℜ→ℜᴳ→ℜᶠ
  □ TDD₂: Interface.MethodB() → ℜ→ℜᴳ→ℜᶠ
  □ TDD₃: AnotherInterface.MethodC() → ℜ→ℜᴳ→ℜᶠ
]
```

**Plan Agent需要具备**：
- 接口级分解能力（而非文件级）
- 为每个方法规划完整RGR流程
- 生成可追溯的plan_step引用

### 2. 主调度器 (claude.md) 核心逻辑

**关键调度协议**：
```
主调度器 → 子Agent传递协议:
{
  plan_step: σ₂.tdd_cycles[i],            // 对应memory-bank中的具体计划
  quality_rules: @agent-tdd-*.md#rules,   // 引用具体质量规则
  context: σ₄.current_context,            // 当前上下文
  cycle_phase: σ₄.STATE.tdd_phase         // RGR相位标识
}
```

**严格执行流程**：
- 每次调用子代理都传递完整上下文
- 子代理必须先分析上下文再开始工作  
- 严格控制目标文件范围，防止偏离
- 失败即终止，不允许跳过或回退

### 3. QA/DE 子代理角色边界

**严格分工**：
```
QA∨Agent(Ω₄ᴿ + Ω₄ᶠᵗᵉˢᵗ):
✓ 写失败测试、重构测试代码、测试覆盖率检查
✗ 绝不触碰业务实现代码

DE∨Agent(Ω₄ᴳ + Ω₄ᶠⁱᵐᵖˡ):  
✓ 最小实现通过测试、重构业务代码、性能优化
✗ 绝不修改测试代码
```

**重构阶段协作流程**：
```
ℜᶠ.flow: QA∨ℜᶠᵗᵉˢᵗ → DE∨ℜᶠⁱᵐᵖˡ → 协作∨✓ → next_cycle

协作∨✓.sequence:
├─ ∀tests_pass: 运行完整测试套件
├─ code_review: QA↔DE 交叉审查  
├─ interface_check: 接口设计一致性
└─ commit_ready: 质量达标，进入下一循环
```

## 实施

## 信息存储架构

### 分层存储策略

**第一层：核心符号协议** (扩展 claude.md)
```
## TDD Protocol Extension  
Ω₄ᵀ: TDD-Enhanced Execution
ℜ→ᴳ→ℜᶠ: Complete TDD cycle
QA∨DE: Role alternation
```

**第二层：Agent具体指令** (新建文件)
```
agent-tdd-qa.md:
- 测试编写规范和失败测试策略
- 重构测试代码的详细指导  
- 测试覆盖率和质量检查清单
- 工具使用指南 (如zen mcp等)

agent-tdd-de.md:
- 最小实现策略和绿色通过技巧
- 代码重构的具体规则和模式
- 命名规范和代码质量标准  
- 性能优化指导原则
```

**第三层：现有Memory协议利用**
```
σ₄.STATE: context + TDD执行状态
├─ Ω_current: Ω₄ᵀ (TDD执行模式)
├─ tdd_phase: 'red'|'green'|'refactor'
├─ current_cycle_index: number
└─ target_method: string

σ₂.patterns: TDD计划存储
├─ tdd_cycles: TDD循环列表
└─ selected_approach: TDD方法

σ₅.progress: 循环完成状态
├─ cycle_completion: boolean[]
└─ current_step_info: step详情
```

**第四层：运行时传递**
```
调度器传递给子Agent的信息包:
- plan_step: 引用memory-bank中的具体计划步骤
- 上下文: 当前项目状态和相关代码
- 相位标识: 明确当前处于RGR的哪个阶段  
- 质量规则: 指向具体操作指导文件的引用
```

## 质量规则和操作指导

### 重构阶段质量标准
```
Ψ_quality_rules = {
  Ψ_naming: 有意义的命名（非TDD随机字符串）
  Ψ_structure: 提取小函数，消除代码重复
  Ψ_coverage: 测试覆盖率保持或提升
  Ψ_performance: 优化算法（保持行为不变）
  Ψ_readability: 代码可读性和可维护性提升
}
```

### QA 重构责任
- 重构测试代码（提取测试辅助函数、优化测试数据设置）
- 确保测试仍然验证正确的业务逻辑
- 检查测试覆盖率是否受影响
- 验证重构后测试仍然能发现潜在bug
- 所有改进机会必须在重构阶段处理，不得延后

### DE 重构责任  
- 重构实现代码（提取小函数、优化算法、改善命名）
- 确保代码结构更清晰
- 优化性能（在不改变行为的前提下）
- 处理代码重复和设计改进
- 所有改进机会必须在重构阶段处理，不得延后

## 实现路径

### 实现优先级
1. **Phase 1**: 扩展 `claude.md` - 添加TDD符号协议
2. **Phase 2**: 修改 `agent-plan.md` - 支持TDD cycles规划输出
3. **Phase 3**: 创建 `agent-tdd-qa.md` - QA角色具体指导
4. **Phase 4**: 创建 `agent-tdd-de.md` - DE角色具体指导  
5. **Phase 5**: 更新主调度器逻辑 - 支持RGR循环调度

### 文件结构变更
```
CursorRIPER.agent/
├─ riper-sigma-core.mdc (扩展TDD符号)
├─ agent-plan.md (修改输出格式)  
├─ agent-tdd-qa.md (新建)
├─ agent-tdd-de.md (新建)
├─ agent-execute.md (废弃/重命名为参考)
└─ 其他现有文件 (保持不变)
```

### 现有σ内存协议利用
```
σ₄.STATE扩展:
├─ Ω_current: Ω₄ᵀ
├─ tdd_phase: 'red'|'green'|'refactor'
├─ current_cycle_index: number
└─ target_method: string

σ₂.patterns扩展:
├─ tdd_cycles: [...] (替代implementation_plan)
└─ cycle_dependencies: dependency_graph

σ₅.progress扩展:
├─ cycle_completion: boolean[]
└─ quality_metrics: test_coverage等
```

## 预期效果

### 稳定性提升
- 每个功能都经过测试验证，减少错误级联
- 渐进式实现降低复杂度，提高成功率
- 重构阶段确保代码质量不衰减

### 质量保证
- 强制测试覆盖，提前发现问题
- QA/DE严格分工，避免越权导致的混乱
- 每个循环都有质量检查关卡

### 用户体验
- 更可靠的执行结果，减少返工
- 清晰的进度反馈（每个RGR循环的完成）
- 高质量的最终代码产出

---

**关键成功因素**：
1. 严格执行角色边界，QA和DE绝不越权
2. 完整执行每个RGR循环，不允许跳过任何阶段
3. 质量规则在重构阶段强制执行
4. 失败即终止原则，避免复杂的异常处理