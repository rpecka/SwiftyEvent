# SwiftyEvent

## Overview
Add an overview here

## Build

To build SwiftyEvent from the command line:

```bash
% cd <path-to-clone>
% swift build
```

## Testing

To run the supplied unit tests for **SwiftyEvent** from the command line:

```bash
% cd <path-to-clone>
% swift build
% swift test

```

## Using SwiftyEvent

### Including in your project

#### Swift Package Manager

To include SwiftyEvent into a Swift Package Manager package, add it to the `dependencies` attribute defined in your `Package.swift` file. You can select the version using the `majorVersion` and `minor` parameters. For example:
```
	dependencies: [
		.package(url: "https://github.com/Streebor/SwiftyEvent.git", .upToNextMajor(from: "1.0.0")),
	]
```

### Example

```Swift
	
	class ObservableClass {
		var propertyChangedEvent = Event<String>()
	
		var property: String = "" {
			didSet {
				propertyChangedEvent(sender: self, arguments: self.property)
			}
		}
	}
	
	class SubscriberClass {
		private let observableClass: ObservableClass
		private var handle: Event<String>.Handle? = nil
		private var newObservableValue: String? = nil
	
		init(_ newObservableClass: ObservableClass) {
			self.observableClass = newObservableClass
			self.handle = self.observableClass.propertyChangedEvent.subscribe() { [weak self] sender, arg in
				self?.newObservableValue = arg // This is where you should add your code to react to the Event
			}
		}
	}
	
	let observableClass = ObservableClass()
	let subscriberClass = SubscriberClass(observableClass)
	
```
