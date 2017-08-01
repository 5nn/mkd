

`架构图`

<img src="./arrch.png" width="500" height="400" alt="架构图"/>


`归类`

```
View : 视图的布局、渲染、动画、UIViewController的转场

ViewModel : 纯业务逻辑处理

Model : 提供数据，如网络请求数据，本地数据库、UserDefaults
```

`use`

---

`First step`

```
import RxSwift
import RxCocoa
```

```
class ViewController: UIViewController {

    //.... many ui
    @IBOutlet weak var tapButton: UIButton!

    //disposebag
    fileprivate let disposeBag = DisposeBag()

      func addEvent() {
            tapButton.rx.tap.subscribe({ [weak self] _ in
                       guard let this = self else {
                           return
                       }
                       guard let text = this.numberLabel.text else {
                           return
                       }
                       guard let number = Int(text) else {
                           return
                       }
                       this.numberLabel.text = String(number+1)
                   }).addDisposableTo(disposeBag)

       }



}
```

`so usage one`

```
 tapButton.rx.tap.subscribe({ [weak self] _ in

                   }).addDisposableTo(disposeBag)
```

`rx.XXX  xxx是rxswift扩展UI的部分`

`subscribe 函数二种形式`

```
第一种
tapButton.rx.tap.subscribe({ [weak self] _ in

                   }).addDisposableTo(disposeBag)

```

```
第二种 onNext ...

 let longPressGesture = UILongPressGestureRecognizer()
        longPressGesture.rx.event
            .subscribe(onNext: { [weak self] _ in
                guard let this = self else {
                    return
                }
                guard let text = this.numberLabel.text else {
                    return
                }
                guard let number = Int(text) else {
                    return
                }
                this.numberLabel.text = String(number+1)
            }).addDisposableTo(disposeBag)
        self.tapButton.addGestureRecognizer(longPressGesture)


```

`map bind`
```
resetButton.rx.tap.map({
            x in
            let dateformatter = DateFormatter()
            dateformatter.dateStyle = .medium
            dateformatter.timeStyle = .medium
            return dateformatter.string(from: Date())
        }).bind(to: numberLabel.rx.text).addDisposableTo(disposeBag)

```