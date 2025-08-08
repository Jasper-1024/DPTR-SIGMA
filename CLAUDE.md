# RIPER·Σ Core Protocol

## Modes & Permissions
Ω₁ᴾ: CC PLAN MODE (Γ₁₋₃,₆) - architecture & module design
Ω₂ᴬ: ARCH CRITIC (review only) - design quality validation  
Ω₃ᴾ: SPECIFY (exact plans) - implementation planning
Ω₄ᶜ: PLAN CRITIC (review only) - execution feasibility validation
Ω₅ᵀ: EXECUTE (TDD cycles) - implementation with testing
Ω₆ⱽ: VALIDATE (no fix) - final quality verification

## State Machine
σ₄.Ω_current ∈ [Ω₁ᴾ,Ω₂ᴬ,Ω₃ᴾ,Ω₄ᶜ,Ω₅ᵀ,Ω₆ⱽ]
FLOW: Ω₁ᴾ→Ω₂ᴬ↑↓→Ω₃ᴾ→Ω₄ᶜ↑↓→Ω₅ᵀ→Ω₆ⱽ
ENFORCE: current==agent_mode

## Memory Protocol
σ₁: brief | σ₂: patterns | σ₃: tech
σ₄: context+STATE | σ₅: progress | σ₆: protection

## Handoff Protocol
EXIT: /handoff→σ₄{to:Ω_next,summary}
ENTRY: CHECK(σ₄.Ω_current==my_mode)

## Protection Levels
Ψ₁-₃: proceed | Ψ₄-₆: caution+confirm

## Commands
/plan=Ω₁ᴾ /arch-critic=Ω₂ᴬ /p=Ω₃ᴾ /plan-critic=Ω₄ᶜ /tdd-execute=Ω₅ᵀ /rev=Ω₆ⱽ
/tdd-execute=Ω₅ᵀ (TDD-Enhanced Execution Mode)

## Cross-Reference Notation
[↗️σₓ:Rₓ] = Reference to memory file section
Γ₁=Files Γ₂=Folders Γ₃=Code Γ₄=Commands Γ₅=Modify Γ₆=Web

## Session Protocol
SESSION: @σ₄.Ω_session (maintained across modes)
LOCK: σ₄.locked_by (prevent concurrent updates)

## CC Plan Mode Integration
Ω₁ᴾ: CC Plan Mode (replaces original Ω₁+Ω₂)
TRIGGER: User uses CC native Plan Mode
OUTPUT: Direct to memory bank
  ├─ σ₂.architecture_design (overall architecture)
  ├─ σ₂.module_specifications (module details)
  └─ σ₂.tech_stack (technology choices)
HANDOFF: Automatic transition to Ω₂ᴬ for design audit

## Dual Loop Protocol

### Design Quality Loop (Ω₁ᴾ ↔ Ω₂ᴬ)
DESIGN_LOOP: Ω₁ᴾ → Ω₂ᴬ audit → σ₄.arch_critique → decision
DECISION: 
├─ APPROVED → UPDATE σ₄.design_approved=true → Ω₃ᴾ
└─ REVISION → σ₄.design_feedback → re-enter Ω₁ᴾ
ITERATIONS: Individual developer optimized (avoid over-engineering)

### Plan Quality Loop (Ω₃ᴾ ↔ Ω₄ᶜ)  
PLAN_LOOP: Ω₃ᴾ → Ω₄ᶜ audit → σ₄.plan_critique → decision
DECISION:
├─ FEASIBLE → UPDATE σ₄.plan_approved=true → Ω₅ᵀ
└─ ADJUSTMENT → σ₄.plan_feedback → modify in Ω₃ᴾ
ITERATIONS: Reality-based assessment for personal projects

## TDD Protocol Extension
Ω₅ᵀ: TDD-Enhanced Execution (replaces Ω₅ᵀ when enabled)
ℜ→ℜᴳ→ℜᶠ: Complete TDD cycle (Red→Green→Refactor)
QA∨DE: Role alternation within Ω₅ᵀ
⟲[method]: Cycle iteration marker

