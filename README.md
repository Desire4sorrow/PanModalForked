
### PanModal is an elegant and highly customizable presentation API for constructing bottom sheet modals on iOS.

<p align="center">
    <img src="https://github.com/slackhq/PanModal/raw/master/Screenshots/panModal.gif" width="30%" height="30%" alt="Screenshot Preview" />
</p>

<p align="center">
    <img src="https://img.shields.io/badge/Platform-iOS_10+-green.svg" alt="Platform: iOS 10.0+" />
    <a href="https://developer.apple.com/swift" target="_blank"><img src="https://img.shields.io/badge/Language-Swift_5-blueviolet.svg" alt="Language: Swift 5" /></a>
    <a href="https://cocoapods.org/pods/PanModal" target="_blank"><img src="https://img.shields.io/badge/CocoaPods-v1.0-red.svg" alt="CocoaPods compatible" /></a>
    <a href="https://github.com/Carthage/Carthage" target="_blank"><img src="https://img.shields.io/badge/Carthage-compatible-blue.svg" alt="Carthage compatible" /></a>
    <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License: MIT" />
</p>

<p align="center">
    <a href="#features">Features</a>
  • <a href="#compatibility">Compatibility</a>
  • <a href="#installation">Installation</a>
  • <a href="#usage">Usage</a>
  • <a href="#documentation">Documentation</a>
  • <a href="#contributing">Contributing</a>
  • <a href="#authors">Authors</a>
  • <a href="#license">License</a>
</p>

<p align="center">
Read our <a href="https://slack.engineering/panmodal-better-support-for-thumb-accessibility-on-slack-mobile-52b2a7596031" target="_blank">blog</a> on how Slack is getting more :thumbsup: with PanModal

Swift 4.2 support can be found on the `Swift4.2` branch.
</p>

## Features

* Supports any type of `UIViewController`
* Seamless transition between modal and content
* Maintains 60 fps performance

## Compatibility

PanModal requires **iOS 10+** and is compatible with **Swift 4.2** projects.

## Installation

* <a href="https://guides.cocoapods.org/using/using-cocoapods.html" target="_blank">CocoaPods</a>:

```ruby
pod 'PanModal'
```

* <a href="https://github.com/Carthage/Carthage" target="_blank">Carthage</a>:

```ruby
github "slackhq/PanModal"
```

* <a href="https://swift.org/package-manager/" target="_blank">Swift Package Manager</a>:

```swift
dependencies: [
  .package(url: "https://github.com/slackhq/PanModal.git", .exact("1.2.6")),
],
```

## Usage

PanModal was designed to be used effortlessly. Simply call `presentPanModal` in the same way you would expect to present a `UIViewController`

```swift
.presentPanModal(yourViewController)
```

The presented view controller must conform to `PanModalPresentable` to take advantage of the customizable options

```swift
extension YourViewController: PanModalPresentable {

    var panScrollable: UIScrollView? {
        return nil
    }
}
```

### PanScrollable

If the presented view controller has an embedded `UIScrollView` e.g. as is the case with `UITableViewController`, panModal will seamlessly transition pan gestures between the modal and the scroll view

```swift
class TableViewController: UITableViewController, PanModalPresentable {

    var panScrollable: UIScrollView? {
        return tableView
    }
}
```

### Adjusting Heights

Height values of the panModal can be adjusted by overriding `shortFormHeight` or `longFormHeight`

```swift
var shortFormHeight: PanModalHeight {
    return .contentHeight(300)
}

var longFormHeight: PanModalHeight {
    return .maxHeightWithTopInset(40)
}
```

### Updates at Runtime

Values are stored during presentation, so when adjusting at runtime you should call `panModalSetNeedsLayoutUpdate()`

```swift
func viewDidLoad() {
    hasLoaded = true

    panModalSetNeedsLayoutUpdate()
    panModalTransition(to: .shortForm)
}

var shortFormHeight: PanModalHeight {
    if hasLoaded {
        return .contentHeight(200)
    }
    return .maxHeight
}
```
