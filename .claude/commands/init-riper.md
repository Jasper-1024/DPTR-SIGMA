---
description: "Initialize TDD-RIPER framework: memory-bank + CLAUDE.md via session-based orchestration"
allowed-tools: Read, Write, Edit, LS, Bash, Glob, Grep, WebSearch, WebFetch, TodoWrite, Task
version: "3.0"
---

# RIPER Initialization Command v3.0

Use 4-Opus model, if Opus model is not available, this command will fallback to Sonnet for reliable performance.

**ultrathink** - Session-based atomic task framework with MCP Memory data flow. 8-stage dependency-driven execution with minimal context usage. Scales 42-92 tasks based on project complexity.

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
**Base Tasks**: 42 fixed tasks
**Module Tasks**: 5 × N (N = confirmed modules)  
**Total Range**: 42-92 tasks

### 🔄 Execution Stages

**R-1: Template Initialization** `[1 task]`
- T00: INIT_TEMPLATES → Template Manager Agent → MCP["RIPER_TEMPLATES"]

**R0: Project Foundation Scan** `[4 tasks]`
- T01: SCAN_PROJECT → Complete file/directory inventory + project type detection
- T02: DETECT_CONFIGS → Configuration file presence mapping  
- T03: CLASSIFY_FILES → File type classification by extension
- T04: DETECT_DOCS → Documentation and special directories

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

**R1: Technology Stack Analysis** `[3 tasks]`
- T05: PARSE_CONFIGS → Extract dependencies from detected configs
- T06: INFER_TECH_STACK → Deduce complete technology stack
- T07: GENERATE_TECH_CONTEXT → Create techContext.md

**R2: Project Information Extraction** `[3 tasks]`  
- T08: EXTRACT_PROJECT_INFO → Gather project metadata from all sources
- T09: INFER_PROJECT_PURPOSE → Determine project type and objectives
- T10: GENERATE_PROJECT_BRIEF → Create projectbrief.md

**R3: Code Architecture Analysis** `[10 tasks]`
- T11: SCAN_CODE_ORGANIZATION → Directory patterns and file distribution
- T12: ANALYZE_NAMING_CONVENTIONS → Code style and naming patterns  
- T13: EXTRACT_IMPORTS_DEPENDENCIES → All dependency declarations
- T14: BUILD_DEPENDENCY_GRAPH → File interdependency mapping
- T15a: SCAN_DIRECTORY_PATTERNS → Scan directory structure patterns (controllers/, models/, services/)
- T15b: ANALYZE_CODE_PATTERNS → Analyze code organization patterns (imports, class hierarchies)
- T15c: CLASSIFY_ARCHITECTURE → Classify architecture based on T15a and T15b results
- T16: IDENTIFY_ENTRY_POINTS → Application entry points and interfaces
- T17: ANALYZE_PUBLIC_INTERFACES → External API surface analysis
- T18: GENERATE_SYSTEM_PATTERNS_ARCH → Create systemPatterns.md (architecture only)

**R4: Module Identification & User Confirmation** `[7 tasks]`
- T19: IDENTIFY_FUNCTIONAL_MODULES → Business logic based grouping
- T20: IDENTIFY_STRUCTURAL_MODULES → Structure boundary based grouping  
- T21: MERGE_MODULE_CANDIDATES → Consolidate overlapping candidates
- T22: REFINE_MODULE_BOUNDARIES → Optimize size and responsibility
- T23: FORMAT_MODULE_PRESENTATION → User-friendly display format
- T24: 👤USER_CONFIRM_MODULES → Interactive module confirmation
- T25: PROCESS_MODULE_FEEDBACK → Apply user modifications + update systemPatterns.md

**R5: Module Detailed Design** `[5×N tasks where N = confirmed modules]`
- T26-T30 per module: responsibilities, interfaces, data, errors, design.md

**R6: Auxiliary Memory-Bank Files** `[9 tasks]`
- T40-T42: activeContext.md (analyze → generate → validate)
- T43-T45: progress.md (analyze → generate → validate)
- T46-T48: protection.md (analyze → generate → validate)

**R7: Project Configuration Files** `[6 tasks]`
- T49-T52: CLAUDE.md (commands → constraints → generate → validate)
- T53-T54: symbols.md (generate → validate)

## Execution Framework

### 🤖 Agent Assignment

**Template Manager**: T00 → Initialize templates to MCP["RIPER_TEMPLATES"]

**Generator Agent** (task_id, σ_session):
- Tasks: T01, T03, T05-T07, T08-T10, T11-T18, T19-T23, T26-T30+, T40-T41, T43-T44, T46-T47, T49-T51, T53
- Output: memory-bank/*.md + MCP[σ_session + "_" + task_id]

**Validator Agent** (task_id, σ_session):
- Tasks: T02, T04, T25, T42, T45, T48, T52, T54
- Output: Validation results + corrections

**Main Thread**: T24 (user interaction) + orchestration

### 📋 Dependency Control

**Stage Dependencies**: Strict serial execution R0→R1→R2→R3→R4→R5→R6→R7
**Task Dependencies**: Within-stage tasks may have dependencies
**Parallel Opportunities**:
- R5: Module tasks can run in parallel (max 3 concurrent)  
- R6: Three auxiliary files can be processed in parallel

### ⚡ Error Handling

**Critical Tasks**: `[T02, T07, T10, T18, T25, T51]` → Failure terminates execution
**Retry Tasks**: `[T06, T14, T15c, T30+ series]` → Failure triggers 3 retries  
**Degrade Tasks**: `[T04, T12, T15a, T15b, T46]` → Failure allows graceful degradation

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
  "T14": ["T13"],
  "T15c": ["T15a", "T15b"],
  "T18": ["T11-T17"],
  "T25": ["T19-T24"],
  "T30+": ["T25"]
}
```