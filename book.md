### UINavigationController checklist
- [ ] add a self.title

### Polish

#### large titles in table view
```swift
// only put this in the first screen on your app
navigationController?.navigationBar.prefersLargeTitles = true

// this requires this stupid property in your other screens though
navigationItem.largeTitleDisplayMode = .never
```


#### hide the navigation bar + status bar + home indicator on tap
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
