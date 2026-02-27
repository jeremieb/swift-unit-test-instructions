# Xcode / Swift Project Structure Reference

## Folder Structure — SwiftUI App

```
MyApp/
├── App/
│   ├── MyAppApp.swift              # @main entry point
│   └── ContentView.swift           # Root view (keep thin — delegates to features)
│
├── Features/                       # One folder per user-facing feature
│   ├── Home/
│   │   ├── HomeView.swift
│   │   ├── HomeViewModel.swift
│   │   └── HomeModel.swift         # Feature-specific data model (if needed)
│   ├── Profile/
│   │   ├── ProfileView.swift
│   │   └── ProfileViewModel.swift
│   └── Settings/
│       ├── SettingsView.swift
│       └── SettingsViewModel.swift
│
├── Services/                       # Business logic and data access
│   ├── Networking/
│   │   ├── APIClient.swift
│   │   ├── Endpoint.swift
│   │   └── HTTPClientProtocol.swift
│   ├── Auth/
│   │   ├── AuthService.swift
│   │   └── AuthServiceProtocol.swift
│   └── Storage/
│       ├── UserDefaultsService.swift
│       └── PersistenceController.swift  # SwiftData / Core Data stack
│
├── Core/
│   ├── Extensions/                 # Swift / Foundation / SwiftUI extensions
│   │   ├── String+Extensions.swift
│   │   ├── Date+Extensions.swift
│   │   └── View+Extensions.swift
│   ├── Components/                 # Reusable SwiftUI views (design system)
│   │   ├── PrimaryButton.swift
│   │   ├── LoadingView.swift
│   │   └── ErrorView.swift
│   ├── Utilities/                  # Stateless helpers
│   │   ├── PriceFormatter.swift
│   │   └── DateFormatter+Shared.swift
│   └── Models/                     # Shared domain models (used across features)
│       ├── User.swift
│       └── APIError.swift
│
├── Resources/
│   ├── Assets.xcassets
│   ├── Localizable.xcstrings       # iOS 16+ strings catalog
│   └── Info.plist
│
└── tasks/                          # Claude task tracking (not compiled)
    ├── todo.md
    └── lessons.md
```

Test targets (Xcode targets, not source folders):
```
MyAppTests/                         # Unit test target
│   ├── Features/
│   │   ├── HomeViewModelTests.swift
│   │   └── ProfileViewModelTests.swift
│   ├── Services/
│   │   └── AuthServiceTests.swift
│   └── Mocks/
│       ├── MockAuthService.swift
│       └── MockHTTPClient.swift
│
MyAppUITests/                       # UI test target
│   └── Flows/
│       ├── LoginFlowTests.swift
│       └── OnboardingFlowTests.swift
```

---

## Folder Structure — UIKit App

```
MyApp/
├── App/
│   ├── AppDelegate.swift
│   ├── SceneDelegate.swift
│   └── AppCoordinator.swift        # Root coordinator
│
├── Features/
│   └── Home/
│       ├── HomeViewController.swift
│       ├── HomeViewModel.swift
│       ├── HomeCoordinator.swift   # Navigation logic
│       └── Views/                  # UIView subclasses for this feature only
│           └── HomeHeaderView.swift
│
├── Services/                       # Same as SwiftUI
│   ├── Networking/
│   └── Storage/
│
├── Core/
│   ├── Extensions/
│   ├── Components/                 # Reusable UIView subclasses
│   ├── Utilities/
│   └── Models/
│
└── Resources/
    ├── Assets.xcassets
    ├── Localizable.xcstrings
    ├── Main.storyboard             # Only if using storyboards
    └── Info.plist
```

---

## Folder Structure — Mixed (SwiftUI + UIKit)

```
MyApp/
├── App/
│   ├── AppDelegate.swift
│   └── SceneDelegate.swift
│
├── Features/
│   ├── Home/                       # SwiftUI feature
│   │   ├── HomeView.swift
│   │   └── HomeViewModel.swift
│   └── LegacyDashboard/            # UIKit feature (being migrated)
│       ├── DashboardViewController.swift
│       └── DashboardViewModel.swift
│
├── Bridge/                         # UIHostingController / UIViewRepresentable wrappers
│   ├── HomeViewHostingController.swift
│   └── LegacyPickerRepresentable.swift
│
├── Services/
├── Core/
└── Resources/
```

---

## File Naming Conventions

### Good

