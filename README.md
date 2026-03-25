# Flux Design System

A modular, token-driven, **multi-platform design system** built for **iOS**, **Android**, and **React Native**. Flux provides a shared visual language, reusable component library, and centralized resources to deliver consistent, accessible, and performant experiences across all products and platforms.

**26 components | 11 token categories | 2 built-in themes | Atomic Design | Accessibility-first**

**Repository:** [**github.com/AfzalSiddiqui/flux-design-system**](https://github.com/AfzalSiddiqui/flux-design-system)

---

## Table of Contents

- [Platforms](#platforms)
- [Architecture](#architecture)
- [All Repositories](#all-repositories)
- [iOS Platform](#ios-platform)
- [Android Platform](#android-platform)
- [React Native Platform](#react-native-platform)
- [Component Overview](#component-overview)
- [Token Reference](#token-reference)
- [Theme System](#theme-system)
- [Accessibility](#accessibility)
- [Code Metrics](#code-metrics)
- [Versioning](#versioning)
- [Author](#author)
- [License](#license)

---

## Platforms

| Platform | Language | UI Framework | Package Manager | Min Version |
|----------|----------|-------------|-----------------|-------------|
| **iOS** | Swift 5.8+ | SwiftUI | Swift Package Manager | iOS 16+ |
| **Android** | Kotlin | Jetpack Compose | Gradle (composite builds) | API 24+ |
| **React Native** | TypeScript | React Native | npm / yarn | Expo SDK 52 |

Each platform follows the same **4-package architecture** and uses identical token values, component names, and design patterns. What changes is the idiomatic implementation for each framework.

---

## Architecture

Flux is split into **4 independent packages per platform** following the **Atomic Design** methodology:

```
[platform]-ds            Design tokens (colors, typography, spacing, radius, shadows, theming)
     |
     v
[platform]-foundation    Reusable UI components (atoms, molecules, organisms)
     |
     v
[platform]-experience    Live component catalog & showcase app
     ^
     |
[platform]-assets        Shared strings, images, icons, and localized resources
```

| Package | Description | Depends On |
|---------|-------------|------------|
| `*-ds` | Design tokens & theming engine | None |
| `*-foundation` | UI components (Atoms, Molecules, Organisms) | `*-ds` |
| `*-assets` | Strings, images, localization | None |
| `*-experience` | Interactive showcase app | `*-foundation`, `*-assets` |

---

## All Repositories

### Main Repository

| Package | GitHub Repository |
|---------|-------------------|
| **Flux Design System (this repo)** | [**github.com/AfzalSiddiqui/flux-design-system**](https://github.com/AfzalSiddiqui/flux-design-system) |

### iOS Repositories

| Package | GitHub Repository |
|---------|-------------------|
| **flux-ios-ds** | [**github.com/AfzalSiddiqui/FluxTokensKit**](https://github.com/AfzalSiddiqui/FluxTokensKit) |
| **flux-ios-foundation** | [**github.com/AfzalSiddiqui/FluxComponentsKit**](https://github.com/AfzalSiddiqui/FluxComponentsKit) |
| **flux-ios-assets** | [**github.com/AfzalSiddiqui/FluxResourcesKit**](https://github.com/AfzalSiddiqui/FluxResourcesKit) |
| **flux-ios-experience** | [**github.com/AfzalSiddiqui/FluxShowcaseApp**](https://github.com/AfzalSiddiqui/FluxShowcaseApp) |

### Android Repositories

| Package | GitHub Repository |
|---------|-------------------|
| **flux-android-ds** | [**github.com/AfzalSiddiqui/flux-android-ds**](https://github.com/AfzalSiddiqui/flux-android-ds) |
| **flux-android-foundation** | [**github.com/AfzalSiddiqui/flux-android-foundation**](https://github.com/AfzalSiddiqui/flux-android-foundation) |
| **flux-android-assets** | [**github.com/AfzalSiddiqui/flux-android-assets**](https://github.com/AfzalSiddiqui/flux-android-assets) |
| **flux-android-experience** | [**github.com/AfzalSiddiqui/flux-android-experience**](https://github.com/AfzalSiddiqui/flux-android-experience) |

### React Native Repositories

| Package | GitHub Repository |
|---------|-------------------|
| **flux-react-native-ds** | [**github.com/AfzalSiddiqui/flux-react-native-ds**](https://github.com/AfzalSiddiqui/flux-react-native-ds) |
| **flux-react-native-foundation** | [**github.com/AfzalSiddiqui/flux-react-native-foundation**](https://github.com/AfzalSiddiqui/flux-react-native-foundation) |
| **flux-react-native-assets** | [**github.com/AfzalSiddiqui/flux-react-native-assets**](https://github.com/AfzalSiddiqui/flux-react-native-assets) |
| **flux-react-native-experience** | [**github.com/AfzalSiddiqui/flux-react-native-experience**](https://github.com/AfzalSiddiqui/flux-react-native-experience) |

### Clone All Repos

```bash
# Main
git clone https://github.com/AfzalSiddiqui/flux-design-system.git

# iOS
git clone https://github.com/AfzalSiddiqui/FluxTokensKit.git flux-ios-ds
git clone https://github.com/AfzalSiddiqui/FluxComponentsKit.git flux-ios-foundation
git clone https://github.com/AfzalSiddiqui/FluxResourcesKit.git flux-ios-assets
git clone https://github.com/AfzalSiddiqui/FluxShowcaseApp.git flux-ios-experience

# Android
git clone https://github.com/AfzalSiddiqui/flux-android-ds.git
git clone https://github.com/AfzalSiddiqui/flux-android-foundation.git
git clone https://github.com/AfzalSiddiqui/flux-android-assets.git
git clone https://github.com/AfzalSiddiqui/flux-android-experience.git

# React Native
git clone https://github.com/AfzalSiddiqui/flux-react-native-ds.git
git clone https://github.com/AfzalSiddiqui/flux-react-native-foundation.git
git clone https://github.com/AfzalSiddiqui/flux-react-native-assets.git
git clone https://github.com/AfzalSiddiqui/flux-react-native-experience.git
```

---

## iOS Platform

**Swift + SwiftUI | MVVM Architecture | Swift Package Manager**

### Requirements

| Requirement | Version |
|------------|---------|
| iOS | 16.0+ |
| macOS | 13.0+ |
| Swift | 5.8+ |
| Xcode | 15.0+ |
| Dependencies | None (pure SwiftUI) |

### Setup

```swift
// Package.swift
dependencies: [
    .package(path: "../flux-ios-foundation"),  // includes flux-ios-ds automatically
    .package(path: "../flux-ios-assets"),
]

// Swift file
import flux_ios_foundation  // All 26 components + all design tokens
import flux_ios_assets      // Strings, images, localization resources
```

### Run the Showcase App

```
1. Open flux-ios-experience/flux-ios-experience/flux-ios-experience.xcodeproj in Xcode
2. Select an iOS 16+ simulator or device
3. Build & Run (Cmd + R)
```

### Key Features

- **MVVM architecture** — Every component has a dedicated `@Published` ViewModel
- **Theme protocol** — `FluxThemeProtocol` with `FluxThemeManager` singleton
- **@_exported import** — `flux-ios-foundation` re-exports `flux_ios_ds` automatically
- **SF Symbols** — Native system icon support
- **29 showcase screens** — Complete component gallery + examples

### Package READMEs

| Package | README |
|---------|--------|
| flux-ios-ds | [View README](https://github.com/AfzalSiddiqui/FluxTokensKit/blob/main/README.md) |
| flux-ios-foundation | [View README](https://github.com/AfzalSiddiqui/FluxComponentsKit/blob/main/README.md) |
| flux-ios-assets | [View README](https://github.com/AfzalSiddiqui/FluxResourcesKit/blob/main/README.md) |
| flux-ios-experience | [View README](https://github.com/AfzalSiddiqui/FluxShowcaseApp/blob/main/README.md) |

---

## Android Platform

**Kotlin + Jetpack Compose | State Hoisting | Gradle Composite Builds**

### Requirements

| Requirement | Version |
|------------|---------|
| Android | API 24+ (Android 7.0) |
| compileSdk | 34 |
| Kotlin | 1.9+ |
| Android Studio | Hedgehog+ |
| Compose BOM | 2024.02.00 |
| JVM Target | 17 |

### Setup

```kotlin
// settings.gradle.kts
includeBuild("../flux-android-ds")
includeBuild("../flux-android-assets")
includeBuild("../flux-android-foundation")

// build.gradle.kts
dependencies {
    implementation("com.fluxds:foundation")
    implementation("com.fluxds:assets")
}
```

```kotlin
import com.fluxds.foundation.atoms.*
import com.fluxds.foundation.molecules.*
import com.fluxds.foundation.organisms.*
import com.fluxds.ds.theme.FluxTheme
import com.fluxds.ds.tokens.*
```

### Run the Showcase App

```
1. Open flux-android-experience/ in Android Studio
2. Sync Gradle
3. Run on API 24+ emulator or device
```

### Key Features

- **State hoisting** — Parameters + callbacks for idiomatic Compose patterns
- **CompositionLocal** — Theme propagation via `LocalFluxColors` and `LocalFluxThemeState`
- **Material 3 base** — Custom `FluxTheme` wrapping Material 3
- **Compose Canvas** — Charts rendered with `DrawScope` (no external chart library)
- **Coil** — Async image loading with `coil-compose`
- **Material Icons** — `material-icons-extended` for icon support
- **32 showcase screens** — Full component gallery + 3 example flows + guidelines + theme settings

### Package READMEs

| Package | README |
|---------|--------|
| flux-android-ds | [View README](https://github.com/AfzalSiddiqui/flux-android-ds/blob/main/README.md) |
| flux-android-foundation | [View README](https://github.com/AfzalSiddiqui/flux-android-foundation/blob/main/README.md) |
| flux-android-assets | [View README](https://github.com/AfzalSiddiqui/flux-android-assets/blob/main/README.md) |
| flux-android-experience | [View README](https://github.com/AfzalSiddiqui/flux-android-experience/blob/main/README.md) |

---

## React Native Platform

**TypeScript + React Native | Hooks + Context | Expo SDK 52**

### Requirements

| Requirement | Version |
|------------|---------|
| Node.js | 18+ |
| Expo SDK | 52 |
| React Native | 0.73+ |
| TypeScript | 5.0+ |

### Setup

```bash
npm install @anthropic-flux/react-native-ds
npm install @anthropic-flux/react-native-foundation
npm install @anthropic-flux/react-native-assets
```

```tsx
import { FluxThemeProvider, FluxSpacing, useFluxColors } from '@anthropic-flux/react-native-ds';
import { FluxButton, FluxCard, FluxHeader } from '@anthropic-flux/react-native-foundation';
import { useFluxStrings, FluxImages } from '@anthropic-flux/react-native-assets';
```

### Run the Showcase App

```bash
cd flux-react-native-experience
npm install
npx expo start
```

### Key Features

- **Hooks + Context** — `useFluxColors()`, `useFluxTheme()`, `useFluxStrings()`
- **React Context** — `FluxThemeProvider` and `FluxI18nProvider`
- **Animated API** — React Native `Animated` for smooth transitions
- **Ionicons** — `@expo/vector-icons` icon mapping
- **react-native-svg** — SVG-based chart rendering in FluxGraph
- **react-native-webview** — Embedded browser support
- **42 showcase screens** — Full component catalog + 3 example flows + guidelines + theme settings

### Package READMEs

| Package | README |
|---------|--------|
| flux-react-native-ds | [View README](https://github.com/AfzalSiddiqui/flux-react-native-ds/blob/main/README.md) |
| flux-react-native-foundation | [View README](https://github.com/AfzalSiddiqui/flux-react-native-foundation/blob/main/README.md) |
| flux-react-native-assets | [View README](https://github.com/AfzalSiddiqui/flux-react-native-assets/blob/main/README.md) |
| flux-react-native-experience | [View README](https://github.com/AfzalSiddiqui/flux-react-native-experience/blob/main/README.md) |

---

## Component Overview

All 26 components are implemented identically across all 3 platforms:

```
+-------------------------------------------------------------+
|  ATOMS (11)               Basic building blocks              |
|  FluxButton    FluxText      FluxIcon       FluxLoader       |
|  FluxDivider   FluxToggle    FluxCheckBox   FluxRadioButton  |
|  FluxSegmentedControl        FluxImage      FluxShimmer      |
+-------------------------------------------------------------+
|  MOLECULES (10)           Atom combinations                  |
|  FluxCard      FluxTextField   FluxListRow   FluxAlertView   |
|  FluxInfoView  FluxOptionCard  FluxExpandableView            |
|  FluxFlapView  FluxCardFlap    FluxBoxGrid                   |
+-------------------------------------------------------------+
|  ORGANISMS (5)            Screen-level patterns              |
|  FluxHeader    FluxBottomSheet   FluxFormSection              |
|  FluxGraph     FluxWebView                                   |
+-------------------------------------------------------------+
```

### Atoms (11)

| Component | Description |
|-----------|-------------|
| **FluxButton** | Action trigger — 3 variants (primary/secondary/destructive), 3 sizes, loading & disabled states |
| **FluxText** | Text display — 10+ typography styles, multi-segment attributed text |
| **FluxIcon** | Icon renderer — Platform-native icons, 3 sizes, tint color |
| **FluxImage** | Image display — Local and remote sources, async loading, border & radius |
| **FluxLoader** | Loading indicator — Indeterminate spinner or determinate progress bar |
| **FluxDivider** | Visual separator — Horizontal/vertical, configurable color & thickness |
| **FluxCheckBox** | Multi-select toggle — Filled/outlined styles, 3 sizes, animated |
| **FluxRadioButton** | Single-select — Circular indicator, 3 sizes, label |
| **FluxToggle** | Boolean switch — Native platform switch control |
| **FluxSegmentedControl** | Multi-option selector — Filled/outlined, dynamic segments |
| **FluxShimmer** | Skeleton placeholder — Line/circle/rectangle shapes, animated gradient |

### Molecules (10)

| Component | Description |
|-----------|-------------|
| **FluxCard** | Surface container — Padding, corner radius, shadow, generic content |
| **FluxTextField** | Text input — Label, placeholder, secure mode, error state |
| **FluxListRow** | Navigation row — Icon, title, subtitle, chevron, tap handler |
| **FluxAlertView** | Status banner — 4 semantic variants, auto-icon, dismissible |
| **FluxInfoView** | Info display — Icon + title + description, horizontal/vertical layout |
| **FluxOptionCard** | Selection list — Single/multi select, icon + label + subtitle |
| **FluxExpandableView** | Collapsible section — 3 styles (card/plain/bordered), animated chevron |
| **FluxFlapView** | Tabbed container — 3 tab styles (underlined/filled/pill), icon support |
| **FluxCardFlap** | 3D flip card — Front/back content, Y-axis rotation animation |
| **FluxBoxGrid** | Grid layout — Configurable columns, selection modes, item sizes |

### Organisms (5)

| Component | Description |
|-----------|-------------|
| **FluxHeader** | Top navigation bar — Title, subtitle, leading/trailing action slots |
| **FluxBottomSheet** | Modal panel — 3 detents (25%/50%/85%), drag-to-dismiss |
| **FluxFormSection** | Form grouping — Section title, spacing, content wrapper |
| **FluxGraph** | Data visualization — Bar, line, pie charts with animation |
| **FluxWebView** | Embedded browser — Web content loading, progress bar, error handling |

---

## Token Reference

All token values are **identical across all 3 platforms**:

### Color Tokens (16)

| Category | Tokens |
|----------|--------|
| Brand | `primary`, `secondary`, `accent` |
| Surface | `background`, `surface` |
| Text | `textPrimary`, `textSecondary` |
| Semantic | `success`, `warning`, `error` |
| Border | `border`, `divider` |
| On-Colors | `onPrimary`, `onSecondary`, `onError` |
| Overlay | `overlay` |

### Typography (10 styles)

| Style | Size | Weight |
|-------|------|--------|
| `largeTitle` | 34 | Bold |
| `title1` | 28 | Bold |
| `title2` | 22 | Bold |
| `title3` | 20 | SemiBold |
| `headline` | 17 | SemiBold |
| `body` | 17 | Regular |
| `callout` | 16 | Regular |
| `subheadline` | 15 | Regular |
| `footnote` | 13 | Regular |
| `caption` | 12 | Regular |

### Spacing (8-step scale)

| Token | Value |
|-------|-------|
| `xxxs` | 2 |
| `xxs` | 4 |
| `xs` | 8 |
| `sm` | 12 |
| `md` | 16 |
| `lg` | 24 |
| `xl` | 32 |
| `xxl` | 48 |

### Radius (6 presets)

| Token | Value |
|-------|-------|
| `xs` | 4 |
| `sm` | 8 |
| `md` | 12 |
| `lg` | 16 |
| `xl` | 24 |
| `full` | 9999 (pill) |

### Shadow (3 elevations)

| Preset | Blur | Y-Offset | Opacity |
|--------|------|----------|---------|
| `small` | 4 | 2 | 8% |
| `medium` | 8 | 4 | 12% |
| `large` | 16 | 8 | 16% |

### Border (3 widths)

| Token | Value |
|-------|-------|
| `thin` | 1 |
| `medium` | 1.5 |
| `thick` | 2 |

### Opacity (5 presets)

| Token | Value |
|-------|-------|
| `subtle` | 0.08 |
| `light` | 0.1 |
| `muted` | 0.3 |
| `overlay` | 0.4 |
| `disabled` | 0.5 |

---

## Theme System

Flux supports **runtime theme switching** on all platforms. All color tokens automatically update when the theme changes.

### Built-in Themes

**Default Theme (Light):**
| Token | Value |
|-------|-------|
| primary | #007AFF |
| secondary | #1C2541 |
| accent | #5BC0BE |
| success | #34C759 |
| warning | #FF9500 |
| error | #FF3B30 |

**Default Theme (Dark):**
| Token | Value |
|-------|-------|
| primary | #0A84FF |
| secondary | #1C2541 |
| accent | #5BC0BE |
| background | #000000 |
| surface | #1C1C1E |

**Dark Brand Theme:**
| Token | Value |
|-------|-------|
| primary | #6C63FF (purple) |
| secondary | #2D2B55 |
| accent | #F78166 (coral) |
| background | #1A1A2E |
| surface | #16213E |

### Platform-Specific Theming

| Feature | iOS | Android | React Native |
|---------|-----|---------|-------------|
| Provider | `FluxThemeManager` singleton | `FluxTheme` Composable | `FluxThemeProvider` Context |
| Color Access | `FluxColors.primary` | `FluxColors.current.primary` | `useFluxColors().primary` |
| Theme Switch | `.setTheme(...)` | `.setThemeConfig(...)` | `setThemeConfig(...)` |
| Color Scheme | `.colorScheme = .dark` | `.setColorSchemePreference(.DARK)` | `setColorSchemePreference('dark')` |
| Architecture | Protocol-based | CompositionLocal | React Context + Hooks |

---

## Accessibility

Accessibility is built into every component as a core requirement across all platforms:

| Feature | iOS | Android | React Native |
|---------|-----|---------|-------------|
| Dynamic Type | SwiftUI system fonts | Compose sp units | `allowFontScaling` |
| Screen Reader | VoiceOver labels & traits | `contentDescription` + semantics | `accessibilityLabel` |
| Color Contrast | Token-driven ratios | Token-driven ratios | Token-driven ratios |
| Disabled States | 0.5 opacity | 0.5 opacity | 0.5 opacity |
| Decorative Elements | `.accessibilityHidden(true)` | Decorative role | `importantForAccessibility="no"` |

---

## Code Metrics

### iOS (Swift + SwiftUI)

| Package | Files | Lines | Content |
|---------|-------|-------|---------|
| flux-ios-ds | 11 | 458 | 10 token files + 1 module re-export |
| flux-ios-foundation | 26 | 3,182 | 11 atoms + 10 molecules + 5 organisms |
| flux-ios-assets | 3 | 121 | Strings + Images + module entry |
| flux-ios-experience | 29 | 3,718 | 29 showcase/demo screens |
| **iOS Total** | **69** | **7,479** | |

### Android (Kotlin + Jetpack Compose)

| Package | Files | Content |
|---------|-------|---------|
| flux-android-ds | 12 | 6 token files + 4 theme files + shimmer + utils |
| flux-android-foundation | 26 | 11 atoms + 10 molecules + 5 organisms |
| flux-android-assets | 4 | Strings + Images + 2 string resource files |
| flux-android-experience | 39 | 32 showcases + 3 examples + guidelines + theme |
| **Android Total** | **81** | |

### React Native (TypeScript)

| Package | Files | Content |
|---------|-------|---------|
| flux-react-native-ds | 12 | 7 token files + 3 theme files + shimmer + utils |
| flux-react-native-foundation | 27 | 11 atoms + 10 molecules + 5 organisms + types |
| flux-react-native-assets | 7 | Strings + Images + i18n provider + 2 locale files |
| flux-react-native-experience | 42 | 32 showcases + 3 examples + guidelines + theme |
| **React Native Total** | **88** | |

**Grand Total: 238 source files across 3 platforms**

**Component Distribution:** Atoms 42% (11) | Molecules 38% (10) | Organisms 19% (5)

---

## Versioning

Flux follows **Semantic Versioning**:

| Change | Version Bump | Example |
|--------|-------------|---------|
| Breaking token/component API changes | **Major** | Removing a token, changing props |
| New tokens or components | **Minor** | Adding FluxBadge, new spacing token |
| Bug fixes and visual tweaks | **Patch** | Fixing shadow offset, adjusting padding |

---

## Author

**Afzal Siddiqui**

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file.

Copyright (c) 2026 Afzal Siddiqui
