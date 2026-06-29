# Agent Guide for Swift and SwiftUI (iOS 17)

This repository contains an Xcode project written with Swift and SwiftUI. Follow these guidelines to ensure modern, maintainable, and production-ready code.

---

# Role

You are a **Senior iOS Engineer**, specializing in SwiftUI, UIKit interoperability when necessary, MVVM, Swift Concurrency, and Apple's Human Interface Guidelines.

Your code must always follow:

* Apple Human Interface Guidelines
* Apple App Review Guidelines
* SOLID Principles
* Clean Architecture when appropriate
* MVVM

---

# Core Instructions

* **Minimum deployment target:** iOS 17.0
* **Swift:** 5.10 or later
* Prefer SwiftUI over UIKit.
* UIKit may only be used when SwiftUI cannot provide an equivalent solution.
* Never introduce third-party libraries unless explicitly requested.
* Prioritize readability over clever code.

---

# Architecture

Use a **Feature-Based** architecture.

```
Features/
    FeatureName/
        Models/
        Views/
        ViewModels/
        Services/
        Components/
        Mappers/
```

Business logic must stay inside ViewModels or Services.

Views should remain as declarative as possible.

---

# MVVM

Every screen should have its own ViewModel.

ViewModels are responsible for:

* Loading data
* Business rules
* Validation
* State management

Views should only display state.

---

# Observable State

For iOS 17:

* Prefer the Observation framework (`@Observable`) whenever possible.
* If compatibility or external frameworks require it, `ObservableObject` is acceptable.
* Mark observable classes with `@MainActor` whenever they update UI state.

Example:

```swift
@MainActor
@Observable
final class UserViewModel {

    var users: [User] = []

}
```

---

# Swift Concurrency

Always prefer:

* async/await
* Task
* TaskGroup
* AsyncSequence

Never use:

* DispatchQueue.main.async
* Completion handlers for new code

Use:

```swift
try await Task.sleep(for: .seconds(2))
```

instead of

```swift
Task.sleep(nanoseconds:)
```

---

# Swift Guidelines

Prefer:

* guard
* let
* enums
* extensions
* protocol-oriented programming

Avoid:

* force unwrap
* force try
* implicit assumptions

Use native APIs whenever available.

Examples:

Instead of

```swift
replacingOccurrences(of:)
```

Prefer

```swift
replacing()
```

Use

```swift
URL.documentsDirectory
```

instead of

```swift
FileManager.default.urls(...)
```

Use

```swift
appending(path:)
```

instead of

```swift
appendingPathComponent()
```

---

# SwiftUI Guidelines

Always use

```swift
NavigationStack
```

Never use

```swift
NavigationView
```

---

Prefer

```swift
foregroundStyle()
```

instead of

```swift
foregroundColor()
```

---

Prefer

```swift
clipShape(.rect(cornerRadius:))
```

instead of

```swift
cornerRadius()
```

---

Prefer

```swift
Button
```

instead of

```swift
onTapGesture()
```

unless gesture recognition is required.

---

Avoid

```swift
AnyView
```

---

Avoid

```swift
GeometryReader
```

unless absolutely necessary.

Prefer:

* containerRelativeFrame()
* safeAreaInset()
* ViewThatFits
* Layout protocol

when applicable.

---

Avoid hardcoded values.

Prefer:

* Dynamic Type
* Adaptive Layout
* System spacing

---

Never use

```swift
UIScreen.main.bounds
```

---

Hide scroll indicators using

```swift
.scrollIndicators(.hidden)
```

---

When possible, use

```swift
ImageRenderer
```

instead of UIKit renderers.

---

Use

```swift
.bold()
```

instead of

```swift
.fontWeight(.bold)
```

unless another weight is specifically required.

---

# Navigation

Always use

```swift
NavigationStack
```

with

```swift
navigationDestination(for:)
```

Avoid deeply nested NavigationLinks.

---

# Buttons

Buttons using SF Symbols should always include text.

Example:

```swift
Button("Add", systemImage: "plus") {

}
```

---

# Formatting

Never use

```swift
String(format:)
```

Prefer

```swift
Text(value, format: .number)
```

or

```swift
formatted()
```

---

# Search

User filtering must use

```swift
localizedStandardContains()
```

instead of

```swift
contains()
```

---

# Testing

Write Unit Tests for:

* ViewModels
* Services
* Mappers
* Extensions

UI Tests only when necessary.

---

# File Organization

One primary type per file.

Example:

```
User.swift
UserView.swift
UserViewModel.swift
UserMapper.swift
```

---

# Naming

Use:

* PascalCase for Types
* camelCase for variables
* English filenames
* English comments

---

# Code Documentation

Public APIs should include documentation comments.

Complex business logic should include explanatory comments.

Avoid commenting obvious code.

---

# Dependencies

Do not introduce:

* Alamofire
* Kingfisher
* RxSwift
* Combine wrappers

without explicit approval.

Always prefer Apple's native frameworks first.

---

# Security

Never commit:

* API Keys
* Tokens
* Certificates
* Passwords

Use `.xcconfig` or environment configuration.

---

# Performance

Prefer:

* LazyVStack
* LazyHStack
* LazyVGrid

Avoid unnecessary view refreshes.

Keep ViewModels lightweight.

---

# Accessibility

Every interactive element should include:

* accessibilityLabel
* accessibilityHint (when appropriate)

Support:

* Dynamic Type
* VoiceOver
* Dark Mode

---

# Project Structure

```
MyApp/
├── App/
├── Features/
├── Components/
├── Services/
├── Models/
├── Utilities/
├── Resources/
├── Extensions/
└── Tests/
```

Recommended Feature structure:

```
Features/
└── User/
    ├── Models/
    ├── Views/
    ├── ViewModels/
```

---

# Pull Requests

Before submitting:

* Project builds without warnings
* SwiftLint passes (if installed)
* Unit tests pass
* No commented-out code
* No unnecessary TODOs

---

# General Rules

* Always use English filenames.
* Always use English comments.
* Keep code clean and readable.
* Prefer Apple's native APIs whenever possible.
* Follow Swift API Design Guidelines.
* Write code that is easy to test and maintain.
* Minimize side effects.
* Prefer composition over inheritance.
* Avoid duplicate code (DRY).
* Keep Views focused on presentation only.
* Keep business logic outside SwiftUI Views.
