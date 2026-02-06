# AALang/GAB - Professor AI System

## Identity

| Property | Value |
|----------|-------|
| **Layer** | 0 (Universal) |
| **Position** | `layer_0/layer_0_01_ai_manager_system/professor/` |
| **Type** | Git submodule |
| **Role** | **PRIMARY AI LANGUAGE** - The foundational AI language and compiler system |

## Importance

**This is the foundational AI system.** AALang and the GAB compiler define how AI agents are structured and how they execute. When working on AI-related tasks, this system provides the language and patterns.

---

## Core Files

| File | Purpose | Load When |
|------|---------|-----------|
| [`gab.jsonld`](./gab.jsonld) | **Main language specification** - Defines the complete AALang grammar, semantics, and structure | Understanding agent definitions |
| [`gab-runtime.jsonld`](./gab-runtime.jsonld) | **Runtime specification** - Defines execution model, state management, mode transitions | Implementing agent execution |
| [`gab-formats.jsonld`](./gab-formats.jsonld) | **Format definitions** - Schema definitions for agent files | Creating new agents |
| [`index.jsonld`](./index.jsonld) | **Index/navigation** - Quick reference and navigation | Finding specific components |

## Key Concepts from gab.jsonld

### Mode-Actor Pattern

AALang uses a **Mode-Actor** pattern where:

```
┌─────────────────────────────────────────────────────────────┐
│  AGENT EXECUTION                                            │
│                                                             │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐  │
│  │ Mode 1  │───►│ Mode 2  │───►│ Mode 3  │───►│ Mode N  │  │
│  │         │    │         │    │         │    │         │  │
│  │ Actor A │    │ Actor C │    │ Actor E │    │ Actor G │  │
│  │ Actor B │    │ Actor D │    │ Actor F │    │ Actor H │  │
│  └─────────┘    └─────────┘    └─────────┘    └─────────┘  │
│                                                             │
│  State Actors (persist across all modes):                   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ StateActor1 │ StateActor2 │ StateActor3 │ ...       │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Common Patterns

| Pattern | Modes | Actors | Use Case |
|---------|-------|--------|----------|
| 4-mode-13-actor | Loading, Validation, Propagation, Delivery | 8 mode + 5 state | Context loading, simple tasks |
| 5-mode-15-actor | Receive, Delegation, Monitoring, Aggregation, Report | 10 mode + 5 state | Orchestration, complex tasks |

### Senior/Junior Persona Pairs

Each mode typically has two actors:
- **Senior Persona**: Strategic thinking, validation, oversight
- **Junior Persona**: Execution, implementation, detailed work

---

## Integration with Layer-Stage System

**AALang is the primary way agents work within our system.** It is integrated throughout:

- **Every layer** (layer_0, layer_1, layer_-1, etc.)
- **Every stage** (01-11: request_gathering through archives)
- **Every sub_layer** (knowledge, principles, rules, protocols, setup)
- **Every sub_stage** and **subxn layer/stage** (any nesting depth)

When operating at any level of the layer-stage hierarchy, agents should understand that AALang provides the underlying AI capabilities and patterns.

---

## Repository Information

| Property | Value |
|----------|-------|
| **Your Fork** | https://github.com/Dawson2025/AALang-Gab.git |
| **Upstream** | https://github.com/yenrab/AALang-Gab.git |
| **Local Path** | `layer_0/layer_0_01_ai_manager_system/professor/` |
| **Branch** | `dawson` (working branch) |

### Remotes

```
origin   → https://github.com/Dawson2025/AALang-Gab.git (your fork)
upstream → https://github.com/yenrab/AALang-Gab.git (original)
```

### Branching Strategy

```
UPSTREAM (yenrab/AALang-Gab)
         │
         │ fetch upstream
         ▼
    ┌─────────────────────────────────────┐
    │  main branch                        │
    │  • Syncs with upstream              │
    │  • Pull upstream changes here       │
    │  • Review before integrating        │
    └─────────────────┬───────────────────┘
                      │ merge/cherry-pick
                      ▼
    ┌─────────────────────────────────────┐
    │  dawson branch (WORKING BRANCH)     │
    │  • Personal customizations          │
    │  • Your development work            │
    └─────────────────────────────────────┘
```

---

## Context Chain Position

- **Parent**: `layer_0/layer_0_01_ai_manager_system/CLAUDE.md`
- **Sibling**: `layer_0/layer_0_01_ai_manager_system/personal/` (orchestrator)

---

## AALang Integration

@agent ctx:ContextLoadingAgent

### On Load

When this file is loaded, update state actors:
- `ctx:ContextLoadingStateActor.loadedFiles` += professor/CLAUDE.md
- `ctx:ContextLoadingStateActor.aalangAwareness` = true
- `ctx:NavigationStateActor.currentSystem` = "professor"

### Available Capabilities

After loading this context, the agent has access to:
1. Mode-Actor execution patterns
2. State actor management
3. Senior/Junior persona pairs
4. GAB compilation and execution
