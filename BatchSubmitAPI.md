### 批量提交API

省份和城市名称请前往[ [https://blacklist.me99.cc](https://blacklist.me99.cc) ]查证后再提交

- Swift 5.2 & Alamofire

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
            
            print(data["msg"]!)
        }
        
        print(response.error ?? "")
})

```

- PHP

```php
$companies = array();

$company1 = array(
    'name' => '南京原谷信息科技有限公司',
    'type' => '不详',
    'province' => '江苏省',
    'city' => '南京市',
    'address' => '不详',
    'issue' => '工资不写入劳动合同，扣发工资',
    'detail' => '工资不写入劳动合同，扣发工资'
);
array_push($companies, $company1);

$company2 = array(
    'name' => '南京橘子星球网络科技有限公司',
    'type' => '不详',
    'province' => '江苏省',
    'city' => '南京市',
    'address' => '不详',
    'issue' => '恶意拖欠工资',
    'detail' => '恶意拖欠工资'
);
array_push($companies, $company2);

/*
 * 依此类推
 */

$jsonstring = json_encode($companies);
$data = http_build_query(array('data' => $jsonstring));

$options = array(
    'http' => array(
        'method' => 'POST',
        'header' => 'Content-type:application/x-www-form-urlencoded',
        'content' => $data,
        'timeout' => 30 // 超时时间（单位:s）
    )
);

$url = "https://blacklist.me99.cc/data/add_backlist.php";
$context = stream_context_create($options);
$result = file_get_contents($url, false, $context);

echo json_decode($result)->msg;
```
- JavaSript & jQuery

```javasript
var companies = [
        {
            name: '南京橘子星球网络科技有限公司',
            type: '不详',
            province: '江苏省',
            city: '南京市',
            address: '不详',
            issue: '恶意拖欠工资',
            detail: '恶意拖欠工资'
        },
        {
            name: '南京原谷信息科技有限公司',
            type: '不详',
            province: '江苏省',
            city: '南京市',
            address: '不详',
            issue: '工资不写入劳动合同，扣发工资',
            detail: '工资不写入劳动合同，扣发工资'

        }
    ];

    var url = 'https://blacklist.me99.cc/data/add_backlist.php';
    $.post(url, {"data": JSON.stringify(companies)}, function(data){

        console.log(data.msg)
    }, 'json');
```