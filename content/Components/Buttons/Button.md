---
title: Button
draft:
tags:
  - component
  - SwiftUI
---

> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview

---

**Interactive backbone element of any application. Used in navigation, actions, and confirmations.**

- This button is used when users need to respond to an action or move to the next set of steps in a sequence. If you want a button that is meant to initiate an action or alter a user's view, use the [[ActionButton]].
- This button does not support icons. If your interaction **requires** an icon, consider using the [[ActionButton]] or [[Circular Button]].

# Use

---

## SwiftUI

Our main button can be accessed through a global SwiftUI style called `RoundedButtonStyle()`.

Use `RoundedButtonStyle()` as a property inside of a [`.buttonStyle`](https://developer.apple.com/documentation/swiftui/buttonstyle) to Initialize the view.

```swift title="ContentView.swift"
//nest inside of some view ....
	Button("Button label"){
		// action
	}.buttonStyle(RoundedButtonStyle())
```

### Parameters

| Parameter    | Arg type                      | Options                                                      | Default    | Description                                                       |
| ------------ | ----------------------------- | ------------------------------------------------------------ | ---------- | ----------------------------------------------------------------- |
| `buttonType` | [`ButtonType`](#`ButtonType`) | `.primary`<br>`.secondary`<br>`.tertiary`<br>`.negative`<br> | `.primary` | This is the color of the icon.                                    |
| `fillWidth`  | Bool                          | `true` or `false`                                            | `true`     | Determines if the button will fill all available horizontal space |
| `Size`       | [`Size`](#`Size`)             | `.small`<br>`.medium`<br>`.large`                            | `.medium`  | Determines the size of the button                                 |

### Modifiers

Accepts all SwiftUI Button modifiers, including `.disabled()`

### Enums

##### `ButtonType`

> Determines what hierarchy of button is displayed.
> Handles the `foregroundColor()`, `backgroundColor()`, as well as `.disabled()` state.
> Argument accepts `.primary,` `.secondary`, `.tertiary`, and `.negative`

##### `Size`

> Determines the size of the button, out of small, medium, and large.
> Controls both the `fontSize` and `paddingScale` of the button.
> Argument accepts `.small,` `.medium`, and `.large`.

%% ```swift
enum Size {
case small, medium, large

        var paddingScale: CGFloat {
            switch self {
            case .small: return 0.5
            case .medium: return 0.7
            case .large: return 0.8
            }
        }

        var fontSize: Font {
            switch self {
            case .small: return .interButtonSmall
            case .medium: return .interButtonMedium
            case .large: return .interButtonLarge
            }
        }
    }

````%%

%% ## React
Use `<ReactComponent />` to Initialize the component

```tsx title="React"
//React Usage
````

Properties of `SwiftComponent(_:)`

| Properties | Type    | Default    | Description                    |
| ---------- | ------- | ---------- | ------------------------------ |
| `Color`    | `Color` | `.blue600` | This is the color of the icon. |

%%

# Definition

---

```swift title="GlobalStyles.swift"
struct RoundedButtonStyle: ButtonStyle {
    @Environment(\.isEnabled) private var isEnabled

    enum Size {
        case small, medium, large

        var paddingScale: CGFloat {
            switch self {
            case .small: return 0.5
            case .medium: return 0.7
            case .large: return 0.8
            }
        }

        var fontSize: Font {
            switch self {
            case .small: return .interButtonSmall
            case .medium: return .interButtonMedium
            case .large: return .interButtonLarge
            }
        }
    }

    enum ButtonType {
        case primary, secondary, tertiary, negative

        var backgroundColor: Color {
            switch self {
            case .primary: return Color.blue600
            case .secondary: return Color.BackgroundSecondary
            case .tertiary: return Color.clear
            case .negative: return Color.red600
            }
        }

        var bacgroundColor: Color {
            switch self {
            case .primary, .negative: return Color.gray100
            case .secondary: return Color.TextPrimary
            case .tertiary: return Color.TextPrimary
            }
        }

        var disabledForegroundColor: Color {
            switch self {
            case .primary, .negative: return Color.gray100.opacity(0.30)
            case .secondary, .tertiary: return Color.TextPrimary.opacity(0.30)
            }
        }

        var disabledBackgroundColor: Color {
            switch self {
            case .primary, .negative: return Color.BackgroundSecondary
            case .secondary: return Color.BackgroundSecondary.opacity(0.30)
            case .tertiary: return Color.clear

            }
        }

        var borderColor: Color {
            switch self {
            case .primary, .secondary, .negative: return Color.clear
            case .tertiary: return Color.TextTertiary
            }
        }


    }

    let fillWidth: Bool
    let size: Size
    let buttonType: ButtonType

    init(fillWidth: Bool = true, size: Size = .medium, buttonType: ButtonType = .primary) {
        self.fillWidth = fillWidth
        self.size = size
        self.buttonType = buttonType
    }

    func makeBody(configuration: Configuration) -> some View {
        configuration.label
            .padding(.horizontal, 30 * size.paddingScale)
            .padding(.vertical, 20 * size.paddingScale)
            .frame(maxWidth: fillWidth ? .infinity : nil)
            .background(isEnabled ? buttonType.backgroundColor : buttonType.disabledBackgroundColor)
            .foregroundColor(isEnabled ? buttonType.bacgroundColor : buttonType.disabledForegroundColor)
            .overlay(
                Capsule()
                    .stroke(isEnabled ? buttonType.borderColor : Color.clear, lineWidth: buttonType == .tertiary ? 2 : 0)
            )
            .clipShape(Capsule())
            .cornerRadius(100)
            .scaleEffect(configuration.isPressed ? 0.95 : 1)
            .font(size.fontSize)
            .contentShape(Capsule())

    }
}
```

# Design

---

 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1); borderRadius: 0.5rem;" width="100%" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2749-163%26t%3DffNokx75ia2y6qWQ-1" allowfullscreen></iframe>
