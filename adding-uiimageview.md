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

## use the solution to avoid rookie mistake #1
from [setup layout constraints](https://github.com/theptrk/iosnotes/blob/master/setup-layout-constraints.md)
```swift
setLayoutConstraints(view: imageView, constraints: [
    imageView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
    imageView.centerYAnchor.constraint(equalTo: view.centerYAnchor),
    imageView.widthAnchor.constraint(equalToConstant: 120),
    imageView.heightAnchor.constraint(equalToConstant: 120),
])
```
