
`YYLabel`

```
    var topicTitleLabel: YYLabel = {
        let label = YYLabel()
        label.textVerticalAlignment = .top
        label.font=UIFont.systemFont(ofSize: 18);
        label.displaysAsynchronously = true
        label.numberOfLines=0
        return label
    }()


1
//title from request

2  NSMutableAttributedString
  self.topicTitleAttributedString = NSMutableAttributedString(string: title,
                    attributes: [
                        NSFontAttributeName:v2Font(17),
                        NSForegroundColorAttributeName:V2EXColor.colors.v2_TopicListTitleColor,
                    ])
                self.topicTitleAttributedString?.yy_lineSpacing = 3
3 caculate size by yytextlayout
     let layout  = YYTextLayout(containerSize: CGSize(width: SCREEN_WIDTH-24, height: 9999), text: self.topicTitleAttributedString)
    self.topicTitleLabel.textLayout = layout
4 use size when layout or cellheight
    height = model.topicTitleLayout?.textBoundingRect.size.height

```


`UILabel`
```
var userNameLabel: UILabel = {
        let label = UILabel()
        label.font = v2Font(14)
        label.textColor=UIColor.red
         label.textAlignment= .center
        return label;
    }()


    var avatarImageView: UIImageView = {
        let imageview = UIImageView()
        imageview.contentMode=UIViewContentMode.scaleAspectFit
        return imageview
    }()



```

`UILabel 一般形式`
```
    letlabel =UILabel.init(frame:CGRect(x:10,y:20,width:300,height:100))

    label.text="summerZao"

    label.textColor=UIColor.red

    label.backgroundColor=UIColor.black

    label.textAlignment= .right

    label.shadowColor=UIColor.gray//灰色阴影

    label.shadowOffset=CGSize(width:1.5,height:1.5)//阴影的偏移量

    label.font=UIFont(name:"Zapfino",size:20)

    // label.font = UIFont.systemFont(ofSize: 20)

    label.lineBreakMode= .byTruncatingTail//隐藏尾部并显示省略号

    label.lineBreakMode= .byTruncatingMiddle//隐藏中间部分并显示省略号

    label.lineBreakMode= .byTruncatingHead//隐藏头部并显示省略号

    label.lineBreakMode= .byClipping//截去多余部分也不显示省略号

    label.numberOfLines=2//显示两行文字（默认只显示一行，设为0表示没有行数限制）

    label.isHighlighted=true//设置文本高亮

    label.highlightedTextColor=UIColor.green//设置文本高亮颜色

    //富文本设置

    /*

    let attributeString = NSMutableAttributedString(string:"welcome to hangge.com")

    //从文本0开始6个字符字体HelveticaNeue-Bold,16号

    attributeString.addAttribute(NSFontAttributeName,

    value: UIFont(name: "HelveticaNeue-Bold", size: 16)!,

    range: NSMakeRange(0,6))

    //设置字体颜色

    attributeString.addAttribute(NSForegroundColorAttributeName, value: UIColor.blue,

    range: NSMakeRange(0, 3))

    //设置文字背景颜色

    attributeString.addAttribute(NSBackgroundColorAttributeName, value: UIColor.green,

    range: NSMakeRange(3,3))

    label.attributedText = attributeString

    */

    self.view.addSubview(label)


```


`add target`

```

self.userNameLabel.isUserInteractionEnabled = true
var userNameTap = UITapGestureRecognizer(target: self, action: #selector(HomeTopicListTableViewCell.userNameTap(_:)))
self.userNameLabel.addGestureRecognizer(userNameTap)

```