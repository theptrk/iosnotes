# uiview - divide your screen
Say you want to split your screen in half vertically 
AND have it justify correctly on orientation change
```
Portrait mode
     _______________
    |               |
    |  top half     |
    |    w/image    |
    |               |
     _______________
    |               |
    |  bottom half  |
    |    w/image    |
    |               |
     _______________

Landscape mode
     _________________________
    |       top half          |
    |         w/image         |
     _________________________
    |       bottom half       |
    |         w/image         |
     _________________________

```

![Ice Bear Portrait](/assets/ice-bear-portrait.png)
![Ice Bear Landscape](/assets/ice-bear-landscape.png)

## strategy - use two UIViews

```swift
// step 1: create your "top half" view
let topHalfView = UIView()
view.addSubview(topHalfView)

// step 2: add your top half constraints
setLayoutConstraints(view: topHalfView, constraints: [
    topHalfView.topAnchor.constraint(equalTo: view.topAnchor),
    topHalfView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
    topHalfView.trailingAnchor.constraint(equalTo: view.trailingAnchor),
    topHalfView.heightAnchor.constraint(equalTo: view.heightAnchor, multiplier: 0.5),
])

// step 3: add your image view to this top half
topHalfView.addSubview(iceBearImageView)
setLayoutConstraints(view: iceBearImageView, constraints: [
    iceBearImageView.centerXAnchor.constraint(equalTo: topHalfView.centerXAnchor),
    iceBearImageView.centerYAnchor.constraint(equalTo: topHalfView.centerYAnchor),
    iceBearImageView.heightAnchor.constraint(equalTo: topHalfView.heightAnchor, multiplier: 0.5),
])
```
