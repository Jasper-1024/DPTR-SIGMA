# DPTR·Σ Core Protocol

Claude Code orchestrates SubAgents through Design(Loop)→Plan(Loop)→TDD(Loop)→Review workflow, coordinating via MCP Memory(agent dialogues) and σ Memory-Bank (persistent artifacts).

## Framework Core

Ω₁: Design Loop → Ω₂: Plan Loop → Ω₃: TDD Loop → Ω₄: Review

MT = Main Thread = Claude Code (Primary Scheduler) = CC

### Schedule & SubAgent

Ω₁: User manual scheduled

- Ω₁ᴰ: Design Mode (Architecture & Module Design) = CC Plan Mode
- Ω₁ᶜ: Design Critic SubAgent (Audit)

Ω₂: MT scheduled

- Ω₂ˢ: Spec Agent (Planning)
- Ω₂ᶜ: Spec Critic SubAgent (Validation)

Ω₃: MT scheduled

- Ω₃ᵍ: QA SubAgent (Testing)
- Ω₃ᴱ: DE SubAgent (Development)

Ω₄: User manual scheduled

- Ω₄ᴿ: Review SubAgent (Final validation)

## Symbol System

σ[Memory]: σ₁=Brief, σ₂=Patterns, σ₃=Tech, σ₄=Context/State, σ₅=Progress
S[Session]: session_id(Plan↔Critic), tdd_session_id(QA↔DE per cycle)
∇[Decision]: ACCEPT|REVISE|REJECT
→[Flow], ↔[Interact], ⟷[Loop], ⟲[Iterate]

Logic: ∈, ∃, ∧, ∨, ¬
Status: ✅(success), ❌(failure), ⚠️(warning)
Cross-Reference: [↗️σₓ:Rₓ] = Reference to memory file section

## SubAgent Communication

1. **SubAgent I/O**: Status code + brief message → MT scheduling
2. **MCP Memory**: Detailed session dialogues → Inter-agent communication
3. **σ Memory Bank**: Persistent artifacts → Cross-phase handoffs

SubAgents decide what to read/write from MCP/σ internally.

**Session Isolation**:

- Ω₂: One session_id for entire Ω₂ˢ↔Ω₂ᶜ dialogue
- Ω₃: New tdd_session_id per cycle (QA↔DE isolation)

### SubAgent I/O Protocol

**Parameter Definitions**:

- S:{sid} - Session ID (for dialogue)
- R:{round} - Round number (for dialogue)  
- C:{cycle} - Cycle number (for Ω₃)
- P:{phase} - Phase identifier (for Ω₃)
- M:{module} - Module path (for Ω₂)
- CTX:{context} - Context data (REQUIRED for Ω₃, contains design/plan/interface paths)

**Input Format**: `[S{sid}?,R{round}?,C{cycle}?,P{phase}?,M{module}?,CTX{context}]` - Only pass required parameters, `?` means optional
**Output Format**: `→[{STATUS_CODE},{optional_message}]`

**Agent Parameter Requirements**:

- Ω₁ᶜ: `[CTX:{module}]` - architecture or module context
- Ω₂ˢ/Ω₂ᶜ: `[S:{sid},R:{round},M:{module},CTX:{context}]` - session, round, module, other context
- Ω₃ᵍ/Ω₃ᴱ: `[S:{sid},R:{round},C:{cycle},P:{phase},CTX:{context}]` - session, round, cycle, phase, other context
- Ω₄ᴿ: `[]` - no parameters

**CTX Format Standards**:
- Ω₁ᶜ: `CTX:module=/memory-bank/modules/{name}`
- Ω₂: `CTX:module=/memory-bank/modules/{name}, design={path}`
- Ω₃: `CTX:design={path}, plan={path}, interface="{exact_signature}"`

**Status Codes**:

- Ω₁: →ACCEPT|→REVISE|→REJECT
- Ω₂ˢ: →PC(Plan Created)|→PR(Plan Revised)|→DG(Disagree with Critique)
- Ω₂ᶜ: →NR(Needs Revision)|→PA(Plan Accepted)|→EN(Escalation Needed)|→DA(Dialogue Active)
- Ω₃ᵍ: →RC(Red Complete)|→TA(Test Adjusted)|→RTC(Refactor Test Complete)
- Ω₃ᴱ: →GC(Green Complete)|→TI(Test Issue)|→RIC(Refactor Implementation Complete)|→P0C(Phase 0 Complete)
- Ω₃-Review: →APPROVED|→NEEDS_CHANGE (cross-review phase)
- Ω₄: →VC(Validation Complete)|→DF(Deviations Found)|→QP(Quality Passed)|→QF(Quality Failed)
- Errors: →ME(Memory Error)|→TO(Timeout)|→EX(Exception)|→BL(Blocked)

