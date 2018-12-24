# Say No To Storyboards
NIB or code are easier to keep track of with version control systems,
provide a clean interface (code) to track visual constraints
and make it easier to reuse views

Prerequisites:
- Delete Main Interface from Deployment Info Settings
- Delete the Main.storyboard file

# How to: set up a iOS project without storyboard

## Step 1: Create a UIWindow with the frame using the bounds of the UIScreen
`UIWindow(frame: UIScreen.main.bounds)`

## Step 2: Assign this to the AppDelegate window property
`window = ...`

## Step 3: Make the window "key" and "visible" 
`window?.makeKeyAndVisible`

## Step 4: Set the window `rootViewController` to the VC of your choice
`window?.rootViewController = ...`

```swift
window = UIWindow(frame: UIScreen.main.bounds)
window?.makeKeyAndVisible()
window?.rootViewController = HomeViewController();
```
