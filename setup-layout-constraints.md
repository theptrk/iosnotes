# rookie mistake #1
forgetting to set translatesAutoresizingMaskIntoConstraints to false

## solution 1
Create function that bundles setting translatesAutoresizingMaskIntoConstraints to false
AND setting constraints to active 
```swift
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

## solution 2
Create a UIView extension achiving the same functionality
```swift
extension UIView {
    func setLayoutConstraints(view: UIView, constraints: [NSLayoutConstraint]) {
        view.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate(constraints)
    }
}
yourView.setLayoutConstraints(view: yourView, constraints: [
    // ...
])
```

## solution 2 alternative (best)
Pass in the context of the view into an extension function callback
```swift
extension UIView {

    // notice that the callback should return an array of ns layout constraints
    func applyLayoutConstraints(_ constraints: (UIView) -> [NSLayoutConstraint]) {
        self.translatesAutoresizingMaskIntoConstraints = false
        
        // here the callback will be passed `self`
        NSLayoutConstraint.activate(constraints(self))
    }
}

// now you can pass a closure that operates on `self`
myView.applyLayoutConstraints({ target_view in [
    target_view.bottomAnchor.constraint(equalTo: view.bottomAnchor),
    target_view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
    target_view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
    target_view.heightAnchor.constraint(equalTo: view.heightAnchor, multiplier: 0.5)
]})
```
Q: Why is this the best solution?
A: Reusable constraints! You can know abstract out constraints and pass it in as the callback
```swift
func constraint_bottomMiddle(_ target_view: UIView) -> [NSLayoutConstraint] {
    return [
        target_view.bottomAnchor.constraint(equalTo: view.bottomAnchor),
        target_view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
        target_view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
        target_view.heightAnchor.constraint(equalTo: view.heightAnchor, multiplier: 0.5)
    ]
}
myView.setLayoutConstraints(constraint_bottomMiddle)
```
Q: But what about the use of `view`, isnt that context specific? Can we fix this without chaning the API of our extension function?
A: Yes! you can instead create a function that deals with context before returning the callback
```swift
// this function will take the parent view as a parameter and pass a callback that will recieve the target view and set the appropirate constraints
func constraintToBottomMiddleOf(_ parent: UIView) -> (UIView) -> [NSLayoutConstraint] {
    return {(_ target_view) in
         [
            target_view.bottomAnchor.constraint(equalTo: parent.bottomAnchor),
            target_view.leadingAnchor.constraint(equalTo: parent.leadingAnchor),
            target_view.trailingAnchor.constraint(equalTo: parent.trailingAnchor),
            target_view.heightAnchor.constraint(equalTo: parent.heightAnchor, multiplier: 0.5)
        ]
    }
}

// this is how you would use it
myView.setLayoutConstraints(constraintToBottomMiddleOf(self.view))
```
