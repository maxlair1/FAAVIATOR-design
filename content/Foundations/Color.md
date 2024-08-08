---
title: Color
draft: 
tags:
  - Foundation
  - React
  - SwiftUI
---
**Our colors represent first-responders, public safety, and aviation. One of the most visually expressive parts of a brand identity, and particularly a user interface.**

>[!example]    &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

## Overview
---
![[Colors_cover.png]]
## Use
---
This is how to use the component
### SwiftUI

use `SwiftComponent(_:)` to Initialize the component

```swift title="SwiftUI"
//SwiftUI Usage
```
##### Properties of `SwiftComponent(_:)`

| Properties | Type    | Default    | Description                    |
| ---------- | ------- | ---------- | ------------------------------ |
| `Color`    | `Color` | `.blue600` | This is the color of the icon. |

### React
Use `<ReactComponent />` to Initialize the component

```tsx title="React"
//React Usage
```

Properties of `SwiftComponent(_:)`

| Properties | Type    | Default    | Description                    |
| ---------- | ------- | ---------- | ------------------------------ |
| `Color`    | `Color` | `.blue600` | This is the color of the icon. |

## Install
---
### SwiftUI

```swift title="Color+FAATheme.swift"

import Foundation
import SwiftUI

extension Color {
    // MARK: - Gray Colors
    static let gray100 = Color(red: 254/255, green: 254/255, blue: 254/255)
    static let gray200 = Color(red: 238/255, green: 238/255, blue: 238/255)
    static let gray300 = Color(red: 214/255, green: 214/255, blue: 214/255)
    static let gray400 = Color(red: 181/255, green: 181/255, blue: 181/255)
    static let gray500 = Color(red: 149/255, green: 149/255, blue: 149/255)
    static let gray600 = Color(red: 118/255, green: 118/255, blue: 118/255)
    static let gray700 = Color(red: 89/255, green: 89/255, blue: 89/255)
    static let gray800 = Color(red: 66/255, green: 66/255, blue: 66/255)
    static let gray900 = Color(red: 43/255, green: 43/255, blue: 43/255)
    static let gray1000 = Color(red: 28/255, green: 28/255, blue: 28/255)

    // MARK: - Blue Colors
    static let blue100 = Color(red: 253/255, green: 254/255, blue: 255/255)
    static let blue200 = Color(red: 224/255, green: 240/255, blue: 255/255)
    static let blue300 = Color(red: 179/255, green: 218/255, blue: 255/255)
    static let blue400 = Color(red: 113/255, green: 186/255, blue: 255/255)
    static let blue500 = Color(red: 49/255, green: 151/255, blue: 255/255)
    static let blue600 = Color(red: 1/255, green: 112/255, blue: 244/255)
    static let blue700 = Color(red: 0/255, green: 82/255, blue: 194/255)
    static let blue800 = Color(red: 0/255, green: 61/255, blue: 147/255)
    static let blue900 = Color(red: 0/255, green: 40/255, blue: 98/255)
    static let blue1000 = Color(red: 0/255, green: 27/255, blue: 64/255)

    // MARK: - Green Colors
    static let green100 = Color(red: 252/255, green: 255/255, blue: 251/255)
    static let green200 = Color(red: 208/255, green: 250/255, blue: 197/255)
    static let green300 = Color(red: 113/255, green: 241/255, blue: 82/255)
    static let green400 = Color(red: 41/255, green: 209/255, blue: 0/255)
    static let green500 = Color(red: 34/255, green: 172/255, blue: 0/255)
    static let green600 = Color(red: 27/255, green: 137/255, blue: 0/255)
    static let green700 = Color(red: 20/255, green: 103/255, blue: 0/255)
    static let green800 = Color(red: 15/255, green: 77/255, blue: 0/255)
    static let green900 = Color(red: 10/255, green: 50/255, blue: 0/255)
    static let green1000 = Color(red: 7/255, green: 33/255, blue: 0/255)

    // MARK: - Orange Colors
    static let orange100 = Color(red: 255/255, green: 254/255, blue: 252/255)
    static let orange200 = Color(red: 253/255, green: 235/255, blue: 208/255)
    static let orange300 = Color(red: 250/255, green: 208/255, blue: 145/255)
    static let orange400 = Color(red: 246/255, green: 163/255, blue: 40/255)
    static let orange500 = Color(red: 210/255, green: 131/255, blue: 15/255)
    static let orange600 = Color(red: 167/255, green: 104/255, blue: 12/255)
    static let orange700 = Color(red: 126/255, green: 78/255, blue: 9/255)
    static let orange800 = Color(red: 94/255, green: 58/255, blue: 6/255)
    static let orange900 = Color(red: 61/255, green: 38/255, blue: 4/255)
    static let orange1000 = Color(red: 40/255, green: 25/255, blue: 3/255)

    // MARK: - Red Colors
    static let red100 = Color(red: 255/255, green: 253/255, blue: 253/255)
    static let red200 = Color(red: 255/255, green: 233/255, blue: 233/255)
    static let red300 = Color(red: 255/255, green: 200/255, blue: 200/255)
    static let red400 = Color(red: 255/255, green: 152/255, blue: 152/255)
    static let red500 = Color(red: 255/255, green: 93/255, blue: 93/255)
    static let red600 = Color(red: 223/255, green: 49/255, blue: 49/255)
    static let red700 = Color(red: 172/255, green: 32/255, blue: 32/255)
    static let red800 = Color(red: 130/255, green: 22/255, blue: 22/255)
    static let red900 = Color(red: 87/255, green: 15/255, blue: 15/255)
    static let red1000 = Color(red: 58/255, green: 10/255, blue: 10/255)

    // MARK: - Semantic Colors
    static let modeNeutral = Color.white

    static let Primary = Color.blue600
    static let Secondary = Color.red600
    static let Tertiary = Color.orange400
    //Note: The following are assigned from the color sets. Alternatively bring in these colors through the snippet pop-up (CMD + SHIFT + L > Color)
    
    //ex: .foregroundColor(Color."TextPrimary")) OR .foregroundColor(Color.TextPrimary)
    // Background Colors
    static let BackgroundPrimary = Color("BackgroundPrimary")
    static let BackgroundSecondary = Color("BackgroundSecondary")
    static let BackgroundTertiary = Color("BackgroundTertiary")
    static let BackgroundQuaternary = Color("BackgroundQuaternary")

    // Text Colors
    static let TextPrimary = Color("TextPrimary")
    static let TextSecondary = Color("TextSecondary")
    static let TextTertiary = Color("TextTertiary")
    static let TextInvert = Color("TextInvert")

    // Button Colors
    static let buttonsChipDefault = Color.gray500
    static let buttonsChipDefaultContrast = Color.gray900
    static let buttonsChipSelected = Color.blue600
    static let buttonsChipSelectedContrast = Color.gray100
    static let buttonsFocusOutline = Color.gray800
    static let buttonsNegativePrimary = Color.red600
    static let buttonsNegativePrimaryActive = Color.red600.opacity(0.75)
    static let buttonsNegativePrimaryContrast = Color.gray100
    static let buttonsNegativePrimaryDisabled = Color.gray300
    static let buttonsNegativePrimaryDisabledContrast = Color.gray500
    static let buttonsNegativePrimaryHover = Color.red600.opacity(0.9)
    static let buttonsPositivePrimary = Color.blue600
    static let buttonsPositivePrimaryActive = Color.blue600.opacity(0.75)
    static let buttonsPositivePrimaryContrast = Color.blue100
    static let buttonsPositivePrimaryDisabled = Color.gray300
    static let buttonsPositivePrimaryDisabledContrast = Color.gray500
    static let buttonsPositivePrimaryHover = Color.blue600.opacity(0.9)
    static let buttonsPositiveSecondary = Color.gray200
    static let buttonsPositiveSecondaryActive = Color.gray200.opacity(0.5)
    static let buttonsPositiveSecondaryContrast = Color.gray900
    static let buttonsPositiveSecondaryDisabled = Color.gray200
    static let buttonsPositiveSecondaryDisabledContrast = Color.gray500
    static let buttonsPositiveTertiaryStroke = Color.gray500
    static let buttonsPositiveTertiaryActive = Color.gray100
    static let buttonsPositiveTertiaryContrast = Color.gray900
    static let buttonsPositiveTertiaryDisabledStroke = Color.gray500.opacity(0)
    static let buttonsPositiveTertiaryDisabledContrast = Color.gray500
    static let buttonsPositiveTertiaryHover = Color.gray200.opacity(0.5)
    static let buttonsSegmentedButtonsActiveBackground = Color.gray200
    static let buttonsSegmentedButtonsActiveText = Color.gray1000
    static let buttonsSegmentedButtonsBackground = Color.gray300
    static let buttonsSegmentedButtonsInactiveText = Color.gray700

    // Icons Colors
    static let iconsBase = Color.gray700

    // Input Colors
    static let inputsCheckboxActive = Color.blue600
    static let inputsCheckboxInactiveOutline = Color.gray700
    static let inputsCheckboxIcon = Color.gray100
    static let inputsCheckboxLabel = Color.textPrimary
    static let inputsCheckboxOutline = Color.gray600
    static let inputsTextInputLabel = Color.gray700
    static let inputsTextInputNote = Color.gray900
    static let inputsTextInputOutline = Color.gray600
    static let inputsTextInputPlaceholder = Color.gray400
    static let inputsTextInputText = Color.gray800

    // Overlays Colors
    static let overlaysBackdrop = Color.black.opacity(0.45)

    // Snackbar Colors
    static let snackbarBackground = Color.gray1000
    static let snackbarText = Color.textInvert

    // Tabs Colors
    static let tabsActive = Color.blue600
    static let tabsInactive = Color.gray800
    
}

```
### React
```
//how to use the colors in react
```

## Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D454-1%26t%3DhtxkjYoMJasVsPWv-1" allowfullscreen></iframe>  