---
description: "Initialize RIPER workflow with incremental updates and enhanced quality control"
allowed-tools: Read, Write, Edit, LS, Bash, Glob, Grep, WebSearch, WebFetch, TodoWrite
version: "4.0"
---

# RIPER Initialization Command v4.0

Use 4-Opus model, if Opus model is not available, this command will fallback to Sonnet for reliable performance.

**ultrathink** - This advanced initialization uses incremental update strategy with systematic task planning for robust quality control. Protects existing user content while ensuring memory-bank completeness and accuracy through intelligent file assessment and targeted updates.

Initialize the RIPER memory-bank structure with incremental updates and quality assurance.

## Execution Strategy

**Incremental Update Approach**: File status assessment → Selective information collection → Targeted content generation → Section-level auditing → Precision correction

- **User Protection**: Preserve existing user content and customizations
- **Efficiency**: Only update files that need updating based on assessment
- **Quality**: Multi-stage auditing with complete template compliance verification
- **Safety**: Automatic backup before any modifications
- **Tracking**: TodoWrite-driven task management throughout process

## File Status Classification

```
MISSING: File does not exist → Full generation required
EMPTY: File exists but contains only placeholders → Full generation required  
PARTIAL: File exists but missing required template sections → Incremental completion
OUTDATED: File complete but content appears stale → Selective updates
CURRENT: File complete and content appears accurate → Skip processing
```

## User Content Protection Strategy

**Custom Content Detection:**
- **Title-based**: Chapters with ## headers not in template
- **Position-based**: Content inserted between template sections
- **Format-based**: Sections without template emoji format

**Preservation Method:**
- Custom user sections automatically moved to end of file
- Template sections updated/added as needed
- User content preserved exactly as written

## Task Planning Framework

### **Phase 0: Pre-initialization (7 tasks)**
```
1. [PREP] Check existing CLAUDE.md status and memory-bank integration
2. [PREP] Scan memory-bank directory structure and existing σ files
3. [ASSESS] Evaluate existing σ files status (MISSING/EMPTY/PARTIAL/OUTDATED/CURRENT)
4. [BACKUP] Create safety backup of existing memory-bank files in backups/ directory  
5. [DETECT] Identify user custom content and mark for preservation
6. [PREP] Identify missing files and required updates to existing files
7. [PREP] Create directory structure for new files
```

### **Phase 1: Information Collection (12 parallel tasks)**

**📋 Project Foundation:**
```
8. [COLLECT] Extract project name, description, and core features from README.md
9. [COLLECT] Analyze CONTRIBUTING.md and docs/ for development standards
10. [COLLECT] Scan source code structure for main modules and entry points
11. [COLLECT] Analyze git history for project activity and key milestones
```

**🛠️ Technical Intelligence:**
```
12. [COLLECT] Parse package.json/requirements.txt/Cargo.toml for tech stack
13. [COLLECT] Analyze source imports/includes for actual library usage
14. [COLLECT] Detect configuration files for databases, cloud services, deployment
15. [COLLECT] Examine build scripts for development commands and workflows
```

**🏗️ Architecture Analysis:**
```
16. [COLLECT] Analyze directory structure for architectural patterns
17. [COLLECT] Identify design patterns and naming conventions from code
18. [COLLECT] Examine error handling and logging strategies
19. [COLLECT] Assess testing approaches and quality assurance practices
```

### **Phase 2: Incremental Content Generation & Quality Control (40 tasks)**

**Each σ file follows: Generate/Update → Audit → Structure Check → Correct → Confirm**

**σ₁ Project Brief (5 tasks):**
```
20. [UPDATE-σ₁] Generate/update projectbrief.md based on file status assessment
21. [AUDIT-σ₁] Verify project description accuracy and requirement completeness
22. [STRUCT-σ₁] Verify complete template compliance: ✓Contains ALL required sections (Overview, Requirements, Goals & Objectives, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper header format with emojis
23. [FIX-σ₁] Correct any inaccurate descriptions, missing objectives, or structural deviations
24. [CONFIRM-σ₁] Final validation of goals alignment and cross-references
```

