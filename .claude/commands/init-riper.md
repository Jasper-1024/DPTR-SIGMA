---
description: "Initialize TDD-RIPER framework: memory-bank + CLAUDE.md via session-based orchestration"
allowed-tools: Read, Write, Edit, MultiEdit, LS, Bash, Glob, Grep, WebSearch, WebFetch, TodoWrite, Task
version: "3.0"
---

# RIPER Initialization Command v3.0

Use 4-Opus model, if Opus model is not available, this command will fallback to Sonnet for reliable performance.

**ultrathink** - Session-based atomic task framework with MCP Memory data flow. 8-stage dependency-driven execution with minimal context usage. Scales 28-55 tasks based on project complexity.

Initialize complete TDD-RIPER framework: memory-bank files + project-level CLAUDE.md integration.

## Session-Based Execution Framework

**Zero-Assumption Principle**: No pre-existing project structure, documentation, or configuration assumptions.

### 📊 Session Protocol
```
σ_session = "RIPER_{timestamp}"
Templates: MCP["RIPER_TEMPLATES"]  
Task Data: MCP[σ_session + "_" + task_id]
State: MCP[σ_session + "_STATE"]
```

### 📊 Task Distribution
**Base Tasks**: 25 fixed tasks
**Module Tasks**: 3 × N (N = confirmed modules)  
**Total Range**: 28-55 tasks

### 🔄 Execution Stages

**R-1: Template Initialization** `[1 task]`
- T00: INIT_TEMPLATES → Template Manager Agent → MCP["RIPER_TEMPLATES"]
  └─ `INIT[∅→MCP_TEMPLATES]`

**R0: Project Foundation Scan** `[1 task]`
- T01: COMPREHENSIVE_SCAN → Complete project scan (files + configs + classifications + docs)
  └─ `SCN[∅→M01]`
  └─ Output includes: {file_inventory, config_files, file_classifications, documentation}

**R1: Technology Stack Analysis** `[3 tasks]`
- T02: ANALYZE_TECH_STACK → Parse configs + infer complete technology stack
  └─ `ANZ[M01,F(*)→M02]`
- T03: GENERATE_TECH_CONTEXT → Create techContext.md
  └─ `GEN[M02,τ₃→σ₃]`
- T04: VALIDATE_TECH_CONTEXT → Verify σ₃ quality and completeness
  └─ `VAL[σ₃,M02→σ₃,M04]`

**R2: Project Information Extraction** `[4 tasks]`  
- T05: EXTRACT_PROJECT_INFO → Gather project metadata from all sources
  └─ `ANZ[M01,F(README.md,package.json)→M05]`
- T06: INFER_PROJECT_PURPOSE → Determine project type and objectives
  └─ `ANZ[M05→M06]`
- T07: GENERATE_PROJECT_BRIEF → Create projectbrief.md
  └─ `GEN[M05,M06,τ₁→σ₁]`
- T08: VALIDATE_PROJECT_BRIEF → Verify σ₁ quality and completeness
  └─ `VAL[σ₁,M06→σ₁,M08]`

**R3: Code Architecture Analysis** `[6 tasks]`
- T09: SCAN_CODE_STRUCTURE → Directory patterns + naming conventions + import analysis
  └─ `SCN[M01,F(src/*)→M09]`
  └─ Output includes: {code_organization, naming_patterns, imports_dependencies}
- T10: BUILD_DEPENDENCY_GRAPH → File interdependency mapping
  └─ `ANZ[M09→M10]`
- T11: CLASSIFY_ARCHITECTURE → Directory patterns + code patterns + architecture classification
  └─ `ANZ[M09,M10→M11]`
  └─ Output includes: {directory_patterns, code_patterns, architecture_type}
- T12: ANALYZE_INTERFACES → Entry points + public API surface analysis
  └─ `ANZ[M10,F(index.*,main.*,app.*,routes/*,api/*)→M12]`
  └─ Output includes: {entry_points, public_interfaces}
- T13: GENERATE_SYSTEM_PATTERNS_ARCH → Create systemPatterns.md (architecture only)
  └─ `GEN[M09-12,τ₂→σ₂]`
- T14: VALIDATE_SYSTEM_PATTERNS → Verify σ₂ architecture accuracy and completeness
  └─ `VAL[σ₂,M11→σ₂,M14]`

