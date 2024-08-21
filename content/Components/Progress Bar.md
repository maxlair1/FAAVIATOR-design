---
title: Progress Bar
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

# Overview
---

**Static step indicator that shares with the user the progress they are making on a current task.**
- This is not a [[content/Components/Loading Bar|Loading Bar]]. You will want to use a Loading Bar when providing visual feedback to the user that an external task or process is working.
- This component should not be used in a static page, instead a collection of screens when you break up inputs.
# Use

---
## SwiftUI

use `ProgressBarView()` to Initialize the component

```swift
ProgressBarView(totalSteps: 5, currentSteps: 2)
```
- The two parameters, total and current steps, accept dynamic [CGFloats](https://developer.apple.com/documentation/corefoundation/cgfloat).
- The internal colored bar, represented by `currentSteps`, animates if new a new value is found.
> [!warning] If `currentSteps` exceeds `totalSteps` then the colored bar will maintain 100% until the value is less than `totalSteps`

### Parameters

| Parameter      | Argument type | Default | Description                                   |
| -------------- | ------------- | ------- | --------------------------------------------- |
| `totalSteps`   | `CGFloat`     | `nil`   | The total steps                               |
| `currentSteps` | `CGFloat`     | `nil`   | The amount of steps filled in <= `totalSteps` |
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
```swift title="ProgressBar.swift"
//
//  LoadingBar.swift
//  Faaviator
//
//  Created by Max Lair on 8/21/24.
//

import Foundation
import SwiftUI

struct ProgressBarView: View {
    let totalSteps: CGFloat
    let currentSteps: CGFloat
    
    init(totalSteps: CGFloat, currentSteps: CGFloat) {
        self.totalSteps = totalSteps
        self.currentSteps = currentSteps
    }
    
  var body: some View {
    var percentFilled = currentSteps / totalSteps
      
    GeometryReader { geometry in
      ZStack(alignment: .leading) {
        Rectangle()
              .frame(width: .infinity, height: 8)
          .opacity(0.3)
          .foregroundColor(.gray)
          .cornerRadius(25)

        Rectangle()
          .frame(
            width: min(percentFilled * geometry.size.width,
                       geometry.size.width),
            height: 8
          )
          .cornerRadius(25)
          .foregroundColor(.blue)
          .animation(.easeInOut(duration: 0.4), value: percentFilled)
      }
    }
  }
}

struct ProgressBar: View {
    @State var totalSteps: CGFloat = 2
    @State var currentSteps: CGFloat = 5

  var body: some View {
    VStack {
      ProgressBarView(totalSteps: totalSteps, currentSteps: currentSteps)
        .frame(height: 8)
        .padding()
        HStack {
            Text("\(Int(currentSteps)) steps of \(Int(totalSteps)) total steps.")
            Spacer()
            Text("Percent Filled: \(Int(currentSteps / totalSteps * 100))%")
        }.padding(.horizontal)
        
      Button(action: {
        currentSteps += 1
      }) {
          
        Text("Increase Progress")
      }
        Button(action: {
          totalSteps += 1
        }) {
          Text("Add steps")
        }
    }
  }
}


struct ProgressBarView_Previews: PreviewProvider {
    static var previews: some View {
        ProgressBar()
    }
}

```
