# iOS Testing Standards

A practical, production-ready testing standard for **Swift, UIKit, and SwiftUI** projects.

This repository provides two structured testing guidelines:

- **Enterprise Standard** — strict, scalable, CI-ready governance
- **Indie Standard** — lean, pragmatic, and sustainable for solo or small teams

Both versions are designed to be:
- Clear for humans
- Deterministic for CI
- Easy for AI tools to follow
- Aligned with Apple’s official testing guidance (XCTest, Swift Testing, XCUITest, Test Plans)

---

## Why This Exists

Testing culture in iOS projects often drifts toward:

- Testing implementation details instead of behavior
- Fragile UI tests
- Over-reliance on snapshots
- Poor async handling
- Coverage-driven vanity metrics
- Inconsistent architecture affecting testability

This repository defines a **consistent, architecture-driven testing contract** for modern Apple platform projects.

---

## What’s Included

### 1. Enterprise Version

For:
- Large teams
- Regulated environments
- CI/CD-heavy pipelines
- Code review governance
- High stability requirements

Includes:
- Strict architectural requirements
- Coverage expectations
- Async policies
- UI test boundaries
- Prohibited anti-patterns
- Test plan governance

---

### 2. Indie Version

For:
- Solo developers
- Small product teams
- Rapid iteration cycles
- Product-first experimentation

Focuses on:
- Fast feedback loops
- Minimal UI test overhead
- Testing logic over UI
- Keeping tests maintainable long-term

---

## Design Philosophy

These standards follow a few core principles:

### Behavior > Implementation
Tests must validate observable outcomes, not private internals.

### Determinism
No real network calls, no sleeping, no flakiness.

### Architecture First
If something is hard to test, the architecture likely needs improvement.

### Thin UI Layers
Business logic does not belong inside ViewControllers or SwiftUI Views.

### Async Correctness
Modern Swift concurrency must be tested with proper async patterns.

---

## Framework Compatibility

Designed for:

- Swift Testing (recommended for new Swift-first projects)
- XCTest
- XCUITest
- Xcode Test Plans
- Swift Concurrency (async/await)
- UIKit
- SwiftUI

---

## How To Use

1. Copy the version that fits your project:
   - `enterprise.md`
   - `indie.md`

2. Add it to:
   - `/Docs/Testing.md`
   - or your `/AI_INSTRUCTIONS.md`
   - or your `/CONTRIBUTING.md`

3. Enforce it in:
   - Pull requests
   - CI pipelines
   - Code review guidelines

---

## Who This Is For

- iOS engineers
- Swift developers
- Technical leads
- Indie Apple developers
- Teams adopting Swift Concurrency
- Teams modernizing legacy UIKit projects

---

## Not Included (On Purpose)

This repository does NOT include:

- Snapshot testing mandates
- Third-party testing frameworks
- Opinionated architecture frameworks (e.g., TCA, VIPER, etc.)
- Mocking library requirements

It stays framework-neutral while enforcing quality boundaries.

---

## Contribution Philosophy

If contributing:

- Propose changes that align with Apple’s official guidance.
- Avoid adding opinionated architectural mandates unless widely accepted.
- Prioritize clarity and maintainability.
- Keep rules enforceable and practical.

---

## License

MIT — use freely in personal or commercial projects.

---

## Final Note

Good tests don’t slow teams down.  
Bad tests do.

These standards aim to make testing:
- Reliable
- Predictable
- Architecture-aligned
- Sustainable over time