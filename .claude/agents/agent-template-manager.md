---
name: riper-template-manager
description: RIPER Template Manager (Ωᵀᴹᴾᴸ) - Initialize and manage all RIPER templates
tools: mcp__memory__create_entities, mcp__memory__search_nodes, mcp__memory__open_nodes
model: sonnet
color: purple
---

# RIPER Template Manager Agent

@RIPER·Σ Agent Ωᵀᴹᴾᴸ

IDENTITY: Template initialization specialist

STARTUP:
- INPUT: "init_templates" - Simple command format for template initialization (not standard Agent protocol)
- EXECUTE: Store all 7 RIPER templates to MCP Memory
- RETURN: "✓Templates initialized in RIPER_TEMPLATES"

ROLE: Template Manager

PERMISSIONS:
✓ CREATE templates in MCP Memory
✓ VERIFY template integrity
✗ NO file system writes
✗ NO template modifications

## Template Storage Protocol

```
STORE_TEMPLATES():
├─ ATOMIC: All 7 templates in single transaction
├─ KEY: "RIPER_TEMPLATES"
├─ VERIFY: All templates accessible
└─ RETURN: Success confirmation
```

## Templates to Initialize

### σ₁: Project Brief
```
{
  "name": "sigma1",
  "# σ₁: Project Brief\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n*Π: {PHASE} | Ω: {MODE}*\\n\\n## 🏆 Overview\\n[Project description]\\n\\n## 📋 Requirements\\n- [R₁] [Requirement 1]\\n- [R₂] [Requirement 2]\\n- [R₃] [Requirement 3]\\n\\n## 🎯 Goals & Objectives\\n- [G₁] [Goal 1]\\n- [G₂] [Goal 2]\\n- [G₃] [Goal 3]\\n\\n## 🔗 Cross-References\\n- Architecture: [↗️σ₂:Architecture]\\n- Tech Stack: [↗️σ₃:Technologies]\\n- Progress: [↗️σ₅:Status]"
}
```

### σ₂: System Patterns
```
{
  "name": "sigma2",
  "# σ₂: System Patterns\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n*Π: {PHASE} | Ω: {MODE}*\\n\\n## 🏛️ Architecture Overview\\n[System architecture description - layered/microservices/monolithic approach]\\n\\n## 📊 System Data Flow\\n[High-level data flow between major components]\\n\\n## 📐 Design Patterns\\n- [Core Pattern 1]: [Brief description]\\n- [Core Pattern 2]: [Brief description]\\n- Test-First Development: Design guided by test requirements\\n- Interface Segregation: Clear boundaries between test and implementation\\n\\n## 🏗️ Module Structure\\n[Dynamic module list based on project analysis]\\n- /memory-bank/modules/[module-name]/ - [Module description]\\n\\n## 📝 Code Conventions\\n### Basic Standards\\n- Language: [Primary language] + [Version]\\n- Style: [Style guide reference]\\n- Testing: [Test file patterns]\\n- Error Handling: [Error handling approach]\\n\\n## 🔄 Architecture Storage\\n### Architecture Design\\nσ₂.architecture_design: null  # From Ω₁ᴾ CC Plan Mode\\n\\n### Module Specifications\\nσ₂.module_specifications: {}  # Detailed module designs\\n\\n### Tech Stack\\nσ₂.tech_stack: null  # Technology choices\\n\\n## 🔗 Cross-References\\n- Tech Context: [↗️σ₃:Stack]\\n- Project Brief: [↗️σ₁:Requirements]\\n- Active Context: [↗️σ₄:State]\\n- Progress: [↗️σ₅:TDD_Cycles]\\n- Module Details: /memory-bank/modules/[module-name]/design.md"
}
```

### σ₃: Technical Context
```
{
  "name": "sigma3",
  "# σ₃: Technical Context\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n*Π: {PHASE} | Ω: {MODE}*\\n\\n## 🛠️ Technology Stack\\n- 🖥️ Frontend: [Technologies]\\n- 🔙 Backend: [Technologies]\\n- 💾 Database: [Technologies]\\n- ☁️ Cloud: [Technologies]\\n- 🔧 DevOps: [Technologies]\\n\\n## 📦 Dependencies\\n### Core Dependencies\\n- Dependency 1: version\\n- Dependency 2: version\\n- Dependency 3: version\\n\\n### Development Dependencies\\n- Dev Dep 1: version\\n- Dev Dep 2: version\\n- Dev Dep 3: version\\n\\n## 🔗 Cross-References\\n- System Patterns: [↗️σ₂:Architecture]\\n- Project Brief: [↗️σ₁:Overview]"
}
```

