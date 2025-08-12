# RIPER·Σ Core Protocol

## Modes & Permissions
Ω₁ᴾ: CC PLAN MODE (Γ₁₋₃,₆) - architecture & module design *(CC native plan mode)*
Ω₂ᴬ: ARCH DEVIL'S ADVOCATE (Λ₁|Λ₂) - dual-layer design opposition  
Ω₃ᴾ: SPECIFY (exact plans) - implementation planning
Ω₄ᶜ: PLAN CRITIC (review only) - practical feasibility validation
Ω₅ᵀ: EXECUTE (TDD cycles) - implementation with testing
Ω₆ⱽ: VALIDATE (no fix) - final quality verification

## Memory Protocol
σ₁: brief | σ₂: patterns | σ₃: tech
σ₄: context+STATE | σ₅: progress | σ₆: protection

## Handoff Protocol
EXIT: /handoff→σ₄{to:Ω_next,summary}
ENTRY: CHECK(σ₄.Ω_current==my_mode)

## Protection Levels
Ψ₁-₃: proceed | Ψ₄-₆: caution+confirm

## Commands
/arch-critic=Ω₂ᴬ{Λ₁|Λ₂,module_name} /p=Ω₃ᴾ /plan-critic=Ω₄ᶜ /tdd-execute=Ω₅ᵀ /rev=Ω₆ⱽ

## Cross-Reference Notation
[↗️σₓ:Rₓ] = Reference to memory file section
Γ₁=Files Γ₂=Folders Γ₃=Code Γ₄=Commands Γ₅=Modify Γ₆=Web

## Session Protocol
SESSION: session_id→MCP_Memory (per-dialogue isolation)
STATE: σ₄.Ω_current (maintained by Main Thread/MT)
MT: Main Thread (RIPER mode coordinator)

## Communication Protocol

### Symbolic Format
DISPATCH: Agent[S{sid},R{round},C{cycle},P{phase},CTX{context}]
RESPONSE: →{STATUS_CODE}: {optional_message}

### Status Codes
Plan Loop: →PC|→PR|→NR|→PA|→DG
TDD Loop: →RC|→GC|→RTC|→RIC
Errors: →ME|→TO|→EX|→BL

### MCP Storage Format
OBS[S{sid},R{n},A:{agent},T:{timestamp}]: {content}

### Query Patterns
QUERY: OBS[S{sid},R{current},*,*]      # Current round
QUERY: OBS[S{sid},R{n-1},*,*]          # Previous round  
QUERY: OBS[S{sid},*,A:{agent},*]       # All from agent

## CC Plan Mode Integration
Ω₁ᴾ: CC Plan Mode - architecture & module design *(CC native plan mode)*
TRIGGER: User uses CC native Plan Mode
OUTPUT: Direct to memory bank
  ├─ σ₂.architecture_design (overall architecture)
  ├─ σ₂.module_specifications (module details)
  └─ σ₂.tech_stack (technology choices)
HANDOFF: Automatic transition to Ω₂ᴬ for design audit

## State Machine
σ₄.Ω_current ∈ [Ω₁ᴾ,Ω₂ᴬ,Ω₃ᴾ,Ω₄ᶜ,Ω₅ᵀ,Ω₆ⱽ]
FLOW: Ω₁ᴾ→Ω₂ᴬ→(Ω₃ᴾ⟷Ω₄ᶜ)→Ω₅ᵀ→Ω₆ⱽ
ENFORCE: current==agent_mode

## Dual Loop Protocol

### Design Quality Loop (Ω₁ᴾ → Ω₂ᴬ)
DESIGN_LOOP: Ω₁ᴾ → Ω₂ᴬ{Λ₁|Λ₂,module_name} → σ₄.arch_critique → ∇decision
∇decision: 
├─ ACCEPT → σ₄.design_approved=true → Ω₃ᴾ
├─ REVISE → σ₄.design_feedback → re-enter Ω₁ᴾ
└─ REJECT → σ₄.design_rejected → HALT

