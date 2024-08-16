---
title: Switch
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**A switch lets the user toggle an individual setting on or off.**
# Use

---
## SwiftUI

use `.SwitchStyle()` on a `Toggle()` component to apply the styling.

```swift
Toggle("", isOn: $isOn)
	.SwitchStyle()
```
%%

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
```swift title="GlobalStyles.swift"
struct Switch: ToggleStyle {
	var onColor: Color = .blue600
	var offColor: Color = .BackgroundSecondary
	var thumbColor: Color = .gray100

	func makeBody(configuration: Configuration) -> some View {
	RoundedRectangle(cornerRadius: 8)
		.fill(configuration.isOn ? onColor : offColor)
		.frame(width: 55, height: 32)
		.overlay(
			RoundedRectangle(cornerRadius: 4)
				.fill(thumbColor)
				.shadow(radius: 0.5, x: 0, y: 1)
				.padding(4)
				.offset(x: configuration.isOn ? 10 : -10)
				.frame(width: 35, height: 33)
		)
		.animation(.spring(response: 0.2, dampingFraction: 0.9), value: configuration.isOn)
		.onTapGesture {
			configuration.isOn.toggle()
		}
}
...
extension View {
    func SwitchStyle(
        ) -> some View {
            self.toggleStyle(Switch())
        }
}

}
```

# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2890-1707%26t%3D6U3BTj3WLzRUilCx-1" allowfullscreen></iframe> 