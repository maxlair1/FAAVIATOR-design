---
title: Bottom Sheet
draft:
tags:
  - component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**A bottom sheet is a container you can use to display supporting content or a short, supplementary task on mobile experiences.**
# Use

---
## SwiftUI

use the modifier `.BottomSheetView` on a [`ZStack`](https://developer.apple.com/documentation/swiftui/zstack) to Initialize the component.

> [!WARNing ] *Modifier MUST be applied to a `ZStack` for the Bottom Sheet to layer correctly.*

```swift title="SwiftUI"
@State private var showBottomSheet = false
var body: some View {
            ZStack {
                // rest of screen content, and element that triggers 'showBottomSheet'
            }
            .BottomSheetView(isPresented: $showBottomSheet, title: "Title") {
                // sheet content
            }
        }
```

- The bottom sheet utilizes [`.scrollOnOverflow()`](scrollOnOverflow()) utility to prevent inner content from scrolling if it's height does not overflow container.

### Parameters

| Parameter     | Argument type | Default | Description                                                 |
| ------------- | ------------- | ------- | ----------------------------------------------------------- |
| `Title`       | String        | `nil`   | The title displayed at the top of the Bottom Sheet          |
| `isPresented` | Boolean       | `nil`   | Determines if Bottom Sheet is presented in the current view |

# Definition
---
```swift title="BottomSheet.swift"
import SwiftUI

struct BottomSheet<Content: View>: View {
    @Binding var isPresented: Bool
    let title: String
    let content: Content
    
    @State private var currentHeight: CGFloat
    @State private var isFullyExpanded: Bool = false
    
    let minHeight: CGFloat
    let maxHeight: CGFloat
    
    init(isPresented: Binding<Bool>, title: String, @ViewBuilder content: () -> Content) {
        self._isPresented = isPresented
        self.title = title
        self.content = content()
        
        let screenHeight = UIScreen.main.bounds.height
        self.minHeight = screenHeight * 0.35
        self.maxHeight = screenHeight * 0.9
        self._currentHeight = State(initialValue: minHeight)
    }
    
    var body: some View {
        VStack {
            sheetHeader
            sheetContent
        }
        .frame(maxWidth: .infinity, maxHeight: currentHeight)
        .background(Color.backgroundPrimary)
        .cornerRadius(24)
        .frame(maxWidth: .infinity, maxHeight: .infinity, alignment: .bottom)
        .gesture(dragGesture)
        .animation(.spring(response: 0.5, dampingFraction: 0.7, blendDuration: 0), value: currentHeight)
        .padding(8)
    }
    
    private var sheetHeader: some View {
        VStack {
            closeButton
            Text(title)
                .font(.interTitle)
                .frame(maxWidth: .infinity, alignment: .leading)
        }
        .frame(maxWidth: .infinity)
        .padding()
    }
    
    private var closeButton: some View {
        Button(action: {
            dismissSheet()
        }) {}
        .circularButtonStyle(
            icon: Image(systemName: "xmark"),
            size: .small
        )
        .frame(maxWidth: .infinity, alignment: .trailing)
    }
    
    private var sheetContent: some View {
        
            VStack(alignment: .leading, spacing: 16) {
                content
            }
            .padding()
            .scrollOnOverflow(allowScrolling:(isFullyExpanded))
    }
    
    private var dragGesture: some Gesture {
        DragGesture()
            .onChanged(handleDragChange)
            .onEnded(handleDragEnd)
    }
    
    private func dismissSheet() {
        withAnimation(.easeInOut(duration: 0.3)) {
            isPresented.toggle()
        }
    }
    
    private func handleDragChange(_ gesture: DragGesture.Value) {
        let dragAmount = gesture.translation.height
        let newHeight = currentHeight - dragAmount / 15
        currentHeight = max(minHeight, min(maxHeight, newHeight))
    }
    
    private func handleDragEnd(_ gesture: DragGesture.Value) {
        let offsetY = gesture.translation.height
        if offsetY > 150 {
            dismissSheet()
        } else if currentHeight >= maxHeight - 50 || offsetY < -100 {
            expandSheet()
        } else {
            resetSheet()
        }
    }
    
    private func expandSheet() {
        withAnimation(.spring(response: 0.5, dampingFraction: 0.7, blendDuration: 0)) {
            currentHeight = maxHeight
            isFullyExpanded = true
        }
    }
    
    private func resetSheet() {
        withAnimation(.spring(response: 0.5, dampingFraction: 0.7, blendDuration: 0)) {
            currentHeight = minHeight
            isFullyExpanded = false
        }
    }
}

extension View {
    func BottomSheetView<Content: View>(
        isPresented: Binding<Bool>,
        title: String,
        @ViewBuilder content: @escaping () -> Content
    ) -> some View {
        ZStack {
            self
            ZStack {
                if isPresented.wrappedValue {
                    Color.gray1000
                        .opacity(0.4)
                        .edgesIgnoringSafeArea(.all)
                        .transition(.opacity)
                    
                    BottomSheet(isPresented: isPresented, title: title, content: content)
                        .transition(.move(edge: .bottom))
                        .zIndex(1)
                }
            }
            .animation(.easeInOut(duration: 0.3), value: isPresented.wrappedValue)
        }
    }
}

```
# Figma
---

 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="100%" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2903-632%26t%3DCJuV3vJs6YRqidJ3-1" allowfullscreen></iframe> 