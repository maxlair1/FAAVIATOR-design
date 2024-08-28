---
title: Card
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Container element used to visually organize similar information together.**
# Use

---
## SwiftUI

use `Card` to Initialize the component

```swift
Card {
	  //content
}
```
# Definition
---
```swift title="Card.swift"
import SwiftUI
import Foundation

struct Card<Content: View>: View {
    let content: Content
    
    init(@ViewBuilder content: () -> Content) {
        self.content = content()
    }
    
    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            content
        }
        .frame(maxWidth: /*@START_MENU_TOKEN@*/.infinity/*@END_MENU_TOKEN@*/, alignment: .leading)
        .padding()
        .background(Color.BackgroundSecondary)
        .cornerRadius(16)
        .shadow(color: Color(red: 0.22, green: 0.25, blue: 0.3).opacity(0.05), radius: 5, x: 0, y: 4)
    }
}

// Example usage:

// Preview
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        Card {
            Text("This is text").font(.inter(.semiBold, size: 28)).foregroundStyle(.textPrimary)
            Text("This is how I would imagine some body text This is how I would imagine some body text ").font(.interBody).foregroundStyle(.textSecondary)
        }.padding()
    }
}

```
# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D165-0%26m%3Ddev" allowfullscreen></iframe>