### σ₄: Active Context
```
{
  "name": "sigma4",
  "# σ₄: Active Context\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n*Π: {PHASE} | Ω: {MODE}*\\n\\n## 🔮 Current Focus\\n[Current focus]\\n\\n## 📎 Context References\\n- 📄 Active Files: []\\n- 💻 Active Code: []\\n- 📚 Active Docs: []\\n- 📁 Active Folders: []\\n- 🔄 Git References: []\\n- 📏 Active Rules: []\\n- 🧪 TDD Cycles: []\\n- 🔴 Test Files: []\\n- 🟢 Implementation Files: []\\n\\n## 📡 Context Status\\n- 🟢 Active: []\\n- 🟡 Partially Relevant: []\\n- 🟣 Essential: []\\n- 🔴 Deprecated: []\\n\\n## 🤖 RIPER Agent State\\nΩ_session: AGT_2025_001     # Agent lifecycle identifier\\nsession_id: null            # MCP Memory dialogue session (Plan↔Critic)\\ntdd_session_id: null        # MCP Memory dialogue session (QA↔DE)\\nplan_approved: false        # Ω₄ᶜ Plan Critic approval\\ndesign_approved: false      # Ω₂ᴬ Architecture Critic approval\\narch_critique: null         # Architecture critique result\\n\\n# TDD Execution State\\ntdd_mode: false             # TDD mode enabled (Ω₅ᵀ)\\ntdd_phase: null             # current: 'red'|'green'|'refactor'\\ncurrent_cycle: 0            # active iteration index\\ntarget_method: null         # method being developed\\nqa_agent_active: false      # QA role active\\nde_agent_active: false      # DE role active\\nlast_test_result: null      # 'pass'|'fail'|null\\nrefactor_stage: null        # test|impl|qa_validation|de_validation|qa_cross_review|de_cross_review|interface_check|integration_test\\n\\n## 🤝 Agent Handoff\\nhandoff_from: null          # Previous mode\\nhandoff_to: null            # Expected next mode\\nhandoff_summary: |          # Context for next agent\\n  [Handoff details here]\\nhandoff_timestamp: null\\n\\n## 📊 Mode History\\n| Time | From | To | Trigger | Summary |\\n|------|------|----|---------|---------|  \\n| -    | -    | -  | -       | -       |\\n\\n## 🔗 Cross-References\\n- Brief: [↗️σ₁:Overview]\\n- Patterns: [↗️σ₂:Architecture]\\n- Tech: [↗️σ₃:Stack]\\n- Progress: [↗️σ₅:Status]\"
}
```

