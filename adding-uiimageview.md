# Adding UIImageView

## create a UIImageView 
```swift
// step 1: create a UIImage
let myImage = UIImage(named:"icebear")

// step 2: create a UIImageView
let myImageView = UIImageView(myImage)

// step 3: add UIImageView to UIView 
// your ViewController will have a property `view`
view.addSubview(myImageView)
```

## use autolayout
```swift
// step 1: set this manually
// when you use interface builder, this is set automatically
imageView.translatesAutoresizingMaskIntoConstraints = false

// step 2: add your contraints (remember to set active to true)
imageView.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
imageView.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true

// step 3: set your size (this is necessary for autolayout; remember to set active to true)
imageView.widthAnchor.constraint(equalToConstant: 120).isActive = true
imageView.heightAnchor.constraint(equalToConstant: 120).isActive = true
```

## refactoring layout constraint setting
```swift
// lets create a function that deals with the issue of setting
// translatesAutoresizingMaskIntoConstraints to false and setting constraints to "active"
func setLayoutConstraints(view: UIView, constraints: [NSLayoutConstraint]) {
    view.translatesAutoresizingMaskIntoConstraints = false
    constraints.forEach({constraint in constraint.isActive = true })
}

// now your views can set constraints like this
setLayoutConstraints(view: imageView, constraints: [
    imageView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
    imageView.centerYAnchor.constraint(equalTo: view.centerYAnchor),
    imageView.widthAnchor.constraint(equalToConstant: 120),
    imageView.heightAnchor.constraint(equalToConstant: 120),
])
```