```
UserProfileView.swift           ← type name matches file name exactly
UserProfileViewModel.swift      ← one primary type per file
AuthServiceProtocol.swift       ← protocol in its own file when non-trivial
String+Validation.swift         ← extension: Type+Purpose
DateFormatter+Shared.swift      ← extension: Type+Purpose
MockAuthService.swift           ← test mock: Mock + protocol name
HomeViewModelTests.swift        ← tests: TypeName + Tests
```

### Bad

```
Helpers.swift                   ← vague, becomes a dumping ground
Utils.swift                     ← same problem
Extensions.swift                ← too broad
NewFile.swift                   ← Xcode default, never keep it
Manager.swift                   ← what does it manage?
VC.swift                        ← abbreviation
homeview.swift                  ← not UpperCamelCase
UserProfile+ViewModel.swift     ← + is for extensions, not ViewModel pairing
```

---

## Xcode Group Naming Conventions

```
Features/       ← plural noun, title case
Services/       ← plural noun
Core/           ← singular (it's one core layer)
Resources/      ← plural noun
Tests/          ← not "Test" — plural
Mocks/          ← not "Mock" — plural
Views/          ← only inside a UIKit feature folder, not top-level
Extensions/     ← plural noun
Components/     ← plural noun
```

Rules:
- Title case, no spaces
- Plural for collections of types (`Features/`, `Services/`, `Models/`)
- Match the folder name to what's inside — no surprise contents
- Never create a `Misc/` or `Other/` group

---

## What Never Goes Where

| Code | Wrong location | Right location |
|---|---|---|
| Network calls | `View`, `ViewController` | `Services/Networking/` |
| `UserDefaults` access | `View`, `ViewModel` | `Services/Storage/` |
| Business logic | `View`, `ViewController` | `ViewModel`, `Service` |
| Navigation | `ViewModel` | `Coordinator` (UIKit) or parent `View` (SwiftUI) |
| Reusable UI | Inside a `Feature/` | `Core/Components/` |
| Domain models | `Services/Networking/` | `Core/Models/` |
| Test mocks | Main target | Test target `Mocks/` |
| `UIHostingController` wrappers | `Features/` | `Bridge/` |

---

## .gitignore — Xcode / Swift

```gitignore
# Xcode build artifacts
build/
DerivedData/
*.pbxuser
*.mode1v3
*.mode2v3
*.perspectivev3
!default.pbxuser
!default.mode1v3
!default.mode2v3
!default.perspectivev3

# User-specific Xcode settings
*.xcuserstate
xcuserdata/
*.xcscmblueprint

# Xcode schemes (keep shared ones, ignore personal)
*.xcodeproj/xcuserdata/
*.xcworkspace/xcuserdata/

# Swift Package Manager
.build/
.swiftpm/
*.resolved          # Commit this if you want reproducible builds across team

# CocoaPods (if used)
Pods/
*.xcworkspace       # Re-add if CocoaPods generated — see note below

# Carthage (if used)
Carthage/Build/

# Fastlane
fastlane/report.xml
fastlane/Preview.html
fastlane/screenshots/**/*.png
fastlane/test_output

# OS
.DS_Store
Thumbs.db

# Secrets — never commit
*.p12
*.mobileprovision
*.cer
GoogleService-Info.plist    # If using Firebase — use env vars or CI secrets instead
```

> **Note on `.resolved`**: Commit `Package.resolved` in apps (reproducible builds). Do not commit it in libraries (let consumers resolve versions).

---

## SPM Package.swift Skeleton

For extracting a module into a local or shared Swift Package:

```swift
// swift-tools-version: 5.9
import PackageDescription

let package = Package(
    name: "MyFeatureKit",
    platforms: [
        .iOS(.v17)
    ],
    products: [
        .library(
            name: "MyFeatureKit",
            targets: ["MyFeatureKit"]
        )
    ],
    dependencies: [
        // .package(url: "https://github.com/...", from: "1.0.0")
    ],
    targets: [
        .target(
            name: "MyFeatureKit",
            dependencies: [],
            path: "Sources/MyFeatureKit"
        ),
        .testTarget(
            name: "MyFeatureKitTests",
            dependencies: ["MyFeatureKit"],
            path: "Tests/MyFeatureKitTests"
        )
    ]
)
```

Local package folder structure:
```
MyFeatureKit/
├── Package.swift
├── Sources/
│   └── MyFeatureKit/
│       ├── MyFeatureKit.swift      # Public API surface
│       └── Internal/               # Internal implementation
└── Tests/
    └── MyFeatureKitTests/
        └── MyFeatureKitTests.swift
```
