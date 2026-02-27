# CLAUDE.md — Swift / SwiftUI / UIKit Project Instructions

## Project Configuration
<!-- Fill these in at the start of every project or when onboarding -->
- **Project Name**: [MyApp]
- **Testing Mode**: [enterprise | indie]
- **UI Framework**: [SwiftUI | UIKit | Both]
- **Min iOS Version**: [17.0]
- **Architecture**: MVVM

---

## Swift Standards

### Naming
- Types: `UpperCamelCase`
- Functions / variables: `lowerCamelCase`
- Protocols: noun or adjective (`Repository`, `Configurable`, `UserServiceProtocol`)
- Booleans: assertion form (`isLoading`, `hasError`, `canSubmit`)
- Test methods: `test_when_<Condition>_should_<ExpectedOutcome>()`

### Architecture (MVVM — Default)
- **Views** are thin, declarative shells — no business logic, no network calls, no storage access
- **ViewModels** own state (`@Observable` or `ObservableObject`) and orchestrate services
- **Services / Repositories** handle data access (network, persistence, etc.)
- **All external dependencies** are injected via initializer or environment — no hardcoded singletons
- Business logic inside `UIViewController` subclasses or SwiftUI `View` bodies is forbidden

### Swift Concurrency
- Use `async/await` for all new asynchronous code — no completion handlers
- Mark UI-bound state with `@MainActor`
- No `DispatchQueue.main.async` in ViewModel or Service layers — use `@MainActor` instead
- Never use `sleep()` — use proper async coordination

### Code Style
- Prefer `let` over `var`
- No force unwrapping (`!`) in production paths
- Use `throws` or `Result<T, Error>` for error propagation — no silent failures
- Keep files focused: one primary type per file
- No magic numbers — use named constants

---

## Workflow Orchestration

### 1. Plan First
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways: STOP and re-plan — don't keep pushing
- Write detailed specs upfront to reduce ambiguity
- Use plan mode for verification steps, not just building

### 2. Subagent Strategy
- Use subagents to keep the main context window clean
- Offload codebase exploration, research, and parallel analysis to subagents
- One task per subagent for focused execution

### 3. Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules that prevent the same mistake
- Review lessons at session start for relevant context

### 4. Verification Before Done
- Never mark a task complete without proving it works
- Run tests, check the build, verify behavior matches intent
- Ask: "Would a senior iOS engineer approve this PR?"

### 5. Demand Elegance
- For non-trivial changes: pause and ask "is there a more elegant solution?"
- If a fix feels hacky: re-approach from first principles
- Skip for simple, obvious fixes — don't over-engineer

### 6. Autonomous Bug Fixing
- When given a bug report: fix it — don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them

---

## Task Management

1. Write plan to `tasks/todo.md` with checkable items
2. Check in before starting implementation on complex tasks
3. Mark items complete as you go
4. High-level summary at each step
5. Update `tasks/lessons.md` after any correction

---

## Core Principles

- **Simplicity First**: Make every change as simple as possible. Minimal code impact.
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standards.
- **Testability**: If something is hard to test, the architecture likely needs improvement.
- **Thin UI Layers**: Business logic does not belong in Views or ViewControllers.
- **Minimal Impact**: Changes should only touch what is necessary. Avoid introducing bugs.

---

## Available Skills

Install these in `.claude/skills/` for repeatable, auto-triggering workflows.
Copy from the `swift-unit-test-instructions` repo.

| Skill folder | Use when... |
|---|---|
| `swift-project-setup` | Starting a new Swift/SwiftUI/UIKit project |
| `swift-testing` | Writing unit or UI tests for any Swift code |
| `swift-architecture-audit` | Auditing or onboarding to an existing codebase |
| `swiftui-component` | Creating SwiftUI views or screens |
| `swift-networking` | Building a networking layer with async/await |
| `swift-code-review` | Reviewing Swift code for standards compliance |
