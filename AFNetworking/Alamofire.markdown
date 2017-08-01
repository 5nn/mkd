#### Alamofire

&emsp;&emsp;`基本用法`
```
    Alamofire.request("https://httpbin.org/get").responseJSON { response in
    print(response.request)  // original URL request
    print(response.response) // HTTP URL response
    print(response.data)    // server data
    print(response.result)  // result of response serialization
    if let JSON = response.result.value {
    print("JSON: \(JSON)")
    }}
```


`Response handlers 默认是在主线程上运行的，可以添加到GCD队列中。`

```
let utilityQueue = DispatchQueue.global(qos: .utility)

Alamofire.request("https://httpbin.org/get").responseJSON(queue: utilityQueue) { response in

print("Executing response handler on utility queue")

}
```

`判断返回数据有效性`

```
Alamofire.request("https://httpbin.org/get")

.validate(statusCode: 200..<300)

.validate(contentType: ["application/json"])

.responseData { response in
  ...
}
```

`添加请求头，和编码方式`
```
 Alamofire.request(
            URL(string: "http://localhost:5984/rooms/_all_docs")!,
            method: .get,
            parameters: ["include_docs": "true"],
            encoding:URLEncoding.default,
            headers: [

                    "Authorization": "Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==",

                    "Accept": "application/json"

                    ]
            )

            .validate()
            .responseJSON { `[nowned self]` (response) -> Void in  ...
```

---

`添加验证`
```
  URLCredential(证书管理类):
   //相当于账号密码认证
    public init(user: String, password: String, persistence: URLCredential.Persistence)

//客户端证书 存在本地客户端(获取本地P12证书, 用于客户端认证)
  public init(identity: SecIdentity, certificates certArray: [Any]?, persistence: URLCredential.Persistence)

  //具体的trust生成的证书(用于获取远端证书与本地cer证书对比的双向认证)
  public init(trust: SecTrust)
```



```

        Alamofire.request("http://localhost:5984/rooms/_all_docs")
            .validate().authenticate(user: "", password: "")
            .responseJSON {  (response) -> Void in
            }


```

`用户名和密码放在请求头`
```
let user = "user"
let password = "password"
var headers: HTTPHeaders = [:]
if let authorizationHeader = Request.authorizationHeader(user: user, password: password) {
    headers[authorizationHeader.key] = authorizationHeader.value
}
Alamofire.request("https://httpbin.org/basic-auth/user/password", headers: headers)
    .responseJSON { response in
        debugPrint(response)
}
```

`upload DATA`
```
let imageData = UIImagePNGRepresentation(image)!
Alamofire.upload(imageData, to: "https://httpbin.org/post").responseJSON { response in
    debugPrint(response)
}
```

`upload file`
```
let fileURL = Bundle.main.url(forResource: "video", withExtension: "mov")!
Alamofire.upload(fileURL, to: "https://httpbin.org/post").responseJSON { response in
    debugPrint(response)
}
```

`upload many file`
```
Alamofire.upload(
    multipartFormData: { multipartFormData in
        multipartFormData.append(ImageURL1, withName: "image1")
        multipartFormData.append(ImageURL2, withName: "image2")
    },
    to: "https://httpbin.org/post",
    encodingCompletion: { encodingResult in
        switch encodingResult {
        case .success(let upload, _, _):
            upload.responseJSON { response in
                debugPrint(response)
            }
        case .failure(let encodingError):
            print(encodingError)
        }
    }
)

```

`url编码`
```
Alamofire.request("https://httpbin.org/get", parameters: parameters) // encoding defaults to `URLEncoding.default`
Alamofire.request("https://httpbin.org/get", parameters: parameters, encoding: URLEncoding.default)
Alamofire.request("https://httpbin.org/get", parameters: parameters, encoding: URLEncoding(destination: .methodDependent))

Alamofire.request("https://httpbin.org/post", method: .post, parameters: parameters, encoding: JSONEncoding.default)
Alamofire.request("https://httpbin.org/post", method: .post, parameters: parameters, encoding: JSONEncoding(options: []))
```

