### 批量提交API

- Alamofire & Swift

```swift
import Alamofire

// 数组，用来保存公司数据
var companies: [[String: String]] = []
  
let company1 = [
    "name":"南京原谷信息科技有限公司",
    "type":"不详",
    "province":"江苏省",
    "city":"南京市",
    "address":"不详",
    "issue":"工资不写入劳动合同，扣发工资",
    "detail":"工资不写入劳动合同，扣发工资"
  ]
// 添加到数组
companies.append(company1)
  
let company2 = [
    "name":"南京橘子星球网络科技有限公司",
    "type":"不详",
    "province":"江苏省",
    "city":"南京市",
    "address":"不详",
    "issue":"恶意拖欠工资",
    "detail":"恶意拖欠工资"
  ]
// 添加到数组
companies.append(company2)
  
/*
 * 依此类推
 */
  
// 将公司数据转JSON
guard let jsonData = try? JSONSerialization.data(withJSONObject: companies, options: .prettyPrinted),
    let jsonString: String = String(data: jsonData , encoding: .utf8) else {
        
        print("转JSON异常")
        return
  }
  
let params: [String: Any] = ["data": jsonString]
let url = "https://blacklist.me99.cc/data/add_backlist.php"
  
request(url, method: .post, parameters: params)
    .responseJSON(completionHandler: { (response) in
        
        if let data = response.value as? [String: Any] {
            
            print(data["count"]!) // 记录数量
            print(data["msg"]!)
        }
        
        print(response.error ?? "")
})

```
