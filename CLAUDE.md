# AALang AI System

## Identity

**Layer**: 0 (Universal)
**Position**: sub_layer_0_01_ai_system
**Type**: Git submodule
**Role**: **PRIMARY AI SYSTEM** - The AI language and compiler system used for most everything

## Importance

**This is the main AI system we use.** AALang and the gab compiler are central to how we work with AI. When working on AI-related tasks, this system is the foundation.

## Integration with Layer-Stage System

**AALang is the primary way agents work within our system.** It is integrated throughout:

- **Every layer** (layer_0, layer_1, layer_-1, etc.)
- **Every stage** (01-11: request_gathering through archives)
- **Every sub_layer** (knowledge, principles, rules, protocols, setup)
- **Every sub_stage** and nested structure

When operating at any level of the layer-stage hierarchy, agents should understand that AALang provides the underlying AI capabilities and patterns for how work gets done.

## Repository Information

| Property | Value |
|----------|-------|
| **Your Fork** | https://github.com/Dawson2025/AALang-Gab.git |
| **Upstream** | https://github.com/yenrab/AALang-Gab.git |
| **Local Path** | `layer_0/layer_0_03_sub_layers/sub_layer_0_01_ai_system/` |

## Branching Strategy

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
    │  • DO NOT work directly on main     │
    └─────────────────┬───────────────────┘
                      │
                      │ merge/cherry-pick desired changes
                      ▼
    ┌─────────────────────────────────────┐
    │  dawson branch (WORKING BRANCH)     │
    │  • Personal customizations          │
    │  • Your development work            │
    │  • Safe to experiment               │
    └─────────────────────────────────────┘
```

### Branch Purposes

| Branch | Purpose | Usage |
|--------|---------|-------|
| `main` | Upstream sync | Pull from upstream, review changes, never work here directly |
| `dawson` | Personal work | All customizations, development, experiments |

## Workflow

### Syncing with Upstream

```bash
# Add upstream remote (one-time setup)
git remote add upstream https://github.com/yenrab/AALang-Gab.git

# Fetch upstream changes
git fetch upstream

# Merge upstream into main (for review)
git checkout main
git merge upstream/main

# Review changes, then integrate desired ones into dawson
git checkout dawson
git merge main  # or cherry-pick specific commits
```

### Daily Development

```bash
# Always work on dawson branch
git checkout dawson

# Make changes, commit, push
git add .
git commit -m "Description of changes"
git push origin dawson
```

## Contents

This repository contains:
- **AALang** - AI-focused programming language
- **Gab Compiler** - Compiler for AALang
- **JSON-LD schemas** - Language and runtime specifications

## Key Files

| File | Purpose |
|------|---------|
| `gab.jsonld` | Main language specification |
| `gab-runtime.jsonld` | Runtime specification |
| `gab-formats.jsonld` | Format definitions |
| `index.jsonld` | Index/navigation |
| `README.md` | Project documentation |

## Parent Context

- **Parent**: `layer_0/layer_0_03_sub_layers/`
- **Siblings**: knowledge_system, principles, rules, protocols, setup_dependant_hierarchy

---

*This file is maintained on the `dawson` branch for context chain integration.*
