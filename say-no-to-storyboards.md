# Say No To Storyboards
NIB or code are easier to keep track of with version control systems,
provide a clean interface (code) to track visual constraints
and make it easier to reuse views

## Step 1: Delete `Main Interface` from Deployment Info Settings
## Step 2: Delete `Main.storyboard`
## Step 3: Set a new window in `AppDelegate.swift`

```swift
window = UIWindow(frame: UIScreen.main.bounds)
window?.makeKeyAndVisible()
window?.rootViewController = HomeViewController();
```
