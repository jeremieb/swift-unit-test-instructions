# Swift Claude Code Framework

A reusable framework of Claude Code instructions for **Swift, SwiftUI, and UIKit** projects.

It combines a project-level `CLAUDE.md` template with a set of focused skills that auto-trigger based on what you ask Claude to do — so you stop re-explaining standards on every project and every conversation.

---

## What's Inside

```
CLAUDE.md                           # Drop into any Swift project root
enterprise.md                       # Enterprise testing standard (human reference)
indiedev.md                         # Indie testing standard (human reference)
skills/
├── swift-project-setup/            # Scaffold a new project
├── swift-testing/                  # Write unit and UI tests
│   └── references/
│       ├── enterprise.md           # Strict, CI-ready standard
│       └── indie.md                # Lean, pragmatic standard
├── swift-architecture-audit/       # Audit or onboard to an existing codebase
├── swiftui-component/              # Create SwiftUI views and ViewModels
├── swift-networking/               # Build a networking layer with async/await
├── swift-code-review/              # Review Swift code for standards compliance
└── swift-project-setup/
    └── references/
        ├── structure-swiftui.md    # SwiftUI folder structure
        ├── structure-uikit.md      # UIKit folder structure
        ├── structure-mixed.md      # Mixed SwiftUI + UIKit structure
        ├── file-naming.md          # Naming conventions and group rules
        ├── gitignore-xcode.md      # .gitignore for Xcode projects
        └── spm-skeleton.md         # Package.swift skeleton
```

---

## Quick Start

### New project

1. **Copy `CLAUDE.md`** into your project root
2. **Fill in the config block** at the top:
   ```
   - Project Name: MyApp
   - Testing Mode: enterprise | indie
   - UI Framework: SwiftUI | UIKit | Both
   - Min iOS Version: 17.0
   ```
3. **Copy the `skills/` folder** into `.claude/skills/` in your project
4. Ask Claude: *"set up the project structure"* — it picks the right template and scaffolds everything

### Existing project

1. **Copy `CLAUDE.md`** into your project root and fill in the config block
2. **Copy the `skills/` folder** into `.claude/skills/`
3. Ask Claude: *"audit the architecture"* — it scans the codebase, compares against the standard structure, and gives you a prioritized list of issues to fix

---

## How Skills Work

Skills are instruction packages that Claude loads **only when relevant** — you don't pay the token cost of loading testing rules when you're building a view, or networking rules when you're writing tests.

| Skill | Ask Claude... |
|---|---|
| `swift-project-setup` | *"scaffold a new SwiftUI app"*, *"set up the project"* |
| `swift-testing` | *"write tests for this ViewModel"*, *"add unit tests"* |
| `swift-architecture-audit` | *"audit the architecture"*, *"why is this hard to test"* |
| `swiftui-component` | *"create a profile screen"*, *"add a SwiftUI view"* |
| `swift-networking` | *"add a networking layer"*, *"fetch data from this API"* |
| `swift-code-review` | *"review this code"*, *"check this PR"* |

Each skill asks a clarifying question before loading detail — for example, `swift-project-setup` asks SwiftUI, UIKit, or Mixed before pulling in the relevant folder structure template. `swift-testing` checks your `Testing Mode` config to apply enterprise or indie standards.

---

## Testing Standards

The `enterprise.md` and `indiedev.md` files at the root are **standalone human references** — copy them into your project docs, CONTRIBUTING.md, or CI guidelines. They are also bundled inside the `swift-testing` skill as references Claude reads when writing tests.

**Enterprise** — for large teams, regulated environments, CI/CD pipelines:
- Strict architecture requirements and coverage expectations
- Mandatory test plan governance
- Async determinism policy

**Indie** — for solo developers and small product teams:
- Fast feedback loops, minimal overhead
- Test logic over UI
- Sustainable long-term

---

## Design Principles

- **Thin UI layers** — business logic never lives in Views or ViewControllers
- **Behavior over implementation** — tests validate outcomes, not internals
- **Testability as a design signal** — if something is hard to test, the architecture needs improvement
- **MVVM by default** — ViewModels own state, Services own data access, Views own nothing

---

## License

MIT — use freely in personal or commercial projects.