**σ₂ System Patterns - Lightweight (5 tasks):**
```
25. [UPDATE-σ₂] Generate/update systemPatterns.md with lightweight architecture + module index
26. [AUDIT-σ₂] Verify architecture overview accuracy and module boundary identification
27. [STRUCT-σ₂] Verify template compliance: ✓Architecture Overview ✓System Data Flow ✓Design Patterns ✓Module Structure (with @modules/ refs) ✓TDD Planning Storage ✓Cross-References
28. [FIX-σ₂] Correct architecture misidentification or module organization issues
29. [CONFIRM-σ₂] Validate architecture clarity and module index completeness
```

**Modules Structure Generation (10 tasks):**
```
30. [ANALYZE-MODULES] Identify project modules from source code structure and imports
31. [CREATE-MODULES-DIR] Create memory-bank/modules/ directory structure
32. [GENERATE-REG-MODULE] Generate modules/registration/design.md for registration functionality
33. [GENERATE-SSE-MODULE] Generate modules/sse-connection/design.md for SSE/WebSocket functionality
34. [GENERATE-EXEC-MODULE] Generate modules/test-execution/design.md for test execution engine
35. [GENERATE-TIMEOUT-MODULE] Generate modules/timeout-control/design.md for timeout management
36. [GENERATE-STATE-MODULE] Generate modules/state-management/design.md for state/session management
37. [GENERATE-MSG-MODULE] Generate modules/message-broadcast/design.md for message/notification system
38. [AUDIT-MODULES] Verify each module design.md contains: Core Responsibilities, Key Interfaces, Data Structures, Technical Decisions
39. [UPDATE-MODULE-REFS] Update σ₂ systemPatterns.md with correct @modules/ references
```

**Project-Level CLAUDE.md (5 tasks):**
```
40. [ANALYZE-PROJECT] Extract project-specific tech stack, commands, and conventions
41. [GENERATE-CLAUDE-MD] Create project-level CLAUDE.md with Tech Stack, Project Structure, Commands, Code Style, Do Not, Memory Integration
42. [VALIDATE-COMMANDS] Verify build/test/run commands are project-specific and functional
43. [AUDIT-CLAUDE-MD] Ensure CLAUDE.md contains memory-bank integration references
44. [CONFIRM-CLAUDE-MD] Final validation of project-level constraints and team conventions
```

**σ₃ Technical Context (5 tasks):**
```
45. [UPDATE-σ₃] Generate/update techContext.md based on file status assessment
46. [AUDIT-σ₃] Verify technology stack accuracy and dependency completeness
47. [STRUCT-σ₃] Verify complete template compliance: ✓Contains ALL required sections (Technology Stack with 5 categories, Dependencies with Core/Dev subsections, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper technology categorization
48. [FIX-σ₃] Correct technology misidentifications, missing dependencies, or structural deviations
49. [CONFIRM-σ₃] Validate tech stack relevance and version accuracy
```

**σ₄ Active Context (5 tasks):**
```
50. [UPDATE-σ₄] Generate/update activeContext.md based on file status assessment
51. [AUDIT-σ₄] Verify context references validity and state initialization
52. [STRUCT-σ₄] Verify complete template compliance: ✓Contains ALL required sections (Current Focus, Context References, Context Status, RIPER Agent State, Agent Handoff, Mode History, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper agent state format
53. [FIX-σ₄] Correct invalid references, agent state configuration, or structural issues
54. [CONFIRM-σ₄] Validate context relevance and handoff mechanisms
```

**σ₅ Progress Tracker (5 tasks):**
```
55. [UPDATE-σ₅] Generate/update progress.md based on file status assessment
56. [AUDIT-σ₅] Verify milestone relevance and task categorization logic
57. [STRUCT-σ₅] Verify complete template compliance: ✓Contains ALL required sections (Project Status, Completed Tasks, In Progress, Pending Tasks, Milestones, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper task list format
58. [FIX-σ₅] Adjust milestones, refine task organization, or fix structural deviations
59. [CONFIRM-σ₅] Validate progress tracking alignment with project goals
```

**σ₆ Protection Registry (5 tasks):**
```
60. [UPDATE-σ₆] Generate/update protection.md based on file status assessment
61. [AUDIT-σ₆] Verify protection classifications and critical file identification
62. [STRUCT-σ₆] Verify complete template compliance: ✓Contains ALL required sections (Protected Regions, Critical Files, Protected Functions, Protection History, Approvals, Permission Violations, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper protection classification format
63. [FIX-σ₆] Refine protection levels, add missing critical elements, or fix structural issues
64. [CONFIRM-σ₆] Validate protection registry completeness and accuracy
```