### Plan Quality Loop (Ω₃ᴾ ⟷ Ω₄ᶜ) - MCP Session
SESSION_INIT: MT→sid→MCP_Memory  
SESSION_STORE: σ₄.session_id=sid
PLAN_LOOP: MT→Ω₃ᴾ[S,R]→status→MT→Ω₄ᶜ[S,R]→status→MT
⟲[round]: status-driven iteration

#### Plan MCP Router (Main Thread)
```
PLAN_MCP_ROUTER():
├─ INIT: sid=generate() → MCP_Memory
├─ STORE: σ₄.session_id=sid, r=0
├─ DISPATCH: Ω₃ᴾ[S{sid},R{r}]  
├─ RECEIVE: →PC|→PR
├─ DISPATCH: Ω₄ᶜ[S{sid},R{r}]
├─ RECEIVE: →NR|→PA  
├─ DECISION_ROUTING:
│   ├─ IF →PA → ADVANCE→Ω₅ᵀ
│   └─ IF →NR → CONTINUE_LOOP
└─ LOOP_CONTINUE:
    ├─ r++
    ├─ DISPATCH: Ω₃ᴾ[S{sid},R{r},CTX:revise]
    ├─ RECEIVE: →PR|→DG
    ├─ IF →PR → DISPATCH: Ω₄ᶜ[S{sid},R{r}] 
    ├─ IF →DG → DISPATCH: Ω₄ᶜ[S{sid},R{r},CTX:disagree]
    └─ ⟲ until →PA
```

#### Summary Protocol  
STATES: →PC|→PR|→DG|→NR|→PA|→EN|→ME
  →EN: Error/Not-converging (dialogue failed to reach agreement)
ROUTING: status_code→decision_logic→next_dispatch
CONVERGE: →PA→σ₄.plan_approved=true→Ω₅ᵀ

ITERATIONS: MCP Memory dialogue optimized for individual developers

## TDD Protocol Extension
Ω₅ᵀ: TDD-Enhanced Execution (replaces Ω₅ when enabled)
ℜ→ℜᴳ→ℜᶠ: Complete TDD cycle (Red→Green→Refactor)
QA↔DE: Role interaction within Ω₅ᵀ
⟲[method]: Cycle iteration marker

### TDD Sub-phase Symbols
Ω₅ᴿ: RED phase (QA writes failing tests)  
Ω₅ᴳ: GREEN phase (DE minimal implementation)
Ω₅ᶠᵗᵉˢᵗ: Refactor phase for test code
Ω₅ᶠⁱᵐᵖˡ: Refactor phase for implementation code

### TDD State Machine
Ω₅ᵀ.state ∈ [ℜ,ℜᴳ,ℜᶠ]
FLOW: ℜ→ℜᴳ→ℜᶠ→next_cycle
ROLES: ℜ=QA | ℜᴳ=DE | ℜᶠ=QA↔DE

### TDD State Transitions
ENTRY: Ω₅ → Ω₅ᵀ (when σ₅.tdd_cycles exists)
EXIT: Ω₅ᵀ → Ω₆ⱽ (when ALL cycles complete)

#### Cycle Transitions
ℜ→ℜᴳ: WHEN test_fails AND qa_complete
ℜᴳ→ℜᶠ: WHEN test_passes AND de_complete  
ℜᶠ→next_cycle: WHEN refactor_complete AND quality_check
FAIL: ANY_ERROR → STOP + handoff_summary

#### Role Switching
QA_ACTIVE: σ₄.tdd_phase ∈ [ℜ,ℜᶠᵗᵉˢᵗ]
DE_ACTIVE: σ₄.tdd_phase ∈ [ℜᴳ,ℜᶠⁱᵐᵖˡ]
STRICT: QA∧DE_NEVER_CONCURRENT

