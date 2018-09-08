# rookie mistake #1
forgetting to set translatesAutoresizingMaskIntoConstraints to false

## solution
```swift
// lets create a function that deals with the issue of setting
// translatesAutoresizingMaskIntoConstraints to false and setting constraints to "active"
func setLayoutConstraints(view: UIView, constraints: [NSLayoutConstraint]) {
    view.translatesAutoresizingMaskIntoConstraints = false
    NSLayoutConstraint.activate(constraints)
}

// now your views can set constraints like this
setLayoutConstraints(view: imageView, constraints: [
    imageView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
    imageView.centerYAnchor.constraint(equalTo: view.centerYAnchor),
    imageView.widthAnchor.constraint(equalToConstant: 120),
    imageView.heightAnchor.constraint(equalToConstant: 120),
])
```