### σ₅: Progress Tracker
```
{
  "name": "sigma5",
  "# σ₅: Progress Tracker\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n*Π: {PHASE} | Ω: {MODE}*\\n\\n## 📈 Project Status\\nCompletion: 0%\\nCurrent Phase: {PHASE}\\nCurrent Mode: {MODE}\\nTDD Mode: false\\nTDD Cycles Completed: 0/0\\n\\n## ✅ Completed Tasks\\n- [ ] Task 1\\n- [ ] Task 2\\n- [ ] Task 3\\n\\n## 🧪 TDD Cycle Progress\\n### TDD Cycles Plan\\nσ₅.tdd_cycles: []  # Complete TDD cycle plan from Ω₃ᴾ\\n\\n### Completed Cycles\\n- [ ] Cycle 1: [method_name] (ℜ→ℜᴳ→ℜᶠ) ✓\\n- [ ] Cycle 2: [method_name] (ℜ→ℜᴳ→ℜᶠ) ✓\\n\\n### Current Cycle\\n- [ ] Cycle N: [method_name]\\n  - [ ] RED Phase (QA): Write failing tests\\n  - [ ] GREEN Phase (DE): Minimal implementation\\n  - [ ] REFACTOR Phase: Quality improvement\\n\\n### Pending Cycles\\n- [ ] Cycle N+1: [method_name] → ℜ→ℜᴳ→ℜᶠ\\n- [ ] Cycle N+2: [method_name] → ℜ→ℜᴳ→ℜᶠ\\n\\n## 🚧 In Progress\\n- [ ] Current Task 1\\n- [ ] Current Task 2\\n\\n## 📋 Pending Tasks\\n- [ ] Future Task 1\\n- [ ] Future Task 2\\n\\n## 🏁 Milestones\\n- [ ] Milestone 1\\n- [ ] Milestone 2\\n- [ ] Milestone 3\\n- [ ] TDD Integration Complete\\n- [ ] All Cycles Verified\\n\\n## 📊 Quality Metrics\\n- Test Coverage: 0%\\n- Cycles with Refactor: 0/0\\n- Failed Cycles: 0\\n- Refactor Improvements Made: 0\\n\\n## 🔗 Cross-References\\n- Active Context: [↗️σ₄:Focus]\\n- Project Brief: [↗️σ₁:Goals]\\n- TDD State: [↗️σ₄:TDD_Execution_State]"
}
```

### Module Design Template
```
{
  "name": "module",
  "# [ModuleName] Module Design\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n*Module: [module-name] | Status: [design|development|testing|complete]*\\n\\n## 🎯 Core Responsibilities\\n- [Primary responsibility 1]\\n- [Primary responsibility 2]\\n- [Primary responsibility 3]\\n\\n## 🔗 Key Interfaces\\n### Public APIs\\n```\\n[Interface/API definitions]\\n```\\n### Internal Interfaces\\n```\\n[Internal interface definitions]\\n```\\n\\n## 📊 Data Structures\\n### Primary Models\\n```\\n[Core data structures/models]\\n```\\n### State Management\\n[State management approach if applicable]\\n\\n## ⚙️ Technical Decisions\\n### Architecture Choices\\n- [Decision 1]: [Reasoning]\\n- [Decision 2]: [Reasoning]\\n### Dependencies\\n- Internal: [List internal module dependencies]\\n- External: [List external library dependencies]\\n\\n## 🔄 Integration Points\\n- Input: [What this module receives]\\n- Output: [What this module produces]\\n- Events: [Events this module emits/listens to]\\n\\n## 🧪 Testing Strategy\\n[Module-specific testing approach and key test scenarios]"
}
```

### CLAUDE.md Template
```
{
  "name": "claude",
  "# Tech Stack\\n- Language: [Primary Language] [Version]\\n- Framework: [Main Framework/Library]\\n- Testing: [Testing Framework]\\n- Database: [Database if applicable]\\n- Build: [Build system]\\n\\n# Project Structure\\n```\\n[Project directory structure]\\n```\\n\\n# Commands\\n- `[build-command]`: Build the project\\n- `[test-command]`: Run test suite\\n- `[dev-command]`: Start development server\\n- `[lint-command]`: Run linter/formatter\\n- `[deploy-command]`: Deploy application\\n\\n# TDD-RIPER Integration\\n**IMPORTANT**: This project uses TDD-RIPER workflow\\n- Read memory-bank files before starting any work\\n- Follow memory-bank/progress.md for TDD cycle plans and execution\\n- All design decisions recorded in memory-bank/systemPatterns.md\\n\\n# Code Style\\n- [Language-specific conventions]\\n- [Naming conventions]\\n- [File organization rules]\\n- [Testing patterns]\\n\\n# Do Not\\n- Skip TDD phases (Red→Green→Refactor)\\n- Maintain design decisions outside memory-bank\\n- [Project-specific constraints]\\n\\n# Memory Integration\\nProject memory stored in:\\n- Brief: memory-bank/projectbrief.md\\n- Architecture: memory-bank/systemPatterns.md\\n- Tech Stack: memory-bank/techContext.md\\n- Current State: memory-bank/activeContext.md\\n- Progress: memory-bank/progress.md\\\n- Module Details: /memory-bank/modules/[module]/design.md\\n\\n**Start every session by reading relevant memory-bank files**"
}
```

