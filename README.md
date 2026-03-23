# Flux Design System for iOS

A modular, token-driven design system for iOS built with **SwiftUI**. Flux provides a shared visual language, reusable component library, and centralized resources to deliver consistent, accessible, and performant experiences across all products.

**26 components | 11 token categories | 2 built-in themes | MVVM architecture | Accessibility-first**

**Repository:** [**github.com/AfzalSiddiqui/flux-design-system**](https://github.com/AfzalSiddiqui/flux-design-system)

---

## Table of Contents

- [Architecture](#architecture)
- [Repositories](#repositories)
- [Clone & Setup](#clone--setup)
- [Requirements](#requirements)
- [Package 1: flux-ios-ds (Design Tokens)](#package-1-flux-ios-ds)
- [Package 2: flux-ios-foundation (UI Components)](#package-2-flux-ios-foundation)
  - [Atoms (11)](#atoms-11)
  - [Molecules (10)](#molecules-10)
  - [Organisms (5)](#organisms-5)
- [Package 3: flux-ios-assets (Resources)](#package-3-flux-ios-assets)
- [Package 4: flux-ios-experience (Showcase App)](#package-4-flux-ios-experience)
- [Theme System](#theme-system)
- [Accessibility](#accessibility)
- [Integration Guide](#integration-guide)
- [Code Metrics](#code-metrics)
- [Versioning](#versioning)
- [Author](#author)
- [License](#license)

---

## Architecture

Flux is split into **4 independent Swift Packages** following the **Atomic Design** methodology:

```
flux-ios-ds            Design tokens (colors, typography, spacing, radius, shadows, theming)
     |
     v
flux-ios-foundation    Reusable UI components (atoms, molecules, organisms)
     |
     v
flux-ios-experience    Live component catalog & showcase app
     ^
     |
flux-ios-assets        Shared strings, images, icons, and localized resources
```

| Package | Description | Swift Module | Depends On |
|---------|-------------|-------------|------------|
| [`flux-ios-ds`](./flux-ios-ds) | Design tokens & theming engine | `flux_ios_ds` | None |
| [`flux-ios-foundation`](./flux-ios-foundation) | UI components (Atoms, Molecules, Organisms) | `flux_ios_foundation` | `flux-ios-ds` |
| [`flux-ios-assets`](./flux-ios-assets) | Strings, images, localization | `flux_ios_assets` | None |
| [`flux-ios-experience`](./flux-ios-experience) | Interactive showcase app | `flux_ios_experience` | `flux-ios-foundation`, `flux-ios-assets` |

> SPM auto-converts hyphens to underscores for Swift module names, so `flux-ios-ds` becomes `import flux_ios_ds`.

---

## Repositories

| Package | GitHub Repository |
|---------|-------------------|
| **Main (this repo)** | [**github.com/AfzalSiddiqui/flux-design-system**](https://github.com/AfzalSiddiqui/flux-design-system) |
| **flux-ios-ds** | [**github.com/AfzalSiddiqui/FluxTokensKit**](https://github.com/AfzalSiddiqui/FluxTokensKit) |
| **flux-ios-foundation** | [**github.com/AfzalSiddiqui/FluxComponentsKit**](https://github.com/AfzalSiddiqui/FluxComponentsKit) |
| **flux-ios-assets** | [**github.com/AfzalSiddiqui/FluxResourcesKit**](https://github.com/AfzalSiddiqui/FluxResourcesKit) |
| **flux-ios-experience** | [**github.com/AfzalSiddiqui/FluxShowcaseApp**](https://github.com/AfzalSiddiqui/FluxShowcaseApp) |

```bash
# Clone all repos
git clone https://github.com/AfzalSiddiqui/flux-design-system.git
git clone https://github.com/AfzalSiddiqui/FluxTokensKit.git flux-ios-ds
git clone https://github.com/AfzalSiddiqui/FluxComponentsKit.git flux-ios-foundation
git clone https://github.com/AfzalSiddiqui/FluxResourcesKit.git flux-ios-assets
git clone https://github.com/AfzalSiddiqui/FluxShowcaseApp.git flux-ios-experience
```

---

## Clone & Setup

```bash
# Clone the repository
git clone https://github.com/AfzalSiddiqui/flux-design-system.git
cd flux-design-system
```

### Run the Showcase App

```
1. Open flux-ios-experience/flux-ios-experience/flux-ios-experience.xcodeproj in Xcode
2. Select an iOS 16+ simulator or device
3. Build & Run (Cmd + R)
```

The Xcode project automatically references `flux-ios-foundation` and `flux-ios-assets` as local packages.

### Use in Your Own App

Add the packages as local SPM dependencies in Xcode:

```
File > Add Package Dependencies > Add Local > select flux-ios-foundation/
Repeat for flux-ios-assets/
```

Or in `Package.swift`:

```swift
dependencies: [
    .package(path: "../flux-ios-foundation"),  // includes flux-ios-ds automatically
    .package(path: "../flux-ios-assets"),
]
```

Then import:

```swift
import flux_ios_foundation  // All 26 components + all design tokens
import flux_ios_assets      // Strings, images, localization resources
```

> **Note:** `flux-ios-foundation` re-exports `flux_ios_ds` via `@_exported import`, so you get all tokens automatically.

### Verify Builds (Terminal)

```bash
cd flux-ios-ds && swift build
cd ../flux-ios-foundation && swift build
cd ../flux-ios-assets && swift build
```

---

## Requirements

| Requirement | Version |
|------------|---------|
| iOS | 16.0+ |
| macOS | 13.0+ |
| Swift | 5.8+ |
| Xcode | 15.0+ |
| Dependencies | None (pure SwiftUI) |

---

## Package 1: flux-ios-ds

**Design tokens — the visual foundation of the entire system.**

Every visual property used by components is defined here as type-safe Swift tokens. No hard-coded magic numbers anywhere. All color tokens read from `FluxThemeManager.shared.currentTheme` for automatic theme switching.

[View full README](./flux-ios-ds/README.md)

### Color Tokens (FluxColors)

16 semantic color properties driven by the active theme:

| Category | Tokens | Usage |
|----------|--------|-------|
| **Brand** | `primary`, `secondary`, `accent` | Buttons, links, highlights |
| **Surface** | `background`, `surface` | Page bg, card bg |
| **Text** | `textPrimary`, `textSecondary` | Main text, subtle text |
| **Semantic** | `success`, `warning`, `error` | Alerts, validation, status |
| **Border** | `border`, `divider` | Outlines, separators |
| **On-Colors** | `onPrimary`, `onSecondary`, `onError` | Text on filled backgrounds |
| **Overlay** | `overlay` | Modal dimming |

```swift
Text("Hello").foregroundColor(FluxColors.textPrimary)
VStack { }.background(FluxColors.surface)
```

**Hex Color Helper:**
```swift
Color(hex: 0x007AFF, alpha: 1.0)
```

### Typography Tokens (FluxTypography)

11 text styles using system fonts with appropriate weights:

| Style | Weight | Usage |
|-------|--------|-------|
| `largeTitle` | Bold | Hero headings |
| `title` | Bold | Page titles |
| `title2` | Semibold | Section titles |
| `title3` | Semibold | Subsection titles |
| `headline` | Semibold | Emphasized labels |
| `subheadline` | Regular | Supporting text |
| `body` | Regular | Main content |
| `callout` | Regular | Highlighted info |
| `footnote` | Regular | Small descriptions |
| `caption` | Regular | Metadata, timestamps |
| `code` | Monospaced | Code snippets |

```swift
Text("Title").font(FluxTypography.title.font)
```

### Spacing Tokens (FluxSpacing)

8-step scale based on a 4pt grid:

| Token | Value | Usage |
|-------|-------|-------|
| `xxxs` | 2pt | Hairline gaps |
| `xxs` | 4pt | Tight padding |
| `xs` | 8pt | Small gaps |
| `sm` | 12pt | Compact padding |
| `md` | 16pt | Default padding |
| `lg` | 24pt | Section spacing |
| `xl` | 32pt | Large gaps |
| `xxl` | 48pt | Page margins |

```swift
VStack(spacing: FluxSpacing.md) { ... }
.padding(FluxSpacing.lg)
```

### Radius Tokens (FluxRadius)

| Token | Value | Usage |
|-------|-------|-------|
| `xs` | 4pt | Small chips |
| `sm` | 8pt | Input fields |
| `md` | 12pt | Cards, buttons |
| `lg` | 16pt | Modals, sheets |
| `xl` | 24pt | Large containers |
| `full` | 9999pt | Pills, circles |

### Shadow Tokens (FluxShadow)

| Preset | Blur | Y-Offset | Opacity | Usage |
|--------|------|----------|---------|-------|
| `.small` | 4px | 2pt | 8% | Cards, subtle elevation |
| `.medium` | 8px | 4pt | 12% | Dropdowns, popovers |
| `.large` | 16px | 8pt | 16% | Modals, sheets |

```swift
FluxCard(viewModel: vm) { content }  // uses .small by default
MyView().fluxShadow(.medium)         // view modifier
```

### Border Tokens (FluxBorder)

| Token | Value | Usage |
|-------|-------|-------|
| `thin` | 1pt | Default borders |
| `medium` | 1.5pt | Focused inputs |
| `thick` | 2pt | Selected states |

### Opacity Tokens (FluxOpacity)

| Token | Value | Usage |
|-------|-------|-------|
| `subtle` | 0.08 | Background tints |
| `light` | 0.1 | Light overlays |
| `muted` | 0.3 | Muted elements |
| `overlay` | 0.4 | Modal dimming |
| `disabled` | 0.5 | Disabled states |

### Shimmer Effect (FluxShimmerEffect)

Animated gradient sweep for skeleton loading states:

```swift
Text("Loading...")
    .fluxShimmer(active: true, cornerRadius: FluxRadius.sm)
```

- 1.5s linear loop animation
- Left-to-right gradient sweep
- Hides content while preserving frame

---

## Package 2: flux-ios-foundation

**26 production-ready SwiftUI components organized in 3 hierarchical levels.**

Every component follows MVVM with a dedicated `ViewModel` class using `@Published` properties for reactive state management. All components use tokens from `flux-ios-ds` — no hard-coded values.

[View full README](./flux-ios-foundation/README.md)

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

---

### Atoms (11)

#### FluxButton

Primary action trigger with 3 variants, 3 sizes, and loading/disabled states.

**ViewModel:** `FluxButtonViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `title` | `String` | — | Button label |
| `variant` | `.primary / .secondary / .destructive` | `.primary` | Visual style |
| `size` | `.small / .medium / .large` | `.medium` | Size preset |
| `isLoading` | `Bool` | `false` | Shows spinner, hides title |
| `isDisabled` | `Bool` | `false` | Dims with 0.5 opacity |
| `action` | `() -> Void` | — | Tap callback |

**Size Details:**
| Size | Font | V-Padding | H-Padding | Radius |
|------|------|-----------|-----------|--------|
| `.small` | footnote | 8pt | 12pt | 8pt |
| `.medium` | body | 12pt | 16pt | 12pt |
| `.large` | headline | 16pt | 24pt | 16pt |

**Variants:** `.primary` = filled primary bg, `.secondary` = outlined with primary border, `.destructive` = filled error bg

```swift
@StateObject var vm = FluxButtonViewModel(
    title: "Continue",
    variant: .primary,
    size: .large
) { print("Tapped!") }

FluxButton(viewModel: vm)
```

---

#### FluxText

Text display supporting plain text and multi-segment attributed text.

**ViewModel:** `FluxTextViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `content` | `String?` | — | Plain text content |
| `segments` | `[FluxTextSegment]?` | — | Attributed segments |
| `style` | Style enum | `.body` | Typography style |
| `color` | `Color?` | `nil` | Override color |

**Styles:** `.largeTitle`, `.title`, `.title2`, `.title3`, `.headline`, `.subheadline`, `.body`, `.callout`, `.footnote`, `.caption`, `.code`

**Default Colors:** `.caption` / `.footnote` / `.subheadline` use `textSecondary`; all others use `textPrimary`.

**FluxTextSegment** (for attributed text):

| Property | Type | Default |
|----------|------|---------|
| `text` | `String` | — |
| `isBold` | `Bool` | `false` |
| `isItalic` | `Bool` | `false` |
| `isUnderline` | `Bool` | `false` |
| `isStrikethrough` | `Bool` | `false` |
| `color` | `Color?` | `nil` |
| `fontSize` | `CGFloat?` | `nil` |
| `link` | `URL?` | `nil` |

```swift
// Plain text
FluxText("Welcome Back", style: .title)

// Attributed text
FluxText(
    segments: [
        .init(text: "Hello "),
        .init(text: "World", isBold: true, color: FluxColors.primary),
    ],
    style: .body
)
```

---

#### FluxIcon

Renders icons from SF Symbols, asset catalog, or remote URLs.

**ViewModel:** `FluxIconViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `source` | `.system(String) / .asset(String) / .url(URL)` | — | Icon source |
| `size` | `.small / .medium / .large / .custom(CGFloat)` | `.medium` | Size preset |
| `color` | `Color` | `primary` | Tint color |

**Sizes:** `.small` = 24pt, `.medium` = 32pt, `.large` = 48pt, `.custom(CGFloat)` = any

```swift
FluxIcon(source: .system("star.fill"), size: .large, color: FluxColors.accent)
```

---

#### FluxImage

Displays images from SF Symbols, assets, or async URLs with loading states.

**ViewModel:** `FluxImageViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `source` | `.system(String) / .asset(String) / .url(URL)` | — | Image source |
| `size` | `.small / .medium / .large / .custom(CGFloat) / .flexible` | `.medium` | Size |
| `contentMode` | `ContentMode` | `.fill` | Aspect ratio |
| `cornerRadius` | `CGFloat` | `0` | Corner rounding |
| `borderColor` | `Color?` | `nil` | Border color |
| `borderWidth` | `CGFloat` | `0` | Border width |
| `onTap` | `(() -> Void)?` | `nil` | Tap callback |

**Sizes:** `.small` = 40pt, `.medium` = 80pt, `.large` = 160pt, `.flexible` = fills available space

```swift
@StateObject var vm = FluxImageViewModel(
    source: .url(URL(string: "https://example.com/photo.jpg")!),
    size: .large,
    cornerRadius: FluxRadius.md
)
FluxImage(viewModel: vm)
```

---

#### FluxLoader

Loading indicator supporting indeterminate spinner or determinate progress bar.

**ViewModel:** `FluxLoaderViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `size` | `.small / .medium / .large` | `.medium` | Size |
| `tint` | `Color` | `primary` | Color |
| `progress` | `Double?` | `nil` | `nil` = spinner, `0.0–1.0` = progress bar |

```swift
// Indeterminate spinner
FluxLoader(viewModel: FluxLoaderViewModel(size: .large))

// Determinate progress bar
FluxLoader(viewModel: FluxLoaderViewModel(progress: 0.65))
```

---

#### FluxDivider

Visual separator line — horizontal or vertical.

**ViewModel:** `FluxDividerViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `axis` | `.horizontal / .vertical` | `.horizontal` | Direction |
| `color` | `Color` | `divider` | Line color |
| `thickness` | `CGFloat` | `1` | Line width |
| `cornerRadius` | `CGFloat` | `0` | Rounded ends |

```swift
FluxDivider(viewModel: FluxDividerViewModel(axis: .horizontal))
```

---

#### FluxCheckBox

Multi-select toggle with label — filled or outlined.

**ViewModel:** `FluxCheckBoxViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `isChecked` | `Bool` | `false` | Checked state |
| `label` | `String` | — | Label text |
| `style` | `.filled / .outlined` | `.filled` | Visual style |
| `size` | `.small / .medium / .large` | `.medium` | Size |
| `color` | `Color` | `primary` | Check color |
| `isDisabled` | `Bool` | `false` | Disabled |
| `onToggle` | `((Bool) -> Void)?` | `nil` | Callback |

**Size Details:**
| Size | Box | Checkmark | Text Style | Radius |
|------|-----|-----------|------------|--------|
| `.small` | 16pt | 8pt | `.footnote` | 3pt |
| `.medium` | 20pt | 10pt | `.body` | 4pt |
| `.large` | 24pt | 14pt | `.headline` | 6pt |

---

#### FluxRadioButton

Single-select option with circular indicator.

**ViewModel:** `FluxRadioButtonViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `String` | — | Label text |
| `isSelected` | `Bool` | `false` | Selected state |
| `size` | `.small / .medium / .large` | `.medium` | Size |
| `color` | `Color` | `primary` | Selection color |
| `isDisabled` | `Bool` | `false` | Disabled |
| `onSelect` | `(() -> Void)?` | `nil` | Callback |

**Sizes:** `.small` = 16pt circle / 8pt dot, `.medium` = 20pt / 10pt, `.large` = 24pt / 12pt

---

#### FluxToggle

Boolean switch using native iOS toggle control.

**ViewModel:** `FluxToggleViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `isOn` | `Bool` | `false` | Toggle state |
| `label` | `String` | — | Label text |
| `size` | `.small / .medium / .large` | `.medium` | Size |
| `tintColor` | `Color` | `primary` | Tint |
| `isDisabled` | `Bool` | `false` | Disabled |
| `onToggle` | `((Bool) -> Void)?` | `nil` | Callback |

---

#### FluxSegmentedControl

Multi-option selector with filled or outlined styles.

**ViewModel:** `FluxSegmentedControlViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `[String]` | — | Segment labels |
| `selectedIndex` | `Int` | `0` | Selected segment |
| `size` | `.small / .medium / .large` | `.medium` | Size |
| `style` | `.filled / .outlined` | `.filled` | Visual style |
| `isDisabled` | `Bool` | `false` | Disabled |
| `onSelectionChanged` | `((Int) -> Void)?` | `nil` | Callback |

**Size Padding:**
| Size | V-Padding | H-Padding |
|------|-----------|-----------|
| `.small` | 4pt | 8pt |
| `.medium` | 8pt | 12pt |
| `.large` | 12pt | 16pt |

---

#### FluxShimmer

Skeleton loading placeholder with animated gradient sweep.

**ViewModel:** `FluxShimmerViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `shape` | `.line(w,h) / .circle(d) / .rectangle(w,h,r)` | — | Placeholder shape |
| `isAnimating` | `Bool` | `true` | Animation toggle |

**Helpers:**
```swift
FluxShimmer.textBlock(lines: 3, spacing: FluxSpacing.xs)  // Multi-line placeholder
FluxShimmer.card()                                          // Avatar + title + image + text
```

---

### Molecules (10)

#### FluxCard

Generic surface container with padding, rounded corners, and shadow.

**ViewModel:** `FluxCardViewModel`

| Property | Type | Default |
|----------|------|---------|
| `padding` | `CGFloat` | `16` (FluxSpacing.md) |
| `cornerRadius` | `CGFloat` | `12` (FluxRadius.md) |
| `shadow` | `FluxShadow` | `.small` |

```swift
FluxCard(viewModel: FluxCardViewModel()) {
    VStack {
        FluxText("Card Title", style: .headline)
        FluxText("Card content goes here", style: .body)
    }
}
```

---

#### FluxTextField

Text input with label, placeholder, error state, and secure mode.

**ViewModel:** `FluxTextFieldViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `label` | `String` | — | Field label |
| `placeholder` | `String` | `""` | Placeholder text |
| `text` | `String` | `""` | Bound input value |
| `errorMessage` | `String?` | `nil` | Error text (shows red border) |
| `isSecure` | `Bool` | `false` | Password mode |

```swift
@StateObject var emailVM = FluxTextFieldViewModel(
    label: "Email",
    placeholder: "Enter your email"
)
FluxTextField(viewModel: emailVM)

// Access value: emailVM.text
// Show error: emailVM.errorMessage = "Invalid email"
```

---

#### FluxListRow

Navigation row with icon, title, subtitle, and chevron.

**ViewModel:** `FluxListRowViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `icon` | `FluxIcon.Source?` | `nil` | Leading icon |
| `iconColor` | `Color` | `primary` | Icon tint |
| `title` | `String` | — | Title text |
| `subtitle` | `String?` | `nil` | Subtitle text |
| `showChevron` | `Bool` | `true` | Trailing arrow |
| `action` | `(() -> Void)?` | `nil` | Tap handler |

```swift
FluxListRow(viewModel: FluxListRowViewModel(
    icon: .system("person.fill"),
    title: "Profile",
    subtitle: "Edit your profile"
) { navigateToProfile() })
```

---

#### FluxAlertView

Status banner with 4 semantic variants and auto-icon.

**ViewModel:** `FluxAlertViewViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `variant` | `.info / .success / .warning / .error` | — | Alert type |
| `title` | `String` | — | Title |
| `message` | `String` | — | Message body |
| `icon` | `FluxIcon.Source?` | auto per variant | Override icon |
| `isDismissible` | `Bool` | `true` | Show close button |
| `isVisible` | `Bool` | `true` | Visibility toggle |
| `onDismiss` | `(() -> Void)?` | `nil` | Dismiss callback |

**Auto-Icons by Variant:**
| Variant | Icon | Color | Background |
|---------|------|-------|------------|
| `.info` | `info.circle.fill` | primary | primary 10% |
| `.success` | `checkmark.circle.fill` | success | success 10% |
| `.warning` | `exclamationmark.triangle.fill` | warning | warning 10% |
| `.error` | `xmark.circle.fill` | error | error 10% |

Left border: 4pt accent color. Transition: opacity + slide from top on dismiss.

---

#### FluxInfoView

Icon + text information display in horizontal or vertical layout.

**ViewModel:** `FluxInfoViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `icon` | `FluxIcon.Source` | — | Display icon |
| `iconColor` | `Color` | `primary` | Icon tint |
| `title` | `String` | — | Title |
| `description` | `String` | — | Description |
| `alignment` | `.horizontal / .vertical` | `.horizontal` | Layout |

---

#### FluxOptionCard

Selection card list supporting single or multi selection.

**ViewModel:** `FluxOptionCardViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `options` | `[FluxOption]` | — | Option list |
| `selectionMode` | `.single / .multi` | `.single` | Selection mode |
| `selectedIndices` | `Set<Int>` | `[]` | Current selection |
| `onSelectionChanged` | `((Set<Int>) -> Void)?` | `nil` | Callback |

**FluxOption:** `icon: FluxIcon.Source`, `label: String`, `subtitle: String?`

Selection indicator: radio button (single) or checkbox (multi). Selected state: primary border + primary background tint.

---

#### FluxExpandableView

Collapsible content section with 3 visual styles.

**ViewModel:** `FluxExpandableViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `title` | `String` | — | Header title |
| `icon` | `FluxIcon.Source?` | `nil` | Header icon |
| `isExpanded` | `Bool` | `false` | Expand state |
| `style` | `.card / .plain / .bordered` | `.card` | Visual style |
| `onToggle` | `((Bool) -> Void)?` | `nil` | Callback |

**Styles:** `.card` = surface bg + shadow, `.plain` = no bg + divider, `.bordered` = surface bg + border

Chevron rotates 90 degrees on expand/collapse.

```swift
FluxExpandableView(viewModel: vm) {
    FluxText("Hidden content revealed here", style: .body)
}
```

---

#### FluxFlapView (Tabbed Container)

Tab bar container with 3 visual styles and icon support.

**ViewModel:** `FluxFlapViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `tabs` | `[FluxFlapTab]` | — | Tab definitions |
| `selectedIndex` | `Int` | `0` | Active tab |
| `style` | `.underlined / .filled / .pill` | `.underlined` | Tab bar style |
| `onTabChanged` | `((Int) -> Void)?` | `nil` | Callback |

**FluxFlapTab:** `title: String`, `icon: FluxIcon.Source?`

```swift
FluxFlapView(viewModel: vm) { selectedIndex in
    switch selectedIndex {
    case 0: Text("Tab 1 Content")
    case 1: Text("Tab 2 Content")
    default: EmptyView()
    }
}
```

---

#### FluxCardFlap (3D Flip Card)

Dual-sided card with 3D flip animation.

**ViewModel:** `FluxCardFlapViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `isFlipped` | `Bool` | `false` | Flip state |
| `padding` | `CGFloat` | `16` | Content padding |
| `cornerRadius` | `CGFloat` | `12` | Corner radius |
| `shadow` | `FluxShadow` | `.small` | Elevation |
| `flipDuration` | `Double` | `0.6` | Animation seconds |
| `onFlip` | `((Bool) -> Void)?` | `nil` | Callback |

```swift
FluxCardFlap(viewModel: vm,
    front: { FluxText("Front Side", style: .title) },
    back: { FluxText("Back Side", style: .title) }
)
```

Tap to flip. 180-degree Y-axis 3D rotation.

---

#### FluxBoxGrid

Grid layout with optional selection support.

**ViewModel:** `FluxBoxGridViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `items` | `[FluxBoxGridItem]` | — | Grid items |
| `columns` | `Int` | `3` | Column count |
| `selectionMode` | `.none / .single / .multi` | `.none` | Selection behavior |
| `selectedIndices` | `Set<Int>` | `[]` | Current selection |
| `itemSize` | `.small / .medium / .large` | `.medium` | Item preset |
| `onSelectionChanged` | `((Set<Int>) -> Void)?` | `nil` | Callback |

**FluxBoxGridItem:** `icon: FluxIcon.Source`, `label: String`, `color: Color`

**Item Sizes:**
| Size | Icon | Padding | Text |
|------|------|---------|------|
| `.small` | `.small` | 8pt | `.caption` |
| `.medium` | `.medium` | 12pt | `.footnote` |
| `.large` | `.large` | 16pt | `.body` |

Uses `LazyVGrid` for efficient rendering.

---

### Organisms (5)

#### FluxHeader

Top navigation bar with title, subtitle, and action slots.

**ViewModel:** `FluxHeaderViewModel`

| Property | Type | Default |
|----------|------|---------|
| `title` | `String` | — |
| `subtitle` | `String?` | `nil` |

```swift
FluxHeader(viewModel: FluxHeaderViewModel(title: "Dashboard", subtitle: "Welcome back"),
    leadingAction: { Button("Back") { goBack() } },
    trailingAction: { Button("Settings") { openSettings() } }
)
```

---

#### FluxBottomSheet

Modal overlay panel with 3 size detents and drag-to-dismiss.

**ViewModel:** `FluxBottomSheetViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `isPresented` | `Bool` | `false` | Show/hide |
| `title` | `String?` | `nil` | Sheet title |
| `detent` | `.small / .medium / .large` | `.medium` | Height |
| `showHandle` | `Bool` | `true` | Drag indicator |
| `showCloseButton` | `Bool` | `true` | Close button |
| `isDismissibleByDrag` | `Bool` | `true` | Drag to dismiss |
| `onDismiss` | `(() -> Void)?` | `nil` | Dismiss callback |

**Detent Heights:** `.small` = 25%, `.medium` = 50%, `.large` = 85% of screen

Drag threshold: 100pt downward triggers dismiss. Background overlay at 40% opacity.

```swift
FluxBottomSheet(viewModel: sheetVM) {
    VStack(spacing: FluxSpacing.md) {
        FluxListRow(viewModel: option1)
        FluxListRow(viewModel: option2)
    }
}
```

---

#### FluxFormSection

Form grouping container with optional section title.

**ViewModel:** `FluxFormSectionViewModel`

| Property | Type | Default |
|----------|------|---------|
| `title` | `String?` | `nil` |
| `spacing` | `CGFloat` | `12` (FluxSpacing.sm) |

```swift
FluxFormSection(viewModel: FluxFormSectionViewModel(title: "Personal Info")) {
    FluxTextField(viewModel: nameVM)
    FluxTextField(viewModel: emailVM)
}
```

---

#### FluxGraph

Data visualization supporting bar, line, and pie charts with animation.

**ViewModel:** `FluxGraphViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `chartType` | `.bar / .line / .pie` | — | Chart type |
| `data` | `[FluxDataPoint]` | — | Data points |
| `title` | `String?` | `nil` | Chart title |
| `showLabels` | `Bool` | `true` | X-axis labels |
| `showValues` | `Bool` | `true` | Value labels |
| `barColor` | `Color` | `primary` | Bar/line color |
| `lineColor` | `Color` | `primary` | Line color |
| `animate` | `Bool` | `true` | Animate on appear |

**FluxDataPoint:** `label: String`, `value: Double`, `color: Color?` (optional per-point override)

**Chart Details:**
| Type | Height | Features |
|------|--------|----------|
| Bar | 150pt | Vertical bars, value labels above, labels below |
| Line | 180pt | Polyline with circle markers, labels below |
| Pie | 200pt | Animated slices, color legend, percentages |

Animation: 0.8s easeInOut from 0% to 100%.

```swift
FluxGraph(viewModel: FluxGraphViewModel(
    chartType: .bar,
    data: [
        FluxDataPoint(label: "Jan", value: 120),
        FluxDataPoint(label: "Feb", value: 200),
        FluxDataPoint(label: "Mar", value: 160, color: .red),
    ],
    title: "Monthly Revenue"
))
```

---

#### FluxWebView

Embedded WKWebView with progress indicator and error handling.

**ViewModel:** `FluxWebViewViewModel`

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `url` | `URL?` | `nil` | Page URL |
| `isLoading` | `Bool` | `false` | Loading state (auto) |
| `progress` | `Double` | `0` | Load progress (auto) |
| `errorMessage` | `String?` | `nil` | Error message (auto) |
| `showProgressBar` | `Bool` | `true` | Progress bar toggle |
| `title` | `String?` | `nil` | Page title (auto) |

**Method:** `loadURL(_ urlString: String)` — validates and loads URL

iOS: Full WKWebView with KVO observers for progress & title. Error state shows retry button.
macOS: Stub view with "WebView not available on macOS" message.

---

## Package 3: flux-ios-assets

**Centralized app resources — type-safe, localized, and multi-language ready.**

[View full README](./flux-ios-assets/README.md)

### Localized Strings (FluxStrings)

All strings accessed via `NSLocalizedString` with `bundle: .module`:

| Category | Keys |
|----------|------|
| **Common** | `ok`, `cancel`, `done`, `save`, `delete`, `edit`, `close`, `retry`, `loading`, `error`, `success` |
| **Auth** | `login`, `logout`, `signUp`, `email`, `password`, `forgotPassword` |
| **Dashboard** | `title`, `welcome` |
| **Payment** | `title`, `amount`, `pay`, `confirmPayment` |

```swift
Text(FluxStrings.Auth.login)          // "Login"
Text(FluxStrings.Common.cancel)       // "Cancel"
Text(FluxStrings.Payment.pay)         // "Pay"
```

**Supported Languages:**

| Language | Code | Direction | File |
|----------|------|-----------|------|
| English | `en` | LTR | `Resources/en.lproj/Localizable.strings` |
| Arabic | `ar` | RTL | `Resources/ar.lproj/Localizable.strings` |

### Image References (FluxImages)

SF Symbol name constants organized by category:

| Category | Icons |
|----------|-------|
| **Navigation** | `home` (house.fill), `profile` (person.fill), `settings` (gear), `notifications` (bell.fill), `search` (magnifyingglass), `back` (arrow.left), `forward` (arrow.right) |
| **Editing** | `close` (xmark), `check` (checkmark), `plus`, `minus`, `trash`, `edit` (pencil), `share` (square.and.arrow.up) |
| **Media** | `heart` (heart.fill), `star` (star.fill) |
| **Status** | `warning` (exclamationmark.triangle.fill), `error` (xmark.circle.fill), `success` (checkmark.circle.fill), `info` (info.circle.fill) |
| **Financial** | `creditCard` (creditcard.fill) |
| **Security** | `lock` (lock.fill), `eye` (eye.fill), `eyeSlash` (eye.slash.fill) |

```swift
FluxIcon(source: .system(FluxImages.System.home), size: .medium)
```

**RemoteImage Helper:** `FluxImages.RemoteImage(url:)` — AsyncImage wrapper with placeholder fallback.

---

## Package 4: flux-ios-experience

**Live interactive showcase app — 29 screens demonstrating every component.**

[View full README](./flux-ios-experience/README.md)

### App Structure

The app uses a **4-tab TabView**:

```
+-----------------------------------------------+
|  flux-ios-experience                           |
|  +-------------------------------------------+ |
|  | Tab 1: Catalog                            | |
|  |   Tokens > Colors, Typography, Spacing,   | |
|  |           Radius, Shadows                  | |
|  |   Atoms  > Button, Text, Icon, Loader,    | |
|  |           Divider, Toggle, CheckBox,       | |
|  |           RadioButton, SegmentedControl,   | |
|  |           Image, Shimmer, AttributedText   | |
|  |   Molecules > TextField, Card, ListRow,    | |
|  |           AlertView, InfoView, OptionCard, | |
|  |           ExpandableView, BoxGrid,         | |
|  |           FlapView, CardFlap               | |
|  |   Organisms > FormSection, Header, Graph,  | |
|  |           BottomSheet, WebView             | |
|  +-------------------------------------------+ |
|  | Tab 2: Examples                            | |
|  |   Login Flow | Dashboard Flow | Payment   | |
|  +-------------------------------------------+ |
|  | Tab 3: Guidelines                          | |
|  |   Do's & Don'ts for Colors, Typography,   | |
|  |   Spacing, Components, Accessibility       | |
|  +-------------------------------------------+ |
|  | Tab 4: Theme                               | |
|  |   Color Scheme: [System] [Light] [Dark]    | |
|  |   Brand: [Default] [Dark Brand]            | |
|  |   Live color preview swatches              | |
|  +-------------------------------------------+ |
|  |  [ Catalog ] [ Examples ] [ Guide ] [Theme]| |
|  +-------------------------------------------+ |
+-----------------------------------------------+
```

### All 29 Showcase Screens

| # | Screen | Component | Demonstrates |
|---|--------|-----------|-------------|
| 1 | ContentView | Navigation | Master tab view with all sections |
| 2 | FluxButtonShowcase | FluxButton | 3 variants, 3 sizes, loading, disabled |
| 3 | FluxTextShowcase | FluxText | All 11 text styles |
| 4 | FluxAttributedTextShowcase | FluxText | Bold, italic, underline, colors, URLs |
| 5 | FluxIconShowcase | FluxIcon | SF Symbols, assets, URL, sizes, colors |
| 6 | FluxImageShowcase | FluxImage | Sources, sizes, borders, async loading |
| 7 | FluxLoaderShowcase | FluxLoader | Spinner, progress bar, 3 sizes |
| 8 | FluxDividerShowcase | FluxDivider | H/V orientation, thickness, colors |
| 9 | FluxCheckBoxShowcase | FluxCheckBox | Filled/outlined, sizes, animated |
| 10 | FluxRadioButtonShowcase | FluxRadioButton | Single-select groups, sizes |
| 11 | FluxToggleShowcase | FluxToggle | Native toggle, labels, tint colors |
| 12 | FluxSegmentedControlShowcase | FluxSegmentedControl | Filled/outlined, dynamic segments |
| 13 | FluxShimmerShowcase | FluxShimmer | Shapes, text block, card skeleton |
| 14 | FluxCardShowcase | FluxCard | Padding, radius, shadow variations |
| 15 | FluxTextFieldShowcase | FluxTextField | Label, placeholder, secure, errors |
| 16 | FluxListRowShowcase | FluxListRow | Icon, title, subtitle, chevron, tap |
| 17 | FluxAlertViewShowcase | FluxAlertView | Info/success/warning/error, dismiss |
| 18 | FluxInfoViewShowcase | FluxInfoView | Horizontal/vertical layouts |
| 19 | FluxOptionCardShowcase | FluxOptionCard | Single/multi selection |
| 20 | FluxExpandableViewShowcase | FluxExpandableView | Card/plain/bordered styles |
| 21 | FluxFlapViewShowcase | FluxFlapView | Underlined/filled/pill tabs |
| 22 | FluxCardFlapShowcase | FluxCardFlap | 3D flip animation |
| 23 | FluxBoxGridShowcase | FluxBoxGrid | Columns, selection modes, sizes |
| 24 | FluxHeaderShowcase | FluxHeader | Title, subtitle, action buttons |
| 25 | FluxBottomSheetShowcase | FluxBottomSheet | 3 detents, drag-to-dismiss |
| 26 | FluxFormSectionShowcase | FluxFormSection | Grouped form fields |
| 27 | FluxGraphShowcase | FluxGraph | Bar, line, pie charts |
| 28 | FluxWebViewShowcase | FluxWebView | URL loading, progress, errors |
| 29 | flux_ios_experienceApp | App Entry | @main app entry point |

---

## Theme System

Flux supports **runtime theme switching** via a protocol-based architecture. All color tokens automatically update when the theme changes.

### FluxThemeProtocol

Defines 16 required color properties:

```swift
protocol FluxThemeProtocol {
    var primary: Color { get }
    var secondary: Color { get }
    var accent: Color { get }
    var background: Color { get }
    var surface: Color { get }
    var textPrimary: Color { get }
    var textSecondary: Color { get }
    var success: Color { get }
    var warning: Color { get }
    var error: Color { get }
    var border: Color { get }
    var divider: Color { get }
    var onPrimary: Color { get }
    var onSecondary: Color { get }
    var onError: Color { get }
    var overlay: Color { get }
}
```

### Built-in Themes

**FluxDefaultTheme** (System):
| Token | Light | Dark |
|-------|-------|------|
| primary | #007AFF | #007AFF |
| secondary | #1C2541 | #1C2541 |
| accent | #5BC0BE | #5BC0BE |
| background | System | System |
| surface | System secondary | System secondary |
| success | #34C759 | #34C759 |
| warning | #FF9500 | #FF9500 |
| error | #FF3B30 | #FF3B30 |

**FluxDarkBrandTheme** (Custom dark):
| Token | Value |
|-------|-------|
| primary | #6C63FF (purple) |
| secondary | #2D2B55 (dark purple) |
| accent | #F78166 (coral) |
| background | #1A1A2E |
| surface | #16213E |

### FluxThemeManager

Singleton `ObservableObject` for runtime control:

```swift
// Switch theme
FluxThemeManager.shared.setTheme(FluxDarkBrandTheme())

// Toggle color scheme
FluxThemeManager.shared.colorScheme = .dark
FluxThemeManager.shared.toggleColorScheme()     // cycles light <-> dark
FluxThemeManager.shared.useSystemColorScheme()   // reset to system

// Apply to view hierarchy
ContentView()
    .fluxTheme(FluxThemeManager.shared)
```

### Create Your Own Theme

```swift
struct MyBrandTheme: FluxThemeProtocol {
    var primary: Color { Color(hex: 0xFF6B35) }
    var secondary: Color { Color(hex: 0x004E89) }
    var accent: Color { Color(hex: 0x00B4D8) }
    var background: Color { .white }
    var surface: Color { Color(hex: 0xF8F9FA) }
    var textPrimary: Color { Color(hex: 0x212529) }
    var textSecondary: Color { Color(hex: 0x6C757D) }
    var success: Color { .green }
    var warning: Color { .orange }
    var error: Color { .red }
    var border: Color { Color(hex: 0xDEE2E6) }
    var divider: Color { Color(hex: 0xE9ECEF) }
    var onPrimary: Color { .white }
    var onSecondary: Color { .white }
    var onError: Color { .white }
    var overlay: Color { .black.opacity(0.4) }
}

// Use it
FluxThemeManager.shared.setTheme(MyBrandTheme())
```

---

## Accessibility

Accessibility is built into every component as a core requirement:

| Feature | Implementation |
|---------|---------------|
| **Dynamic Type** | All text uses SwiftUI system fonts — respects user font size preferences |
| **VoiceOver** | Every interactive component has `.accessibilityLabel()` and `.accessibilityAddTraits()` |
| **Color Contrast** | Token-driven colors ensure sufficient contrast ratios |
| **Disabled States** | Visual feedback via 0.5 opacity (FluxOpacity.disabled) |
| **Decorative Elements** | Dividers and icons marked `.accessibilityHidden(true)` |
| **Progress Indicators** | Loaders announce percentage to screen readers |
| **Button Traits** | `.accessibilityAddTraits(.isButton)` on all tappable elements |

---

## Integration Guide

### Minimal Setup (Components + Tokens)

```swift
// Package.swift
.package(path: "../flux-ios-foundation")

// Swift file
import flux_ios_foundation  // gives you ALL components + ALL tokens
```

### Full Setup (Components + Tokens + Assets)

```swift
// Package.swift
dependencies: [
    .package(path: "../flux-ios-foundation"),
    .package(path: "../flux-ios-assets"),
]

// Swift file
import flux_ios_foundation
import flux_ios_assets
```

### Complete App Example

```swift
import SwiftUI
import flux_ios_foundation
import flux_ios_assets

struct LoginView: View {
    @StateObject var emailVM = FluxTextFieldViewModel(
        label: FluxStrings.Auth.email,
        placeholder: "you@example.com"
    )
    @StateObject var passwordVM = FluxTextFieldViewModel(
        label: FluxStrings.Auth.password,
        isSecure: true
    )
    @StateObject var loginBtn = FluxButtonViewModel(
        title: FluxStrings.Auth.login,
        variant: .primary,
        size: .large
    ) { print("Login tapped") }

    @StateObject var alert = FluxAlertViewViewModel(
        variant: .error,
        title: "Login Failed",
        message: "Invalid credentials",
        isDismissible: true
    )

    var body: some View {
        VStack(spacing: FluxSpacing.lg) {
            FluxHeader(
                viewModel: FluxHeaderViewModel(title: "Welcome Back"),
                leadingAction: { EmptyView() },
                trailingAction: { EmptyView() }
            )

            FluxCard(viewModel: FluxCardViewModel()) {
                VStack(spacing: FluxSpacing.md) {
                    FluxIcon(source: .system(FluxImages.System.lock), size: .large)
                    FluxTextField(viewModel: emailVM)
                    FluxTextField(viewModel: passwordVM)
                    FluxButton(viewModel: loginBtn)
                }
            }

            if alert.isVisible {
                FluxAlertView(viewModel: alert)
            }
        }
        .padding(FluxSpacing.lg)
        .background(FluxColors.background)
        .fluxTheme(FluxThemeManager.shared)
    }
}
```

---

## Code Metrics

| Package | Swift Files | Lines of Code | Content |
|---------|-------------|---------------|---------|
| flux-ios-ds | 11 | 458 | 10 token files + 1 module re-export |
| flux-ios-foundation | 26 | 3,182 | 11 atoms + 10 molecules + 5 organisms |
| flux-ios-assets | 3 | 121 | Strings + Images + module entry |
| flux-ios-experience | 29 | 3,718 | 29 showcase/demo screens |
| **Total** | **69** | **7,479** | **Complete design system** |

**Component Distribution:** Atoms 42% (11) | Molecules 38% (10) | Organisms 19% (5)

---

## File Structure

```
flux-design-system/
|-- README.md                          <- You are here
|-- CHARTER.md                         <- Mission, principles, architecture
|-- LICENSE                            <- MIT License
|
|-- flux-ios-ds/                       <- Design Tokens Package
|   |-- Package.swift
|   |-- README.md
|   |-- LICENSE
|   +-- Sources/flux-ios-ds/
|       |-- flux_ios_ds.swift
|       +-- Tokens/
|           |-- FluxColors.swift
|           |-- FluxTypography.swift
|           |-- FluxSpacing.swift
|           |-- FluxRadius.swift
|           |-- FluxShadow.swift
|           |-- FluxBorder.swift
|           |-- FluxOpacity.swift
|           |-- FluxShimmerEffect.swift
|           |-- FluxTheme.swift
|           +-- FluxThemeManager.swift
|
|-- flux-ios-foundation/               <- UI Components Package
|   |-- Package.swift
|   |-- README.md
|   |-- LICENSE
|   +-- Sources/flux-ios-foundation/
|       |-- flux_ios_foundation.swift
|       |-- Atoms/
|       |   |-- FluxButton.swift
|       |   |-- FluxText.swift
|       |   |-- FluxIcon.swift
|       |   |-- FluxImage.swift
|       |   |-- FluxLoader.swift
|       |   |-- FluxDivider.swift
|       |   |-- FluxCheckBox.swift
|       |   |-- FluxRadioButton.swift
|       |   |-- FluxToggle.swift
|       |   |-- FluxSegmentedControl.swift
|       |   +-- FluxShimmer.swift
|       |-- Molecules/
|       |   |-- FluxCard.swift
|       |   |-- FluxTextField.swift
|       |   |-- FluxListRow.swift
|       |   |-- FluxAlertView.swift
|       |   |-- FluxInfoView.swift
|       |   |-- FluxOptionCard.swift
|       |   |-- FluxExpandableView.swift
|       |   |-- FluxFlapView.swift
|       |   |-- FluxCardFlap.swift
|       |   +-- FluxBoxGrid.swift
|       +-- Organisms/
|           |-- FluxHeader.swift
|           |-- FluxBottomSheet.swift
|           |-- FluxFormSection.swift
|           |-- FluxGraph.swift
|           +-- FluxWebView.swift
|
|-- flux-ios-assets/                   <- Resources Package
|   |-- Package.swift
|   |-- README.md
|   |-- LICENSE
|   +-- Sources/flux-ios-assets/
|       |-- flux_ios_assets.swift
|       |-- Strings/FluxStrings.swift
|       |-- Images/FluxImages.swift
|       +-- Resources/
|           |-- en.lproj/Localizable.strings
|           +-- ar.lproj/Localizable.strings
|
+-- flux-ios-experience/               <- Showcase App
    |-- README.md
    |-- LICENSE
    +-- flux-ios-experience/
        |-- flux-ios-experience.xcodeproj
        +-- flux-ios-experience/
            |-- flux_ios_experienceApp.swift
            |-- ContentView.swift
            +-- (27 showcase files)
```

---

## Versioning

Flux follows **Semantic Versioning**:

| Change | Version Bump | Example |
|--------|-------------|---------|
| Breaking token/component API changes | **Major** | Removing a token, changing ViewModel properties |
| New tokens or components | **Minor** | Adding FluxBadge, new spacing token |
| Bug fixes and visual tweaks | **Patch** | Fixing shadow offset, adjusting padding |

---

## Package READMEs

| Package | README | Details |
|---------|--------|---------|
| flux-ios-ds | [View README](./flux-ios-ds/README.md) | Full token reference, theming guide, code examples |
| flux-ios-foundation | [View README](./flux-ios-foundation/README.md) | All 26 components, props, usage examples |
| flux-ios-assets | [View README](./flux-ios-assets/README.md) | String keys, icon names, localization guide |
| flux-ios-experience | [View README](./flux-ios-experience/README.md) | All 29 screens, setup instructions |

---

## Author

**Afzal Siddiqui**

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file.

Copyright (c) 2026 Afzal Siddiqui