### MCP Memory Storage

**Session Design**:

- session_id (sid) = One complete dialogue loop = One MCP Entity
- Entity type: "plan_loop" | "tdd_loop"
- Observations: Sequential agent outputs within that dialogue

**Symbolic Operations**:

- INIT[sid,type] → mcp__filesystem__create_entities(name=sid, entityType=type)
- STORE[sid,content] → mcp__filesystem__add_observations(entityName=sid, contents=[content])
- QUERY[sid,pattern] → mcp__filesystem__search_nodes(query=sid+" "+pattern)
- READ[sid] → mcp__filesystem__open_nodes(names=[sid])

**Content Format**:
"R{round}|{agent}|{status}|{content}" for plan/design loops
"P{phase}|{agent}|{status}|{content}" for TDD loops

**Examples**:

- Full dialogue: READ["plan_2025_001"] → All observations in order
- Query previous round: QUERY["plan_2025_001", "R0"] → Round 0 content
- Store new round: STORE["plan_2025_001", "R1|Ω₂ˢ|→PR|Revised plan..."]

## Ω Specifications

### Ω₁: Design Loop (Manual scheduled)

Ω₁ᴰ(architecture) → Ω₁ᶜ(audit) → ∇
└─ ACCEPT: ∀module ∈ modules:
    └─ Ω₁ᴰ(module_i) → Ω₁ᶜ(module_i) → ∇
        ├─ REVISE: ⟲ redesign module_i
        └─ ACCEPT: next module or → Ω₂

### Ω₂: Plan Loop (MT scheduled)

**OUTPUT**: /memory-bank/modules/{module}/tdd_plan.md
**DIALOGUE**: Ω₂ˢ↔Ω₂ᶜ via MCP Memory

MT→Ω₂ˢ[S,R]→status→MT→Ω₂ᶜ[S,R]→status→MT ⟲ until →PA

PLAN_EXECUTE():
├─ INIT: sid=PLAN_{timestamp} → INIT[sid,"plan_loop"]
├─ STORE: σ₄.session_id=sid, r=0
├─ DISPATCH: Ω₂ˢ[S{sid},R{r}]
├─ RECEIVE: →PC|→PR
├─ DISPATCH: Ω₂ᶜ[S{sid},R{r}]
├─ RECEIVE: →NR|→PA
├─ DECISION:
│   ├─ →PA: σ₅.tdd_cycles ready → Ω₃
│   └─ →NR: r++ → CONTINUE_LOOP
└─ LOOP: ⟲ until →PA

PLAN_OUTPUT:
├─ module.tdd_cycles: [
│   ├─ TDD₁: Method() → ℜ→ℜᴳ→ℜᶠ [interface signature]
│   └─ TDD₂: Method() → ℜ→ℜᴳ→ℜᶠ [interface signature]
│   ]
└─ module.execution_checklist (validation)

### Ω₃: TDD Loop (MT scheduled)

**INPUT**: tdd_cycles from /memory-bank/modules/{module}/tdd_plan.md
**PERMISSIONS**: QA(test-only) | DE(impl-only)

**PARALLEL EXECUTION**: 
For |cycles| instances, invoke Task tool |cycles| times in ONE message.
Example: [Ω₃ᵍ×|cycles|] where cycles={1,2} requires 2 Task invocations in the same message.