**R4: Module Identification & User Confirmation** `[7 tasks]`
- T15: IDENTIFY_FUNCTIONAL_MODULES → Business logic based grouping
  └─ `ANZ[M10,M11→M15]`
- T16: IDENTIFY_STRUCTURAL_MODULES → Structure boundary based grouping
  └─ `ANZ[M09,M11→M16]`
- T17: MERGE_MODULE_CANDIDATES → Consolidate overlapping candidates
  └─ `ANZ[M15,M16→M17]`
- T18: REFINE_MODULE_BOUNDARIES → Optimize size and responsibility
  └─ `ANZ[M17→M18]`
- T19: FORMAT_MODULE_PRESENTATION → User-friendly display format
  └─ `ANZ[M18→M19]`
- T20: 👤USER_CONFIRM_MODULES → Interactive module confirmation
  └─ `USER[M19→U20]`
- T21: PROCESS_MODULE_FEEDBACK → Apply complete user module feedback + update systemPatterns.md (preserve all user requirements)
  └─ `PRC[M19,U20→σ₂,M21]`

**R5: Module Detailed Design** `[3×N tasks where N = confirmed modules]`
∀μ ∈ modules:
- T22: MODULE_FULL_ANALYSIS → Comprehensive module analysis (responsibilities + interfaces + data + errors)
  └─ `ANZ[M21,F(@μ/*)→M22μ]`
  └─ Output includes: {responsibilities, public_interfaces, data_structures, error_strategies}
- T23: GENERATE_MODULE_DESIGN → Create design.md
  └─ `GEN[M22μ,τ_module→@μ/design.md]`
- T24: VALIDATE_MODULE_DESIGN → Verify module quality and LLD compliance
  └─ `VAL[@μ/design.md,M21→@μ/design.md,M24μ]`

**R6: Auxiliary Memory-Bank Files** `[9 tasks]`
- T25: ANALYZE_ACTIVE_CONTEXT → Analyze current state and focus
  └─ `ANZ[M21,σ₂→M25]`
- T26: GENERATE_ACTIVE_CONTEXT → Create activeContext.md
  └─ `GEN[M25,τ₄→σ₄]`
- T27: VALIDATE_ACTIVE_CONTEXT → Verify σ₄ completeness
  └─ `VAL[σ₄,M25→σ₄,M27]`
- T28: ANALYZE_PROGRESS → Calculate completion status
  └─ `ANZ[M21,M24*→M28]`
- T29: GENERATE_PROGRESS → Create progress.md
  └─ `GEN[M28,τ₅→σ₅]`
- T30: VALIDATE_PROGRESS → Verify σ₅ accuracy
  └─ `VAL[σ₅,M28→σ₅,M30]`
- T31: ANALYZE_PROTECTION → Identify protected regions
  └─ `ANZ[σ₁,σ₂→M31]`
- T32: GENERATE_PROTECTION → Create protection.md
  └─ `GEN[M31,τ₆→σ₆]`
- T33: VALIDATE_PROTECTION → Verify σ₆ validity
  └─ `VAL[σ₆,M31→σ₆,M33]`

**R7: Project Configuration Files** `[6 tasks]`
- T34: EXTRACT_COMMANDS → Identify build/test/run commands
  └─ `ANZ[M02,F(package.json,Makefile)→M34]`
- T35: DEFINE_CONSTRAINTS → Project-specific constraints
  └─ `ANZ[σ₂,σ₆→M35]`
- T36: GENERATE_CLAUDE_MD → Create project CLAUDE.md
  └─ `GEN[M34,M35,τ_claude→CLAUDE.md]`
- T37: VALIDATE_CLAUDE_MD → Verify CLAUDE.md completeness
  └─ `VAL[CLAUDE.md,M35→CLAUDE.md,M37]`
- T38: GENERATE_SYMBOLS → Create symbols.md reference
  └─ `GEN[τ_symbols→symbols.md]`
- T39: VALIDATE_SYMBOLS → Verify symbols.md accuracy
  └─ `VAL[symbols.md→symbols.md,M39]`

## Execution Framework

### 📡 Task Instruction Protocol

**Symbolic instruction format:** `T{id}:{OP}[{inputs}→{outputs}]`