### **Phase 3: Integration & Final Validation (15 tasks)**
```
65. [INTEGRATE] Verify all σ₁-σ₆ cross-references are valid and complete
66. [VALIDATE-MODULE-REFS] Verify all @modules/ references in σ₂ point to existing design.md files
67. [XREF-UPDATE] Update cross-references that point to renamed or restructured sections
68. [VALIDATE] Ensure placeholder replacement completeness ({DATE}, {PHASE}, {MODE})
69. [VERIFY-CLAUDE-MD] Confirm project-level CLAUDE.md memory-bank integration links are functional
70. [VERIFY-GLOBAL] Confirm global CLAUDE.md memory-bank integration links are functional
71. [CHECK] Validate RIPER Agent State initialization and session setup
72. [META-CHECK] Verify metadata consistency across all σ files and modules (version, date, phase, mode)
73. [QUALITY-CHECK-CORE] Ensure all core σ files have actual content (no empty placeholders)
74. [QUALITY-CHECK-MODULES] Ensure all module design.md files have complete sections
75. [FORMAT-CHECK] Validate Markdown format standardization and emoji consistency
76. [MODULE-INDEX-CHECK] Verify σ₂ module index accuracy and completeness
77. [PROJECT-CLAUDE-CHECK] Verify project-level CLAUDE.md contains all required sections
78. [REPORT] Generate initialization summary and quality assessment with change log
79. [FINALIZE] Create/update symbols.md reference guide
```

## Quality Assurance Features

### **Built-in Quality Checks:**
- **Accuracy Verification**: Technology stack vs actual dependencies
- **Completeness Validation**: All template sections properly filled
- **Consistency Auditing**: Cross-reference integrity across all σ files
- **Context Relevance**: Generated content matches actual project characteristics
- **User Protection**: Custom user content preserved and repositioned

### **Error Correction Strategy:**
- **Targeted Fixes**: Only correct identified errors, preserve accurate content
- **Source Re-analysis**: Re-examine original files for correction information
- **Incremental Updates**: Apply fixes without disrupting correct sections
- **User Content Preservation**: Move custom sections to end, never delete
- **Validation Loops**: Confirm corrections resolve identified issues

### **Backup & Safety Mechanisms:**
- **Automatic Backup**: All existing files backed up to memory-bank/backups/ before modification
- **File Archiving**: Changed files archived with timestamp for recovery
- **Error Recovery**: Partial failure handling with ability to resume or rollback

## Expected Quality Improvements

| Metric | Before | After (v3.0) |
|--------|--------|--------------|
| Content Accuracy | ~70% | ~90% |
| Template Completeness | ~80% | ~95% |
| Cross-reference Integrity | ~75% | ~95% |
| Project Relevance | ~65% | ~85% |
| User Content Preservation | ~0% | ~100% |

## Incremental Update Logic

### **File Processing Decision Tree:**
```
For each σ file:
├── Status = MISSING → Full generation with template
├── Status = EMPTY → Full generation with collected info
├── Status = PARTIAL → Add missing sections, preserve existing
├── Status = OUTDATED → Update stale content, preserve structure
└── Status = CURRENT → Skip processing, preserve as-is
```

### **Update Granularity:**
- **Section-level**: Update individual template sections as needed
- **Content-preserving**: Never overwrite user customizations
- **Structure-completing**: Add missing template sections
- **Reference-updating**: Fix broken cross-references

## Memory Bank Templates

**σ₁ projectbrief.md:** # σ₁: Project Brief\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🏆 Overview\n[Project description]\n\n## 📋 Requirements\n- [R₁] [Requirement 1]\n- [R₂] [Requirement 2]\n- [R₃] [Requirement 3]\n\n## 🎯 Goals & Objectives\n- [G₁] [Goal 1]\n- [G₂] [Goal 2]\n- [G₃] [Goal 3]\n\n## 🔗 Cross-References\n- Architecture: [↗️σ₂:Architecture]\n- Tech Stack: [↗️σ₃:Technologies]\n- Progress: [↗️σ₅:Status]

