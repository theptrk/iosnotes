# Contents
* [UINavigationController](UINavigationController)
* [UITableView](UITableView)
* [Xcode](Xcode)

# UINavigationController
## UINavigationController checklist
- [ ] add a self.title

## How to embed VC in NagivationController
- step 1: Go to storyboard.swift and click on VC
- step 2: Editor Menu -> Embed In -> Navigation Controller

## How to hide the navigation bar + status bar + home indicator on tap
- great when viewing images
```swift
override var prefersStatusBarHidden: Bool {
    return navigationController?.hidesBarsOnTap ?? false
}
override var prefersHomeIndicatorAutoHidden: Bool {
    return navigationController?.hidesBarsOnTap ?? false
}
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    navigationController?.hidesBarsOnTap = true
}
override func viewWillDisappear(_ animated: Bool) {
    super.viewWillDisappear(animated)
    navigationController?.hidesBarsOnTap = false
}
```

# UITableView
## How to enable large titles in table view
```swift
// step 1: only put this in the first screen on your app
navigationController?.navigationBar.prefersLargeTitles = true

// step 2: this requires this stupid property in your other screens though
navigationItem.largeTitleDisplayMode = .never
```


# Xcode
## How to import assets into assets catalog
- step 1: save files as `france.png`, `france@2x.png`, `france@3x.png`
- step 2: drag and drop into `Assets.xcassets`
