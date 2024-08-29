---
title: Picker Sheet
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Sheet that opens at the bottom of the screen and contains a [[iOS wheel picker]](https://developer.apple.com/documentation/swiftui/pickerstyle/wheel).**
- Use this if you have loads of values that a user needs to quickly jump through. A good way to determine this is if the location and number of values is *predictable* even if it is long.
- Use a regular [[content/Components/Popups/Bottom Sheet|Bottom Sheet]] If you want to display content.
# Use

---
## SwiftUI

use `.PickerSheetView` on any container to Initialize the component

```swift
//some container
	.PickerSheetView(
		isPresented: $isPickerPresented,
		title: "Select an Option",
		options: options,
		selectedValue: $selectedOption,
		displayString: { $0.name },
		onConfirm: { selected in
			print("Confirmed selection: \(selected.name)")
		}
	)
```

### Parameters

| Parameter       | Argument type   | Default       | Description                                                       |
| --------------- | --------------- | ------------- | ----------------------------------------------------------------- |
| `isPresented`   | Boolean         | `nil`         | This is the color of the icon.                                    |
| `title`         | String          | "Pick one"    | Headline of the sheet                                             |
| `options`       | `[T]`           | `nil`         | String of values that can be picked from                          |
| `selectedValue` | `T?`            | `nil`         | Var that stores the selected value                                |
| `displayString` | `(T) -> String` | `{ "\($0)" }` | What is displayed per option element in place of the actual value |
| `onConfirm`     | `(T) -> Void`   | `nil`         | Function run when a value is selected                             |

# Definition
---
```swift title="PickerSheet.swift"

import Foundation
import SwiftUI

struct PickerSheet<T: Hashable & Identifiable>: View {
    @Binding var isPresented: Bool
    @Binding var selectedValue: T?
    let title: String
    let options: [T]
    let displayString: (T) -> String
    let onConfirm: ((T) -> Void)?
    
    @State private var tempSelectedValue: T?
    @State private var offset: CGFloat = 1000 // Start offscreen

    init(isPresented: Binding<Bool>,
         selectedValue: Binding<T?>,
         title: String,
         options: [T],
         displayString: @escaping (T) -> String = { "\($0)" },
         onConfirm: ((T) -> Void)? = nil) {
        self._isPresented = isPresented
        self._selectedValue = selectedValue
        self.title = title
        self.options = options
        self.displayString = displayString
        self.onConfirm = onConfirm
    }

    var body: some View {
        GeometryReader { geometry in
            ZStack(alignment: .bottom) {
                Color.black
                    .opacity(isPresented ? 0.4 : 0)
                    .edgesIgnoringSafeArea(.all)
                    .onTapGesture {
                        dismissSheet()
                    }

                VStack(spacing: 0) {
                    sheetHeader
                    sheetContent
                    confirmButton
                }
                .frame(maxWidth: .infinity)
                .background(Color.backgroundPrimary)
                .cornerRadius(24)
                .frame(height: geometry.size.height * 0.45)
                .offset(y: offset)
                .padding(8)
            }
        }
        .edgesIgnoringSafeArea(.all)
        .onAppear {
            tempSelectedValue = selectedValue
            DispatchQueue.main.asyncAfter(deadline: .now() + 0) {
                withAnimation(.easeInOut(duration: 0.5)) {
                    offset = 0
                }
            }
        }
    }

    private var sheetHeader: some View {
        VStack {
            closeButton
            Text(title)
                .font(.interBottomSheetTitle)
                .frame(maxWidth: .infinity, alignment: .leading)
        }
        .frame(maxWidth: .infinity)
        .padding(.horizontal)
        .padding(.top)
    }

    private var closeButton: some View {
        Button(action: {
            dismissSheet()
        }) {
        }
        .circularButtonStyle(icon: Image(systemName: "xmark"), size: .small)
        .frame(maxWidth: .infinity, alignment: .trailing)
    }

    var sheetContent: some View {
        Picker("", selection: $tempSelectedValue) {
            ForEach(options) { value in
                Text(displayString(value))
                    .tag(value as T?)
            }
        }
        .pickerStyle(WheelPickerStyle())
        .frame(height: 150)
        .padding(.horizontal)
    }

    var confirmButton: some View {
        Button("Confirm") {
            if let value = tempSelectedValue {
                selectedValue = value
                onConfirm?(value)
            }
            dismissSheet()
        }
        .buttonStyle(RoundedButtonStyle(buttonType: .primary))
        .padding()
    }

    private func dismissSheet() {
        withAnimation(.spring(response: 0.5, dampingFraction: 0.7, blendDuration: 0)) {
            offset = 1000 // Move offscreen
        }
        DispatchQueue.main.asyncAfter(deadline: .now() + 0.3) {
            isPresented = false
        }
    }
}

extension View {
    func PickerSheetView<T: Hashable & Identifiable>(
        isPresented: Binding<Bool>,
        title: String,
        options: [T],
        selectedValue: Binding<T?>,
        displayString: @escaping (T) -> String = { "\($0)" },
        onConfirm: ((T) -> Void)? = nil
    ) -> some View {
        ZStack {
            self
            if isPresented.wrappedValue {
                PickerSheet(
                    isPresented: isPresented,
                    selectedValue: selectedValue,
                    title: title,
                    options: options,
                    displayString: displayString,
                    onConfirm: onConfirm
                )
            }
        }
    }
}

```
