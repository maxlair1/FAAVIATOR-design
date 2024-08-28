---
title: Password Input
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Simple text input. Used when the application expects the user to return a vital keyword or password.**
# Use
---
## SwiftUI

If you would like to create a password input, with the "eyeball" icon that toggles visibility of the user input, then use `PasswordInput`. It uses `.customTextInputStyle()`.

```swift
PasswordInput(password: password)
```

### Parameters

| Parameter     | Argument type    | Default | Description                                                                          |
| ------------- | ---------------- | ------- | ------------------------------------------------------------------------------------ |
| `Password`    | Binding\<String> | `nil`   | the binding that stores the users input                                              |
| `label`       | String           | `""`    | Title representing the input                                                         |
| `desc`        | String           | `""`    | Additonal description of label                                                       |
| `text`        | String           | `""`    | *PRE-TYPED* text in the input                                                        |
| `isFocused`   | Bool             | `nil`   | Currently does **nothing**                                                           |
| `placeholder` | String           | `" "`   | The sample text that is in the box to represent the value that the user might input. |

# Definition
---
```swift title="PasswordInput.swift"
//
//  PasswordField.swift
//  Faaviator
//
//  Created by Robert Lair on 7/19/24.
//

import SwiftUI

public struct PasswordInput: View {
    @State var password: String
    
    @State private var isSecure: Bool = true
    @State private var isFocused: Bool
    
    let label: String
    let desc: String
    let text: String
    let placeholder: String
    
    init(placeholder: String = "", text: String = "", desc: String = "", label: String = "", isFocused: Bool = false, password: String, isSecure: Bool = true) {
        self.password = password
        self.isSecure = isSecure
        self.label = label
        self.desc = desc
        self.text = text
        self.isFocused = isFocused
        self.placeholder = placeholder
    }
    
    public var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            VStack(alignment: .leading, spacing: 4) {
                if !label.isEmpty {
                    Text(label).font(.interInputLabel)
                }
                if !desc.isEmpty {
                    Text(desc).font(.interInputDesc)
                }
            }
            HStack {
                if isSecure {
                    SecureField("Placeholder", text: $password, prompt: Text(placeholder).font(.interInputType).foregroundStyle(Color.TextTertiary)
                    )
                } else {
                    TextField("Placeholder", text: $password, prompt: Text(placeholder).font(.interInputType).foregroundStyle(Color.TextTertiary)
                    )
                }
                
                Button(action: {
                    isSecure.toggle()
                }) {
                    Image(systemName: isSecure ? "eye.slash" : "eye")
                        .foregroundColor(.gray)
                }
            }
            .customTextInputStyle()
        }.frame(maxWidth: /*@START_MENU_TOKEN@*/.infinity/*@END_MENU_TOKEN@*/)
    }
}

#Preview {
    PasswordInput(password: "Password")
}

```

