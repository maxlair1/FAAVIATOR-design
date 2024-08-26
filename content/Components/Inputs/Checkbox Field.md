---
title: Checkbox Field
draft: 
tags:
  - Component
  - Input
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Input type that has a simple “checked/unchecked” interaction. Used when the user is expected to answer using a “yes” or “no.” OR can be used when a user needs to select one (or a few) options from a list**
- Uses the [[content/Components/Checkbox|Checkbox]] component.
- There are two types of Checkbox Fields:
	1) [[#Standalone Checkbox]] meant when multiple checkbox's are used. in succession.
	2) [[#Contained Checkbox]] used when a singular field is required
# Use

---
## SwiftUI

### Standalone Checkbox

```swift
StandaloneCheckbox(isChecked: $isChecked, label: "Check me!")
```

### Contained Checkbox

```swift
ContainedCheckbox(isChecked: $isChecked, label: "Check me too!")
```

### Parameters

| Parameter   | Argument type  | Default | Description                                                                             |
| ----------- | -------------- | ------- | --------------------------------------------------------------------------------------- |
| `label`     | String         | `nil`   | The label of the CheckboxField                                                          |
| `isChecked` | Boolean        | `nil`   | Determines weather the checkbox is checked or not. The var where that boolean is held.  |
| `action`    | `(() -> Void)` | `nil`   | The action that is performed on a check.                                                |
| Radio       | Boolean        | `False` | Weather the checkbox style inside the field is round (radio), or square (multi-select). |
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
```swift title="CheckboxField.swift"
import Foundation
import SwiftUI

//MARK Contained Checkbox
struct ContainedCheckbox: View {
    @Binding var isChecked: Bool
    let label: String
    let radio: Bool
    let action: (() -> Void)?
    
    init(isChecked: Binding<Bool>, label: String, radio: Bool = false, action: (() -> Void)? = nil) {
        self._isChecked = isChecked
        self.label = label
        self.radio = radio
        self.action = action
    }
    
    var body: some View {
        Button(action: {
            isChecked.toggle()
        }) {
            HStack(spacing: 14) {
                Toggle("", isOn: $isChecked)
                            .toggleStyle(CheckboxStyle())
                Text(label)
                    .font(.interInputType)
                Spacer()
            }
            .padding(.horizontal, 14)
            .padding(.vertical, 16)
            .background(
                RoundedRectangle(cornerRadius: 8)
                    .stroke(Color.gray500, lineWidth: 1)
            ).background(Color.BackgroundPrimary)
        }
        .buttonStyle(PlainButtonStyle())
    }
}

//MARK Standalone Checkbox
struct StandaloneCheckbox: View {
    @Binding var isChecked: Bool
    let label: String
    let action: (() -> Void)?
    let radio: Bool
    
    init(isChecked: Binding<Bool>, label: String, action: (() -> Void)? = nil, radio: Bool = false) {
        self._isChecked = isChecked
        self.label = label
        self.action = action
        self.radio = radio
    }
    
    var body: some View {
        Button(action: {
            isChecked.toggle()
            action?()
        }) {
            HStack {
                Text(label)
                    .font(.system(size: 16))
                Spacer()
                Toggle("", isOn: $isChecked)
                    .toggleStyle(CheckboxStyle(radio: radio, action: action))
            }
            .padding(.vertical, 8)
            .padding(.trailing, 8)
            .background(Color.BackgroundPrimary)
        }
        .buttonStyle(PlainButtonStyle())
        .cornerRadius(8)
    }
}

```
# Figma
---
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2890-126%26t%3DfSbyYOn9zNHADTrZ-1" allowfullscreen></iframe>
