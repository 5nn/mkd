`define`

//Closures Are Reference Types

```
{ (parameters) -> return type in
    statements
}
```

```
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // function body goes here
}

```

```
someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})
```

```
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}

```

`escap closure`

```
//闭包是自包含的函数代码块，可以在代码中被传递和使用,闭包可以捕获和存储其所在上下文中任意常量和变量的引用（对象的内存地址）(比如说回调),闭包是引用类型

//demo1 函数作为参数
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

func backward(_ ls: String, _ rs:String) ->Bool{
    return ls > rs
}

let sortedNames = names.sorted(by: backward)

// 闭包表达式
//        { (parameters) -> returnType in
//            statements
//         }
//闭包表示
let sortedNamesTwo = names.sorted(by: {
    (s1: String, s2: String) -> Bool in
    //以下是闭包的函数体部分
    return s1 > s2
})
//如果闭包表达式是 函数或方法 的唯一参数，则当你使用尾随闭包时，
let sortedNamesTwoTwo = names.sorted(){
        (s1: String, s2: String) -> Bool in
        //以下是闭包的函数体部分
        return s1 > s2
    }

//你甚至可以把 () 省略掉
let sortedNamesTwoTwoTwo = names.sorted{
    (s1: String, s2: String) -> Bool in
    //以下是闭包的函数体部分
    return s1 > s2
}

//如果闭包函数体很短
//单行表达式闭包可以通过省略 return 关键字来隐式返回单行表达式的结果
let sortedNamesThree = names.sorted(by: { $0 > $1})
let sortedNamesFour = names.sorted(by: >)

//使用尾随闭包进行函数调用
let sortedNamesFive = names.sorted(){$1 > $0}

let sortedNamesSix = names.sorted{$1 > $0}


//如果闭包函数体很长
func someFunctionThatTakesAClosure(closure: () -> Void) { // 函数体部分
}
// 以下是不使用尾随闭包进行函数调用 someFunctionThatTakesAClosure(closure: {
// 闭包主体部分 })
// 以下是使用尾随闭包进行函数调用 someFunctionThatTakesAClosure() {
// 闭包主体部分 }


/****  值捕获  ****/
//闭包可以在其被定义的上下文中捕获常量或变量。即使定义这些常量和变量的原作用域已经不存在，闭包仍然可
//以在闭包函数体内引用和修改这些值。常用来实现回调。Swift 中，可以捕获值的闭包的最简单形式是嵌套函数，也就是定义在其他函数的函数体内的函数。嵌套函数可 以捕获其外部函数所有的参数以及定义的常量和变量。

//demo
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        //incrementer从 外围函数捕获了 runningTotal 和 amount 变量的引用，makeIncrementer消失后这2个不会消失
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

let incrementByTen = makeIncrementer(forIncrement: 10)  //() -> Int
incrementByTen()//10
incrementByTen()//20
incrementByTen()//30
incrementByTen()//40
let other = incrementByTen
other()//50
let incrementByTenTwo = makeIncrementer(forIncrement: 10)
incrementByTenTwo()//10


//无论你将函数或闭包赋值给一个常量还是变量，你实际上都是将常量或变量的值设置为对应函数或闭包的引 用

//闭包逃逸：网络请求请求结束后的回调的闭包则是逃逸的，闭包函数代码会马上执行的则是非逃逸
func startRequest(callBack: @escaping ()->Void ) {
    //逃逸闭包必须 @escaping 显式声明
    DispatchQueue.global().asyncAfter(deadline: DispatchTime.now() + 1) {
        callBack()
    }
}


//非逃逸闭包，这意味着它可以隐式引用 self

var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}

func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()
}
class SomeClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { self.x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}
let instance = SomeClass()
instance.doSomething()
print(instance.x)
// 打印出 "200"
completionHandlers.first?()

print(instance.x)
// 打印出 "100"

//解决闭包引用问题
//var someClosure: (Int, String) -> String = {
////    [unowned self, weak delegate = self.delegate!] (index: Int, stringToProcess: String) -> String in // 这里是闭包的函数体
//}
class HTMLElement {
    let name: String
    let text: String?
    lazy var asHTML: (Void) -> String = {
        [unowned self] in
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}


var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
print(paragraph!.asHTML())
// 打印 “<p>hello, world</p>”
```