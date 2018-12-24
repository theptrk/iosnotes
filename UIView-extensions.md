# extensions (that should be default)

## UIView

### set layout constraints

autolayout is the best way to layout your views so you need to turn off 
autoresizing mask, BUT this is easily forgotten and xcode does not remind you
this extension function will make sure you never encounter that bug

```swift
extension UIView {
    func setLayoutConstraints(_ constraints: [NSLayoutConstraint]) {
        self.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate(constraints)
    }
}
```
