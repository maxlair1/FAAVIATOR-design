---
title: Checkbox
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Simple checkbox used in [[content/Components/Inputs/Checkbox Field|Checkbox Fields]].**

>[!danger] Avoid using this component alone. Only use inside of [[content/Components/Inputs/Checkbox Field|Checkbox Fields]]. 
# Use
---
## SwiftUI

Use `.CheckboxStyle()` on a `Toggle()` object to Initialize the component.

```swift
Toggle("", isOn: $isChecked)
	.toggleStyle(CheckboxStyle(radio: true, action: {
		//action when clicked
	}))
```
### Parameters

| Parameter | Argument type | Default | Description                                                                      |
| --------- | ------------- | ------- | -------------------------------------------------------------------------------- |
| `radio`   | Boolean       | `false` | Is the checkbox a square (all that apply), or is it a circle (radio/select one). |
| `action`  | `() -> Void`  | `nil`   | Run an action on check.                                                          |

# Definition
---
```swift title="GlobalStyles.swift"
struct CheckboxStyle: ToggleStyle {
    var radio: Bool = false
    var action: (() -> Void)?
    
    func makeBody(configuration: Configuration) -> some View {
        Button(action: {
            withAnimation(.spring(response: 0.3, dampingFraction: 0.7, blendDuration: 0.05)) {
                configuration.isOn.toggle()}
            action?()
        }) {
            RoundedRectangle(cornerRadius: radio ? 12 : 4)
                .stroke((configuration.isOn ? Color.blue600 : Color.gray500), lineWidth: 2).transition(.scale(scale: 0.8).combined(with: .opacity))
                .frame(width: 18, height: 18)
                .background(
                    ZStack {
                        if configuration.isOn {
                            RoundedRectangle(cornerRadius: radio ? 12 : 4)
                                .fill(Color.blue600)
                                .transition(.scale(scale: 0.8).combined(with: .opacity))
                            
                            Image(systemName:"checkmark").resizable()
                                .scaledToFit()
                                .frame(width: 12, height: 12)
                                .fontWeight(.semibold)
                                .foregroundColor(.white)
                                .transition(.scale.combined(with: .opacity))
                                
                        }
                    }
                )
        }
        .buttonStyle(PlainButtonStyle())
    }
}
```
