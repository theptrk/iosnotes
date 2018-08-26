# autolayout code
```swift
// avoid rookie mistake 1:
view.translatesAutoresizingMaskIntoConstraints = false

// avoid rookie mistake 2:
// set your constraints "isActive" property to true
yourView.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: 100).isActive = true,

// avoid rookie mistake 3:
// remember to set both X and Y constraints
.width, .height, {leading,trailing, centerX}, {top, bottom, centerY}
```

## anchoring horizontally
```swift
// centered on X (horizontally)
yourView.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true

// anchor to left+
// some languages read from right to left so apple recommends using
// trailingAnchor instead of leftAnchor
yourView.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: 100).isActive = true,

// anchor to right+ (notice the negative value)
// some languages read from right to left so apple recommends using
// trailingAnchor instead of rightAnchor
yourView.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: -100).isActive = true,
```

## anchoring vertically
```swift
// centered on Y (vertically)
yourView.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true

// anchor to top+
yourView.topAnchor.constraint(equalTo: view.topAnchor, constant: 100).isActive = true

// anchor to bottom+
yourView.topAnchor.constraint(equalTo: view.topAnchor, constant: 100).isActive = true
```

## solution to rookie mistakes
```swift
func setLayoutConstraints(view: UIView, constraints: [NSLayoutConstraint]) {
    view.translatesAutoresizingMaskIntoConstraints = false
    constraints.forEach({constraint in constraint.isActive = true })
}

```

[blog](https://theptrk.com/2018/08/26/forgetting-to-set-translatesautoresizingmaskintoconstraints-to-false/)
