
`var`
```
var str = "Hello, playground"
var dota: String? = "Dota"
let dd = dota!//解包
assert(dd == "Dota")//测试一下

var lose: String?

```
`lazy init`
```
lazy var fibonacciOfAge: Int = {
        return 44
    }()
```


`get setter`
```
 var demo: String {
        get{return "yyy"}

        set(newValue){

        }
    }
```

`array`
```
var book = ["四库全书":"纪晓岚","春江花月夜":"张若虚",]
var emptyArray = [String]()
let emptyArraySix =  [Array<Any>]()
```

`for-in`
```
var teamScore = 0
for score in individualScores {
    //if 后面可以是bool表达式，oc中的if（a）{}报错
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    } }
print(teamScore)


var total = 0
for i in 0..<4 {
    total += i }
print(total)//6

for i in 0...4 {
    total += i }
print(total)//16

for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number // 执行了8次
        }
    } }
```

`if-let`
```
//可以一起使用 if 和 let 来处理值缺失的情况，这些值可由可选型来代表
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"

if let name = optionalName {
    //如果不是 nill ，会将值解包并赋给 后面的常量，这样代码块中就可以使用这个值了
    greeting = "Hello, \(name)"
}else{
    greeting = "Hello world!"
}
//此时等同于
let world = "world!"
let  greetingTwo = "Hello\(optionalName ?? world)"
```

`switch-case`
```
//demo two
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
    //hasSuffix 判断结束是否包含pepper单词，利用正则表达式从最后一个字符往前匹配
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}

```

`repeat`
```
repeat {
    m=m * 2
} while m < 100
```
