Implement a new Swift feature end-to-end: analysis, confirmation, implementation, and build validation.

## Usage

/swift-feature [description of the feature]

Example: `/swift-feature user profile screen that displays name, avatar, and a logout button`

## Phase 1 — Analysis

Before writing a single line of code:

1. Read the existing folder structure to understand where the feature belongs
2. Identify which files need to be created vs modified
3. Check if any required services or protocols already exist
4. Determine: does this need a new ViewModel? A new Service? A persistence change?

Present a concise plan:
```
Feature: [name]
New files:
  - Features/[Name]/[Name]View.swift
  - Features/[Name]/[Name]ViewModel.swift
Modified files:
  - App/ContentView.swift (add navigation entry)
Dependencies needed:
  - [Service] — already exists / needs to be created
```

**STOP. Wait for user confirmation before proceeding.**

---

## Phase 2 — Implementation

Apply the confirmed plan:

- Follow MVVM strictly: thin View, logic in ViewModel, data access in Service
- Inject all dependencies via `init`
- Handle loading state, error state, and empty state
- Add `#Preview` that compiles with mock or default data
- Use `async/await` — no completion handlers
- Consult the matching skill for detailed patterns:
  - UI → `swift-swiftui-component` or `swift-uikit-component` skill
  - Networking → `swift-networking` skill
  - Persistence → `swift-persistence` skill

---

## Phase 3 — Build Validation

Run `/swift-build` to confirm the project compiles.

- On success: proceed to Phase 4
- On failure: fix errors (max 2 attempts), then re-run
- If still failing after 2 attempts: stop and present errors to user

---

## Phase 4 — Test Check

Check if the new ViewModel or Service has tests:
- If yes: run tests for the affected target
- If no: flag it — "No tests found for [FeatureName]ViewModel. Use the `swift-testing` skill to add them."

Do not write tests automatically — keep this command focused on the feature implementation.

---

## Phase 5 — Summary

```
Feature complete: [name]

Files created:
  - [list]
Files modified:
  - [list]
Build: PASSED
Tests: [PASSED / Missing — use swift-testing skill]

Next steps:
  - [ ] Add tests with swift-testing skill
  - [ ] Run /swift-arch-check to verify compliance
```
