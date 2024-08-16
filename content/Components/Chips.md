---
title: Chips
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Chips allow users to filter content or make a choice from a set of options within a compact area. Can also serve as tags for specific information.**

Types:
1) Static Chip
2) Selectable Chip
3) Status Chip
# Use

---
## SwiftUI

```swift
@State private var isSelected = false
@State private var statusState: StatusState = .pending

SelectableChip(text: "Selectable Chip", isSelected: $isSelected) {
	isSelected = false
}
	             
StaticChip(text: "Static Tag")

StatusChip(state: statusState)
```
>[!Danger] There is currently no way to map and collect `SelectableChip()` information. Goal is to add this in **Version 2**
### Parameters

#### SelectableChip():

| Parameter    | Argument type | Default | Description                               |
| ------------ | ------------- | ------- | ----------------------------------------- |
| `Text`       | String        | `nil`   | The chips label.                          |
| `isSelected` | Boolean       | `nil`   | Determines if the chip is selected or not |
> **Function Body** -> Runs the code inside on chip click.
#### StaticChip():

| Parameter | Argument type | Default | Description      |
| --------- | ------------- | ------- | ---------------- |
| `Text`    | String        | `nil`   | The chips label. |
#### StatusChip():

| `Text`  | String        | Argument Options                             | `nil` | The chips label.                          |
| ------- | ------------- | -------------------------------------------- | ----- | ----------------------------------------- |
| `state` | `StatusState` | `.pending`,<br>`.incomplete`,<br>`.complete` | `nil` | Determines if the chip is selected or not |
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
```swift title="Chip.swift"
import Foundation
import SwiftUI

//MARK: Static Chip
struct StaticTag: View {
    let text: String
    
    var body: some View {
        Text(text).font(.interChip)
            .padding(.horizontal, 12)
            .padding(.vertical, 6)
            .foregroundColor(.TextPrimary)
            .clipShape(Capsule())
            .overlay(
                Capsule()
                    .stroke(Color.BackgroundTertiary, lineWidth: 1)
            )
    }
}

//MARK: Selectable Chip
struct SelectableChip: View {
    let text: String
    @Binding var isSelected: Bool
    let onRemove: () -> Void
    
    var body: some View {
        HStack {
            Text(text).font(.interChip)
            if isSelected {
                Button(action: onRemove) {
                    Image(systemName: "xmark")
                        .foregroundColor(.TextPrimary)
                        .font(.system(size: 12))
                        .padding(4).frame(height:14)
                }
            }
        }
        .padding(.horizontal, 12)
        .padding(.vertical, 6)
        .background(isSelected ? Color.blue600 : Color.clear)
        .overlay(
            Capsule()
                .stroke(isSelected ? Color.clear : Color.BackgroundQuaternary, lineWidth: 1)
        )
        .foregroundColor(isSelected ? .gray100 : .textPrimary)
        .cornerRadius(20)
        .onTapGesture {
            isSelected = true
        }
    }
}

//MARK: Status Chip
enum StatusState {
    case complete, incomplete, pending
}

struct StatusTag: View {
    let state: StatusState
    
    var body: some View {
        HStack(spacing: 6) {
            Circle().overlay {
                statusIcon
                    .foregroundColor(state == .pending ? .TextPrimary : .gray900.opacity(0.80))
                    .font(.system(size: 14, weight: .semibold))
            }.frame(width: 20, height: 20).foregroundColor(backgroundColor)
            statusText.font(.interChip)
        }
        .padding(.leading, 6)
        .padding(.trailing, 12)
        .padding(.vertical, 6)
        .overlay(
            Capsule()
                .stroke(Color.BackgroundTertiary, lineWidth: 1)
        )
    }
    
    private var statusIcon: some View {
        switch state {
        case .complete:
            return Image(systemName: "checkmark")
        case .incomplete:
            return Image(systemName: "exclamationmark")
        case .pending:
            return Image(systemName: "clock")
        }
    }
    
    private var statusText: some View {
        switch state {
        case .complete:
            return Text("Complete")
        case .incomplete:
            return Text("Incomplete")
        case .pending:
            return Text("Pending")
        }
    }
    
    private var backgroundColor: Color {
        switch state {
        case .complete:
            return .green400
        case .incomplete:
            return .orange400
        case .pending:
            return .BackgroundSecondary
        }
    }
}

```

# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D1360-15673%26t%3DNSCH05sMA19HUM0C-1" allowfullscreen></iframe>
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D3008-437%26t%3DNSCH05sMA19HUM0C-1" allowfullscreen></iframe>