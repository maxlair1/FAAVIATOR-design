---
title: Dropdown
draft: 
tags:
  - Component
  - Input
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**A dropdown (sometimes called a select) lets users choose a single item from a dropdown list.**
# Use

---
## SwiftUI

Use `DropdownField()` to Initialize the component

```swift
DropdownField(options: options, selectedOption: listOfOptions, action: {
     //click action
})
```

To create a standard list select (Toggle) with a toggling [[content/Components/Popups/Bottom Sheet|Bottom Sheet]], you use a `ForEach` item, and list out each option as `Standalone Checkbox's` use:

```swift
ZStack {
		DropdownField(props..., action: {
			bottomSheetPresented = true
		})
}..BottomSheetView(isPresented: $bottomSheetPresented, title: "Choose option") {
            VStack(spacing: 24) {
	            //list out Array<String> of options
                ForEach(options, id: \.self) { option in
                    StandaloneCheckbox(
                        isChecked: Binding(
	                        // set selected option to the current option
                            get: { selectedOption == option },
                            set: { _ in }
                        ),
                        label: option,
                        action: {
	                        //set the checkbox option to selected option
                            dropdown1_selectedOption = option
                            //close bottom sheet
                            dropdown1_sheet = false
                        },
                        // radio = true: select ONE option
                        // radio = false: select ALL THAT APPLY
                        radio: true
                    )
                }
            }
        }
```
### Parameters

| Parameter        | Argument type   | Default | Description                                                                                                                                                      |
| ---------------- | --------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `options`        | `Array<String>` | `nil`   | Array of options that user can choose from.                                                                                                                      |
| `selectedOption` | `String`        | `nil`   | The variable that stores which option is selected.                                                                                                               |
| `action`         | `() -> Void`    | `nil`   | This is the action that occurs when the dropdown is tapped. Should be used to trigger the opening of a [[content/Components/Popups/Bottom Sheet\|Bottom Sheet]]. |
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
```swift title="DropdownInput.swift"

import Foundation
import SwiftUI

//MARK: Dropdown Field (Input/button)
struct DropdownField: View {
    @Binding var selectedOption: String
    @State private var showBottomSheet = false
    var label: String
    var desc: String
    let placeholder: String
    let options: [String]
    let action: (() -> Void)

    init(placeholder: String = "Select", options: [String], label: String = "", desc: String = "", selectedOption: Binding<String>, action: @escaping (() -> Void)) {
        self.options = options
        self.label = label
        self.desc = desc
        self.placeholder = placeholder
        self._selectedOption = selectedOption
        self.action = action
    }

    var body: some View {
        ZStack {
            VStack(alignment: .leading, spacing: 8) {
                if !label.isEmpty {
                    Text(label)
                        .font(.interInputLabel)
                        .foregroundStyle(Color.TextPrimary)
                }
                
                if !desc.isEmpty {
                    Text(desc)
                        .font(.interInputLabel)
                        .foregroundStyle(Color.TextTertiary)
                }
                
                Button(action: {
                    action()
                }) {
                    HStack {
                        Text(selectedOption.isEmpty ? placeholder : selectedOption)
                            .foregroundColor(selectedOption.isEmpty ? .TextTertiary : .TextPrimary)
                        
                        Spacer()
                        
                        Image(systemName: "chevron.down")
                            .foregroundColor(.blue)
                            .rotationEffect(Angle(degrees: showBottomSheet ? 180 : 0))
                    }
                    .font(.interInputType)
                    .padding()
                    .background(
                        RoundedRectangle(cornerRadius: 8)
                            .stroke(Color.gray, lineWidth: 1)
                    )
                }
            }
        }
    }
}

```
# Figma
---
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2903-512%26t%3DfSbyYOn9zNHADTrZ-1" allowfullscreen></iframe>