### TDD Sub-phase Symbols
Ω₅ᵀᴿ: RED phase (QA writes failing tests)  
Ω₅ᵀᴳ: GREEN phase (DE minimal implementation)
Ω₅ᵀᶠᵗᵉˢᵗ: Refactor phase for test code
Ω₅ᵀᶠⁱᵐᵖˡ: Refactor phase for implementation code

### TDD State Machine
Ω₅ᵀ.state ∈ [ℜ,ℜᴳ,ℜᶠ]
FLOW: ℜ→ℜᴳ→ℜᶠ→next_cycle
ROLES: ℜ=QA | ℜᴳ=DE | ℜᶠ=QA∨DE

### TDD State Transitions
ENTRY: Ω₅ᵀ → Ω₅ᵀ (when σ₂.tdd_cycles exists)
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
σ₂.tdd_cycles: [method₁,method₂,...]
σ₄.tdd_phase: current TDD state  
σ₄.current_cycle: active iteration
σ₄.qa_agent_active: boolean
σ₄.de_agent_active: boolean
σ₄.refactor_stage: test|impl|qa_validation|de_validation|qa_cross_review|de_cross_review|interface_check|integration_test (for refactor phase coordination)
σ₄.last_test_result: pass|fail|null

## Master Scheduler Protocol

### Agent Dispatch Protocol
```
Master Scheduler → Sub-Agent Transfer Protocol:
{
  plan_step: σ₂.tdd_cycles[i],            // Specific plan in memory-bank
  quality_rules: @agent-tdd-*.md#rules,   // Reference to quality rules
  context: σ₄.current_context,            // Current context state
  cycle_phase: σ₄.STATE.tdd_phase         // RGR phase identifier
}
```

### TDD Cycle Execution Flow
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
  │   └─ Sequential_Validation∨✓(qa_validation + de_validation + cross_review + integration_test)
  │   }
  └─ UPDATE σ₅.progress[i] = ✓
```

### Refactor Collaboration Flow
```
ℜᶠ.flow: QA∨ℜᶠᵗᵉˢᵗ → DE∨ℜᶠⁱᵐᵖˡ → QA_validation → DE_validation → Cross_Review → Integration_Test → next_cycle

Sequential_Validation.sequence:
├─ QA_validation: QA validates refactored test quality (QA_active, DE_inactive)
├─ DE_validation: DE validates refactored implementation quality (QA_inactive, DE_active)
├─ QA_cross_review: QA reviews DE's implementation changes (QA_active, DE_inactive)
├─ DE_cross_review: DE reviews QA's test changes (QA_inactive, DE_active)
├─ interface_check: Automated interface consistency validation (both_inactive)
├─ integration_test: Complete test suite execution (both_inactive)
└─ commit_ready: Quality standards met, proceed to next cycle
```

## TDD Master Scheduler Implementation

### TDD Execute Command
`/tdd-execute` - Initiates TDD-Enhanced Execution Mode

PREREQUISITES:
- σ₂.tdd_cycles must exist (from Ω₃ Plan Agent)
- σ₄.Ω_current must be Ω₄ or transitioning to Ω₄ᵀ

### Scheduler Execution Logic
```
TDD_SCHEDULER_MAIN():
├─ VALIDATE: σ₂.tdd_cycles exists
├─ INIT: σ₄.STATE(tdd_mode=true, current_cycle=0, tdd_phase="red")
├─ FOR cycle_index IN σ₂.tdd_cycles:
│   ├─ EXECUTE_RGR_CYCLE(cycle_index)
│   └─ IF FAILURE → TERMINATE(error_summary)
└─ COMPLETE: σ₄.Ω_current → Ω₅

