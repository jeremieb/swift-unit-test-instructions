Validate that the Swift project builds successfully. Run this after any code change before considering work done.

## Steps

### 1. Detect project type

Look for (in order):
- `*.xcworkspace` → use xcodebuild with workspace
- `*.xcodeproj` → use xcodebuild with project
- `Package.swift` → use swift build

### 2. Find scheme

For xcodebuild projects, read available schemes:
```bash
xcodebuild -list 2>/dev/null
```
Use the first non-test scheme found. If ambiguous, ask the user which scheme to use.

### 3. Run the build

**Xcode project / workspace:**
```bash
xcodebuild build \
  -scheme "$SCHEME" \
  -destination "generic/platform=iOS Simulator" \
  -quiet 2>&1 | grep -E "error:|warning:|BUILD SUCCEEDED|BUILD FAILED"
```

**Swift Package:**
```bash
swift build 2>&1
```

### 4. Report result

**On success:**
```
BUILD SUCCEEDED
Scheme: $SCHEME
No errors or warnings.
```

**On failure:**
```
BUILD FAILED
Scheme: $SCHEME

Errors:
- $FILE:$LINE — $ERROR_MESSAGE
```

### 5. On failure — attempt fix (max 2 attempts)

- Read each file containing an error
- Apply the fix
- Re-run the build
- If still failing after 2 attempts: stop, present the remaining errors, and ask the user how to proceed

Never force-ignore compiler errors with `@discardableResult`, forced casts, or suppression comments.