**σ₂ systemPatterns.md (Lightweight):** # σ₂: System Patterns\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🏛️ Architecture Overview\n[System architecture description - layered/microservices/monolithic approach]\n\n## 📊 System Data Flow\n[High-level data flow between major components]\n\n## 📐 Design Patterns\n- [Core Pattern 1]: [Brief description]\n- [Core Pattern 2]: [Brief description]\n- Test-First Development: Design guided by test requirements\n- Interface Segregation: Clear boundaries between test and implementation\n\n## 🏗️ Module Structure\n- @modules/registration/ - User/service registration functionality\n- @modules/sse-connection/ - Server-Sent Events connection management\n- @modules/test-execution/ - Test execution engine and scheduling\n- @modules/timeout-control/ - Timeout and lifecycle management\n- @modules/state-management/ - Session and state persistence\n- @modules/message-broadcast/ - Message routing and broadcasting\n\n## 📝 Code Conventions\n### Basic Standards\n- Language: [Primary language] + [Version]\n- Style: [Style guide reference]\n- Testing: [Test file patterns]\n- Error Handling: [Error handling approach]\n\n## 🔄 TDD Planning Storage\n### Selected Approach\n[TDD methodology selection]\n\n## 🔗 Cross-References\n- Tech Context: [↗️σ₃:Stack]\n- Project Brief: [↗️σ₁:Requirements]\n- Active Context: [↗️σ₄:TDD_State]\n- Module Details: @modules/[module-name]/design.md

**σ₃ techContext.md:** # σ₃: Technical Context\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🛠️ Technology Stack\n- 🖥️ Frontend: [Technologies]\n- 🔙 Backend: [Technologies]\n- 💾 Database: [Technologies]\n- ☁️ Cloud: [Technologies]\n- 🔧 DevOps: [Technologies]\n\n## 📦 Dependencies\n### Core Dependencies\n- Dependency 1: version\n- Dependency 2: version\n- Dependency 3: version\n\n### Development Dependencies\n- Dev Dep 1: version\n- Dev Dep 2: version\n- Dev Dep 3: version\n\n## 🔗 Cross-References\n- System Patterns: [↗️σ₂:Architecture]\n- Project Brief: [↗️σ₁:Overview]

**σ₄ activeContext.md:** # σ₄: Active Context\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🔮 Current Focus\n[Current focus]\n\n## 📎 Context References\n- 📄 Active Files: []\n- 💻 Active Code: []\n- 📚 Active Docs: []\n- 📁 Active Folders: []\n- 🔄 Git References: []\n- 📏 Active Rules: []\n- 🧪 TDD Cycles: []\n- 🔴 Test Files: []\n- 🟢 Implementation Files: []\n\n## 📡 Context Status\n- 🟢 Active: []\n- 🟡 Partially Relevant: []\n- 🟣 Essential: []\n- 🔴 Deprecated: []\n\n## 🤖 RIPER Agent State\nΩ_current: Ω₁              # Current RIPER mode\nΩ_session: AGT_2025_001    # Agent session identifier\nsession_id: null           # MCP Memory dialogue session (Plan Loop)\ntdd_session_id: null       # MCP Memory dialogue session (TDD Loop)\nΩ_transitions: []          # Mode transition history\nlocked_by: null            # Concurrency control\nlock_timestamp: null\n\n# TDD Execution State\ntdd_mode: false            # TDD mode enabled (Ω₄ᵀ)\ntdd_phase: null            # current: 'red'|'green'|'refactor'\ncurrent_cycle: 0           # active iteration index\ntarget_method: null        # method being developed\nqa_agent_active: false     # QA role active\nde_agent_active: false     # DE role active\nlast_test_result: null     # 'pass'|'fail'|null\nrefactor_stage: null       # 'test'|'impl'|null\n\n## 🤝 Agent Handoff\nhandoff_from: null         # Previous mode\nhandoff_to: null           # Expected next mode\nhandoff_summary: |         # Context for next agent\n  [Handoff details here]\nhandoff_timestamp: null\n\n## 📊 Mode History\n| Time | From | To | Trigger | Summary |\n|------|------|----|---------|---------|\n| -    | -    | -  | -       | -       |\n\n## 🔗 Cross-References\n- Brief: [↗️σ₁:Overview]\n- Patterns: [↗️σ₂:Architecture]\n- Tech: [↗️σ₃:Stack]\n- Progress: [↗️σ₅:Status]\n- Protection: [↗️σ₆:Registry]

