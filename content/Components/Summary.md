---
title: Summary
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---
**Essentially the navigation item but has navigation, just displays static information and conditionally links to tied info.**
# Use

---
## SwiftUI

use `Summary()` to Initialize the component

```swift
Summary(
		status: .complete, 
		icon: "battery.100percent", 
		title: "Drone fully charged", 
		subtitle: "Battery status", 
		actionLabel: "Click me", 
		action: { print("Action Clicked")}
		)
```

### Parameters

| Parameter     | Argument type   | Options                                               | Default                 | Description                                                                                         |
| ------------- | --------------- | ----------------------------------------------------- | ----------------------- | --------------------------------------------------------------------------------------------------- |
| `status`      | `SummaryStatus` | `.none`,<br>`.complete`,<br>`.warning`,<br>`.pending` | `.none`                 | This is the tiny indicator to the right of the summary icon.                                        |
| `icon`        | String          |                                                       | `nil`<br>REQ            | The Icon rendered to the left of the summary text. Represents the item.                             |
| `title`       | String          |                                                       | `nil`<br>REQ            | The main label of the Summary item.                                                                 |
| `subtitle`    | String          |                                                       | `nil`                   | Secondary label that is used to describe the title if it needs more context.                        |
| `actionLabel` | String          |                                                       | `"View More"`           | The label for the action button                                                                     |
| `action`      | `() -> Void`    |                                                       | REQ (recommended `nil`) | Action associated with the Summary. Will only appear below the text if there is a specified action. |

# Definition
---
```swift title="Summary.swift"

import Foundation
import SwiftUI

enum SummaryStatus {
    case warning
    case pending
    case complete
    case none
}

struct Summary: View {
    @State var status: SummaryStatus? = Optional.none
    @State var icon: String
    @State var title: String
    @State var subtitle: String?
    @State var actionLabel: String?
    let action: (() -> Void)?

    var body: some View {
        VStack {
            HStack(alignment: .top, spacing: 8) {
                SummaryIcon(
                    icon: Image(systemName: icon),
                    size: .medium,
                    status: status ?? .none
                ).offset(y: -14)
                
                VStack(alignment: .leading, spacing: 4) {
                    Text(title)
                        .font(.interNavigationItemTitle)
                        .foregroundColor(.TextPrimary)
                        .lineLimit(1)
                    
                    if let subtitle = subtitle {
                        Text(subtitle)
                            .font(.interNavigationItemSubtitle)
                            .foregroundColor(.gray500)
                            .lineLimit(1)
                    }
                    
                    if let action = action {
                        Button(action: action) {
                            Text(((actionLabel == nil) ? "See more" : actionLabel)!)
                                .font(.interCaption)
                                .foregroundColor(.TextPrimary).underline()
                        }
                    }
                }
            }
        }.frame(maxWidth: .infinity, alignment: .leading).padding(.vertical, 4)
    }
}


 
struct SummaryIcon: View {
    let icon: Image
    let size: CircularButtonStyle.ButtonSize
    @State var status: SummaryStatus = .none

    var body: some View {
        ZStack {
            icon
                .font(.system(size: 24, weight: .light))
                .frame(width: 48, height: 48)
                .background(.clear)
                .foregroundColor(.textPrimary)
                .padding(0)
                
            if status != .none {
                Image(systemName: statusIcon())
                    .font(.system(size: 12, weight: .bold))
                    .frame(width: 18, height: 18)
                    .background(statusBackgroundColor())
                    .foregroundColor(statusForegroundColor())
                    .clipShape(Circle())
                    .offset(x: 14, y: 12)
            }
        }
    }
    
    private func statusIcon() -> String {
        switch status {
        case .warning:
            return "exclamationmark"
        case .pending:
            return "arrow.trianglehead.clockwise"
        case .complete:
            return "checkmark"
        case .none:
            return ""
        }
    }

    private func statusBackgroundColor() -> Color {
        switch status {
        case .warning:
            return Color.orange400
        case .pending:
            return Color.BackgroundSecondary
        case .complete:
            return Color.green400
        case .none:
            return Color.clear
        }
    }
    private func statusForegroundColor() -> Color {
        switch status {
        case .warning:
            return Color.orange900
        case .pending:
            return Color.TextPrimary
        case .complete:
            return Color.green900
        case .none:
            return Color.clear
        }
    }
}

```

# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D3007-124%26t%3DmMKkrwG6FWkP70kD-1" allowfullscreen></iframe>