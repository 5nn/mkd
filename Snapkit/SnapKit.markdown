`直观`

```
        let testView = UIView()
        testView.backgroundColor = UIColor.cyan
        view.addSubview(testView)
        testView.snp.makeConstraints { (make) in
            make.width.equalTo(100)         // 宽为100
            make.height.equalTo(100)        // 高为100
            make.center.equalTo(view)       // 位于当前视图的中心
        }

```

`SuperView`
```
        let view2 = UIView()
        view2.backgroundColor = UIColor.magenta
        self.view.addSubview(view2)
        view2.snp.makeConstraints { (make) in
            make.top.equalToSuperview().offset(20)      // 当前视图的顶部距离父视图的顶部：20（父视图顶部+20）
            make.left.equalToSuperview().offset(20)     // 当前视图的左边距离父视图的左边：20（父视图左边+20）
            make.bottom.equalToSuperview().offset(-20)  // 当前视图的底部距离父视图的底部：-20（父视图底部-20）
            make.right.equalToSuperview().offset(-20)   // 当前视图的右边距离父视图的右边：-20（父视图右边-20）
        }


```

`frame 搭配 snap`
```
// 黑色视图作为父视图
         let view1 = UIView()
         view1.frame = CGRect(x: 0, y: 0, width: 300, height: 300)
         view1.center = view.center
         view1.backgroundColor = UIColor.black
         view.addSubview(view1)

         // 测试视图
         let view2 = UIView()
         view2.backgroundColor = UIColor.magenta
         view1.addSubview(view2)
         view2.snp.makeConstraints { (make) in
            make.edges.equalToSuperview().inset(UIEdgeInsets(top: 20, left: 20, bottom: 20, right: 20))
         }

    }

  ```

 `frame 搭配 snap`

```
      黑色视图作为父视图
            let view1 = UIView()
            view1.frame = CGRect(x: 0, y: 0, width: 300, height: 300)
            view1.center = view.center
            view1.backgroundColor = UIColor.black
            view.addSubview(view1)

            // 测试视图
            let view2 = UIView()
            view2.backgroundColor = UIColor.magenta
            view1.addSubview(view2)
            view2.snp.makeConstraints { (make) in
                // 让顶部距离view1的底部为10的距离
                make.top.equalTo(view1.snp.bottom).offset(10)
                // 设置宽、高
                make.width.height.equalTo(100)
                // 水平中心线<=view1的左边
                make.centerX.lessThanOrEqualTo(view1.snp.leading)
        }
```

`更新约束 引用约束`

```
var updateConstraint: Constraint?

override func viewDidLoad() {
    super.viewDidLoad()

    // 黑色视图作为父视图
    let view1 = UIView()
    view1.frame = CGRect(x: 0, y: 0, width: 300, height: 300)
    view1.center = view.center
    view1.backgroundColor = UIColor.black
    view.addSubview(view1)

    // 测试视图
    let view2 = UIView()
    view2.backgroundColor = UIColor.magenta
    view1.addSubview(view2)
    view2.snp.makeConstraints { (make) in
        make.width.height.equalTo(100)  // 宽高为100
        self.updateConstraint = make.top.left.equalTo(10).constraint   // 距离父视图上、左为10 ,保存约束
    }

    let updateButton = UIButton(type: .custom)
    updateButton.backgroundColor = UIColor.brown
    updateButton.frame = CGRect(x: 100, y: 80, width: 50, height: 30)
    updateButton.setTitle("更新", for: .normal)
    updateButton.addTarget(self, action: #selector(updateConstraintMethod), for: .touchUpInside)
    view.addSubview(updateButton)
}

// 更新约束
func updateConstraintMethod() {
    self.updateConstraint?.update(offset: 50)   // 更新距离父视图上、左为50
}

```

```

//UPDATE
blackView.snp.updateConstraints { (make) in
        make.width.height.equalTo(20)
        make.top.equalTo(300)
    }

    //remakeConstraints
    清楚原来的，重新约束
```

`向主view约束 用self.contentView.snp.XXX`

```
//向主view contentView约束 用self.contentView.snp.XXX
 self.contentPanel.snp.makeConstraints{ (make) -> Void in
            make.top.left.right.equalTo(self.contentView);
        }
        self.avatarImageView.snp.makeConstraints{ (make) -> Void in
            make.left.top.equalTo(self.contentView).offset(12);
            make.width.height.equalTo(35);
        }
        self.userNameLabel.snp.makeConstraints{ (make) -> Void in
            make.left.equalTo(self.avatarImageView.snp.right).offset(10);
            make.top.equalTo(self.avatarImageView);
        }
        self.dateAndLastPostUserLabel.snp.makeConstraints{ (make) -> Void in
            make.bottom.equalTo(self.avatarImageView);
            make.left.equalTo(self.userNameLabel);
        }
        self.replyCountLabel.snp.makeConstraints{ (make) -> Void in
            make.centerY.equalTo(self.userNameLabel);
            make.right.equalTo(self.contentPanel).offset(-12);
        }
        self.replyCountIconImageView.snp.makeConstraints{ (make) -> Void in
            make.centerY.equalTo(self.replyCountLabel);
            make.width.height.equalTo(18);
            make.right.equalTo(self.replyCountLabel.snp.left).offset(-2);
        }
        self.nodeNameLabel.snp.makeConstraints{ (make) -> Void in
            make.centerY.equalTo(self.replyCountLabel);
            make.right.equalTo(self.replyCountIconImageView.snp.left).offset(-9)
            make.bottom.equalTo(self.replyCountLabel).offset(1);
            make.top.equalTo(self.replyCountLabel).offset(-1);
        }
        self.nodeBackgroundImageView.snp.makeConstraints{ (make) -> Void in
            make.top.bottom.equalTo(self.nodeNameLabel)
            make.left.equalTo(self.nodeNameLabel).offset(-5)
            make.right.equalTo(self.nodeNameLabel).offset(5)
        }
        self.topicTitleLabel.snp.makeConstraints{ (make) -> Void in
            make.top.equalTo(self.avatarImageView.snp.bottom).offset(12);
            make.left.equalTo(self.avatarImageView);
            make.right.equalTo(self.contentPanel).offset(-12);
            make.bottom.equalTo(self.contentView).offset(-8)
        }
        self.contentPanel.snp.makeConstraints{ (make) -> Void in
            make.bottom.equalTo(self.contentView.snp.bottom).offset(-8);
        }


```