Read-only architecture audit. Scans the project and produces a structured report. Makes NO changes to any file.

## Rules

- Read files only — never edit, never write
- If a fix is obvious, describe it in the report but do not apply it
- Cover every layer: structure, MVVM compliance, persistence, networking, concurrency

## Steps

### 1. Detect UI framework

Scan for `@main`, `UIApplicationDelegate`, `UIHostingController`. Determine: SwiftUI / UIKit / Mixed.

### 2. Check folder structure

Compare against the matching reference:
- SwiftUI → `skills/swift-project-setup/references/structure-swiftui.md`
- UIKit → `skills/swift-project-setup/references/structure-uikit.md`
- Mixed → `skills/swift-project-setup/references/structure-mixed.md`

Note every deviation: missing folders, files in wrong locations, misnamed groups.

### 3. Check MVVM compliance

Read 3–5 representative feature files. Flag:
- Business logic inside `View` or `ViewController`
- Network or storage calls not behind a protocol
- Missing `ViewModel` for screens with non-trivial state
- `@State` holding data that belongs in a `ViewModel`

### 4. Check persistence layer (if present)

Identify whether project uses SwiftData, CoreData, or neither. Flag:
- `ModelContext` or `NSManagedObjectContext` used directly in `ViewModel` or `View`
- Missing repository abstraction over persistence
- Models not separated from UI layer

### 5. Check concurrency

Flag:
- `DispatchQueue.main.async` in `ViewModel` or `Service` layer
- Missing `@MainActor` on types that update UI state
- `sleep()` anywhere
- Completion handlers in new code where `async/await` should be used

### 6. Check testability

Flag:
- Dependencies instantiated inside types (`let service = NetworkService()`)
- No protocol abstraction for external dependencies
- `ViewModel` that imports `SwiftUI` or `UIKit`

### 7. Output report

```markdown
# Architecture Audit: [ProjectName]

## Health: [Good / Needs Work / Critical Issues]

## Structure
- [deviation or ✓ Correct]

## MVVM Compliance
- [issue with file:line, or ✓ Compliant]

## Persistence Layer
- [issue with file:line, or ✓ Correct, or — Not used]

## Concurrency
- [issue with file:line, or ✓ Correct]

## Testability
- [issue, or ✓ Testable]

## Priority Fixes
1. [Most critical]
2. [Second]
3. [Third]
```