**σ₅ progress.md:** # σ₅: Progress Tracker\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 📈 Project Status\nCompletion: 0%\nCurrent Phase: {PHASE}\nCurrent Mode: {MODE}\nTDD Mode: false\nTDD Cycles Completed: 0/0\n\n## ✅ Completed Tasks\n- [ ] Task 1\n- [ ] Task 2\n- [ ] Task 3\n\n## 🧪 TDD Cycle Progress\n### Completed Cycles\n- [ ] Cycle 1: [method_name] (ℜ→ℜᴳ→ℜᶠ) ✓\n- [ ] Cycle 2: [method_name] (ℜ→ℜᴳ→ℜᶠ) ✓\n\n### Current Cycle\n- [ ] Cycle N: [method_name]\n  - [ ] RED Phase (QA): Write failing tests\n  - [ ] GREEN Phase (DE): Minimal implementation\n  - [ ] REFACTOR Phase: Quality improvement\n\n### Pending Cycles\n- [ ] Cycle N+1: [method_name] → ℜ→ℜᴳ→ℜᶠ\n- [ ] Cycle N+2: [method_name] → ℜ→ℜᴳ→ℜᶠ\n\n## 🚧 In Progress\n- [ ] Current Task 1\n- [ ] Current Task 2\n\n## 📋 Pending Tasks\n- [ ] Future Task 1\n- [ ] Future Task 2\n\n## 🏁 Milestones\n- [ ] Milestone 1\n- [ ] Milestone 2\n- [ ] Milestone 3\n- [ ] TDD Integration Complete\n- [ ] All Cycles Verified\n\n## 📊 Quality Metrics\n- Test Coverage: 0%\n- Cycles with Refactor: 0/0\n- Failed Cycles: 0\n- Refactor Improvements Made: 0\n\n## 🔗 Cross-References\n- Active Context: [↗️σ₄:Focus]\n- Project Brief: [↗️σ₁:Goals]\n- TDD State: [↗️σ₄:TDD_Execution_State]

**σ₆ protection.md:** # σ₆: Protection Registry\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🛡️ Protected Regions\n[Protected code registry]\n\n### Critical Files\n- File 1: [Protection reason]\n- File 2: [Protection reason]\n\n### Protected Functions\n- Function 1: [Protection reason]\n- Function 2: [Protection reason]\n\n## 📜 Protection History\n[History and changes]\n\n## ✅ Approvals\n[Modification approvals]\n\n## ⚠️ Permission Violations\n[Violation logs]\n\n## 🔗 Cross-References\n- Active Context: [↗️σ₄:Status]\n- System Patterns: [↗️σ₂:Architecture]

**symbols.md:** # 🔣 Symbol Reference Guide\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n\n## 📁 File Symbols\n- 📂 = /memory-bank/\n- 📦 = /memory-bank/backups/\n- 📄 = .md files\n- 📊 = data files\n- 📋 = configuration files\n\n## 🤖 RIPER Symbols\n- Ω₁ = Research Mode\n- Ω₂ = Innovate Mode\n- Ω₃ = Plan Mode\n- Ω₄ = Execute Mode\n- Ω₅ = Review Mode\n\n## 📚 Memory Symbols\n- σ₁ = projectbrief.md\n- σ₂ = systemPatterns.md\n- σ₃ = techContext.md\n- σ₄ = activeContext.md\n- σ₅ = progress.md\n- σ₆ = protection.md\n\n## 🔗 Reference Symbols\n- [↗️σₓ:Rₓ] = Cross-reference to memory file section\n- Γ₁ = Files, Γ₂ = Folders, Γ₃ = Code\n- Γ₄ = Commands, Γ₅ = Modify, Γ₆ = Web\n\n## 🛡️ Protection Symbols\n- Ψ₁-₃ = Proceed (Low risk)\n- Ψ₄-₆ = Caution + Confirm (High risk)

