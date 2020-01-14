# Swift Style Guide
This document is a guide for writing Swift with a consistent style. The primary goal of this document is to provide a foundation for writing clear, consistent, documented code that follows recommendations established by Apple and others.

This document supplements the [Swift.org](https://swift.org/) API design guidelines. Conflicts between this document and those guidelines should be discussed with other developers and resolved.

For guidance on general design principals, see instead `GUIDELINES.md.`

## Table of Contents
- [Philosophy](#philosophy)
- [Spacing](#spacing)
    - [Line breaks](#line-breaks)
    - [Blank lines](#blank-lines)
- [Naming](#naming)
- [Syntax](#syntax)
    - [Braces](#braces)
    - [Semicolons](#semicolons)
- [Constants and Variables](#constants-and-variables)
- [Closures](#closures)
- [Classes and Structs](#classes-and-structs)
    - [Organization](#organization)
    - [Protocol Conformance](#protocol-conformance)
    - [Use of self](#use-of-self)
- [Documentation](#documentation)
- [Example](#example)

### Philosophy
-----
- Refer to the [Language Guide](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/) where this guide is silent.
- Use common sense.
- When you can't have both, prefer readability over conciseness.
- Be consistent.
- Follow conventions established in the file(s) you're working on.

### Spacing
-----
- Vertical whitespace is good.
- Use four spaces for indentation, not tabs.
- Use a space between binary operators and their operands.
- Omit spaces inside parentheses.
- Use a space after a comma, colon or semicolon.
- Omit spaces inside brackets.
- Use a space to separate braces from the body of a closure on the same line.
- Use a space around -> in a closure or method declaration.

##### Bad:
```
func sayHello(personName:String)->String {
    let greeting="Hello, "+personName+"!"
    return greeting
}
```

##### Good:
```
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName + "!"
    return greeting
}
```

- Indent `case` and `default` as deep as `switch`.
```
switch sum {
case 1:
    println("One")
case 2:
    println("Two")
default:
    println("A lot")
}
```

- Align the elements of array or dictionary literals spanning multiple lines.
```
let numbers = [
    "one": 1,
    "two": 2,
    "three": 3,
]
```

#### Line breaks
- Lines are limited to 100 characters except in unusual circumstances. Unusual circumstances are intentionally vague, so use common sense, and be consistent.
- Split long method calls into separate lines by placing named parameters on a new line and indenting by one level.
```
let p = Person(
    name: "John",
    age: 31,
    occupation: "Software Developer",
    phone: "555-1515"
)
```

- Keep the first unnamed parameter on the same line as the method call.
- Keep the opening brace on the same line as a named closure parameter.
```
UIView.animateWithDuration(1.0,
    delay: 0.5,
    options: .AllowAnimatedContent,
    animations: {

    },
    completion: { completed in

    })
```

#### Blank lines
- Include one blank line between each module-level type or function.
- Include one blank line between each property and method within a type.
- Do not put blank lines at the beginning or end of a scope (closure, class and function definitions)

##### Bad:

```
class Person {

    let name: String
    init(name: String) {

        self.name = name

    }

}
```

##### Good:

```
class Person {
    let name: String

    init(name: String) {  
        self.name = name
    }
}
```

### Naming
------
- Use upper camel case to name types (classes, structures, and enumerations).
- Use lower camel case to name constants, variables, and properties.
- Prefer long descriptive names over terse abbreviations.
- Argument labels should follow the guidelines in the [Swift.org API design guidelines](https://swift.org/documentation/api-design-guidelines/#parameter-names)
- Do not use non-ascii characters in code. Non-ascii characters should be avoided in comments.
```
// Fun, but harder to type
let  = true
```

##### Bad:

```
enum coffeeFlavor {
  case Dark
  case Light_And_Smooth
}
```

##### Good:

```
enum CoffeeFlavor {
  case dark
  case light
}
```

### Syntax
-----
#### Braces
- Braces open on the same line as a statement and close on a new line.

##### Bad:

```
if coffees.isEmpty
{
    // Nothing
}
else { // Something }
```

##### Good:

```
if coffees.isEmpty {
    // Nothing
} else {
    // Something
}
```

#### Semicolons
- Omit semicolons at the end of statements.
- Avoid writing multiple statements on a single line.

### Constants and Variables
------
- Declare constants and variables on their own lines.
- Omit type annotations when the type can be inferred.
- Prefer `let` constants over `var` variables unless mutability is absolutely necessary.

##### Bad:

```
var x: Double = 0.0, y: Double = 0.0, z: Double = 0.0
```

##### Good:

```
let x = 0.0
let y = 0.0
let z = 0.0
```

### Closures
-----
- Prefer trailing closure syntax when there is a final, lone closure parameter.
- Omit parameter type when it can be inferred.
- Omit return type when it can be inferred.
- Omit parentheses around parameter and return types.
- Declare closures with no return type as `-> Void` instead of `-> ()`

##### Bad:

```
UIView.animateWithDuration(1.0, animations: { () -> Void in
    self.view.alpha = 0.0
})
```

##### Good:

```
UIView.animateWithDuration(1.0) {
    self.view.alpha = 0.0
}
```

### Optionals
------
- Try to avoid optional types unless `nil` is an acceptable value for that type. Describe what `nil` means in comments.
- Try to avoid implicitly unwrapped optionals whenever possible. Notable exceptions include IBOutlets.
- Try to avoid force unwrapping optionals with `!`. Prefer `if let`, `map`, `flatMap`, `?`, or `??` to safely unwrap optionals.

### Classes and structs
------
- When choosing between classes and structs, follow these [guidelines](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-ID92).
- Mark classes final unless subclassing is necessary.

#### Organization
- Sort imports alphabetically.
- Sort sections inside the implementation in the following order:
    1. Type properties
    2. IBOutlets
    3. Instance properties
    4. Private properties
    5. Type methods
    6. Initializers (`init` methods)
    7. Instance methods
    8. Private methods
    9. Nested types
- Use `// MARK:` comments to separate each section within a type.
- Use `// MARK: -` to separate each type, or extension of a type, within a file.
- Overridden methods should go at the start of the corresponding section. For example, `override func viewDidLoad() { /** ... */ }` should go in between the initializers and the instance methods in a class.

#### Protocol Conformance
- Separate each protocol conformance into its own extension in alphabetical order after the main type declaration.

#### Use of self
- Omit self, except when required in closures or when an initializer parameter matches the name of a property.

### Documentation
------
- Provide documentation for classes, structs, properties, functions and methods. Items should have documentation if their purpose and use are not obvious. Most items are not obvious in purpose, and so require documentation.
- Use `- parameter <parameter name>:` and `- returns:` to describe method usage.
- Use inline comments to explain the reasons why the code does what it does. What the code does should also be made clear through organization and naming.

### Example
------
The following file demonstrates the guidelines put forth in this document.

```
import UIKit

// MARK: - Device

/// Represents a device displayed in the device list.
final class Device {
    /// The unique identifier for this device.
    let identifier: String

    /// The user-visible name of this device.
    let name: String

    /**
     Initializes and returns a new device with the given identifier and name.

     - parameter identifier: A unique identifier for the device.
     - parameter name:       A user-visible name for the device.
     */
    init(identifier: String, name: String) {
        self.identifier = identifier
        self.name = name
    }
}

// MARK: - DeviceListDelegate

/// Defines the methods that the delegate of a `DeviceListViewController` can adopt to manage the
/// device list when a user adds or deletes one.
protocol DeviceListDelegate: class {
    /**
     Invoked when the specified device is added to the list.

     - parameter deviceListViewController: The `DeviceListViewController` that sent the message.
     - parameter device:                   The device that was added to the list.
     */
    func deviceListViewController(deviceListViewController: DeviceListViewController,
        didAddDevice device: Device)

    /**
     Invoked when the specified device is deleted from the list.

     - parameter deviceListViewController: The `DeviceListViewController` that sent the message.
     - parameter device:                   The device that was deleted from the list.
     */
    func deviceListViewController(deviceListViewController: DeviceListViewController,
        didDeleteDevice device: Device)
}

// MARK: - DeviceListViewController

/// This view controller lists a series of mobile devices with an icon for each device. Devices are
/// only visible in the list if their loaned property is set to `false`.
final class DeviceListViewController: UIViewController {
    // MARK: Static Properties

    private static let reuseID = "DeviceCell"

    // MARK: Properties

    /// The object that acts a the delegate of the receiving DeviceListViewController. See docs for
    /// the `DeviceListDelegate` protocol.
    weak var delegate: DeviceListDelegate?

    /// Returns the list of devices that was used to create an instance of this controller.
    private(set) var devices: [Device] = []

    // MARK: Outlets

    @IBOutlet private var tableView: UITableView!

    // MARK: Init and deinit methods

    /**
    Initializes a new instance of the class with a list of devices to display.

    - parameter devices: The devices to display in the list.
    */
    convenience init(devices: [Device]) {
        self.init(nibName: "DeviceListViewController", bundle: nil)

        self.devices = devices
    }

    deinit {
        // Do any necessary cleanup here. This class doesn't require anything, but this method is
        // left here to indicate where it should be placed in the implementation if cleanup was
        // required.
    }

    // MARK:  Private methods

    // Private methods should be implemented here.

    // MARK: Instance methods

    // If this class exposes any instance methods, they should be implemented here.
}

// MARK: - UIViewController

extension DeviceListViewController {
    override func viewWillAppear(animated: Bool) {
        super.viewWillAppear(animated)

        if let selectedIndexPath = tableView.indexPathForSelectedRow {
            tableView.deselectRowAtIndexPath(selectedIndexPath, animated: true)
        }
    }
}

// MARK: - UITableViewDataSource

extension DeviceListViewController: UITableViewDataSource {
    func numberOfSectionsInTableView(tableView: UITableView) -> Int {
        return 1
    }

    func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return devices.count
    }

    func tableView(tableView: UITableView,
        cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
            return tableView.dequeueReusableCellWithIdentifier(reuseIdentifier, forIndexPath: indexPath)
    }
}

// MARK: - UITableViewDelegate

extension DeviceListViewController: UITableViewDelegate {
    func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath) {
        // Do something when the user selects a row in the table.
    }
}
```
