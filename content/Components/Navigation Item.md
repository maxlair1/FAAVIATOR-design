---
title: Navigation Item
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**One of the most used components. Drives core navigation throughout the application, and directs the user to complete tasks.**
- Avoid `subtitles`, but if you must use them, make sure all navigation items on the same screen also use subtitles.
- `Tags` must only be used on the Home screen.
# Use
---
## SwiftUI

use `NavigationItem()` to Initialize the component

```swift
NavigationItem(
	icon: "sf.symbol",
	title: "Navigation Title",
	action: {
		//action
	}
)
```
### Parameters

| Parameter  | Argument type      | Default | Description                                                                                                          |
| ---------- | ------------------ | ------- | -------------------------------------------------------------------------------------------------------------------- |
| `icon`     | String (SF Symbol) | `nil`   | The Icon representing the nav item                                                                                   |
| `title`    | String             | `nil`   | The title representing the nav item                                                                                  |
| `action`   | `() -> Void`       | `nil`   | What action occurs when the nav item is tapped                                                                       |
| `subtitle` | String             | `nil`   | Secondary line of text supporting the nav title                                                                      |
| `tag`      | String             | `nil`   | [[content/Components/Chips#StatusChip()\|Static Chip]] that is used to tag the nav item for organizational purposes. |
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
```swift title="NavigationItem.swift"
import SwiftUI

struct CircularIconItem: View {
    let icon: Image
    let size: CircularButtonStyle.ButtonSize
    
    var body: some View {
        VStack(spacing: 4) {
            icon
                .font(.system(size: 24, weight: .light))
                .frame(width: 48, height: 48)
                .background(Color.BackgroundSecondary)
                .foregroundColor(.TextPrimary)
                .clipShape(Circle())
        }
    }
}

struct NavigationItem: View {
    let icon: String
    let title: String
    let subtitle: String?
    let tag: String?
    private var action: () -> Void
    
    init(icon: String, title: String, subtitle: String? = nil, tag: String? = nil, action: @escaping () -> Void) {
        self.icon = icon
        self.title = title
        self.subtitle = subtitle
        self.tag = tag
        self.action = action
    }

    var body: some View {
        HStack(spacing: 12) {
            CircularIconItem(
                icon: Image(systemName: icon),
                size: .medium
            )
            
            VStack(alignment: .leading, spacing: 4) {
                Text(title)
                    .font(.interNavigationItemTitle)
                    .foregroundColor(.TextPrimary)

                if let subtitle = subtitle {
                    Text(subtitle)
                        .font(.interNavigationItemSubtitle)
                        .foregroundColor(.gray500)
                }
            }

            Spacer()
            
            HStack {
                if let tag = tag {
                    StaticChip(text: tag)
                }
                Image(systemName: "chevron.right").foregroundColor(.TextTertiary)
                
            }
            
            
        }
        .padding(.vertical, 12)
        .onTapGesture {
            action()
        }
    }
}
```

# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2923-712%26t%3D34OXPq7vX2IjlpRK-1" allowfullscreen></iframe>
