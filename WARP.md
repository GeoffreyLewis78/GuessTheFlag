# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

GuessTheFlag is a SwiftUI iOS application. The project structure follows standard Xcode conventions with separate targets for the main app, unit tests, and UI tests.

## Build and Run Commands

### Building the Project
```bash
# Build for iOS simulator (requires Xcode installed, not just Command Line Tools)
xcodebuild -project GuessTheFlag.xcodeproj -scheme GuessTheFlag -sdk iphonesimulator -destination 'platform=iOS Simulator,name=iPhone 15' build

# Build for release
xcodebuild -project GuessTheFlag.xcodeproj -scheme GuessTheFlag -configuration Release build
```

### Running Tests
```bash
# Run unit tests (Swift Testing framework)
xcodebuild test -project GuessTheFlag.xcodeproj -scheme GuessTheFlag -destination 'platform=iOS Simulator,name=iPhone 15' -only-testing:GuessTheFlagTests

# Run UI tests (XCTest framework)
xcodebuild test -project GuessTheFlag.xcodeproj -scheme GuessTheFlag -destination 'platform=iOS Simulator,name=iPhone 15' -only-testing:GuessTheFlagUITests

# Run a specific test
xcodebuild test -project GuessTheFlag.xcodeproj -scheme GuessTheFlag -destination 'platform=iOS Simulator,name=iPhone 15' -only-testing:GuessTheFlagTests/GuessTheFlagTests/example

# Run all tests
xcodebuild test -project GuessTheFlag.xcodeproj -scheme GuessTheFlag -destination 'platform=iOS Simulator,name=iPhone 15'
```

### Opening in Xcode
```bash
open GuessTheFlag.xcodeproj
```

## Architecture

### App Entry Point
- **GuessTheFlagApp.swift**: Main app entry point using `@main` attribute and SwiftUI App protocol

### Views
- **ContentView.swift**: Primary view containing the app's UI logic
- SwiftUI declarative syntax with View protocol conformance
- Preview support using `#Preview` macro

### Testing Structure
- **GuessTheFlagTests/**: Unit tests using Swift Testing framework (`import Testing`)
  - Uses `@Test` attribute for test methods
  - Uses `@testable import` to access internal app symbols
  - Modern async/await support with `async throws`
  
- **GuessTheFlagUITests/**: UI tests using XCTest framework
  - Contains launch tests and general UI tests
  - Uses `XCUIApplication` for app interaction
  - Includes performance measurement capabilities

### Assets
- Flag images stored in Assets.xcassets with imagesets for: Estonia, France, Germany, Ireland, Italy, Monaco, Nigeria, Poland, Spain, UK, US, Ukraine
- Each imageset has its own Contents.json configuration

## Development Notes

### Swift Version
The project uses modern Swift features including:
- Swift Testing framework (for unit tests)
- Swift Concurrency (async/await)
- SwiftUI lifecycle and previews

### Test Frameworks
This project uses **two different testing frameworks**:
- **Swift Testing** (`import Testing`) for unit tests in GuessTheFlagTests
- **XCTest** (`import XCTest`) for UI tests in GuessTheFlagUITests

When adding new tests, follow the existing pattern for each test target.

### Xcode Requirements
Commands require full Xcode installation, not just Command Line Tools. If `xcodebuild` fails with "requires Xcode" error, switch to Xcode developer directory:
```bash
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```
