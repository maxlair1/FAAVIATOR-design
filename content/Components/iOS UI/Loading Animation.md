---
title: Loading Animation
draft: 
tags:
  - Component
---
> [!example] &nbsp;&nbsp;Version 1

> [!warning] This documentation is non-exaustive and a work-in-progress

![[loading_anim_cover.png]]
# Overview
---
**This component uses [Rive](htps://rive.app), and [Rive Runtime (iOS)](https://github.com/rive-app/rive-ios) to render a SVG animation called `faa_step.riv` (which can be found in the `Assets` folder). **

# Use
---
## SwiftUI

use `SwiftComponent(_:)` to Initialize the component

```swift
RiveViewModel(fileName: "faa_step", animationName: "Step", autoPlay: true).view()
// OR

LoadingAnimation()
```
### Parameters

Follow guide for the Runtime [here](https://designcode.io/swiftui-rive-animated-app)
Below is the Swift definition...
```swift title="RiveViewModel()"
init(
    fileName: String,
    extension: String = ".riv",
    in bundle: Bundle = .main,
    animationName: String? = nil,
    fit: RiveFit = .contain,
    alignment: RiveAlignment = .center,
    autoPlay: Bool = true,
    artboardName: String? = nil,
    preferredFramesPerSecond: Int? = nil,
    loadCdn: Bool = true,
    customLoader: LoadAsset? = nil
)
```
# Definition
---
```swift title="LoadingAnimation.swift"
//
// LoadingAnimation.swift
// Faaviator
//
// Created by Max Lair on 10/1/24.
//
import Foundation
import SwiftUI
import RiveRuntime
struct LoadingAnimation: View {
  var body: some View {
    RiveViewModel(fileName: "faa_step", animationName: "Step", autoPlay: true).view()
      .ignoresSafeArea()
      .background(
        Image("Spline")
          .blur(radius: 50)
          .offset(x: 200, y: 100)
      )
  }
}
#Preview {
  LoadingAnimation()
}
```
# Figma
---
 <iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="100%" height="450" src="https://embed.figma.com/design/elpsSOPKuD7xJxyF0PSw8P/Mobile-App?node-id=139-2382&embed-host=share" allowfullscreen></iframe> 