EXECUTE_RGR_CYCLE(i):
├─ RED_PHASE(i):
│   ├─ UPDATE: σ₄.STATE(current_cycle=i, phase="red", qa_agent_active=true)
│   ├─ DISPATCH: riper-tdd-qa-agent with context={
│   │     plan_step: σ₂.tdd_cycles[i],
│   │     context: σ₄.current_context,
│   │     cycle_phase: "red"
│   │   }
│   ├─ WAIT: Agent completion or failure
│   ├─ VALIDATE: Tests written and failing
│   └─ IF SUCCESS → GREEN_PHASE(i) ELSE → TERMINATE
├─ GREEN_PHASE(i):
│   ├─ UPDATE: σ₄.STATE(phase="green", qa_agent_active=false, de_agent_active=true)
│   ├─ DISPATCH: riper-tdd-de-agent with context={
│   │     plan_step: σ₂.tdd_cycles[i],
│   │     context: σ₄.current_context,
│   │     cycle_phase: "green"
│   │   }
│   ├─ WAIT: Agent completion or failure
│   ├─ VALIDATE: Tests passing with minimal implementation
│   └─ IF SUCCESS → REFACTOR_PHASE(i) ELSE → TERMINATE
└─ REFACTOR_PHASE(i):
    ├─ UPDATE: σ₄.STATE(phase="refactor")
    ├─ SEQUENTIAL_REFACTOR_DISPATCH:
    │   ├─ STEP_1_QA_TEST_REFACTOR:
    │   │   ├─ UPDATE: σ₄.STATE(qa_agent_active=true, de_agent_active=false, refactor_stage="test")
    │   │   ├─ DISPATCH: riper-tdd-qa-agent with context={
    │   │   │     plan_step: σ₂.tdd_cycles[i],
    │   │   │     cycle_phase: "refactor",
    │   │   │     refactor_focus: "test_code",
    │   │   │     quality_rules: Ψ_quality_rules
    │   │   │   }
    │   │   ├─ WAIT: QA test refactoring completion
    │   │   ├─ VALIDATE: Test refactoring complete, logic preserved
    │   │   └─ IF FAILURE → TERMINATE
    │   ├─ STEP_2_DE_IMPL_REFACTOR:
    │   │   ├─ UPDATE: σ₄.STATE(qa_agent_active=false, de_agent_active=true, refactor_stage="impl")
    │   │   ├─ DISPATCH: riper-tdd-de-agent with context={
    │   │   │     plan_step: σ₂.tdd_cycles[i],
    │   │   │     cycle_phase: "refactor",
    │   │   │     refactor_focus: "implementation_code",
    │   │   │     quality_rules: Ψ_quality_rules
    │   │   │   }
    │   │   ├─ WAIT: DE implementation refactoring completion
    │   │   ├─ VALIDATE: Code refactoring complete, behavior preserved
    │   │   └─ IF FAILURE → TERMINATE
    │   └─ STEP_3_COLLABORATION_VALIDATION:
    │       ├─ STEP_3A_QA_VALIDATION:
    │       │   ├─ UPDATE: σ₄.STATE(qa_agent_active=true, de_agent_active=false, refactor_stage="qa_validation")
    │       │   ├─ DISPATCH: riper-tdd-qa-agent with context={
    │       │   │     plan_step: σ₂.tdd_cycles[i],
    │       │   │     cycle_phase: "collaboration_qa_review",
    │       │   │     validation_focus: "test_quality_and_coverage"
    │       │   │   }
    │       │   ├─ QA_TASKS:
    │       │   │   ├─ VERIFY: Tests still validate correct business logic
    │       │   │   ├─ CHECK: Test coverage maintained or improved
    │       │   │   └─ CONFIRM: Refactored tests can still detect bugs
    │       │   └─ IF FAILURE → TERMINATE
    │       ├─ STEP_3B_DE_VALIDATION:
    │       │   ├─ UPDATE: σ₄.STATE(qa_agent_active=false, de_agent_active=true, refactor_stage="de_validation")
    │       │   ├─ DISPATCH: riper-tdd-de-agent with context={
    │       │   │     plan_step: σ₂.tdd_cycles[i],
    │       │   │     cycle_phase: "collaboration_de_review",
    │       │   │     validation_focus: "implementation_quality_and_behavior"
    │       │   │   }
    │       │   ├─ DE_TASKS:
    │       │   │   ├─ VERIFY: Implementation behavior unchanged
    │       │   │   ├─ CHECK: Code quality improved (naming, structure, performance)
    │       │   │   └─ CONFIRM: All improvement opportunities handled
    │       │   └─ IF FAILURE → TERMINATE
    │       ├─ STEP_3C_CROSS_REVIEW:
    │       │   ├─ QA_CROSS_REVIEW:
    │       │   │   ├─ UPDATE: σ₄.STATE(qa_agent_active=true, de_agent_active=false, refactor_stage="qa_cross_review")
    │       │   │   ├─ TASK: Review DE's implementation changes for test compatibility
    │       │   │   └─ IF FAILURE → TERMINATE
    │       │   ├─ DE_CROSS_REVIEW:
    │       │   │   ├─ UPDATE: σ₄.STATE(qa_agent_active=false, de_agent_active=true, refactor_stage="de_cross_review")
    │       │   │   ├─ TASK: Review QA's test changes for implementation alignment
    │       │   │   └─ IF FAILURE → TERMINATE
    │       │   └─ INTERFACE_CHECK:
    │       │       ├─ UPDATE: σ₄.STATE(qa_agent_active=false, de_agent_active=false, refactor_stage="interface_check")
    │       │       └─ AUTOMATED: Interface design consistency validation
    │       ├─ STEP_3D_INTEGRATION_TEST:
    │       │   ├─ UPDATE: σ₄.STATE(qa_agent_active=false, de_agent_active=false, refactor_stage="integration_test")
    │       │   └─ AUTOMATED_TASKS:
    │       │       ├─ ∀tests_pass: Run complete test suite ✓
    │       │       ├─ interface_check: Interface design consistency ✓
    │       │       └─ commit_ready: Quality standards met ✓
    │       └─ CYCLE_COMPLETION:
    │           ├─ UPDATE: σ₅.progress[i] = ✓
    │           ├─ UPDATE: σ₄.STATE(qa_agent_active=false, de_agent_active=false)
    │           └─ IF ALL_GATES_PASS → next_cycle ELSE → TERMINATE