TDD_EXECUTE():
├─ INIT: sid=TDD_{timestamp} → INIT[sid,"tdd_loop"]
├─ Phase 0: (first cycle setup)
│   ├─ MT→Ω₃ᴱ[S{sid},R{r},C{0},P:Phase0]
│   ├─ DE implements interface skeleton from design.md
│   └─ WAIT: →P0C (Phase 0 complete)
│
├─ FOR each batch B IN module.tdd_cycles:
│   ├─ EXTRACT: cycles = B.cycles[0:B.parallel] # parallel ∈ {1,2,3}
│   ├─ SESSIONS: For each c in cycles: sid_c = TDD_{timestamp}_C{c}
│   │
│   ├─ RED Phase:
│   │   ├─ MT→[Ω₃ᵍ×|cycles|]: {[S:TDD_{timestamp}_C{c},R:0,C:{c},P:ℜ] | c∈cycles}
│   │   └─ WAIT_ALL: {→RC}×|cycles|
│   │
│   ├─ GREEN Phase:
│   │   ├─ MT→[Ω₃ᴱ×|cycles|]: {[S:TDD_{timestamp}_C{c},R:0,C:{c},P:ℜᴳ] | c∈cycles}
│   │   └─ WAIT_ALL: {→GC}×|cycles|
│   │
│   └─ REFACTOR Phase:
│       ├─ r = 1
│       └─ LOOP until convergence:
│           ├─ MT→[Ω₃ᵍ×|cycles|]: {[S:TDD_{timestamp}_C{c},R:r,C:{c},P:ℜᶠᵗ] | c∈cycles}
│           ├─ WAIT_ALL: {→RTC}×|cycles|
│           ├─ MT→[Ω₃ᴱ×|cycles|]: {[S:TDD_{timestamp}_C{c},R:r,C:{c},P:ℜᶠⁱ] | c∈cycles}
│           ├─ WAIT_ALL: {→RIC}×|cycles|
│           ├─ r++ # for cross-review round
│           ├─ MT→[Ω₃ᴱ×|cycles|]: {[S:TDD_{timestamp}_C{c},R:r,C:{c},P:review_tests] | c∈cycles}
│           ├─ WAIT_ALL: {review_tests}×|cycles|
│           ├─ MT→[Ω₃ᵍ×|cycles|]: {[S:TDD_{timestamp}_C{c},R:r,C:{c},P:review_impl] | c∈cycles}
│           ├─ WAIT_ALL: {review_impl}×|cycles|
│           └─ CONVERGENCE_CHECK:
│               ├─ cycles = {c∈cycles | ¬converged(c)} # update active cycles
│               ├─ IF cycles = ∅:
│               │   └─ BREAK # Move to next batch
│               └─ ELSE:
│                   ├─ r++
│                   └─ CONTINUE # 
└─ UPDATE: σ₅.progress[batch] = ✅

QUALITY_GATES:
├─ RED: Tests written & failing
├─ GREEN: Minimal implementation, all tests pass
└─ REFACTOR: Code quality improved, tests pass, both approved

#### TDD Workflow Refactor Phase
QA Responsibilities:
- Refactor test code (extract test helpers, optimize test data setup)
- Ensure tests still verify correct business logic
- Check if test coverage is affected
- Verify refactored tests can still detect potential bugs
- All improvement opportunities must be handled in refactor phase, not deferred to next TDD cycle

Developer Responsibilities:
- Refactor implementation code (extract small functions, optimize algorithms, improve naming)
- Ensure code structure is clearer
- Handle code duplication and design improvements
- All improvement opportunities must be handled in refactor phase, not deferred to next TDD cycle

Joint Collaboration:
- Discuss whether interface design needs adjustment
- Ensure test and implementation refactoring directions are consistent
- Run complete test suite to verify refactor success
- Code review to ensure quality

Actual Operation Flow:
Refactor phase begins:
├─ QA: Refactor test code, maintain test intent
├─ Developer: Refactor implementation code, maintain behavior
├─ Collaboration: Run tests to ensure all pass
├─ Collaboration: Code review and discussion
└─ Commit refactored code, enter next TDD cycle

### Ω₄: Review (Manual scheduled)

User→Ω₄ᴿ[] → (→VC|→DF|→QP|→QF) with report

## Error Handling

FAILURE_PROTOCOLS:
├─ AGENT_FAILURE: # SubAgent crash
│   ├─ LOG: Error → σ₅.progress
│   ├─ SNAPSHOT: State → σ₄
│   └─ HALT: Cannot continue
├─ TEST_FAILURE: # Normal TDD flow
│   ├─ IF phase=RED: Expected → Continue
│   ├─ IF phase=GREEN: Fix needed → Stay in cycle
│   └─ IF phase=REFACTOR: Regression → Rollback
└─ QUALITY_FAILURE: # Standards not met
    ├─ DOCUMENT: Failed gate → σ₅
    └─ DECISION: Retry or escalate to User
