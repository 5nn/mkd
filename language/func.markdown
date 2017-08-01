
`func`
```
//函数      参数名称: 参数类型                返回对象类型
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}

//默认情况下，函数使用它们的参数名称作为它们参数的标签，在参数名称前可以自定义参数标签，或者使用 _ 表示不使用参数标签。
func che(cheName che: String){

}
che(cheName:"22");

func cheTwo(_ che: String){

}
cheTwo("didi")
```
`func 返回多值`
```
//func 返回多个值的问题：引入元组
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0
    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score }
        sum += score }
    return (min, max, sum)
}
let statistics = calculateStatistics(scores:[5, 3, 100, 3, 9])
print(statistics)//（3，100，120）<--元组：(.0 3, .1 100, .2 120)
print(statistics.2)//120
```
`多个参数`
```
//func 多个参数问题：
func sumOf(numbers: Int...) -> Int {
    print(numbers.count)
    var sum = 0
    for number in numbers {
        sum += number
    }
    return sum
}
sumOf()//0
sumOf(numbers: 1, 2, 3)//6
```
`函数嵌套`
```
//函数嵌套问题
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
```

`函数作为返回值`
```
//函数作为返回值问题
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()//(Int) -> Int
print(increment(3))//(Founction)
increment(7)//8
```

`函数作为参数`
```
//函数作为参数
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        } }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)//true
```

`闭包`
```
//函数实际上是一种特殊的闭包:它是一段能之后被调取的代码
//使用 in 将参数和返回值类型声明与闭包函数体进行分离
numbers.map({
    (number: Int) -> Int in
    /*body*/
    let result = 3 * number
    return result
})

let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)

let sortedNumberList = mappedNumbers.sorted {$0 > $1}
print(sortedNumberList)


```