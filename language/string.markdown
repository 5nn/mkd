
   `字符串获取字节`

 ```
        let greeting = "Guten Tag!"
        greeting[greeting.startIndex]
        // G
        greeting[greeting.index(before: greeting.endIndex)]
        // !
        greeting[greeting.index(after: greeting.startIndex)]
        // u
        let index = greeting.index(greeting.startIndex, offsetBy: 7)
        greeting[index]

        welcome.remove(at: welcome.index(before: welcome.endIndex))
        // welcome now equals "hello there"

        let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
        welcome.removeSubrange(range)
        // welcome now equals "hello"

        let greeting = "Hello, world!"
        let index = greeting.index(of: ",") ?? greeting.endIndex
        let beginning = greeting[..<index]


 ```

 `insert`

```
    var welcome = "hello"
    welcome.insert("!", at: welcome.endIndex)
 ```