### TDD Memory Extensions
σ₅.tdd_cycles: [method₁,method₂,...]
σ₄.tdd_phase: current TDD state  
σ₄.current_cycle: active iteration
σ₄.qa_agent_active: boolean
σ₄.de_agent_active: boolean
σ₄.refactor_stage: test|impl|qa_validation|de_validation|qa_cross_review|de_cross_review|interface_check|integration_test (for refactor phase coordination)
σ₄.last_test_result: pass|fail|null

## Master Scheduler Protocol

### Agent Communication Modes
PLAN_AGENTS: session_id only (MCP Memory driven)
TDD_AGENTS: session_id only (MCP Memory driven)

## TDD Dialogue Protocol (Ω₅ᵀ Extension)
SESSION: tdd_session_id→MCP_Memory (per-cycle isolation)
QA↔DE: Communication through MCP observations
SUMMARY: Agent→status→MT decision routing

### TDD MCP Router (Ω₅ᵀ.router)
```
∀cycle ∈ σ₅.tdd_cycles:
├─ INIT: sid=TDD_{timestamp}_C{i}, r=0
├─ STORE: σ₄.tdd_session_id=sid
├─ ADD: OBS[S{sid},R{r},A:MT,T:now]: cycle.task
├─ ⟲[phase]: 
│   ├─ ℜ: DISPATCH: QA[S{sid},R{r},C{i},P:ℜ]→status
│   ├─ ℜᴳ: DISPATCH: DE[S{sid},R{r},C{i},P:ℜᴳ]→status
│   └─ ℜᶠ: r++ → QA[S{sid},R{r},C{i},P:ℜᶠᵗ]→DE[S{sid},R{r},C{i},P:ℜᶠⁱ]
└─ σ₅.progress[i] = ✅
```

### TDD Cycle Execution (Main Thread)
```
TDD_EXECUTE_COMMAND():
├─ VALIDATE: σ₅.tdd_cycles exists
├─ INIT: σ₄.STATE(tdd_mode=true, current_cycle=0)
└─ FOR each cycle IN σ₅.tdd_cycles:
    └─ EXECUTE_RGR_CYCLE(cycle)

EXECUTE_RGR_CYCLE(cycle):
├─ RED_PHASE:
│   ├─ INIT: sid=TDD_{timestamp}_C{i}, r=0
│   ├─ UPDATE: σ₄.STATE(phase=red, tdd_session_id=sid)
│   ├─ ADD: OBS[S{sid},R{r},A:MT,T:now]: cycle.task + phase:RED
│   ├─ DISPATCH: QA[S{sid},R{r},C{i},P:ℜ]
│   ├─ WAIT: status response
│   └─ IF →RC → GREEN_PHASE
├─ GREEN_PHASE:
│   ├─ UPDATE: σ₄.STATE(phase=green)
│   ├─ ADD: OBS[S{sid},R{r},A:MT,T:now]: phase:GREEN
│   ├─ DISPATCH: DE[S{sid},R{r},C{i},P:ℜᴳ]
│   ├─ WAIT: status response
│   └─ IF →GC → REFACTOR_PHASE
└─ REFACTOR_PHASE:
    ├─ UPDATE: σ₄.STATE(phase=refactor), r++
    ├─ ADD: OBS[S{sid},R{r},A:MT,T:now]: phase:REFACTOR
    ├─ SEQUENTIAL_REFACTOR:
    │   ├─ DISPATCH: QA[S{sid},R{r},C{i},P:ℜᶠᵗ]
    │   ├─ WAIT: →RTC
    │   ├─ DISPATCH: DE[S{sid},R{r},C{i},P:ℜᶠⁱ]
    │   ├─ WAIT: →RIC
    │   └─ COLLABORATION_VERIFY:
    │       ├─ RUN: Test suite verification
    │       ├─ CHECK: Code quality review
    │       └─ GATE: All tests pass → continue
    └─ UPDATE: σ₅.progress[cycle] = ✅
```

