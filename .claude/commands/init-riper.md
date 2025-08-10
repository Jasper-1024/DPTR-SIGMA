---
description: "Initialize TDD-RIPER framework: memory-bank + CLAUDE.md via session-based orchestration"
allowed-tools: Read, Write, Edit, MultiEdit, LS, Bash, Glob, Grep, WebSearch, WebFetch, TodoWrite, Task
version: "3.0"
---

# RIPER Initialization Command v3.0

Use 4-Opus model, if Opus model is not available, this command will fallback to Sonnet for reliable performance.

**ultrathink** - Session-based atomic task framework with MCP Memory data flow. 8-stage dependency-driven execution with minimal context usage. Scales 50-110 tasks based on project complexity.

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
**Base Tasks**: 44 fixed tasks
**Module Tasks**: 6 × N (N = confirmed modules)  
**Total Range**: 50-110 tasks

### 🔄 Execution Stages

**R-1: Template Initialization** `[1 task]`
- T00: INIT_TEMPLATES → Template Manager Agent → MCP["RIPER_TEMPLATES"]
  └─ `INIT[∅→MCP_TEMPLATES]`

**R0: Project Foundation Scan** `[4 tasks]`
- T01: SCAN_PROJECT → Complete file/directory inventory + project type detection
  └─ `SCN[∅→M01]`
- T02: DETECT_CONFIGS → Configuration file presence mapping
  └─ `DETECT[M01→M02]`
- T03: CLASSIFY_FILES → File type classification by extension
  └─ `SCN[M01→M03]`
- T04: DETECT_DOCS → Documentation and special directories
  └─ `DETECT[M01→M04]`

**Project Type Detection** (part of T01):
```python
PROJECT_TYPE_INDICATORS = {
    "webapp": ["index.html", "app.js", "package.json", "src/components"],
    "api": ["routes/", "controllers/", "no frontend files"],
    "cli": ["bin/", "cli.js", "commander|yargs in package.json"],
    "library": ["index.js", "lib/", "no executable entry"],
    "microservices": ["services/", "docker-compose.yml", "multiple packages"],
    "monorepo": ["packages/", "lerna.json", "workspaces in package.json"]
}
```

**R1: Technology Stack Analysis** `[4 tasks]`
- T05: PARSE_CONFIGS → Extract dependencies from detected configs
  └─ `ANZ[M02,F(*)→M05]`
- T06: INFER_TECH_STACK → Deduce complete technology stack
  └─ `ANZ[M05→M06]`
- T07: GENERATE_TECH_CONTEXT → Create techContext.md
  └─ `GEN[M05,M06,τ₃→σ₃]`
- T08: VALIDATE_TECH_CONTEXT → Verify σ₃ quality and completeness
  └─ `VAL[σ₃,M06→σ₃,M08]`

**R2: Project Information Extraction** `[4 tasks]`  
- T09: EXTRACT_PROJECT_INFO → Gather project metadata from all sources
  └─ `ANZ[M02,F(README.md,package.json)→M09]`
- T10: INFER_PROJECT_PURPOSE → Determine project type and objectives
  └─ `ANZ[M09→M10]`
- T11: GENERATE_PROJECT_BRIEF → Create projectbrief.md
  └─ `GEN[M09,M10,τ₁→σ₁]`
- T12: VALIDATE_PROJECT_BRIEF → Verify σ₁ quality and completeness
  └─ `VAL[σ₁,M10→σ₁,M12]`

**R3: Code Architecture Analysis** `[11 tasks]`
- T13: SCAN_CODE_ORGANIZATION → Directory patterns and file distribution
  └─ `SCN[M01→M13]`
- T14: ANALYZE_NAMING_CONVENTIONS → Code style and naming patterns
  └─ `ANZ[M03,F(src/*)→M14]`
- T15: EXTRACT_IMPORTS_DEPENDENCIES → All dependency declarations
  └─ `ANZ[F(src/*)→M15]`
- T16: BUILD_DEPENDENCY_GRAPH → File interdependency mapping
  └─ `ANZ[M15→M16]`
- T17a: SCAN_DIRECTORY_PATTERNS → Scan directory structure patterns (controllers/, models/, services/)
  └─ `SCN[M01→M17a]`
