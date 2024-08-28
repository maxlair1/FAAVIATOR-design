---
title: Input
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Simple text input. Used when the application expects the user to return information via text. This component is used as the base for several other input items.**
- If your input is meant to be a password field, use the [[content/Components/Inputs/Password Input|Password Input]]
# Use
---
## SwiftUI

use `CustomInput()` to Initialize the component, which uses the `.customTextInputStyle()` which can be used on any `Input` item as well...

```swift
CustomInput(placeholder: "Time", userInput: selectedTime)
```
### Parameters

| Parameter     | Argument type     | Default | Description                                                                          |
| ------------- | ----------------- | ------- | ------------------------------------------------------------------------------------ |
| `userInput`   | `Binding<String>` | `nil`   | The variable that saves the typed content that the user inputs.                      |
| `label`       | String            | `""`    | Title representing the input                                                         |
| `desc`        | String            | `""`    | Additonal description of label                                                       |
| `text`        | String            | `""`    | *PRE-TYPED* text in the input                                                        |
| `isFocused`   | Bool              | `nil`   | Currently does **nothing**                                                           |
| `placeholder` | String            | `" "`   | The sample text that is in the box to represent the value that the user might input. |

# Definition
---
```swift title="Input.swift"
//
//  InputField.swift
//  Faaviator
//
//  Created by Max Lair on 8/6/24.
//

//import Foundation
//import SwiftUI
//
//public struct InputField: View {
//    @Binding var text: String
//    var placeholder: String
//    
//    public var body: some View {
//        TextField(placeholder, text: $text)
//            .customTextFieldStyle()
//    }
//}

//struct ContentView: View {
//    @State private var username: String = ""
//    @State private var email: String = ""
//    
//    var body: some View {
//        VStack {
//            InputField(text: $username, placeholder: "Username")
//            InputField(text: $email, placeholder: "Email")
//        }
//    }
//}

import SwiftUI
struct CustomInput: View {
    let label: String
    let desc: String
    let text: String
    @State private var isFocused: Bool
    @State private var userInput: String
    let placeholder: String
    
    init(placeholder: String = "", text: String = "", desc: String = "", label: String = "", isFocused: Bool = false, userInput: String) {
        self.label = label
        self.desc = desc
        self.text = text
        self.isFocused = isFocused
        self.userInput = userInput
        self.placeholder = placeholder
    }
    
    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            VStack(alignment: .leading, spacing: 4) {
                if !label.isEmpty {
                    Text(label).font(.interInputLabel)
                }
                if !desc.isEmpty {
                    Text(desc).font(.interInputDesc)
                }
            }
            TextField("Placeholder", text: $userInput, prompt: Text(placeholder).font(.interInputType).foregroundStyle(Color.TextTertiary)
            )
                .customTextInputStyle()
        }.frame(maxWidth: .infinity)
    }
}


```

# Figma
---
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2854-448%26t%3D8sWbGNgGdjv2OOjJ-1" allowfullscreen></iframe>