### TDD Summary States
ℜ_states: →RC|→TA
ℜᴳ_states: →GC|→TI  
ℜᶠ_states: →RTC|→RIC|→RFC
CONVERGE: QA∧DE both report →RFC


### Error Handling & Termination
```
FAILURE_PROTOCOLS:
├─ AGENT_FAILURE:
│   ├─ LOG: Error details in σ₅.progress
│   ├─ CAPTURE: Current state snapshot
│   ├─ CREATE: Handoff summary for σ₄
│   └─ EXIT: Ω₅ᵀ → Ω₆ⱽ with FAILED status
├─ TEST_FAILURE:
│   ├─ ANALYZE: Root cause (QA vs DE issue)
│   ├─ REPORT: Issue classification  
│   └─ TERMINATE: No retry mechanism
└─ QUALITY_FAILURE:
    ├─ DOCUMENT: Quality gate that failed
    ├─ PRESERVE: Current implementation state
    └─ HANDOFF: To manual review (Ω₆ᵛ)

TERMINATION_PROCEDURE:
├─ UPDATE: σ₄.tdd_mode = false
├─ CLEAR: Agent activation flags
├─ SUMMARY: Create failure analysis
├─ HANDOFF: Prepare σ₄ for next mode
└─ TRANSITION: σ₄.Ω_current → Ω₆ⱽ
```

### Quality Gates
```
CYCLE_VALIDATION_GATES:
├─ RED_GATE:
│   ├─ Tests written ✅
│   ├─ Tests failing ✅ 
│   └─ Test quality meets Ψ standards ✅
├─ GREEN_GATE:
│   ├─ Tests passing ✅
│   ├─ Minimal implementation ✅
│   └─ No test modifications ✅
└─ REFACTOR_GATE:
    ├─ All tests still passing ✅
    ├─ Code quality improved ✅
    ├─ Interface consistency ✅
    ├─ QA refactor: Test code optimized ✅
    ├─ DE refactor: Implementation optimized ✅
    ├─ Collaboration: Code review completed ✅
    ├─ Verification: Test suite fully passes ✅
    └─ Ready for next cycle ✅
```

## Session Terminology
Ω_session: Agent lifecycle identifier (persists across modes)
session_id: MCP Memory dialogue session (Plan↔Critic conversation)
tdd_session_id: MCP Memory dialogue session (QA↔DE per cycle)

## Symbol System
Ω[Modes]: Ω₁ᴾ=CC-Plan, Ω₂ᴬ=Arch-Critic(Λ₁|Λ₂), Ω₃ᴾ=Plan, Ω₄ᶜ=Plan-Critic, Ω₅ᵀ=TDD-Execute, Ω₆ⱽ=Review
  └─ TDD-Phases: Ω₅ᴿ=RED, Ω₅ᴳ=GREEN, Ω₅ᶠ=REFACTOR
σ[Memory]: σ₁=Brief, σ₂=Patterns, σ₃=Tech, σ₄=Context/State, σ₅=Progress, σ₆=Protection
Γ[Perms]: Γ₁=Files, Γ₂=Folders, Γ₃=Code, Γ₄=Commands, Γ₅=Modify, Γ₆=Web
Ψ[Guard]: Ψ₁₋₃=low-risk(proceed), Ψ₄₋₆=high-risk(caution)
Λ[Audit]: Λ₁=Architecture-Level, Λ₂=Module-Level(LLD)
S[Session]: S_p=plan-session(session_id), S_t=tdd-session(tdd_session_id)
∇[Decision]: ACCEPT|REVISE|REJECT; →[Flow], ↔[Interact], ⟷[Loop], ⟲[Iterate]
Logic: ∈(member), ∃(exists), ∧(AND), ∨(OR), ¬(NOT)
Status: ✅(success), ❌(failure), ⚠️(warning), 🔄(processing)