**modules/[module-name]/design.md:** # [ModuleName] Module Design\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Module: [module-name] | Status: [design|development|testing|complete]*\n\n## 🎯 Core Responsibilities\n- [Primary responsibility 1]\n- [Primary responsibility 2]\n- [Primary responsibility 3]\n\n## 🔗 Key Interfaces\n### Public APIs\n```\n[Interface/API definitions]\n```\n### Internal Interfaces\n```\n[Internal interface definitions]\n```\n\n## 📊 Data Structures\n### Primary Models\n```\n[Core data structures/models]\n```\n### State Management\n[State management approach if applicable]\n\n## ⚙️ Technical Decisions\n### Architecture Choices\n- [Decision 1]: [Reasoning]\n- [Decision 2]: [Reasoning]\n### Dependencies\n- Internal: [List internal module dependencies]\n- External: [List external library dependencies]\n\n## 🔄 Integration Points\n- Input: [What this module receives]\n- Output: [What this module produces]\n- Events: [Events this module emits/listens to]\n\n## 🧪 Testing Strategy\n[Module-specific testing approach and key test scenarios]

**Project-Level CLAUDE.md:** # Tech Stack\n- Language: [Primary Language] [Version]\n- Framework: [Main Framework/Library]\n- Testing: [Testing Framework]\n- Database: [Database if applicable]\n- Build: [Build system]\n\n# Project Structure\n```\n[Project directory structure]\n```\n\n# Commands\n- `[build-command]`: Build the project\n- `[test-command]`: Run test suite\n- `[dev-command]`: Start development server\n- `[lint-command]`: Run linter/formatter\n- `[deploy-command]`: Deploy application\n\n# TDD-RIPER Integration\n**IMPORTANT**: This project uses TDD-RIPER workflow\n- Read memory-bank files before starting any work\n- Follow memory-bank/progress.md for current TDD cycles\n- All design decisions recorded in memory-bank/systemPatterns.md\n\n# Code Style\n- [Language-specific conventions]\n- [Naming conventions]\n- [File organization rules]\n- [Testing patterns]\n\n# Do Not\n- Skip TDD phases (Red→Green→Refactor)\n- Maintain design decisions outside memory-bank\n- [Project-specific constraints]\n\n# Memory Integration\nProject memory stored in:\n- Brief: memory-bank/projectbrief.md\n- Architecture: memory-bank/systemPatterns.md\n- Tech Stack: memory-bank/techContext.md\n- Current State: memory-bank/activeContext.md\n- Progress: memory-bank/progress.md\n- Protection: memory-bank/protection.md\n- Module Details: memory-bank/modules/[module]/design.md\n\n**Start every session by reading relevant memory-bank files**

## Implementation Instructions

**Module Generation Logic:**
1. Scan project structure to identify functional modules
2. Create memory-bank/modules/[module-name]/ directories
3. Generate design.md for each identified module
4. Update σ₂ systemPatterns.md with @modules/ references

**Project-Level CLAUDE.md Generation:**
1. Replace any existing CLAUDE.md (not append)
2. Extract actual tech stack from project files
3. Identify real build/test commands from package.json/Makefile/etc
4. Generate project-specific constraints and conventions

**Quality Assurance:**
- Verify all @modules/ references in σ₂ point to existing files
- Ensure project-level CLAUDE.md contains memory-bank integration
- Validate module design.md files contain all required sections
- Confirm σ₂ systemPatterns.md stays under 3000 characters

**This enhanced version provides:**
- Modular memory-bank architecture with lightweight core files
- Module-specific design documents in memory-bank/modules/
- Project-level CLAUDE.md generation with TDD-RIPER integration
- Incremental update strategy with user content protection
- Systematic task planning with 79 structured tasks (vs 59 in v3.0)
- Quality assurance through multi-stage auditing
- Complete template compliance verification
- Automatic backup and safety mechanisms
- Cross-reference integrity management including @modules/ references
- Error correction with targeted fixes
- Progress tracking via TodoWrite integration
- Improved content accuracy and modular organization

**Expected outcomes:**
- Modular memory-bank architecture preventing σ₂ overload
- Higher quality memory-bank initialization with user protection
- Significantly fewer manual corrections required
- Preserved user customizations and enhancements
- Better project context capture with modular organization
- Reliable cross-reference integrity and structure compliance
- Project-specific CLAUDE.md for immediate team alignment