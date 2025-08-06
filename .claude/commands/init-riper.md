---
description: "Initialize RIPER workflow with incremental updates and enhanced quality control"
allowed-tools: Read, Write, Edit, LS, Bash, Glob, Grep, WebSearch, WebFetch, TodoWrite
version: "3.0"
---

# RIPER Initialization Command v3.0

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

### **Phase 2: Incremental Content Generation & Quality Control (30 tasks)**

**Each σ file follows: Generate/Update → Audit → Structure Check → Correct → Confirm**

**σ₁ Project Brief (5 tasks):**
```
20. [UPDATE-σ₁] Generate/update projectbrief.md based on file status assessment
21. [AUDIT-σ₁] Verify project description accuracy and requirement completeness
22. [STRUCT-σ₁] Verify complete template compliance: ✓Contains ALL required sections (Overview, Requirements, Goals & Objectives, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper header format with emojis
23. [FIX-σ₁] Correct any inaccurate descriptions, missing objectives, or structural deviations
24. [CONFIRM-σ₁] Final validation of goals alignment and cross-references
```

**σ₂ System Patterns (5 tasks):**
```
25. [UPDATE-σ₂] Generate/update systemPatterns.md based on file status assessment
26. [AUDIT-σ₂] Verify architecture description matches actual code structure
27. [STRUCT-σ₂] Verify complete template compliance: ✓Contains ALL required sections (Architecture Overview, Design Patterns, Code Conventions, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper subsection structure (Import Order, Naming Conventions, Error Handling)
28. [FIX-σ₂] Correct pattern identification errors, convention descriptions, or structural issues
29. [CONFIRM-σ₂] Validate design patterns and code conventions accuracy
```

**σ₃ Technical Context (5 tasks):**
```
30. [UPDATE-σ₃] Generate/update techContext.md based on file status assessment
31. [AUDIT-σ₃] Verify technology stack accuracy and dependency completeness
32. [STRUCT-σ₃] Verify complete template compliance: ✓Contains ALL required sections (Technology Stack with 5 categories, Dependencies with Core/Dev subsections, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper technology categorization
33. [FIX-σ₃] Correct technology misidentifications, missing dependencies, or structural deviations
34. [CONFIRM-σ₃] Validate tech stack relevance and version accuracy
```

**σ₄ Active Context (5 tasks):**
```
35. [UPDATE-σ₄] Generate/update activeContext.md based on file status assessment
36. [AUDIT-σ₄] Verify context references validity and state initialization
37. [STRUCT-σ₄] Verify complete template compliance: ✓Contains ALL required sections (Current Focus, Context References, Context Status, RIPER Agent State, Agent Handoff, Mode History, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper agent state format
38. [FIX-σ₄] Correct invalid references, agent state configuration, or structural issues
39. [CONFIRM-σ₄] Validate context relevance and handoff mechanisms
```

**σ₅ Progress Tracker (5 tasks):**
```
40. [UPDATE-σ₅] Generate/update progress.md based on file status assessment
41. [AUDIT-σ₅] Verify milestone relevance and task categorization logic
42. [STRUCT-σ₅] Verify complete template compliance: ✓Contains ALL required sections (Project Status, Completed Tasks, In Progress, Pending Tasks, Milestones, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper task list format
43. [FIX-σ₅] Adjust milestones, refine task organization, or fix structural deviations
44. [CONFIRM-σ₅] Validate progress tracking alignment with project goals
```

**σ₆ Protection Registry (5 tasks):**
```
45. [UPDATE-σ₆] Generate/update protection.md based on file status assessment
46. [AUDIT-σ₆] Verify protection classifications and critical file identification
47. [STRUCT-σ₆] Verify complete template compliance: ✓Contains ALL required sections (Protected Regions, Critical Files, Protected Functions, Protection History, Approvals, Permission Violations, Cross-References) ✓No missing chapters ✓No extra non-template sections ✓Correct section order ✓Proper protection classification format
48. [FIX-σ₆] Refine protection levels, add missing critical elements, or fix structural issues
49. [CONFIRM-σ₆] Validate protection registry completeness and accuracy
```

