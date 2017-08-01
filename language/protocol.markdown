
`protocol`

```

protocol SomeProtocol {
    var mustBeSettable: Int { get set }
    var doesNotNeedToBeSettable: Int { get }
}

```

```
        protocol ExampleProtocol {
            var simpleDescription: String { get }
            mutating func adjust()
            //使用 mutating 关键字修饰方法是为了能在该方法中修改 struct 或是 enum 的变量
        }

   ```

`class`
```
        class SimpleClass: ExampleProtocol {
            var simpleDescription: String = "A very simple class."
            var anotherProperty: Int = 69105
            func adjust() {
                simpleDescription += "  Now 100% adjusted."
            }
        }
  ```

  `struct`
  ```
  struct SimpleStructure: ExampleProtocol {
      var simpleDescription: String = "A simple structure"
      //
      mutating func adjust() {
          simpleDescription += " (adjusted)"
      }
  }
  var b = SimpleStructure()
  b.adjust()
  let bDescription = b.simpleDescription
  ```

  `enum`
  ```
  enum SimpleEnum: ExampleProtocol {
      case First, Second, Third
      var simpleDescription: String {
          get {
              switch self {
              case .First:
                  return "first"
              case .Second:
                  return "second"
              case .Third:
                  return "third"
              }
          }

          set {
              simpleDescription = newValue
          }
      }
      //
      mutating func adjust() {

      }
  }

  ```

  `extension`

          extension Int: ExampleProtocol {
              var simpleDescription: String {
                  return "The number \(self)"
              }
              mutating func adjust() {

              }

          }
          print(7.simpleDescription)

`Class-Only Protocols`
```
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
    // class-only protocol definition goes here
}
```

`check weather is some protocol type`

```
if let objectWithArea = object as? SomeProtocol {
        print("Area is \(objectWithArea.area)")
    } else {
        print("Something that doesn't have an area")
    }

```

`Note that @objc protocols can be adopted only by classes that inherit from Objective-C classes or other @objc classes. They can’t be adopted by structures or enumerations.`
```
@objc protocol CounterDataSource {
    @objc optional func increment(forCount count: Int) -> Int
    @objc optional var fixedIncrement: Int { get }
}
```