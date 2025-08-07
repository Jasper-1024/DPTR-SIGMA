# TDD-RIPER Memory-Bank & CLAUDE.md 改进方案

## 背景问题

### 原始Memory-Bank局限性
- **σ₂ systemPatterns.md过载**: 复杂项目中单文件需承载所有模块详设（预估8000-12000字符）
- **信息组织混乱**: 不同层面信息（架构/模块/接口）强行压缩在6个固定文件中
- **缺乏扩展性**: 原始Cline的"可扩展"只是概念，无实际架构支撑
- **维护困难**: 大文件难以查找和更新

### 项目级CLAUDE.md定位不清
- 与全局CLAUDE.md内容重复
- 缺乏项目特定的即时指导
- 与memory-bank信息边界模糊

## 改进方案

### 1. Memory-Bank模块化架构

#### 核心原则
- **6文件核心 + 模块扩展**: σ₁-σ₆保持轻量，模块详设独立存储
- **信息分层**: 系统级 → 模块级 → 实现级
- **按需访问**: 通过引用索引，避免信息过载

#### 文件结构
```
memory-bank/
├─ projectbrief.md (σ₁)       # 项目概述
├─ systemPatterns.md (σ₂)     # 系统架构 + 模块索引
├─ techContext.md (σ₃)        # 技术栈
├─ activeContext.md (σ₄)      # 当前状态
├─ progress.md (σ₅)           # TDD进展
├─ protection.md (σ₆)         # 保护注册
└─ modules/                   # 模块详设扩展
   ├─ registration/
   │  └─ design.md           # 注册模块详细设计
   ├─ sse-connection/
   │  └─ design.md           # SSE连接详细设计
   ├─ test-execution/
   │  └─ design.md           # 测试执行详细设计
   ├─ timeout-control/
   │  └─ design.md           # 超时控制详细设计
   ├─ state-management/
   │  └─ design.md           # 状态管理详细设计
   └─ message-broadcast/
      └─ design.md           # 消息广播详细设计
```

#### σ₂ systemPatterns.md 轻量化
```markdown
## 🏛️ Architecture Overview  
3-layer architecture: API → Business → Transport
[架构图和核心设计理念 ~800字符]

## 📊 System Data Flow
[系统级数据流转图和说明 ~800字符] 

## 📐 Design Patterns
- Event-driven pattern for SSE
- Worker pool for test execution  
- State machine for session lifecycle
[核心设计模式 ~600字符]

## 🏗️ Module Structure
- @modules/registration/ - 注册服务详设
- @modules/sse-connection/ - SSE连接管理详设
- @modules/test-execution/ - 测试执行引擎详设
- @modules/timeout-control/ - 超时控制详设
- @modules/state-management/ - 状态管理详设
- @modules/message-broadcast/ - 消息广播详设
[模块索引 ~400字符]
```
**总长度: ~2600字符** (相比原来12000字符大幅减少)

#### 模块详设文件内容
- **设计思路**: 为什么这样设计？
- **核心接口**: 关键API定义
- **数据结构**: 主要数据模型
- **关键决策**: 技术选择和权衡
- **平均长度**: ~800字符/模块

### 2. 信息边界明确划分

#### Memory-Bank归属（人脑长期记忆）
- **核心设计思路** - 为什么这样设计？
- **架构决策** - 技术选择和权衡
- **模块职责** - 关键接口和数据结构
- **当前状态** - TDD进展和工作上下文

#### 其他位置归属
```bash
项目根目录/
├─ docs/                    # 外界对接
│  ├─ api.md               # API文档（用户手册）
│  ├─ deployment.md        # 部署说明
│  └─ integration.md       # 集成指南
├─ test/                   # 测试相关
│  ├─ scenarios/           # 测试场景
│  └─ performance/         # 性能测试结果
└─ 临时文件                 # 不长期存储
   ├─ 调试日志             # 开发过程流水账
   ├─ 性能笔记             # 临时测试结果
   └─ 实现细节             # 具体技术实现
```

