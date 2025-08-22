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
- CTX:{context} - Context data (when additional info needed)

**Input Format**: `[S{sid}?,R{round}?,C{cycle}?,P{phase}?,CTX{context}]` - Only pass required parameters, `?` means optional
**Output Format**: `→[{STATUS_CODE},{optional_message}]`

**Agent Parameter Requirements**:

- Ω₁ᶜ: `[CTX:{module}]` - architecture or module context
- Ω₂ˢ/Ω₂ᶜ: `[S:{sid},R:{round},CTX:{context}]` - session, round, other context
- Ω₃ᵍ/Ω₃ᴱ: `[S:{sid},R:{round},C:{cycle},P:{phase},CTX:{context}]` - session, round, cycle, phase, other context
- Ω₄ᴿ: `[]` - no parameters

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

**OUTPUT**: σ₅.implementation_plan, σ₅.tdd_cycles, σ₅.execution_checklist
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
├─ σ₅.implementation_plan (method breakdown)
├─ σ₅.tdd_cycles: [
│   ├─ TDD₁: Method() → ℜ→ℜᴳ→ℜᶠ [module ref]
│   └─ TDD₂: Method() → ℜ→ℜᴳ→ℜᶠ [module ref]
│   ]
└─ σ₅.execution_checklist (validation)

### Ω₃: TDD Loop (MT scheduled)

**INPUT**: σ₅.tdd_cycles from Ω₂
**PERMISSIONS**: QA(test-only) | DE(impl-only)

TDD_EXECUTE():
├─ INIT: sid=TDD_{timestamp} → INIT[sid,"tdd_loop"]
├─ Phase 0: (first cycle setup)
│   ├─ MT→Ω₃ᴱ[S{sid},R{r},C{0},P:Phase0]
│   ├─ DE creates minimal interface definitions
│   └─ WAIT: →P0C (Phase 0 complete)
│
├─ FOR each cycle IN σ₅.tdd_cycles:
│   ├─ RED Phase:
│   │   ├─ MT→Ω₃ᵍ[S{sid},R{r},C{i},P:ℜ]
│   │   ├─ QA writes failing tests
│   │   └─ WAIT: →RC (tests written & failing)
│   │
│   ├─ GREEN Phase:
│   │   ├─ MT→Ω₃ᴱ[S{sid},R{r},C{i},P:ℜᴳ]
│   │   ├─ DE implements minimal code
│   │   └─ WAIT: →GC (tests passing)
│   │
│   └─ REFACTOR Phase:
│       ├─ MT: r++ # enter REFACTOR
│       ├─ MT→Ω₃ᵍ[S{sid},R{r},C{i},P:ℜᶠᵗ]
│       │   └─ QA refactors test code →RTC
│       ├─ MT→Ω₃ᴱ[S{sid},R{r},C{i},P:ℜᶠⁱ]
│       │   └─ DE refactors implementation →RIC
│       ├─ MT: Run test suite validation
│       ├─ r++ # for cross-review
│       ├─ MT→Ω₃ᴱ[S{sid},R{r},C{i},P:review_tests]
│       │   └─ DE reviews QA's test code →APPROVED|→NEEDS_CHANGE
│       ├─ MT→Ω₃ᵍ[S{sid},R{r},C{i},P:review_impl]
│       │   └─ QA reviews DE's implementation →APPROVED|→NEEDS_CHANGE
│       └─ MT: Convergence check
│           ├─ IF both →APPROVED AND tests_pass:
│           │   └─ ADVANCE to next_cycle
│           └─ ELSE:
│               ├─ r++ (new iteration)
│               └─ REPEAT REFACTOR sequence
└─ UPDATE: σ₅.progress[cycle] = ✅

QUALITY_GATES:
├─ RED: Tests written & failing
├─ GREEN: Minimal implementation, all tests pass
└─ REFACTOR: Code quality improved, tests pass, both approved

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