- T17b: ANALYZE_CODE_PATTERNS → Analyze code organization patterns (imports, class hierarchies)
  └─ `ANZ[M15,M16→M17b]`
- T17c: CLASSIFY_ARCHITECTURE → Classify architecture based on T17a and T17b results
  └─ `ANZ[M17a,M17b→M17c]`
- T18: IDENTIFY_ENTRY_POINTS → Application entry points and interfaces
  └─ `ANZ[F(index.*,main.*,app.*)→M18]`
- T19: ANALYZE_PUBLIC_INTERFACES → External API surface analysis
  └─ `ANZ[M18,F(routes/*,api/*)→M19]`
- T20: GENERATE_SYSTEM_PATTERNS_ARCH → Create systemPatterns.md (architecture only)
  └─ `GEN[M13-19,τ₂→σ₂]`
- T21: VALIDATE_SYSTEM_PATTERNS → Verify σ₂ architecture accuracy and completeness
  └─ `VAL[σ₂,M17c→σ₂,M21]`

**R4: Module Identification & User Confirmation** `[7 tasks]`
- T22: IDENTIFY_FUNCTIONAL_MODULES → Business logic based grouping
  └─ `ANZ[M16,M17c→M22]`
- T23: IDENTIFY_STRUCTURAL_MODULES → Structure boundary based grouping
  └─ `ANZ[M13,M17a→M23]`
- T24: MERGE_MODULE_CANDIDATES → Consolidate overlapping candidates
  └─ `ANZ[M22,M23→M24]`
- T25: REFINE_MODULE_BOUNDARIES → Optimize size and responsibility
  └─ `ANZ[M24→M25]`
- T26: FORMAT_MODULE_PRESENTATION → User-friendly display format
  └─ `ANZ[M25→M26]`
- T27: 👤USER_CONFIRM_MODULES → Interactive module confirmation
  └─ `USER[M26→U]`
- T28: PROCESS_MODULE_FEEDBACK → Apply complete user module feedback + update systemPatterns.md (preserve all user requirements)
  └─ `PRC[M26,U→σ₂,M28]`

**R5: Module Detailed Design** `[6×N tasks where N = confirmed modules]`
∀μ ∈ modules:
- T29: MODULE_RESPONSIBILITIES → Define module responsibilities
  └─ `ANZ[M28,@μ→M29μ]`
- T30: MODULE_INTERFACES → Define public interfaces
  └─ `ANZ[M29μ,F(@μ/*)→M30μ]`
- T31: MODULE_DATA_STRUCTURES → Define data models
  └─ `ANZ[M30μ,F(@μ/models/*)→M31μ]`
- T32: MODULE_ERROR_HANDLING → Define error strategies
  └─ `ANZ[M31μ→M32μ]`
- T33: GENERATE_MODULE_DESIGN → Create design.md
  └─ `GEN[M29μ-32μ,τ_module→@μ/design.md]`
- T34: VALIDATE_MODULE_DESIGN → Verify module quality and LLD compliance
  └─ `VAL[@μ/design.md,M28→@μ/design.md,M34μ]`

**R6: Auxiliary Memory-Bank Files** `[9 tasks]`
- T35: ANALYZE_ACTIVE_CONTEXT → Analyze current state and focus
  └─ `ANZ[M28,σ₂→M35]`
- T36: GENERATE_ACTIVE_CONTEXT → Create activeContext.md
  └─ `GEN[M35,τ₄→σ₄]`
- T37: VALIDATE_ACTIVE_CONTEXT → Verify σ₄ completeness
  └─ `VAL[σ₄,M35→σ₄,M37]`
- T38: ANALYZE_PROGRESS → Calculate completion status
  └─ `ANZ[M28,M34*→M38]`
- T39: GENERATE_PROGRESS → Create progress.md
  └─ `GEN[M38,τ₅→σ₅]`
- T40: VALIDATE_PROGRESS → Verify σ₅ accuracy
  └─ `VAL[σ₅,M38→σ₅,M40]`
- T41: ANALYZE_PROTECTION → Identify protected regions
  └─ `ANZ[σ₁,σ₂→M41]`
- T42: GENERATE_PROTECTION → Create protection.md
  └─ `GEN[M41,τ₆→σ₆]`
