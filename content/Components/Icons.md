The icons that Faaviator uses are from an open-source and versatile icon pack called [Iconoir](https://Iconoir.com)
# Use
---
```swift
CustomIconView(.iconoir(.icon), size: size, color: .color)
CustomIconView(.system(.icon), size: size, color: .color)
```
Accepts both `.iconoir()` and the default `.system()` (apple icons)`

#### Use the `CustomIcon` in 
#### Use the `CustomIconView` alone
```swift title="Swift"
import SwiftUI  
import Iconoir

struct ContentView: View {  
    var body: some View {  
        VStack(spacing: 20) {
          
            // Using an SF Symbol
            CustomIconView(.system("star.fill"), size: 30, color:.textPrimary)            
            // Using an Iconoir icon  
            CustomIconView(.iconoir(.bell), size: 40, color: .red)            
            
            // Using another Iconoir icon with default size and color  
            CustomIconView(.iconoir(.addUser))            
            
            // You can also use it inline with other views  
            HStack {  
                Text("Notifications")  
                CustomIconView(.iconoir(.bell), size: 20, color: .green)  
            }  
        }  
    }  
}
```
# Install
---
## Adding to SwiftUI

First we need to install the Iconoir Swift Package to the project. 
![[Screenshot 2024-08-07 at 9.57.41 AM 1.png]]

#### Our custom enum and view
``` swift title="Swift"
import Foundation
import SwiftUI
import Iconoir

enum CustomIcon {
    case system(String)
    case iconoir(Iconoir)
}

struct CustomIconView: View {
    let icon: CustomIcon
    let size: CGFloat
    let color: Color
    
    init(_ icon: CustomIcon, size: CGFloat = 24, color: Color = .TextPrimary) {
        self.icon = icon
        self.size = size
        self.color = color
    }
    
    var body: some View {
        switch icon {
        case .system(let name):
            Image(systemName: name)
                .font(.system(size: size))
                .foregroundColor(color)
        case .iconoir(let iconoir):
            iconoir.asImage
                .font(.system(size: size))
                .foregroundColor(color)
        }
    }
}
```


# Design
---
Browse the catalog of icons at [Iconoir.com](https://iconoir.com)
View the Figma components below
#### Figma
<iframe style="border: 1px solid rgba(0, 0, 0, 0.1);" width="800" height="450" src="https://www.figma.com/embed?embed_host=share&url=https%3A%2F%2Fwww.figma.com%2Fdesign%2FYdYApHlAjaKaJwv7ogVBoy%2FFaaviator-Design-System-(v1)%3Fnode-id%3D2738-17578%26t%3D0VKIEGrXKtwZoEbE-1" allowfullscreen></iframe>