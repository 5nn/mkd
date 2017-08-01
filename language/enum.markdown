#### enum
`enum 权举 就像类和其他所有命名类型一样，枚举可以包含方法`

            enum Rank: Int {
                case Ace = 1
                case Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten
                case Jack, Queen, King
                func simpleDescription() -> String {
                    switch self {
                    case .Ace:
                        return "ace"
                    case .Jack:
                        return "jack"
                    case .Queen:
                        return "queen"
                    case .King:
                        return "king"
                    default:
                        return String(self.rawValue)
                    }
                } }
            let ace = Rank.Ace
            let aceRawValue = ace.rawValue//使用 rawValue 属性来访问一个枚举成员的原始值

`init`

        //init?(rawValue:)
        if let convertedRank = Rank(rawValue: 3) {
            let threeDescription = convertedRank.simpleDescription()
        }


`weaning:如果没有比较有意义的原始值，你就不需要提供原始值`

        enum Suit {
            case Spades, Hearts, Diamonds, Clubs
            func simpleDescription() -> String {
                switch self {
                case .Spades:
                    return "spades"
                case .Hearts:
                    return "hearts"
                case .Diamonds:
                    return "diamonds"
                case .Clubs:
                    return "clubs"
                }
            } }
        let hearts = Suit.Hearts//真实值
        let heartsDescription = hearts.simpleDescription()


`change self`
```
enum OnOffSwitch: Togglable {
    case off, on
    mutating func toggle() {
        switch self {
        case .off:
            self = .on
        case .on:
            self = .off
        }
    }
}

var lightSwitch = OnOffSwitch.off
lightSwitch.toggle()
```

`protocol init`
```
protocol SomeProtocol {
    init(someParameter: Int)
}

class SomeClass: SomeProtocol {
    required init(someParameter: Int) {
        // initializer implementation goes here
    }
}


protocol SomeProtocol {
    init()
}

class SomeSuperClass {
    init() {
        // initializer implementation goes here
    }
}

class SomeSubClass: SomeSuperClass, SomeProtocol {
    // "required" from SomeProtocol conformance; "override" from SomeSuperClass
    required override init() {
        // initializer implementation goes here
    }
}


```

