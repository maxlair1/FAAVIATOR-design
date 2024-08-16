---
title: Segmented Button
draft:
tags:
  - component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**Used when two buttons function as tabs, and related in action**.
# Use

---
## SwiftUI

Use `CustomSegmentedControl(_:)` to Initialize the component

```swift
@State private var selectedSegment = 0
let options = ["Option 1", "Option 2", "Option 3"]

CustomSegmentedControl(selection: $selectedSegment, options: options)
	.padding()
```

### Parameters

| Parameter   | Argument type  | Default | Description                                                                        |
| ----------- | -------------- | ------- | ---------------------------------------------------------------------------------- |
| `options`   | Array\<String> | `nil`   | The array of strings that are both the options, and labels for the icons           |
| `selection` | `@State`       | `0`     | Which segment is selected represented by numbers starting with zero. Returns `int` |
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
```swift title="SegmentedButton.swift"
import SwiftUI

struct CustomSegmentedControl: View {
    @Binding var selection: Int
    let options: [String]
    
    var body: some View {
        GeometryReader { geometry in
            ZStack(alignment: .leading) {
                Capsule()
                    .fill(Color.white)
                    .shadow(color: Color.black.opacity(0.1), radius: 2, x: 0, y: 1)
                    .frame(width: segmentWidth(in: geometry), height: geometry.size.height - 8)
                    .offset(x: segmentOffset(in: geometry), y: 0)
                    .animation(.easeInOut(duration: 0.3), value: selection)
                
                HStack(spacing: 0) {
                    ForEach(options.indices, id: \.self) { index in
                        segmentButton(for: index, in: geometry)
                    }
                }
            }
            .padding(4)
            .background(Color.gray.opacity(0.2))
            .clipShape(Capsule())
        }
        .frame(height: 44) // Default height, can be overridden
    }
    
    private func segmentWidth(in geometry: GeometryProxy) -> CGFloat {
        (geometry.size.width - 2) / CGFloat(options.count) // Subtract 8 to account for the outer padding
    }
    
    private func segmentOffset(in geometry: GeometryProxy) -> CGFloat {
        CGFloat(selection) * segmentWidth(in: geometry)
    }
    
    private func segmentButton(for index: Int, in geometry: GeometryProxy) -> some View {
        Button(action: {
            selection = index
        }) {
            Text(options[index])
                .font(.system(size: 14, weight: .medium))
                .frame(width: segmentWidth(in: geometry), height: geometry.size.height - 8)
                .foregroundColor(selection == index ? .black : .gray)
        }
        .buttonStyle(PlainButtonStyle())
    }
}

```
# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2750-389%26t%3DWJboFR1zwjEse5HT-1" allowfullscreen></iframe> 