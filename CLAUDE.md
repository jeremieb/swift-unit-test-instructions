# CLAUDE.md — Swift / SwiftUI / UIKit Project

## Project Configuration
<!-- Fill these in when starting or onboarding to a project -->
- **Project Name**: [MyApp]
- **Testing Mode**: [enterprise | indie]
- **UI Framework**: [SwiftUI | UIKit | Both]
- **Min iOS Version**: [17.0]
- **Architecture**: MVVM

---

## Workflow

- Enter plan mode for any non-trivial task (3+ steps or architectural decisions)
- Never mark a task complete without running tests and verifying the build
- After any user correction: update `tasks/lessons.md` to prevent the same mistake
- When given a bug: fix it autonomously — point at logs, errors, failing tests, then resolve

---

## Core Principles

- Simplicity first. Minimal code impact. One thing at a time.
- Thin UI layers. Business logic never belongs in Views or ViewControllers.
- If something is hard to test, the architecture needs improvement — not the test.

---

## Available Skills

Install in `.claude/skills/` — they auto-trigger based on your request.

| Skill | Triggers on |
|---|---|
| `swift-project-setup` | "new project", "scaffold", "setup app" |
| `swift-testing` | "write tests", "add unit tests", "test this" |
| `swift-architecture-audit` | "audit codebase", "why is this untestable", "onboard" |
| `swiftui-component` | "create view", "add screen", "build UI" |
| `swift-networking` | "add networking", "create API layer" |
| `swift-code-review` | "review this", "check this PR" |
