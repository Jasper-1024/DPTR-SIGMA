# RIPER·Σ Core Protocol v1

## Modes & Permissions
Ω₁·R: READ-ONLY (Γ₁₋₃,₆)
Ω₂·I: IDEATE (no code)
Ω₃·P: SPECIFY (exact plans)
Ω₄·E: EXECUTE (plan only)
  Ω₄ₐ·QA: TEST-FIRST (ρ phase)
  Ω₄ᵦ·DE: IMPLEMENT (γ,ρᵣ phases)
Ω₅·V: VALIDATE (no fix)

## State Machine
σ₄.Ω_current ∈ [Ω₁..Ω₅] | [Ω₄ₐ,Ω₄ᵦ]
FLOW: Ω₁→Ω₂→Ω₃→Ω₄→Ω₅
TDD_FLOW: Ω₄ₐ(ρ)→Ω₄ᵦ(γ)→Ω₄ᵦ(ρᵣ)
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
/r=Ω₁ /i=Ω₂ /p=Ω₃ /e=Ω₄ /rev=Ω₅
/qa=Ω₄ₐ /de=Ω₄ᵦ /tdd=TDD_mode

## Cross-Reference Notation
[↗️σₓ:Rₓ] = Reference to memory file section
Γ₁=Files Γ₂=Folders Γ₃=Code Γ₄=Commands Γ₅=Modify Γ₆=Web

## Session Protocol
SESSION: @σ₄.Ω_session (maintained across modes)
LOCK: σ₄.locked_by (prevent concurrent updates)

## TDD Protocol
Φ₀: PREPARE | Φ₁: RGR_CYCLE | Φ₂: EXPAND
ρ: RED→fail | γ: GREEN→pass | ρᵣ: REFACTOR→improve
τ₁: TEST_FIRST | τ₂: MIN_IMPL | τ₃: NO_BEHAV
δ: HALT_DEV | θ: FOCUS_ONE

### RGR Cycle: ρ→γ→ρᵣ
ρ(Ω₄ₐ): WRITE failing test
γ(Ω₄ᵦ): MINIMAL implementation  
ρᵣ(Ω₄ᵦ): REFACTOR structure
STRICT: no skip, no reverse, δ on deviation