
`类`

```
class Food {
    var name: String
    init(name: String) {
        self.name = name
    }
    convenience init() {
        self.init(name: "sadas")
    }
}

let fp = Food()
print(fp.name)

```

```
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
var shape = Shape()//调用默认构造函数 ==oc [[Shape alloc] init]
```

`class init with something`
```
//demo2
class NamedShape {
    var numberOfSides: Int = 0
    var name: String // need init

    //构造函数 ,
    init(name: String) {
        //self 被用来标示实例变量，类似于c++ this
        self.name = name
    }

    deinit {
        //析构函数
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}

var sharp = NamedShape(name: "sss")
sharp.simpleDescription()
sharp.name

```

`override`
```
class Square: NamedShape {
    var sideLength: Double = 0
    var perimeter: Double {
            get {
                return 3.0 * sideLength
            }
            set {
                sideLength = newValue / 3.0
            }
        }


    init(sideLength: Double, name: String) {
        //....初始化当前类square var
        self.sideLength = sideLength


        super.init(name: name)
        //初始化父类var
        numberOfSides = 4
    }
    func area() ->  Double {
        return sideLength * sideLength
    }
    //override
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    } }
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

```
class func class 修饰的函数是类函数

```