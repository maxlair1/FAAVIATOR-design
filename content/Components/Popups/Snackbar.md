---
title: Snackbar
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**Non-invasive confirmation pop-ups that notify the user of a recent action.**
* Light and dark variants, both with a right and left active version. When more than two items are needed, just duplicate the options. Never more than 3 options.
# Use

---
## SwiftUI

use `.Snackbar` on a view to Initialize the component.

```swift
YourView
	.Snackbar(isPresented: $showSnackbar, message: "Snackbar Message", icon: "checkmark", action: {
		//action
	}, duration: 8.0)
```

### Parameters

| Parameter     | Argument type      | Default       | Description                                             |
| ------------- | ------------------ | ------------- | ------------------------------------------------------- |
| `isPresented` | Boolean            | `nil`         | Condition when snackbar is active.                      |
| `icon`        | String (SF Symbol) | `"Checkmark"` | SF Symbol that is rendered before the Snackbar's label. |
| `Action`      | `() -> Action`     | `nil`         | Action that occurs when snackbar is tapped.             |
| `Message`     | String             | `nil`         | Snackbar label.                                         |
| `Duration`    | Double (Seconds)   |               | Time it takes until it dismisses on its own.            |
### Dependencies 
---
Both the [[content/Components/Popups/Modal|Modal]] and the Snackbar components rely on an external CocoaPods package called [PopupView](https://github.com/exyte/PopupView). Make sure this package is added to your local project.

![[content/dependency_popup.png]]

%%
### Modifiers

| Modifier | Effect | Description |
| -------- | ------ | ----------- |
|          |        |             |

 ## React

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
```swift title="Snackbar.swift"
import SwiftUI
import PopupView

enum ActionType {
    case view, edit
    
    var label: String {
        switch self {
        case .view: return "View"
        case .edit: return "Edit"
        }
    }
}

extension View {
    func Snackbar(
        isPresented: Binding<Bool>,
        message: String,
        icon: String = "checkmark",
        iconColor: Color = .green,
        backgroundColor: Color = .black,
        textColor: Color = .white,
        actionType: ActionType? = .view,
        action: (() -> Void)? = nil,
        duration: Double = 8.0
    ) -> some View {
        self.popup(isPresented: isPresented) {
            HStack(spacing: 8) {
                Image(systemName: icon)
                    .foregroundColor(iconColor)
                    .imageScale(.large)

                Text(message)
                    .foregroundColor(textColor)
                    .font(.interBody)
                    .lineLimit(1)

                Spacer()

                if let actionType = actionType, let action = action {
                    Button(action: action) {
                        Text(actionType.label)
                            .foregroundColor(.gray100)
                            .underline()
                            .font(.interBody)
                        
                    }
                }
            }
            .padding()
            .background(backgroundColor)
            .cornerRadius(8)
            .padding(.horizontal)
            .frame(maxWidth: .infinity, alignment: .bottom)
        } customize: {
            $0
            .autohideIn(duration)
            .type (.floater(verticalPadding: 8, horizontalPadding: 8, useSafeAreaInset: true))
            .dragToDismiss(true)
            .appearFrom(.bottomSlide)
        }
    }
}

```
# Figma
---
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2750-389%26t%3DYGRAyV5h2HYi1VN0-1" allowfullscreen></iframe>