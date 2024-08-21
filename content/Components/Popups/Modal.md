---
title: Modal
draft: 
tags:
  - Component
  - Popup
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**The quintessential pop-up window that displays itself in the center of the screen. Interrupts a user's action in order to draw attention to a hierarchically more important task.**
# Use

---
## SwiftUI

use `.ModalView` ViewModifier to Initialize the component

```swift
YourView
	.ModalView(isPresented: $showModal, title: "Modal", content: {
	     //Modal content
	}
```
### Parameters

| Parameter     | Argument type   | Default | Description                                   |
| ------------- | --------------- | ------- | --------------------------------------------- |
| `isPresented` | Boolean         | `nil`   | Determines weather the modal is shown or not. |
| `title`       | String          | `nil`   | The title at the top of the modal.            |
| `content`     | `() -> content` | `nil`   | The content inside of the modal               |

### Dependencies 
---
Both the Modal and the [[content/Components/Popups/Snackbar|Snackbar]] components rely on an external CocoaPods package called [PopupView](https://github.com/exyte/PopupView). Make sure this package is added to your local project.

![[content/img/dependency_popup.png]]

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
```swift title="Modal.swift"
import Foundation
import SwiftUI
import PopupView

extension Animation {
    static var fadeUpAnimation: Animation {
        Animation.spring(response: 0.2, dampingFraction: 0.7, blendDuration: 0.1)
    }
}

struct Modal<Content: View>: View {
    @Binding var isPresented: Bool
    let title: String
    let content: Content
    
    init(isPresented: Binding<Bool>, title: String, @ViewBuilder content: () -> Content) {
        self._isPresented = isPresented
        self.title = title
        self.content = content()
    }
    
    var body: some View {
        VStack(spacing: 16) {
            modalHeader
            modalContent
        }
        .frame(maxWidth: .infinity)
        .background(Color.backgroundPrimary)
        .cornerRadius(24)
        .padding()
        
    }
    
    private var modalHeader: some View {
        HStack {
            Text(title)
                .font(.interBottomSheetTitle)
                .frame(maxWidth: .infinity, alignment: .leading)
            Spacer()
            closeButton
        }
        .frame(maxWidth: .infinity)
        .padding(.horizontal, 16)
        .padding(.top, 16)
        .padding(.bottom, 8)
    }
    
    private var closeButton: some View {
        Button(action: {
            dismissModal()
        }) {}
        .circularButtonStyle(
            icon: Image(systemName: "xmark"),
            size: .small
        )
        .frame(maxWidth: .infinity, alignment: .trailing)
    }
    
    private var modalContent: some View {
        
            VStack() {
                content
            }
            .padding(.horizontal, 16)
            .padding(.bottom, 16)
    }
    
    private func dismissModal() {
        withAnimation(.easeInOut(duration: 0.3)) {
            isPresented.toggle()
        }
    }
}

extension View {
    func ModalView<Content: View>(
        isPresented: Binding<Bool>,
        title: String,
        @ViewBuilder content: @escaping () -> Content
    ) -> some View {
        self.popup(isPresented: isPresented) {
                    
                    Modal(isPresented: isPresented, title: title, content: content)
                        .transition(.move(edge: .bottom))
                        .zIndex(1)
                        .opacity(isPresented.wrappedValue ? 1 : 0)
                        
        } customize: {
            $0
                .type(.floater(verticalPadding: 16, horizontalPadding: 8, useSafeAreaInset: true))
                .position(.center)
                .animation(.fadeUpAnimation)
                .appearFrom(.centerScale)
                .backgroundColor(.black.opacity(0.4))
                .closeOnTap(false)
                .closeOnTapOutside(true)
                .dragToDismiss(false)
        }
            .animation(.easeInOut(duration: 0.3), value: isPresented.wrappedValue)
        }
    }

```

# Figma
---
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2881-1078%26t%3DZPIkI7GIPvi8MvWr-1" allowfullscreen></iframe> 
