```swift
//
//  Extensions.swift
//  Shapes
//
//  Created by Patrick Tran on 9/8/18.
//  Copyright © 2018 Patrick Tran. All rights reserved.
//

import UIKit

extension CAShapeLayer {
    // more info: https://www.youtube.com/watch?v=lYVazkkjOb8&index=6&list=PL0dzCUj1L5JFz8NarGPXtvEvaAqUOwaFU

    func pulseOut(duration: Double = 5, 
        forKey: String = "someKey-" + String(arc4random())) -> String{
        let pulsingAnimation: CABasicAnimation = {
            let animation = CABasicAnimation(keyPath: "transform.scale")
            animation.toValue = 7
            animation.duration = duration
            animation.timingFunction = CAMediaTimingFunction(name: kCAMediaTimingFunctionEaseOut)
            animation.repeatCount = Float.infinity
            return animation
        }()
        self.add(pulsingAnimation, forKey: forKey)
        return forKey
    }

    func fadeOut(duration: Double = 5, forKey: String = "someKey-" + String(arc4random())) -> String{
        let fadingOutAnimation: CABasicAnimation = {
            // https://medium.com/@joncardasis/better-ios-animations-with-catransaction-72a7425673a6
            let animation = CABasicAnimation(keyPath: #keyPath(CALayer.opacity))
            animation.fromValue = 0.5
            animation.toValue = 0.0
            animation.duration = duration
            animation.repeatCount = Float.infinity
            animation.timingFunction = CAMediaTimingFunction(name: kCAMediaTimingFunctionEaseOut)
            return animation
        }()
        self.opacity = 0.0
        self.add(fadingOutAnimation, forKey: forKey)
        return forKey
    }
}
```