### **Phase 3: Integration & Final Validation (9 tasks)**
```
50. [INTEGRATE] Verify all σ₁-σ₆ cross-references are valid and complete
51. [XREF-UPDATE] Update cross-references that point to renamed or restructured sections
52. [VALIDATE] Ensure placeholder replacement completeness ({DATE}, {PHASE}, {MODE})
53. [VERIFY] Confirm CLAUDE.md memory-bank integration links are functional
54. [CHECK] Validate RIPER Agent State initialization and session setup
55. [META-CHECK] Verify metadata consistency across all σ files (version, date, phase, mode)  
56. [QUALITY-CHECK] Ensure all sections have actual content (no empty placeholders)
57. [FORMAT-CHECK] Validate Markdown format standardization and emoji consistency
58. [REPORT] Generate initialization summary and quality assessment with change log
59. [FINALIZE] Create/update symbols.md reference guide
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

**σ₂ systemPatterns.md:** # σ₂: System Patterns\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🏛️ Architecture Overview\n[Architecture description]\n\n## 📐 Design Patterns\n- Pattern 1: [Description]\n- Pattern 2: [Description]\n- Pattern 3: [Description]\n- Test-First Development: Design guided by test requirements\n- Interface Segregation: Clear boundaries between test and implementation\n\n## 📝 Code Conventions\n### Import Order\n1. Standard library imports\n2. Third-party libraries\n3. Local components\n4. Utilities\n\n### Naming Conventions\n- Components: [Naming convention]\n- Functions: [Naming convention]\n- Constants: [Naming convention]\n- Files: [Naming convention]\n- Test Files: *_test.* or test_*.*\n- Implementation Files: Clear business intent names\n\n### Error Handling\n[Error handling patterns]\n\n## 🔄 TDD Planning Storage\n### Selected Approach\n[TDD methodology selection]\n\n### TDD Cycles\n```\nPhase0: Create minimal interface definitions\n□ TDD₁: Interface.MethodA() → ℜ→ℜᴳ→ℜᶠ\n□ TDD₂: Interface.MethodB() → ℜ→ℜᴳ→ℜᶠ\n□ TDD₃: AnotherInterface.MethodC() → ℜ→ℜᴳ→ℜᶠ\n```\n\n### Cycle Dependencies\n[Method dependency graph]\n\n## 🔗 Cross-References\n- Tech Context: [↗️σ₃:Stack]\n- Project Brief: [↗️σ₁:Requirements]\n- Active Context: [↗️σ₄:TDD_State]

**σ₃ techContext.md:** # σ₃: Technical Context\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🛠️ Technology Stack\n- 🖥️ Frontend: [Technologies]\n- 🔙 Backend: [Technologies]\n- 💾 Database: [Technologies]\n- ☁️ Cloud: [Technologies]\n- 🔧 DevOps: [Technologies]\n\n## 📦 Dependencies\n### Core Dependencies\n- Dependency 1: version\n- Dependency 2: version\n- Dependency 3: version\n\n### Development Dependencies\n- Dev Dep 1: version\n- Dev Dep 2: version\n- Dev Dep 3: version\n\n## 🔗 Cross-References\n- System Patterns: [↗️σ₂:Architecture]\n- Project Brief: [↗️σ₁:Overview]

**σ₄ activeContext.md:** # σ₄: Active Context\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🔮 Current Focus\n[Current focus]\n\n## 📎 Context References\n- 📄 Active Files: []\n- 💻 Active Code: []\n- 📚 Active Docs: []\n- 📁 Active Folders: []\n- 🔄 Git References: []\n- 📏 Active Rules: []\n- 🧪 TDD Cycles: []\n- 🔴 Test Files: []\n- 🟢 Implementation Files: []\n\n## 📡 Context Status\n- 🟢 Active: []\n- 🟡 Partially Relevant: []\n- 🟣 Essential: []\n- 🔴 Deprecated: []\n\n## 🤖 RIPER Agent State\nΩ_current: Ω₁              # Current RIPER mode\nΩ_session: AGT_2025_001    # Agent session ID\nΩ_transitions: []          # Mode transition history\nlocked_by: null            # Concurrency control\nlock_timestamp: null\n\n# TDD Execution State\ntdd_mode: false            # TDD mode enabled (Ω₄ᵀ)\ntdd_phase: null            # current: 'red'|'green'|'refactor'\ncurrent_cycle: 0           # active iteration index\ntarget_method: null        # method being developed\nqa_agent_active: false     # QA role active\nde_agent_active: false     # DE role active\nlast_test_result: null     # 'pass'|'fail'|null\nrefactor_stage: null       # 'test'|'impl'|null\n\n## 🤝 Agent Handoff\nhandoff_from: null         # Previous mode\nhandoff_to: null           # Expected next mode\nhandoff_summary: |         # Context for next agent\n  [Handoff details here]\nhandoff_timestamp: null\n\n## 📊 Mode History\n| Time | From | To | Trigger | Summary |\n|------|------|----|---------|---------|\n| -    | -    | -  | -       | -       |\n\n## 🔗 Cross-References\n- Brief: [↗️σ₁:Overview]\n- Patterns: [↗️σ₂:Architecture]\n- Tech: [↗️σ₃:Stack]\n- Progress: [↗️σ₅:Status]\n- Protection: [↗️σ₆:Registry]

**σ₅ progress.md:** # σ₅: Progress Tracker\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 📈 Project Status\nCompletion: 0%\nCurrent Phase: {PHASE}\nCurrent Mode: {MODE}\nTDD Mode: false\nTDD Cycles Completed: 0/0\n\n## ✅ Completed Tasks\n- [ ] Task 1\n- [ ] Task 2\n- [ ] Task 3\n\n## 🧪 TDD Cycle Progress\n### Completed Cycles\n- [ ] Cycle 1: [method_name] (ℜ→ℜᴳ→ℜᶠ) ✓\n- [ ] Cycle 2: [method_name] (ℜ→ℜᴳ→ℜᶠ) ✓\n\n### Current Cycle\n- [ ] Cycle N: [method_name]\n  - [ ] RED Phase (QA): Write failing tests\n  - [ ] GREEN Phase (DE): Minimal implementation\n  - [ ] REFACTOR Phase: Quality improvement\n\n### Pending Cycles\n- [ ] Cycle N+1: [method_name] → ℜ→ℜᴳ→ℜᶠ\n- [ ] Cycle N+2: [method_name] → ℜ→ℜᴳ→ℜᶠ\n\n## 🚧 In Progress\n- [ ] Current Task 1\n- [ ] Current Task 2\n\n## 📋 Pending Tasks\n- [ ] Future Task 1\n- [ ] Future Task 2\n\n## 🏁 Milestones\n- [ ] Milestone 1\n- [ ] Milestone 2\n- [ ] Milestone 3\n- [ ] TDD Integration Complete\n- [ ] All Cycles Verified\n\n## 📊 Quality Metrics\n- Test Coverage: 0%\n- Cycles with Refactor: 0/0\n- Failed Cycles: 0\n- Refactor Improvements Made: 0\n\n## 🔗 Cross-References\n- Active Context: [↗️σ₄:Focus]\n- Project Brief: [↗️σ₁:Goals]\n- TDD State: [↗️σ₄:TDD_Execution_State]

**σ₆ protection.md:** # σ₆: Protection Registry\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n*Π: {PHASE} | Ω: {MODE}*\n\n## 🛡️ Protected Regions\n[Protected code registry]\n\n### Critical Files\n- File 1: [Protection reason]\n- File 2: [Protection reason]\n\n### Protected Functions\n- Function 1: [Protection reason]\n- Function 2: [Protection reason]\n\n## 📜 Protection History\n[History and changes]\n\n## ✅ Approvals\n[Modification approvals]\n\n## ⚠️ Permission Violations\n[Violation logs]\n\n## 🔗 Cross-References\n- Active Context: [↗️σ₄:Status]\n- System Patterns: [↗️σ₂:Architecture]

**symbols.md:** # 🔣 Symbol Reference Guide\n*v1.0 | Created: {DATE} | Updated: {DATE}*\n\n## 📁 File Symbols\n- 📂 = /memory-bank/\n- 📦 = /memory-bank/backups/\n- 📄 = .md files\n- 📊 = data files\n- 📋 = configuration files\n\n## 🤖 RIPER Symbols\n- Ω₁ = Research Mode\n- Ω₂ = Innovate Mode\n- Ω₃ = Plan Mode\n- Ω₄ = Execute Mode\n- Ω₅ = Review Mode\n\n## 📚 Memory Symbols\n- σ₁ = projectbrief.md\n- σ₂ = systemPatterns.md\n- σ₃ = techContext.md\n- σ₄ = activeContext.md\n- σ₅ = progress.md\n- σ₆ = protection.md\n\n## 🔗 Reference Symbols\n- [↗️σₓ:Rₓ] = Cross-reference to memory file section\n- Γ₁ = Files, Γ₂ = Folders, Γ₃ = Code\n- Γ₄ = Commands, Γ₅ = Modify, Γ₆ = Web\n\n## 🛡️ Protection Symbols\n- Ψ₁-₃ = Proceed (Low risk)\n- Ψ₄-₆ = Caution + Confirm (High risk)

## CLAUDE.md Integration

**Memory-bank reference block to add (if missing):**

## 🧠 Memory Bank Integration

Detailed project memory stored in:

- Project Brief: [memory-bank/projectbrief.md](memory-bank/projectbrief.md)
- System Patterns: [memory-bank/systemPatterns.md](memory-bank/systemPatterns.md)  
- Tech Context: [memory-bank/techContext.md](memory-bank/techContext.md)
- Active Context: [memory-bank/activeContext.md](memory-bank/activeContext.md)
- Progress: [memory-bank/progress.md](memory-bank/progress.md)
- Protection: [memory-bank/protection.md](memory-bank/protection.md)

## Memory Protocol Reference
σ₁=brief | σ₂=patterns | σ₃=tech | σ₄=context | σ₅=progress | σ₆=protection

## Usage

```
/init-riper
```

**This enhanced version provides:**
- Incremental update strategy with user content protection
- Systematic task planning with 59 structured tasks
- Quality assurance through multi-stage auditing  
- Complete template compliance verification (no missing chapters)
- Automatic backup and safety mechanisms
- Cross-reference integrity management
- Error correction with targeted fixes
- Progress tracking via TodoWrite integration
- Improved content accuracy and completeness

**Expected outcomes:**
- Higher quality memory-bank initialization with user protection
- Significantly fewer manual corrections required
- Preserved user customizations and enhancements
- Better project context capture with incremental improvements
- Reliable cross-reference integrity and structure compliance