- T43: VALIDATE_PROTECTION → Verify σ₆ validity
  └─ `VAL[σ₆,M41→σ₆,M43]`

**R7: Project Configuration Files** `[6 tasks]`
- T44: EXTRACT_COMMANDS → Identify build/test/run commands
  └─ `ANZ[M06,F(package.json,Makefile)→M44]`
- T45: DEFINE_CONSTRAINTS → Project-specific constraints
  └─ `ANZ[σ₂,σ₆→M45]`
- T46: GENERATE_CLAUDE_MD → Create project CLAUDE.md
  └─ `GEN[M44,M45,τ_claude→CLAUDE.md]`
- T47: VALIDATE_CLAUDE_MD → Verify CLAUDE.md completeness
  └─ `VAL[CLAUDE.md,M45→CLAUDE.md,M47]`
- T48: GENERATE_SYMBOLS → Create symbols.md reference
  └─ `GEN[τ_symbols→symbols.md]`
- T49: VALIDATE_SYMBOLS → Verify symbols.md accuracy
  └─ `VAL[symbols.md→symbols.md,M49]`

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
- `U`: User input

**Examples:**
```
T01:SCN[∅→M01]                    # Scan project, no deps, output to MCP
T07:GEN[M05,M06,τ₃→σ₃]           # Generate σ₃ from T05,T06 and template
T08:VAL[σ₃,M06→σ₃,M08]           # Validate σ₃ against M06, may fix σ₃
T20:GEN[M13-19,τ₂→σ₂]            # Generate σ₂ from T13-T19 analysis
T28:PRC[M22-27,U→σ₂,M28]         # Process user feedback, update σ₂
```

### 🤖 Agent Assignment

**Template Manager**: T00 → Initialize templates to MCP["RIPER_TEMPLATES"]

**Generator Agent** (instruction, σ_session):
- Tasks: T01, T03, T05-T07, T09-T11, T13-T20, T22-T26, T29-T33, T35-T36, T38-T39, T41-T42, T44-T46, T48
- Input: Symbolic instruction (e.g., "T07:GEN[M05,M06,τ₃→σ₃]")
- Output: memory-bank/*.md + MCP[σ_session + "_" + task_id]

**Validator Agent** (instruction, σ_session):
- Tasks: T02, T04, T08, T12, T21, T28, T34+, T37, T40, T43, T47, T49
- Input: Symbolic instruction (e.g., "T08:VAL[σ₃,M06→σ₃,M08]")
- Output: Validation results + corrections

**Main Thread**: T27 (user interaction) + orchestration

### 📋 Dependency Control

**Stage Dependencies**: Strict serial execution R0→R1→R2→R3→R4→R5→R6→R7
**Task Dependencies**: Within-stage tasks may have dependencies
**Parallel Opportunities**:
- R5: Module tasks can run in parallel (max 3 concurrent)  
- R6: Three auxiliary files can be processed in parallel

### ⚡ Error Handling

**Critical Tasks**: `[T02, T08, T12, T21, T28, T46]` → Failure terminates execution
**Retry Tasks**: `[T06, T16, T17c, T34+ series]` → Failure triggers 3 retries  
**Degrade Tasks**: `[T04, T14, T17a, T17b, T41]` → Failure allows graceful degradation

### 💾 State Management

**Session State**: Stored in MCP[σ_session + "_STATE"]  
**Task Results**: Stored in MCP[σ_session + "_" + task_id]  
**No .riper-execution.json file** - all state in MCP Memory

## Data Flow Protocol

**Agent-MCP Memory**: Agents read dependencies from MCP, write results to MCP  
**File Generation**: GENERATE tasks write to memory-bank/*.md  
**State Management**: All intermediate data in MCP Memory

### Dependency Resolution

```
TASK_DEPENDENCIES = {
  "T03": ["T01"],
  "T06": ["T05"],
  "T07": ["T05", "T06"],
  "T08": ["T07"],
  "T10": ["T09"],
  "T11": ["T09", "T10"],
  "T12": ["T11"],
  "T16": ["T15"],
  "T17c": ["T17a", "T17b"],
  "T20": ["T13-T19"],
  "T21": ["T20"],
  "T28": ["T26", "T27"],
  "T34+": ["T33+ per module"]
}
```