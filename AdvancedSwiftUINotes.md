# Advanced SwiftUI Notes

- [Coordinate Space](#coordinate-space)
- [Geometry Reader](#geometry-reader)
- [Preferences](#preferences)
  * [Generally Needed Constructs](#generally-needed-constructs)
  * [All Preference Methods](#all-preference-methods)
- [Environment](#environment)
  * [Built In Values](#built-in-values)
  * [Custom Objects](#custom-objects)
  * [Need To Research Further](#need-to-research-further)
- [View Builder](#view-builder)

## Coordinate Space


**Local**
Coordinate space relative to the container. <br>
**Global**
The absolute coordinate space of the screen. <br>
**Named**
Named coordinate spaces are those that the user names specifically by calling the `.coordinateSpace(name: "ExampleName")` modifier on a view whose space will be accessed later. One way to access this is from a `GeometryProxy`. <br>
**Example**
``` Swift
struct ExampleNamedSpaceView: View {
  var body: some View {
    VStack {
      Text("Some text with a named coordinateSpace")
      .coordinateSpace(name: "MyNamedSpace")

      GeometryReader { (proxy: GeometryProxy) in
        Rectangle().frame(width: proxy.frame(in: .named("MyNamedSpace")).width)
      }
    }
  }
}
```



## Geometry Reader

Use `GeometryReader` when a child views behavior or size should depend on the geometric data of the parent view.

* `GeometryReader` - A container view that provides size and location data of a parent view for use by a child view. Returns a flexible preferred size to its parent layout
* `GeometryProxy` - Acts as an intermediate to provide access to the geometric data of the container view.

**Example Use**
This example creates a circle view that is 1/3 and 1/4 of the parents width and height respectively.

``` Swift
struct ExampleChildView: View {
  var body: some View {
    GeometryReader { (proxy: GeometryProxy) in
      Circle()
      .frame(width: proxy.size.width/3, height: proxy.size.height/4)
    }
  }
}
```

**Snippet Form**
``` Swift
GeometryReader { (proxy: GeometryProxy) in
  <# View #>
}
```


## Preferences

**Important Notes**
* Order of executed closures called in the View Tree:
    1. Childrens closures are called before Parents.
    2. Siblings closures are called in the order they appear in the code.


Generally two types of preferences are used
  * *Preference*
    * For children views use `.preference`
    * For parent views use `.transformPreference`


  * *Anchor*

    * For children views use `.anchorPreference`.
    * For parent views and adding additional preferences use `transformAnchorPreference`.

    <br>

    When using the Anchor<T> value as an index to the geometry proxy,
                  you get the represented CGRect or CGPoint value. And as a plus, you get it
                  already translated to the coordinate space of the GeometryReader view.

### Generally Needed Constructs

* Preference Data Object
``` Swift
    struct ExamplePreferenceData {
        let someValue: Int

    }    
```
* Preference Key Object
``` Swift
struct ExamplePreferenceKey: PreferenceKey {
    typealias Value = [ExamplePreferenceData]

    static var defaultValue: [ExamplePreferenceData] = []

    static func reduce(value: inout [ExamplePreferenceData], nextValue: () -> [ExamplePreferenceData]) {
        value.append(contentsOf: nextValue())
    }
}
```
* A View to use the preference.


**Snippet Form**
``` Swift
struct <# Data Object Name #>: {
    let <# Data Name #>: <# Data Type #>
}

struct <# Key Name #>: PreferenceKey {
  typealias Value = <# Value Type #>

  static var defaultValue: <# Value Type #> = <# Default Value #>

  static func reduce(value: inout <# Value Type #>, nextValue: () -> <# Value Type #>) {
      <# Implementation #>
  }
}
```

### All Preference Methods

**Setting View Preferences**

* `.preference` - Sets a value to return for the given preference key when accessed by ancestors.
* `.transformPreference` - Sets a callback to return a value for the given preference key when accessed by ancestors.
* `.anchorPreference` - same as `preference` but uses an Anchor that automatically translates to the coordinate space of the geometry reader view
* `.transformAnchorPreference` - same as  `transformPreference` but uses an Anchor that automatically translates to the coordinate space of the geometry reader view

**Responding to View Preferences**

* `.onPreferenceChange` - Adds an action to perform when the specified preference key’s value changes.
* `.backgroundPreferenceValue`- Uses the specified preference value from the view to produce another view as a background to the first view.
* `.overlayPreferenceValue` - Uses the specified preference value from the view to produce another view as an overlay atop the first view.


## Environment

### Built In Values

**@Environment Property**
Use the `@Environment` Property wrapper to create variables that receive their value from a given environment value.

**.environment**

The values given to a view using the `.environment` modifier are passed down to all child views of that view. To override the inherited values use the `.environment` modifier directly on the child view that needs a different value.

[List Of Available Values](https://developer.apple.com/documentation/swiftui/environmentvalues)

**Example**
``` Swift
struct ExampleParentView: View {
  @Environment(\.colorScheme) var scheme
  var body: some View {
    VStack {
      Text("This text follows the color scheme")
      Text("This text is always in light mode")
      .environment(\.colorScheme, .light)
    }
  }
}
```

**Adding Custom Environment Keys and Values**

1. Create a type that conforms to the `EnvironmentKey` protocol, which only has one static variable requirement `defaultValue` and an associated type `Value`.
2. Make an extension to `EnvironmentValues` with a computed variable that makes use of the new environment key

``` Swift
// 1) Make The key
struct MyEnvironmentKey: EnvironmentKey {
  static var defaultValue: String = "Some default thing"
}

// 2) Add value to EnvironmentValues
extension EnvironmentValues {
  var myValue: String {
    get {
      return self[MyEnvironmentKey.self]
    }
    set {
      self[MyEnvironmentKey.self] = newValue
    }
  }
}

// Then access like this
struct ExampleView: View {
  @Environment(\.myValue) var value: String

  var body: some View {
    Text(value)
  }
}
```


**Snippet Form**
``` Swift

struct <# KeyName #>: EnvironmentKey {
  static var defaultValue: <# Value Type #> = <# Default Value #>
}


extension EnvironmentValues {
  var <# Value Name #>: <# Value Type #> {
    get {
      return self[<# KeyName #>.self]
    }
    set {
      self[<# KeyName #>.self] = newValue
    }
  }
}
```

### Custom Objects

**@EnvironmentObject**
Used to provide observable objects needed by specific views from the parents Environment.


**.environmentObject**
Use this to pass specific observable objects from a parents environment to the child's. This method should be used in place of a `init` that provides the object because swiftUI is designed to store and handle these objects optimally.


**Example**
``` Swift
struct ExampleParentView: View {
  @EnvironmentObject var exampleObject: ExampleObject

  var body: some View {
    ExampleChildView()
    .environmentObject(ChildsObject(value: exampleObject.value))
  }
}
```


### Need To Research Further

`.transformEnvironment` modifier


## View Builder

ViewBuilder is a function builder that makes SwiftUI DSL possible. Function builders in general give a developer the ability to design a particular syntax for programming particular things. In the case of swiftUI it makes the View Hierarchy more easily readable and allows for nice things like `ViewModifiers`.

The importance of ViewBuilder becomes apparent when making layout containers(VStack, HStack, etc) or for data generated views (List, ForEach ... ).

**Important**

If creating a custom view that generates sub-views from Data use the initializer.
```
init(@ViewBuilder content: @escaping () -> Content) {
        self.content = content
    }


```
