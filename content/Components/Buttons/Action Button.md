---
title: ActionButton
draft: 
tags:
  - component
  - SwiftUI
---

> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**An action button lets the user perform an action that is independent from the rest of the content on screen.**
- Action button is different from [[content/Components/Buttons/Button|Button]] because it has no `fillWidth` property, only has one size, and contains an icon. It is also meant of different type of interaction.
- Use when
	1) There's a standalone action that the user can take, that isn’t the primary action in context of the screen
	2) The user needs to perform an action, such as initiating a new flow in a separate screen or a bottom sheet
	3) There's one or more possible actions in the same section
- DO NOT use the Action Button if you just want to include an icon in a button. Instead, consider the [[content/Components/Buttons/Circular Button|Circular Button]], or using a standard [Icon](content/Components/Icons).
# Use
---

## SwiftUI

Use `ActionButtonStyle()` as a property inside of a [`.buttonStyle`](https://developer.apple.com/documentation/swiftui/buttonstyle) to Initialize the view.

```swift title="SwiftUI"
Button("Test"){
	//action
}.buttonStyle(ActionButtonStyle())
```

Parameters of Properties of `SwiftComponent(_:)`

### Parameters

| Parameter      | Arg type       | Options                                                                                                                           | Default    | Description                                                                                      |
| -------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------ |
| `buttonType`   | `ButtonType`   | `.primary`<br>`.secondary`<br>`.negative`<br>                                                                                     | `.primary` | This is the color of the icon.                                                                   |
| `fullWidth`    | Bool           | `true` or  `false`                                                                                                                | `true`     | Determines if the button will fill all available horizontal space                                |
| `icon`         | String         | [SF Symbols](https://developer.apple.com/sf-symbols/)<br>[Iconoir Icons(*DEPRECEIATED*)](https://developer.apple.com/sf-symbols/) | `nil`      | Determines what Icon will be rendered<br><br>> [!Warning] Only accepts SF symbols the time being |
| `iconPosition` | `IconPosition` | `.leading`<br>`.trailing`                                                                                                         | `.leading` | Is the icon rendered before or after the label                                                   |

### Modifiers

Accepts all SwiftUI Button modifiers, including `.disabled()`


%% ## React

Use `<ReactComponent />` to Initialize the component

```tsx title="React"
//React Usage
```

Properties of `SwiftComponent(_:)`

| Properties | Type    | Default    | Description                    |
| ---------- | ------- | ---------- | ------------------------------ |
| `Color`    | `Color` | `.blue600` | This is the color of the icon. |
 %%
# Definition
---
```swift title="GlobalStyles.swift"
struct ActionButtonStyle: ButtonStyle {
    @Environment(\.isEnabled) private var isEnabled

    enum ButtonType {
        case primary, secondary, negative
        
        var backgroundColor: Color {
            switch self {
            case .primary: return Color.blue600
            case .secondary: return Color.BackgroundSecondary
            case .negative: return Color.red600
            }
        }
        
        var foregroundColor: Color {
            switch self {
            case .primary, .negative: return Color.gray100
            case .secondary: return Color.TextPrimary
            }
        }
        
        var disabledForegroundColor: Color {
            switch self {
            case .primary, .negative: return Color.TextTertiary
            case .secondary: return Color.TextPrimary.opacity(0.30)
            }
        }
        
        var disabledBackgroundColor: Color {
            switch self {
            case .primary, .negative: return Color.BackgroundSecondary
            case .secondary: return Color.BackgroundSecondary.opacity(0.50)
            }
        }
    }
    
    let buttonType: ButtonType
    // for the time being, we will use SF symbols for the action button icons, because of how restricting the iconoir icons are.
//    let icon: AnyView?
    let icon: String
    let iconPosition: IconPosition

    enum IconPosition {
        case leading, trailing
    }

    init(buttonType: ButtonType, icon: String, iconPosition: IconPosition = .leading) {
        self.buttonType = buttonType
        self.iconPosition = iconPosition
        self.icon = icon
    }

    func makeBody(configuration: Configuration) -> some View {
        HStack(spacing: 0) {
            if iconPosition == .leading {
                Image(systemName:icon).font(.system(size: 14).weight(.semibold))
            }
            configuration.label
                .padding(.horizontal, 4)
            if iconPosition == .trailing {
                Image(systemName:icon).font(.system(size: 14).weight(.semibold))
            }
        }
        .padding(.horizontal, 10.5)
        .padding( .vertical, 7)
        .background(isEnabled ? buttonType.backgroundColor : buttonType.disabledBackgroundColor)
        .foregroundColor(isEnabled ? buttonType.foregroundColor : buttonType.disabledForegroundColor)
        .cornerRadius(100)
        .scaleEffect(configuration.isPressed ? 0.95 : 1)
        .font(.interButtonSmall)
    }
}


```
# Figma

<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2749-321%26t%3DEVa2U7sP6p6mxy6p-1" allowfullscreen></iframe>
# Action Button vs [[content/Components/Buttons/Button|Button]] 
---
- Action button is only available in the small size, whereas button also comes in Large and small sizes.
- The main difference between the two is that the action button doesn’t have a full-width version. Instead, the width of the action button changes to fit its content.
- Action button supports the use of a left or right-aligned icon, whereas button does not.