**Operations:**
- `SCN`: Scan - Project scanning
- `ANZ`: Analyze - Data analysis
- `GEN`: Generate - File generation
- `VAL`: Validate - Validation/fix
- `PRC`: Process - Data processing

**Input/Output Symbols:**
- `M{NN}`: MCP node T{NN} (e.g., M05 = σ_session + "_T05")
- `σ{N}`: Memory-bank file (σ₁=projectbrief, σ₂=systemPatterns, σ₃=techContext, etc.)
- `τ{N}`: Template (τ₁=sigma1, τ₂=sigma2, τ₃=sigma3, etc.)
- `@μ/*`: Module files (@modules/*/design.md)
- `F(*)`: Project files (package.json, README.md, etc.)
- `∅`: No dependencies
- `U{NN}`: User input from T{NN} → stored in MCP[σ_session + "_USER_T{NN}"]

**Examples:**
```
T01:SCN[∅→M01]                   # Comprehensive scan, no deps, output to MCP
T02:ANZ[M01,F(*)→M02]            # Analyze tech stack from scan + files  
T03:GEN[M02,τ₃→σ₃]               # Generate σ₃ from T02 and template
T04:VAL[σ₃,M02→σ₃,M04]           # Validate σ₃ against M02, may fix σ₃
T09:SCN[M01,F(src/*)→M09]        # Scan code structure from M01 + source files
T13:GEN[M09-12,τ₂→σ₂]            # Generate σ₂ from T09-T12 analysis
T21:PRC[M19,U20→σ₂,M21]          # Process user feedback, update σ₂
```

### 🤖 Agent Assignment

**Template Manager**: T00 → Initialize templates to MCP["RIPER_TEMPLATES"]

**Generator Agent** (instruction, σ_session):
- Tasks: T01, T02, T05-T07, T09-T13, T15-T19, T22-T23, T25-T26, T28-T29, T31-T32, T34-T36, T38
- Input: Symbolic instruction (e.g., "T01:SCN[∅→M01]", "T09:SCN[M01,F(src/*)→M09]")
- Output: memory-bank/*.md + MCP[σ_session + "_" + task_id]

**Validator Agent** (instruction, σ_session):
- Tasks: T04, T08, T14, T21, T24+, T27, T30, T33, T37, T39
- Input: Symbolic instruction (e.g., "T04:VAL[σ₃,M02→σ₃,M04]")
- Output: Validation results + corrections

**Main Thread**: T20 (user interaction) + orchestration

### 📋 Dependency Control

**Stage Dependencies**: Strict serial execution R0→R1→R2→R3→R4→R5→R6→R7
**Task Dependencies**: Within-stage tasks may have dependencies
**Parallel Opportunities**:
- R5: Module tasks can run in parallel (max 3 concurrent)  
- R6: Three auxiliary files can be processed in parallel

### ⚡ Error Handling

**Critical Tasks**: `[T04, T08, T14, T21, T36]` → Failure terminates execution
**Retry Tasks**: `[T02, T10, T11, T24+ series]` → Failure triggers 3 retries  
**Degrade Tasks**: `[T31]` → Failure allows graceful degradation

### 💾 State Management

**Session State**: Stored in MCP[σ_session + "_STATE"]  
**Task Results**: Stored in MCP[σ_session + "_" + task_id]  
**User Interactions**: Stored in MCP[σ_session + "_USER_" + task_id]  
**No .riper-execution.json file** - all state in MCP Memory

## Data Flow Protocol

**Agent-MCP Memory**: Agents read dependencies from MCP, write results to MCP  
**File Generation**: GENERATE tasks write to memory-bank/*.md  
**User Interaction Storage**: Main Thread stores user feedback in MCP[σ_session + "_USER_T{NN}"]  
**State Management**: All intermediate data in MCP Memory

### Dependency Resolution

```
TASK_DEPENDENCIES = {
  "T02": ["T01"],
  "T03": ["T02"],
  "T04": ["T03"],
  "T06": ["T05"],
  "T07": ["T05", "T06"],
  "T08": ["T07"],
  "T10": ["T09"],
  "T11": ["T09", "T10"],
  "T12": ["T10"],
  "T13": ["T09", "T10", "T11", "T12"],
  "T14": ["T13"],
  "T21": ["T19", "T20"],
  "T24+": ["T23+ per module"],
  "T28": ["T21", "T24*"],
}
```