```

### Agent Dispatch Mechanism
```
DISPATCH_AGENT(agent_name, context_data):
├─ LOCK: σ₄.locked_by = agent_name
├─ PREPARE: Agent context package
├─ LAUNCH: @agent_name with context_data
├─ MONITOR: Agent execution
├─ HANDLE: Success/Failure response
└─ UNLOCK: σ₄.locked_by = null

Context Package Structure:
{
  current_cycle: σ₄.current_cycle,
  cycle_method: σ₂.tdd_cycles[current_cycle],
  tdd_phase: σ₄.tdd_phase,
  project_context: σ₄.current_context,
  quality_rules: @agent-tdd-*.md#constraints,
  memory_state: {σ₁, σ₂, σ₃, σ₄, σ₅, σ₆}
}
```

### Error Handling & Termination
```
FAILURE_PROTOCOLS:
├─ AGENT_FAILURE:
│   ├─ LOG: Error details in σ₅.progress
│   ├─ CAPTURE: Current state snapshot
│   ├─ CREATE: Handoff summary for σ₄
│   └─ EXIT: Ω₄ᵀ → Ω₅ with FAILED status
├─ TEST_FAILURE:
│   ├─ ANALYZE: Root cause (QA vs DE issue)
│   ├─ REPORT: Issue classification  
│   └─ TERMINATE: No retry mechanism
└─ QUALITY_FAILURE:
    ├─ DOCUMENT: Quality gate that failed
    ├─ PRESERVE: Current implementation state
    └─ HANDOFF: To manual review (Ω₅)

TERMINATION_PROCEDURE:
├─ UPDATE: σ₄.tdd_mode = false
├─ CLEAR: Agent activation flags
├─ SUMMARY: Create failure analysis
├─ HANDOFF: Prepare σ₄ for next mode
└─ TRANSITION: σ₄.Ω_current → Ω₅
```

### Quality Gates
```
CYCLE_VALIDATION_GATES:
├─ RED_GATE:
│   ├─ Tests written ✓
│   ├─ Tests failing ✓ 
│   └─ Test quality meets Ψ standards ✓
├─ GREEN_GATE:
│   ├─ Tests passing ✓
│   ├─ Minimal implementation ✓
│   └─ No test modifications ✓
└─ REFACTOR_GATE:
    ├─ All tests still passing ✓
    ├─ Code quality improved ✓
    ├─ Interface consistency ✓
    └─ Ready for next cycle ✓
```