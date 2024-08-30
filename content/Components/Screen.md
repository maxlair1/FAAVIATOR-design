---
title: Screen
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**The main wrapper component which automatically accepts every Faaviator component**

# Use
---
## SwiftUI

use `Screen(){}` to Initialize the component

```swift
Screen() {
	//all content
}
```

### Parameters
| Parameter | Argument type | Default | Description |
|-----------|---------------|---------|-------------|
| `currentStep` | `Binding<CGFloat>` | `.constant(1)` | The current step in a multi-step process. |
| `totalSteps` | `CGFloat` | `1` | The total number of steps in the process. |
| `content` | `() -> Content` where `Content: View` | (required) | The main content of the screen. |
| `headerContent` | `() -> AnyView?` | `{ nil }` | Optional custom header content. |
| `footerContent` | `() -> AnyView?` | `{ nil }` | Optional custom footer content. |
| `bottomSheetPresented` | `Binding<Bool>` | `.constant(false)` | Controls the presentation of the bottom sheet. |
| `bottomSheetTitle` | `Binding<String>` | `.constant("")` | The title of the bottom sheet. |
| `bottomSheetContent` | `Binding<AnyView?>` | `.constant(nil)` | The content of the bottom sheet. |
| `pickerSheetPresented` | `Binding<Bool>` | `.constant(false)` | Controls the presentation of the picker sheet. |
| `pickerSheetTitle` | `Binding<String>` | `.constant("")` | The title of the picker sheet. |
| `pickerSheetOptions` | `Binding<[String]>` | `.constant([])` | The options available in the picker sheet. |
| `pickerSheetSelectedValue` | `Binding<String?>` | `.constant(nil)` | The currently selected value in the picker sheet. |
| `pickerSheetDisplayString` | `(String) -> String` | `{ $0 }` | A function to customize the display of picker options. |
| `pickerSheetOnConfirm` | `((String) -> Void)?` | `nil` | An optional closure to be called when a picker selection is confirmed. |

# Definition
---
```swift title="Screen.swift"

import Foundation

import SwiftUI

struct Screen: View {
    @Environment(\.dismiss) private var dismiss
    @Binding var currentStep: CGFloat
    var totalSteps: CGFloat
    let content: AnyView
    let headerContent: AnyView?
    let footerContent: AnyView?
    
    @Binding var bottomSheetPresented: Bool
    @Binding var bottomSheetTitle: String
    @Binding var bottomSheetContent: AnyView?
    
    @Binding var pickerSheetPresented: Bool
    @Binding var pickerSheetTitle: String
    @Binding var pickerSheetOptions: [String]
    @Binding var pickerSheetSelectedValue: String?
    var pickerSheetDisplayString: (String) -> String
    var pickerSheetOnConfirm: ((String) -> Void)?
    
    init<Content: View>(
        currentStep: Binding<CGFloat> = .constant(1),
        totalSteps: CGFloat = 1,
        bottomSheetPresented: Binding<Bool> = .constant(false),
        bottomSheetTitle: Binding<String> = .constant(""),
        bottomSheetContent: Binding<AnyView?> = .constant(nil),
        pickerSheetPresented: Binding<Bool> = .constant(false),
        pickerSheetTitle: Binding<String> = .constant(""),
        pickerSheetOptions: Binding<[String]> = .constant([]),
        pickerSheetSelectedValue: Binding<String?> = .constant(nil),
        pickerSheetDisplayString: @escaping (String) -> String = { $0 },
        pickerSheetOnConfirm: ((String) -> Void)? = nil,
        @ViewBuilder content: () -> Content,
        @ViewBuilder headerContent: () -> (AnyView)? = { nil },
        @ViewBuilder footerContent: () -> (AnyView)? = { nil }
    ) {
        self._currentStep = currentStep
        self.totalSteps = totalSteps
        self._bottomSheetPresented = bottomSheetPresented
        self._bottomSheetTitle = bottomSheetTitle
        self._bottomSheetContent = bottomSheetContent
        self._pickerSheetPresented = pickerSheetPresented
        self._pickerSheetTitle = pickerSheetTitle
        self._pickerSheetOptions = pickerSheetOptions
        self._pickerSheetSelectedValue = pickerSheetSelectedValue
        self.pickerSheetDisplayString = pickerSheetDisplayString
        self.pickerSheetOnConfirm = pickerSheetOnConfirm
        self.content = AnyView(content())
        self.headerContent = headerContent()
        self.footerContent = footerContent()
    }
    
    var body: some View {
        ZStack {
            VStack {
                if let header = headerContent {
                    header
                } else {
                    defaultHeader
                }
                
                content
                
                Spacer()
                
                if let footer = footerContent {
                    footer
                } else {
                    defaultFooter
                }
            }
        }
        .toolbar {
            ToolbarItem(placement: .principal) {
                VStack(alignment: .leading) {
                    if (totalSteps >= 0)  {
                        ProgressBarView(totalSteps: totalSteps, currentSteps: currentStep)
                    }
                }
            }
        }
//        .frame(minHeight: 50)
        .BottomSheetView(isPresented: $bottomSheetPresented, title: bottomSheetTitle) {
            bottomSheetContent
        }
        .PickerSheetView(
            isPresented: $pickerSheetPresented,
            title: pickerSheetTitle,
            options: pickerSheetOptions,
            selectedValue: $pickerSheetSelectedValue,
            displayString: pickerSheetDisplayString,
            onConfirm: pickerSheetOnConfirm
        )
    }
    
    private var defaultHeader: some View {
        VStack(alignment: .leading) {
            Button(action: {
                dismiss()
            }) {
            }
            .circularButtonStyle(icon: Image(systemName: "arrow.left"), size: .small)
        }.frame(maxWidth: .infinity, alignment: .leading)
            .padding(.horizontal)
    }
    
    private var defaultFooter: some View {
        EmptyView()
    }
}

extension String: Identifiable {
    public var id: String { self }
}
```
