---
title: Circular Button
draft:
tags:
  - component
---
> [!example] &nbsp;&nbsp;Version 1.1
> - 9/26 Added `.negative` button type

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**A circular button lets the user perform an action with a tap or a click.  Also can be used in a row with descriptive labels, when the high-level interactions on a page are all equally important.

Most commonly used as the navigation [[Components/iOS UI/Back Button|Back Button]], or the close button/interaction on a [[Components/Popups/Bottom Sheet|Bottom Sheet]].**

# Use

---
## SwiftUI

use the modifier `.circularButtonStyle()` to Initialize the component. This button does not use the [buttonStyle](https://developer.apple.com/documentation/swiftui/buttonstyle) modifier because it is not a restyle, instead it is a custom component.

```swift title="SwiftUI"
Button(action: {
	// Your action here
}) {}
.circularButtonStyle(
	icon: Image(systemName: "plus")
)
```
### Parameters

| Parameter | Argument type                                         | Default            | Description                                                                              |
| --------- | ----------------------------------------------------- | ------------------ | ---------------------------------------------------------------------------------------- |
| `Icon`    | Image                                                 | None, **Required** | The SF Symbol rendered in the button. This is a required parameter.                      |
| `Color`   | `.primary`,<br>`.secondary`,<br>`.negative`           | `.primary`         | The color/hierarchy of the button.                                                       |
| `Size`    | `.small`,<br>`.medium`,<br>`.large`,<br>`.extraLarge` | `.medium`          | The size of the entire button. The `label` and `Icon` both scale with this size as well. |
| `label`   | String                                                | `nil`              | The text displayed underneath the button if required. Disabled by default.               |

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
struct CircularButtonStyle: ButtonStyle {
    @Environment(\.isEnabled) private var isEnabled
    
    enum ButtonType {
        case primary, secondary
        
        var backgroundColor: Color {
            switch self {
            case .primary: return Color.blue600
            case .secondary: return Color.gray200
            }
        }
        
        var foregroundColor: Color {
            switch self {
            case .primary: return Color.white
            case .secondary: return Color.TextPrimary
            }
        }
    }
    
    enum ButtonSize {
        case small, medium, large, extraLarge
        
        var diameter: CGFloat {
            switch self {
            case .small: return 40
            case .medium: return 50
            case .large: return 60
            case .extraLarge: return 70
            }
        }
        
        var iconSize: CGFloat {
            switch self {
            case .small, .medium: return 20
            case .large: return 24
            case .extraLarge: return 28
            }
        }
        
        var labelFont: Font {
            switch self {
            case .small, .medium: return .interButtonMedium
            case .large, .extraLarge: return .interButtonLarge
            }
        }
    }
    
    let buttonType: ButtonType
    let icon: Image
    let size: ButtonSize
    let label: String?
    
    init(buttonType: ButtonType, icon: Image, size: ButtonSize = .medium, label: String? = nil) {
        self.buttonType = buttonType
        self.icon = icon
        self.size = size
        self.label = label
    }
    
    func makeBody(configuration: Configuration) -> some View {
        VStack(spacing: 4) {
            icon
                .font(.system(size: size.iconSize, weight: .medium))
                .frame(width: size.diameter, height: size.diameter)
                .background(buttonType.backgroundColor)
                .foregroundColor(buttonType.foregroundColor)
                .clipShape(Circle())
                .scaleEffect(configuration.isPressed ? 0.95 : 1)
            
            if let label = label {
                Text(label)
                    .font(size.labelFont)
                    .foregroundColor(.textSecondary)
            }
        }
    }
}
```
# Figma
---

<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2749-352%26t%3DuT2wGrsGcG7Wzyo9-1" allowfullscreen></iframe>
