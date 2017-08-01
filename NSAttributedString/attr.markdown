let sampleText = "那么，结论就是在自定"

        let paragraphStyle = NSMutableParagraphStyle()
        paragraphStyle.alignment = NSTextAlignment.justified
        //行间距
        //paragraph.lineSpacing = 10;
        //段落间距
        //paragraph.paragraphSpacing = 20;

        let attributedString = NSAttributedString(string: sampleText,
                                                  attributes: [
                                                    NSParagraphStyleAttributeName: paragraphStyle,
                                                    NSBaselineOffsetAttributeName: NSNumber(value: 0),
                                                     NSKernAttributeName: @(-3),
                                                      NSFontAttributeName: [UIFont systemFontOfSize: 20],
                                                       NSForegroundColorAttributeName:UIColor.red
            ])

        let label = UILabel()
        label.attributedText = attributedString
        label.numberOfLines = 0
        label.frame = CGRect(x: 10, y: 20, width: 240, height: 400)


        self.view.addSubview(label)


        // NSStrikethroughStyleAttributeName: @(NSUnderlineStyleDouble), 删除线
        //NSStrikethroughColorAttributeName: UIColor.red,
        //NSUnderlineColorAttributeName: [UIColor blueColor],下划线
         //NSUnderlineStyleAttributeName: @(NSUnderlineStyleSingle),
