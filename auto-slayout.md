# auto slayout

slay auto layout

## extends UIView transparently

### `func setSlayout` and how to use it
setSlayout takes `[NSLayoutConstraint]`, sets that easily forgetable setting to false and activates your constraints

```swift
extension UIView {
    func setSlayout(_ constraints: [NSLayoutConstraint]) {
        self.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate(constraints)
    }
}
```

### `applySlayout`

`applySlayout` takes a callback and invokes it with the context of the UIView
This opens up the possibility of creating reusable auto layout constraints that accept a reference to a target view.

```swift
extension UIView {
    // the passed in `UIView` can 
    func applySlayout(_ constraintCreator: (UIView) -> [NSLayoutConstraint]) {
        self.setSlayout(constraintCreator(self)
    }
}
```

### using `applySlayout`

how to center on X and Y: (version 1: closure)
```swift
func anotherFunction() {
    myView.applySlayout({ targetView in 
        return [
            targetView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            targetView.centerYAnchor.constraint(equalTo: view.centerYAnchor)
        ]
    })
}
```

how to center on X and Y: (version 2: abstracting the closure into a function)
```swift
func centerXYOfView(_ targetView: UIView) -> [NSLayoutConstraint] {
    return [
        // Notice, it very much depends *where* we define this function 
        // since `view` will vary depending on context
        targetView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
        targetView.centerYAnchor.constraint(equalTo: view.centerYAnchor)
    ]
}
func anotherFunction() {
    myView.applySlayout(centerXYOfView)
}
```

how to center on X and Y: (version 2: abstracting the function to accept a relative view)

we can further abstract out the logic so our functions can take a `view` and the underlying logic will position itself relative to that `view`

```swift
func centerXYOf(_ relativeView: UIView) -> (UIView) -> [NSLayoutConstraint] {
    return {(_ targetView) in
        [
            targetView.centerXAnchor.constraint(equalTo: relativeView.centerXAnchor),
            targetView.centerYAnchor.constraint(equalTo: relativeView.centerYAnchor),
        ]
    }
}
func anotherFunction() {
    myView.applySlayout(centerXYOf(self.view))
}
```
