#  Function Builder Guide 

## Intro 

Function Builders are a new feature in swift 5.2 that allow the declaritive syntax of combine and SwiftUI
to exist. Common design problems or minor annoyances when writing reduntant pieces of code can be mitigated with the use of function builders. Frequently used components of like type are ideal candidates for a builder method. This is why Views in swiftUI are designed to be composed and nested. 
Normally you would need to have tons of code everywhere that each has its own unique quirks that need to be accounted for when modified. With function builders and a little foresight, these issues can become solutions. 

The goal when using a functionBuilder is to make a tedious and repetitive task easier and safeguard against common errors. In the case of DSL creations like the HTMLBuilder, the typesafety of the Swift language now overseeing HTML aswell. 


## Use Cases 

### When Related Types Can Be Composed
If a group of objects commonly get composed into a larger, flattened, or mixed group of objects. 
A simple example would be how HTML is nested by using container nodes that hold other HTML Nodes. 


## Getting Started 

Using the new `@functionBuilder` attribute and implementing the required `buildBlock`  method any struct or class can become a function builder. 

### Trivial Example

````Swift
// 1
protocol MyType { }
// 2
struct Single: MyType {  }

// 3,4
@_functionBuilder
struct MyBuilder {
    // 5
    static func buildBlock(_ component: MyType) -> MyType {
            return component
    }

}
//6
struct Example {
    init(@MyBuilder input: () -> MyType) {
        print(input())
    }
}
//7
let test = Example {
    Single()
}


````

Here I 

1. Made a base type of `MyType` with a protocol
2. Declared a struct `Single` that conforms to  `MyType`
3. Created an empty `MyBuild` struct 
4. Added the `@_functionBuilder` attribute above the declaration ( since this is not a release feature you must use `@_functionBuilder` instead of the finalized `@functionBuilder`)
5. Implemented the required `buildBlock` method. 
6. Made an `Example` object uses the `@MyBuilder` Attribute in its init parameter. 
7.  Ran a test to see if the implementation works

If you copy and paste this code into a playground running Xcode 11 Beta 6 the console should print "Single()"

**Composable Example**

One of the common implementations of the function builder is to take in many and return one fully composed result. At its simplest this is basically nesting all of the components into an array that is held by a 
member of the same type. 

```Swift
protocol MyType { }

struct Single: MyType {  }

//1
struct Multi: MyType {
    var children: [MyType]
}


@_functionBuilder
struct MyBuilder {

    static func buildBlock(_ component: MyType) -> MyType {
            return component
    }
    // 2
    static func buildBlock(_ components: MyType...) -> MyType {
        return Multi(children: components)
    }

}

struct Example {
    init(@MyBuilder input: () -> MyType) {
        print(input())
    }
}

let test = Example {
    // 3
    Single()
    Single()
    Single()
}
    
````

1.  Created a MyType conforming object `Multi` that has a property `children` for storing an array of `MyTypes`
2.  Implemented another version of `buildBlock` that takes a variadic `MyType` input and outputs a single 
    `Multi` object
3.  Added Two more `Single()`'s to the test

If you copy and run this in a playground it should print

"Multi(children: [\__lldb_expr_1.Single(), \__lldb_expr_1.Single(), \__lldb_expr_1.Single()])" 

which may not look pretty but tells us everything we need to know. Three `Single()`'s went in 
and one `Multi` containing the `Single()`'s came out.
 
 **Expression Example** 
 
 Sometimes when creating a function builder syntax, being able to build from different types can be an advantage. For instance if you frequently use a type that is really just a wrapper for another type of information or function. 
 
 With `buildExpression` as long as you implement a way for converting your starting type into the built type, writing with the new notation becomes simple and intuitive.
 
 
 ## Full Example
 
 ```Swift
// An Example protocol that all of my builder types will inherit from.
// This is helpful for keeping the types consistent.
// Also in examples like the SwiftUI View protocol, the body property is inherited
// by all Views allowing building to occur within the View itself.
protocol MyBuildableType {  }

struct Single: MyBuildableType {  }

struct Multi: MyBuildableType {
    var children: [MyBuildableType]
}

struct Tuple: MyBuildableType {
    
}

struct Num: MyBuildableType {
    var number: Int
}

// adding the @functionBuilder above tells the system that this struct will
// handle the partial results of the final builder expression
// after implementing the build methods, the @MyBuilder wrapper can
// be used on an escaping expression.

@_functionBuilder
struct MyBuilder {
    
    // Requirements: Only the buildBlock method is required when creating a functionBuilder
    // all the others if not implemented will default to the buildBlock method.
    
    // The simplest build operation which involves only one partial result
    // Takes in the compent and outputs the component
    static func buildBlock(_ component: MyBuildableType) -> MyBuildableType {
        return component
    }
    
    // If the partial results contain multiple children this method will
    // make use of the `Multi` type that inherits from the `MyBuildType`
    // I preemptively created the Multi type with its children property to
    // house the multiple components in one spot.
    static func buildBlock(_ children: MyBuildableType...) -> Multi {
        return Multi(children: children)
    }
    
    // Build optional hands cases where the partial result is an optional value
    // while there are a few ways to handle this circumstance, using the `Multi`
    // with an empty children set is the simplest for our purposes.
    static func buildOptional(_ component: MyBuildableType?) -> MyBuildableType {
        return component ?? Multi(children: [])
    }
    
    // declared to build combined results for do statement bodys
    static func buildDo(_ children: MyBuildableType...) -> Multi {
        return Multi(children: children)
    }
    
    // The buildEither methods must be both declared or else the builder will use buildOptional
    // when multiple options are available such as an if or switch statement, these methods
    // handle the partial build of the optional-executed subblocks
    
    static func buildEither(first: MyBuildableType) -> MyBuildableType {
        return first
    }
    
    static func buildEither(second: MyBuildableType) -> MyBuildableType {
        return second
    }
    
    // Here i am using an Int as my expression type but buildExpression can use any type.
    // This allows your syntax to be more flexible and do things like handling numbers and other literals
    // This method can be declared multiple times with different types, giving a lot of variability in the
    // building blocks.
    static func buildExpression(_ expression: Int) -> MyBuildableType {
        return Num(number: expression)
    }
}


// An example of a class which uses a function builder in its initializer
class SomeExample {
    
    var parameters: MyBuildableType
    
    init(@MyBuilder builder:  () -> MyBuildableType) {
        
        self.parameters = builder()
        print(self.parameters)
    }
}


func example() {
    SomeExample {
        Single()
        Single()
    }
}
```
