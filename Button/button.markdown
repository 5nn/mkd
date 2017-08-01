
`静态标题按钮 - 点击界面不变`
```
let loginButton = UIButton()

self.loginButton.setTitle("登  录", for: UIControlState())
        self.loginButton.titleLabel!.font = v2Font(20)
        self.loginButton.layer.cornerRadius = 3;
        self.loginButton.layer.borderWidth = 0.5
        self.loginButton.layer.borderColor = UIColor(white: 1, alpha: 0.8).cgColor;
        vibrancyView.contentView.addSubview(self.loginButton);

        self.loginButton.snp.makeConstraints{ (make) -> Void in
            make.top.equalTo(self.passwordTextField.snp.bottom).offset(20)
            make.centerX.equalTo(vibrancyView)
            make.width.equalTo(300)
            make.height.equalTo(38)
        }




        let button:UIButton = UIButton(type: UIButtonType.custom)
        button.frame = CGRect(x:20,y:100,width: 200,height:44)//use snapkit
        button.setTitle("按钮", for: UIControlState.normal)
        button.titleLabel?.font = button.titleLabel?.font.withSize(17)
        button.setTitleColor(UIColor.red, for: UIControlState.normal)
        button.backgroundColor = UIColor.gray
        button.addTarget(self, action: #selector(something(bt:)), for: .touchUpInside)
        button.titleLabel?.font = UIFont(name: "Arial-MT", size: 33)
        self.view.addSubview(button)
```
`标题按钮 - 点击改变背景色`

        -- FlatButton

`带图片UIButton 点击整体微亮`

```

- (void)viewDidLoad {
    [super viewDidLoad];
    //
    // Do any additional setup after loading the view, typically from a nib.
    FSCustomButton *button = [[FSCustomButton alloc] initWithFrame:CGRectMake(100, 20, 44, 44)];
    button.adjustsTitleTintColorAutomatically = YES;
    [button setTintColor:UIColorMake(27, 31, 35)];
    button.titleLabel.font = [UIFont systemFontOfSize:8];
    [button setTitle:@"图片在上" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor whiteColor];
    [button setImage:[UIImage imageNamed:@"my_ic_coupon"] forState:UIControlStateNormal];
    button.layer.cornerRadius = 4;
    button.buttonImagePosition = FSCustomButtonImagePositionTop;
    button.titleEdgeInsets = UIEdgeInsetsMake(5, 0, 0, 0);
    [self.view addSubview:button];
//    [button sizeToFit];

    FSCustomButton *button2 = [[FSCustomButton alloc] initWithFrame:CGRectMake(100, 120, 100, 80)];
    button2.adjustsTitleTintColorAutomatically = YES;
    [button2 setTintColor:UIColorMake(27, 31, 35)];
    button2.titleLabel.font = [UIFont boldSystemFontOfSize:14];
    [button2 setTitle:@"图片在下" forState:UIControlStateNormal];
    button2.backgroundColor = UIColorMake(222, 234, 214);
    [button2 setImage:[UIImage imageNamed:@"my_ic_coupon"] forState:UIControlStateNormal];
    button2.layer.cornerRadius = 4;
    button2.buttonImagePosition = FSCustomButtonImagePositionBottom;
    button2.imageEdgeInsets = UIEdgeInsetsMake(10, 0, 0, 0);
    [self.view addSubview:button2];

    FSCustomButton *button3 = [[FSCustomButton alloc] initWithFrame:CGRectMake(220, 20, 100, 80)];
    button3.adjustsTitleTintColorAutomatically = YES;
    [button3 setTintColor:UIColorMake(27, 31, 35)];
    button3.titleLabel.font = [UIFont boldSystemFontOfSize:14];
    [button3 setTitle:@"sizeToFit" forState:UIControlStateNormal];
    button3.backgroundColor = UIColorMake(222, 234, 214);
    [button3 setImage:[UIImage imageNamed:@"my_ic_coupon"] forState:UIControlStateNormal];
    button3.layer.cornerRadius = 4;
    button3.buttonImagePosition = FSCustomButtonImagePositionBottom;
    button3.imageEdgeInsets = UIEdgeInsetsMake(10, 0, 0, 0);
    [self.view addSubview:button3];
    [button3 sizeToFit];

    FSCustomButton *button4 = [[FSCustomButton alloc] initWithFrame:CGRectMake(220, 120, 100, 80)];
    button4.adjustsTitleTintColorAutomatically = YES;
    [button4 setTintColor:UIColorMake(27, 31, 35)];
    button4.titleLabel.font = [UIFont boldSystemFontOfSize:14];
    [button4 setTitle:@"sizeToFit" forState:UIControlStateNormal];
    button4.backgroundColor = UIColorMake(222, 234, 214);
    [button4 setImage:[UIImage imageNamed:@"my_ic_coupon"] forState:UIControlStateNormal];
    button4.layer.cornerRadius = 4;
    button4.buttonImagePosition = FSCustomButtonImagePositionBottom;
    button4.imageEdgeInsets = UIEdgeInsetsMake(10, 0, 0, 0);
    [self.view addSubview:button4];
    [button4 sizeToFit];

    FSCustomButton *button5 = [[FSCustomButton alloc] initWithFrame:CGRectMake(100, 220, 200, 40)];
    button5.titleLabel.font = [UIFont boldSystemFontOfSize:14];
    [button5 setTitle:@"高亮背景色" forState:UIControlStateNormal];
    [button5 setTitleColor:[UIColor blackColor] forState:UIControlStateNormal];
    button5.backgroundColor = UIColorMake(222, 234, 214);
    button5.highlightedBackgroundColor = UIColorMake(0, 168, 225);// 高亮时的背景色
    [button5 setImage:[UIImage imageNamed:@"my_ic_coupon"] forState:UIControlStateNormal];
    button5.layer.cornerRadius = 4;
    button5.titleEdgeInsets = UIEdgeInsetsMake(0, 5, 0, 0);
    [self.view addSubview:button5];

    FSCustomButton *button6 = [[FSCustomButton alloc] initWithFrame:CGRectMake(100, 280, 200, 40)];
    button6.titleLabel.font = [UIFont boldSystemFontOfSize:14];
    [button6 setTitle:@"高亮边框色" forState:UIControlStateNormal];
    [button6 setTitleColor:[UIColor blackColor] forState:UIControlStateNormal];
    button6.backgroundColor = UIColorMake(222, 234, 214);
    button6.highlightedBackgroundColor = UIColorMake(0, 168, 225);// 高亮时的背景色
    [button6 setImage:[UIImage imageNamed:@"my_ic_coupon"] forState:UIControlStateNormal];
    button6.layer.cornerRadius = 4;
    button6.layer.borderWidth = 2;
    button6.highlightedBorderColor = [UIColor redColor];
    button6.titleEdgeInsets = UIEdgeInsetsMake(0, 5, 0, 0);
    [self.view addSubview:button6];
}

```