### 3. 项目级CLAUDE.md设计

#### 核心定位
- **每次对话自动加载**的即时指导
- **团队共享约定**（commit到git）
- **快速命令参考**和**基本约束**
- **Memory-Bank索引入口**

#### 标准结构
```markdown
# Tech Stack
- Language: Go 1.21+
- Framework: net/http, gorilla/mux
- Testing: Go标准testing + testify
- SSE: 原生http.Flusher
- State: 内存 + 可选Redis

# Project Structure  
```
internal/
├─ registration/     # 注册模块
├─ sse/             # SSE连接管理
├─ execution/       # 测试执行引擎
└─ timeout/         # 超时控制

memory-bank/        # RIPER记忆系统
├─ systemPatterns.md # 系统架构
├─ modules/         # 模块设计
└─ [σ₁-σ₆]         # 核心memory文件
```

# Commands
- `go test ./...`: 完整测试套件
- `go test -v ./internal/registration`: 单模块测试  
- `go run main.go`: 启动开发服务器
- `make test`: TDD测试 + 覆盖率
- `curl -X POST localhost:8080/register`: 测试注册接口

# TDD-RIPER Integration
**重要**: 开始任何工作前必须读取 memory-bank/ 相关文件获取上下文
- 严格按照 memory-bank/progress.md 中的TDD cycles执行
- 所有架构决策记录在 memory-bank/systemPatterns.md

# Code Style  
- 标准Go约定 (gofmt, golint)
- 接口命名: I + 名词 (如 IRegistration)
- 测试文件: `*_test.go`
- 错误处理: 显式返回，使用errors.Wrap
- SSE消息格式: JSON with event/data fields

# Do Not
- 跳过任何TDD阶段 (Red→Green→Refactor)
- 在memory-bank外维护重要设计信息
- 修改 internal/legacy/ 中的代码
- 直接推送到main分支

# Memory Integration
项目记忆存储: memory-bank/[projectbrief|systemPatterns|techContext|activeContext|progress|protection].md
```

### 4. 协同关系

#### CLAUDE.md vs Memory-Bank职责分工
- **CLAUDE.md**: 即时约束、快速参考、团队约定
- **Memory-Bank**: 深层知识、设计思路、动态状态

#### 工作流程
1. **CLAUDE.md自动加载** - 提供基础约束和命令参考
2. **按需读取Memory-Bank** - 获取具体上下文和设计细节
3. **更新Memory-Bank** - 记录新的决策和状态变化
4. **维护CLAUDE.md** - 更新团队约定和常用命令

## 实施效果预期

### Memory-Bank容量优化
- **原σ₂**: 12000字符 → **新σ₂**: 2600字符 (78%减少)
- **总体信息**: 更好组织，按需访问
- **维护性**: 模块独立，易于更新

### 开发体验改善
- **上下文获取**: 精准定位相关信息
- **团队协作**: 统一的项目约定
- **TDD工作流**: 清晰的状态管理和进度跟踪

### 可扩展性提升
- **新模块添加**: 简单创建 modules/new-module/design.md
- **复杂功能**: 独立文档空间，不影响核心结构
- **信息分层**: 系统→模块→实现的清晰层次

## 迁移指导

### 现有项目升级步骤
1. **分析现有σ₂**: 识别模块边界和详设内容
2. **创建modules结构**: 提取模块详设到独立文件
3. **重写σ₂**: 保留架构和索引，移除详设
4. **创建项目级CLAUDE.md**: 参考标准模板
5. **验证协同效果**: 测试信息获取流程

### 新项目直接应用
1. **使用改进版init-riper**: 直接生成模块化结构
2. **创建项目级CLAUDE.md**: 基于项目特点定制
3. **按模块开发**: 逐步完善modules/下的设计文档

---

**总结**: 此改进方案解决了原始Memory-Bank的扩展性限制，明确了项目级CLAUDE.md的定位，提供了可持续的项目知识管理架构。核心是"轻量核心+模块扩展"的设计理念，平衡了信息完整性和维护效率。