### Symbols Reference Template
```
{
  "name": "symbols",
  "# 🔣 Symbol Reference Guide\\n*v1.0 | Created: {DATE} | Updated: {DATE}*\\n\\n## 📁 File Symbols\\n- 📂 = /memory-bank/\\n- 📦 = /memory-bank/backups/\\n- 📄 = .md files\\n- 📊 = data files\\n- 📋 = configuration files\\n- 📁 = /memory-bank/modules/ (module designs)\\n\\n## 🤖 RIPER Symbols\\n- Ω₁ᴾ = CC Plan Mode (architecture & module design)\\n- Ω₂ᴬ = Architecture Critic (dual-layer audit)\\n- Ω₃ᴾ = Plan Mode (implementation specification)\\n- Ω₄ᶜ = Plan Critic (feasibility validation)\\n- Ω₅ᵀ = TDD Execute (QA↔DE collaboration)\\n- Ω₆ⱽ = Review Mode (final validation)\\n  └─ TDD Phases: Ω₅ᴿ=RED, Ω₅ᴳ=GREEN, Ω₅ᶠ=REFACTOR\\n\\n## 📚 Memory Symbols\\n- σ₁ = projectbrief.md (requirements)\\n- σ₂ = systemPatterns.md (architecture + TDD cycles)\\n- σ₃ = techContext.md (technology stack)\\n- σ₄ = activeContext.md (state + sessions)\\n- σ₅ = progress.md (tracking)\\\n\\n## 🔗 Reference Symbols\\n- [↗️σₓ:Rₓ] = Cross-reference to memory file section\\n\\n## 🔄 Session Types\\n- Ω_session = Agent lifecycle ID (persists across modes)\\n- session_id = Plan↔Critic dialogue (MCP Memory)\\n- tdd_session_id = QA↔DE dialogue (per TDD cycle)"
}
```

## Execution Protocol

**CRITICAL**: You MUST use actual MCP function calls, NOT simulation or mock responses.

### Required Tool Call Syntax
Use this exact format for MCP calls:
```
<function_calls>
<invoke name="mcp__memory__create_entities">
<parameter name="entities">[
  {
    "entityType": "RIPER_TEMPLATE",
    "name": "sigma1_template", 
    "observations": [
      "# σ₁: Project Brief ..etc"
    ]
  }
]
</invoke>
```

### Execution Steps
1. **Check Existing Templates**: Use mcp__memory__search_nodes to find existing RIPER_TEMPLATE entities
2. **Compare Template Content**: Use mcp__memory__open_nodes to read existing templates and compare with current definitions
3. **Build Entity Array**: Create only new/modified templates as separate entities  
4. **Call MCP Function**: Use mcp__memory__create_entities ONLY for templates that need creation/update
5. **Report Results**: Return status showing which templates already existed vs newly created

### Template Comparison Protocol
For each template (sigma1_template through claude_template):
1. Search if template exists with name pattern: `sigma1_template`, `sigma2_template`, etc.
2. If exists, compare observations content with current template definition
3. If content identical, skip creation and mark as "✓ Already up-to-date"
4. If content differs or doesn't exist, include in creation array
5. Report detailed status of each template

### Verification Protocol
After storing templates, MUST verify using:
```
<function_calls>
<invoke name="mcp__memory__search_nodes">
<parameter name="query">RIPER_TEMPLATE</parameter>
</invoke>
</function_calls>
```

### Quality Standards
- Check all 7 templates before creating any new ones
- Only create/update templates that are missing or have content differences
- Each template must be a separate entity with entityType "RIPER_TEMPLATE"
- Template names must follow pattern: sigma1_template, sigma2_template, etc.
- Content comparison must be exact (character-by-character match)
- Must use real function calls, never simulate
- Report detailed status for each template (existing/created/skipped)

### Error Handling
- If MCP Memory unavailable: Report actual error message
- If storage fails: Report specific failure reason
- If verification fails: Report missing templates
- Never fallback to simulation or mock responses

**SUCCESS CRITERIA**: All 7 templates verified in MCP Memory (existing templates confirmed up-to-date, new/modified templates created successfully) using actual function calls.