---
title: scrollOnOverflow()
draft: 
tags:
  - Utility
  - Modifier
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

Modifier that wraps it's content in a [`ScrollView()`](https://developer.apple.com/documentation/swiftui/scrollview) ONLY WHEN the inner content exceeds the vertical height of its container (overflows).

---
## SwiftUI

use `.scrollOnOverflow()` modifier on content to Initialize.

```swift
.scrollOnOverflow()
```
### Parameters

| Parameter        | Argument type | Default | Description                                                                                   |
| ---------------- | ------------- | ------- | --------------------------------------------------------------------------------------------- |
| `allowScrolling` | Boolean       | True    | If scrolling is conditionally allowed, or permanently disabled. Indented for use with states. |
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
```swift title="ScrollOnOverflow.swift"
import Foundation
import SwiftUI

struct OverflowContentViewModifier: ViewModifier {
    @State private var contentOverflow: Bool = false
    let allowScrolling: Bool
    
    init(allowScrolling: Bool = true) {
        self.allowScrolling = allowScrolling
    }
    
    func body(content: Content) -> some View {
        GeometryReader { geometry in
            content
                .background(
                    GeometryReader { contentGeometry in
                        Color.clear.onAppear {
                            contentOverflow = contentGeometry.size.height > geometry.size.height
                        }
                    }
                )
                .wrappedInScrollView(when: contentOverflow && allowScrolling)
        }
    }
}

extension View {
    @ViewBuilder
    func wrappedInScrollView(when condition: Bool) -> some View {
        if condition {
            ScrollView {
                self
            }
        } else {
            self
        }
    }
}

extension View {
    func scrollOnOverflow(allowScrolling: Bool = true) -> some View {
        modifier(OverflowContentViewModifier(allowScrolling: allowScrolling))
    }
}

```