`自签名https 封装样板`
```

enum JFResponseStatus: Int {
    case success  = 0
    case unusual  = 1
    case notLogin = 2
    case failure  = 3
}

/// 网络请求回调
typealias NetworkFinished = (_ status: JFResponseStatus, _ result: JSON?, _ tipString: String?) -> ()

class JFNetworkTools: NSObject {

    /// 网络工具类单例
    static let shareNetworkTool = JFNetworkTools()

    fileprivate var afManager: SessionManager!

    override init() {
        super.init()

        print("配置ssl，防止抓包工具抓取数据")
        let pathToCert = Bundle.main.path(forResource: "cert", ofType: "cer")
        let localCertificate = NSData(contentsOfFile: pathToCert!)
        let certificates = [SecCertificateCreateWithData(nil, localCertificate!)!]

        let serverTrustPolicy = ServerTrustPolicy.pinCertificates(
            certificates: certificates,
            validateCertificateChain: true,
            validateHost: true
        )
        let serverTrustPolicies = ["xxxxxxxx" : serverTrustPolicy]
        let serverTrustPolicyManager = ServerTrustPolicyManager(policies: serverTrustPolicies)

        afManager = SessionManager(
            configuration: URLSessionConfiguration.default,
            serverTrustPolicyManager: serverTrustPolicyManager
        )

    }

    /// 获取请求头
    ///
    /// - Returns: 请求头
    fileprivate func getHTTPHeaders(parameters: [String : Any]?) -> [String : String] {

        // api版本
        var headers = [
            "X-API-VERSION" : "v2.0.1",
            ]

        // token
//        if let token = JFUserModel.shareAccount()?.token {
//            headers["Authorization"] = "Bearer \(token)"
//            print("请求头加入了token", "Bearer \(token)")
//        }
        let token = "token"
        // uuid
//        if let uuid = JFObjcTools.uuidString() {
//            headers["X-DEVICE-ID"] = uuid
//            print("请求头加入了device", uuid)
//        }
        let uuid = "dfs"
        // 请求签名
        // 字典key排序
        var keys = [String]()
        if let parameters = parameters {
            for key in parameters.keys {
                keys.append(key)
            }
        }
        for key in headers.keys {
            keys.append(key)
        }
        keys = keys.sorted(by: {$0 < $1})

        // 拼接排序后的参数
        var jointParameters = ""
        for key in keys {
            if headers.keys.contains(key) {
                jointParameters += key
                jointParameters += "\(headers[key]!)"
            }
            if let parameters = parameters {
                if parameters.keys.contains(key) {
                    jointParameters += key
                    jointParameters += "\(parameters[key]!)"
                }
            }

        }
//        jointParameters += API_SECRET
        jointParameters += "qwrerryutyuyt"
        let md5Hex =  jointParameters.md5Data()!.map { String(format: "%02hhx", $0) }.joined().uppercased()

        // 算法 hex(md5(headers + parameters + secret))
        headers["X-SIGNATURE"] = md5Hex
        print("请求头加入了signature", md5Hex)

        return headers
    }

}

// MARK: - 普通get/post请求方法，可以根据自己的业务多封装一些通用请求方法
extension JFNetworkTools {

    /**
     GET请求

     - parameter APIString:  urlString
     - parameter parameters: 参数
     - parameter finished:   完成回调
     */
    func get(APIString: String, parameters: [String : Any]?, finished: @escaping NetworkFinished) {

        UIApplication.shared.isNetworkActivityIndicatorVisible = true
        afManager.request(APIString, parameters: parameters, headers: getHTTPHeaders(parameters: parameters)).responseJSON { (response) in
            self.handle(response: response, finished: finished)
        }
    }

    /**
     POST请求

     - parameter APIString:  urlString
     - parameter parameters: 参数
     - parameter finished:   完成回调
     */
    func post(APIString: String, parameters: [String : Any]?, finished: @escaping NetworkFinished) {

        UIApplication.shared.isNetworkActivityIndicatorVisible = true
        afManager.request(APIString, method: .post,parameters: parameters, headers: getHTTPHeaders(parameters: parameters)).responseJSON { (response) in
            self.handle(response: response, finished: finished)
        }
    }

    /// 处理响应结果
    ///
    /// - Parameters:
    ///   - response: 响应对象
    ///   - finished: 完成回调
    fileprivate func handle(response: DataResponse<Any>, finished: @escaping NetworkFinished) {
        UIApplication.shared.isNetworkActivityIndicatorVisible = false

        switch response.result {
        case .success(let value):

            print(response.request?.url ?? "", value)
            let json = JSON(value)
            if json["code"].intValue == 0 {
                finished(.success, json["data"], nil)
            } else if json["code"].intValue == 20104 {
                JFProgressHUD.dismiss()
                // 注销登录
                JFUserModel.logout()
                finished(.notLogin, nil, "请重新登录(\(json["code"].intValue))")
            } else {
                finished(.unusual, nil, json["message"].stringValue + "(\(json["code"].intValue))")
            }

        case .failure(let error):
            finished(.failure, nil, error.localizedDescription)
        }
    }

}

// MARK: - 简单json缓存 本来不应该放这里的，如果项目需要缓存，应该有自己的DAL(Data access layer)工具类。
extension JFNetworkTools {

    /**
     缓存json数据为指定json文件

     - parameter json:     JSON对象
     - parameter jsonPath: json文件路径
     */
    func saveJson(_ json: JSON, jsonPath: String) {
        do {
            if let json = json.rawString() {
                try json.write(toFile: jsonPath, atomically: true, encoding: String.Encoding.utf8)
                print("缓存数据成功", jsonPath)
            }
        } catch {
            print("缓存数据失败", jsonPath)
        }
    }

    /**
     删除指定文件

     - parameter jsonPath: 要删除的json文件路径
     */
    func removeJson(_ jsonPath: String) {
        let fileManager = FileManager.default
        if fileManager.fileExists(atPath: jsonPath) {
            do {
                try fileManager.removeItem(atPath: jsonPath)
                print("删除成功", jsonPath)
            } catch {
                print("删除失败", jsonPath)
            }
        }
    }

    /**
     获取缓存的json数据

     - parameter jsonPath: json文件路径

     - returns: JSON对象
     */
    func getJson(_ jsonPath: String) -> JSON? {
        if let data = try? Data(contentsOf: URL(fileURLWithPath: jsonPath)) {
            print("获取缓存数据成功", jsonPath)
            let json = JSON(data: data)
            return json
        }
        print("获取缓存数据失败", jsonPath)
        return nil
    }
}

// MARK: - 公共业务封装
extension JFNetworkTools {

    /// 检测是否能够签到
    func canCheckin(finished: @escaping (_ can: Bool) -> ()) {

        JFNetworkTools.shareNetworkTool.get(APIString: API_CHECKIN, parameters: nil) { (status, result, tipString) in
            switch status {
            case .success:
                isCanCheckin = result!["can_checkin"].boolValue
                finished(isCanCheckin)
            case .unusual:
                finished(false)
            case .notLogin:
                finished(false)
            case .failure:
                finished(false)
            }
        }

    }

    // 可以封装一些公用的业务接口.........
}

// MARK: - 网络工具方法
extension JFNetworkTools {

    /**
     获取当前网络状态

     - returns: 0未知 1WiFi 2WAN
     */
    func getCurrentNetworkState() -> Int {
        return Reachability.forInternetConnection().currentReachabilityStatus().rawValue
    }

    // 可以封装一些网络相关的工具方法......
}


```