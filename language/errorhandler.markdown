
`func 抛出error`
```
        func canThrowAnError() throws {
            // this function may or may not throw an error
        }

        do {
            try canThrowAnError()
            // no error was thrown
        } catch {
            // an error was thrown
        }
```

`assert`
```
        let age = -3
        assert(age >= 0, "A person's age can't be less than zero.")
```

`error handler`

```
enum PrinterError: Error {
    case OutOfPaper
    case NoToner
    case OnFire
}
//使用 throw 来抛出一个错误并使用 throws 来表示一个可以抛出错误的函数
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.NoToner
    }
    return "Job sent"
}
```

`demo1`
```
do {
    //使用 try 来标记可以抛出错误 的代码
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)//错误会自动命名为 error
}
```

`demo2`
```
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.OnFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
```


