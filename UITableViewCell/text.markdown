
### cell


```

class DemoTableViewCell: UITableViewCell {


    var avatarImageView: UIImageView = {
        let imageView = UIImageView()
        imageView.backgroundColor = UIColor(white: 0.9, alpha: 0.3)
        imageView.layer.borderWidth = 1.5
        imageView.layer.borderColor = UIColor(white: 1, alpha: 0.6).cgColor
        imageView.layer.masksToBounds = true
        imageView.layer.cornerRadius = 38
        return imageView
    }()


    var userNameLabel: UILabel = {
        let label = UILabel()
        //        label.font = v2Font(16)
        label.font = UIFont.preferredFont(forTextStyle: UIFontTextStyle.body)

        return label
    }()

    override init(style: UITableViewCellStyle, reuseIdentifier: String?) {
        super.init(style: style, reuseIdentifier: reuseIdentifier);

    }
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
    }

}

//look v2ex
 func updataCell(_ model:TopicListModel){

        self.dateAndLastPostUserLabel.text = model.date
        self.nodeNameLabel.text = model.nodeName
    }

```

`use`

```
tableView.register(DemoTableViewCell.self, forCellReuseIdentifier: cellIdentifier)
 let cell = tableView.dequeueReusableCell(withIdentifier: cellIdentifier, for: indexPath) as! DemoTableViewCell;
        //...get model for index
        cell.updataCell(model)
        return cell;


```