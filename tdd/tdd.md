深度思考(always use ultra thinkt),请根据 $ARGUMENTS 的需求，进行分析;


## 名词理解
**业务实现计划**
分析需求需要的实现计划，能够指导业务开发.包括接口设计，数据库设计，路由设计等

**单元测试计划**
查看 `$ARGUMENTS` 的详情，对业务实现计划进行分析，并思考单元测试计划的细节。以TDD的方式拆解

**使用子任务尽可能的并行的分析和拆解TDD循环列表**

对TDD循环列表创建todowriter列表，每一项就是TDD的一个循环,tdd循环来源于子任务的调查结果。

### TDD工作流的阶段

**角色定义**：

**QA**: 负责实现单元测试,只允许实现测试代码，不允许修改业务代码。
**Developer**: 角色负责实现业务代码,只允许实现业务代码，不允许修改测试代码。


### TDD循环
**Workflow Guidance**：

- **第一**基于设计文档的接口定义，实现最小的接口或者struct定义,要确保make test是能通过的。
- tdd以接口为单位进行迭代开发，每个接口都经过严格的测试驱动开发（TDD）流程,确保每个接口都经过Red-Green-Refactor的完整流程。
- 要告知角色，只做一个阶段的事，不允许做任何其他阶段的工作。
- 避免一次性创建所有接口，专注于一个功能一个功能地TDD循环，确保每个功能都经过测试和验证。
  - 严格检查每个Phase的TDD循环的Red，Green和Refactor阶段是否都做了。不能跳过任何阶段。
  - 不是QA和Developer的任何独立完成的任务，是描述的Phase的TDD循环。
  - 确保都做过步骤Red→Green→Refactor
  - QA和Developer角色需要紧密协作，交替按照TDD循环进行红绿优化循环。
  - 每个循环步骤都务必聚焦于设计需求和测试需求所涉及的文件和代码，**不得擅自修改和优化其他的代码文件**
  - QA和Developer都不是一次性完成他们的工作，而是一个接口一个接口的去进行实现和测试。
  - 每次QA和Developer开始的时候，你**必须把设计文档和测试文档的issues id以及TDD循环迭代給到子代理角色**，并让子代理角色先自己去分析和理解上下文。
- QA和Developer除了在TDD循环中使用绝对不会自行去实现实现计划的接口和单元测试任务。

#### Phase 0: Ready for TDD,
1. 只定义即将测试的一个方法（如AddLabel）
2. 创建必要的数据结构

#### Phase 1: **TDD循环**
每次QA和Developer开始的时候，你**必须把设计文档、测试文档和TDD循环迭代的issuesID給到子代理角色**，并让子代理角色先自己去分析和理解上下文。
传递消息給子角色,对子角色强烈要求和指导:
  - 分析该阶段可能需要修改的文件和目录，要求聚焦这些目录和文件,不得偏离目标
1. Red: QA为接口编写失败测试
   - 进行完成的功能测试代码编码，不是基础单元测试编码，总是按完整需求编写单元测试代码。但总是预期make test是失败的
   - 参看 @tests/README.md
2. Green: Developer实现最小代码让测试通过
3. Refactor:
   - 该阶段不能并行进行，QA和Developer需要交替进行。
   - QA需要检查(codereview)和优化(refactor)在这个循环中自己修改过的测试相关的代码,不允许去调整实现的代码,重构不需要考虑向下兼容，务必一次性改成最正确的实现
   - Developer需要检查(codereview)和优化(refactor)在这个循环中自己修改过的实现相关的代码，不允许去调整测试代码,重构不需要考虑向下兼容，务必一次性改成最正确的实现
   - 传递給子角色的信息
     - 优化函数名可读，优化文件名有意义，文件名和函数名不能是一个看起来像TDD或者随机的字符串，有意义的名字意味着是为业务服务的。
     - 单元测试的名字不应该有图或者符号，应该是有意义的英文名字。
     - 重构代码的目的是为了提高代码质量和可读性，尽可能的发现bug和有质量和可读性问题的代码，必要的时候使用zen的mcp工具进行分析和重构建议

#### Phase 2: 逐步扩展
1. 添加下一个方法到接口
2. 重复TDD循环
 
#### **phase 分解的例子**
分解的任务必须严格按照TDD循环的步骤进行，确保每个方法都经过Red-Green-Refactor的完整流程。
```
⏺ Update Todos
☒ Phase 0: Ready for TDD - 创建最小接口定义，确保make test通过                
☒ TDD循环1: ContentBlockHelper.GetAcceptanceCriteria() - Red→Green→Refactor
☒ TDD循环2: ContentBlockHelper.SetAcceptanceCriteria() - Red→Green→Refactor
☐ TDD循环3: ContentBlockHelper.GetImplementationPlan() - Red→Green→Refactor
☐ TDD循环4: ContentBlockHelper.SetImplementationPlan() - Red→Green→Refactor
☐ TDD循环5: IssuesManager.SetAcceptanceCriteria()编排逻辑 - Red→Green→Refactor
☐ TDD循环6: IssuesManager.AddLabel()去重逻辑 - Red→Green→Refactor
```


##### TDD工作流的重构阶段
QA负责：
- 重构测试代码（提取测试辅助函数、优化测试数据设置）
- 确保测试仍然验证正确的业务逻辑
- 检查测试覆盖率是否受影响
- 验证重构后测试仍然能发现潜在bug
- 发现的改进机会都必须在重构阶段处理，不得延后到下一个TDD循环

Developer负责：
- 重构实现代码（提取小函数、优化算法、改善命名）
- 确保代码结构更清晰
- 优化性能（在不改变行为的前提下）
- 处理代码重复和设计改进
- 发现的改进机会都必须在重构阶段处理，不得延后到下一个TDD循环


共同协作：
- 讨论接口设计是否需要调整
- 确保测试和实现的重构方向一致
- 运行完整测试套件验证重构成功
- 代码审查确保质量

实际操作流程：
重构阶段开始：
├─ QA：重构测试代码，保持测试意图不变
├─ Developer：重构实现代码，保持行为不变
├─ 协作：运行测试确保全部通过
├─ 协作：代码审查和讨论
└─ 提交重构后的代码，进入下一个TDD循环
 
