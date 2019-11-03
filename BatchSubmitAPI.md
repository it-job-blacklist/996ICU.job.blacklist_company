### 批量提交API

省份和城市名称请前往[ [https://job.me88.top](https://job.me88.top) ]查证后再提交

#### 参数说明
- name：企业名称，这是必须的
- type：所在行业，如果不知道不确定可以使用`不详`代替
- province：所在省份，这是必须的
- city：所在城市，这是必须的
- address：详细地址，如果有最好填写，否则使用`不详`代替
- issue：存在问题，公司存在问题简要描述，这是必须的
- detail：详细描述，对存在问题详细描述，这是必须的，

*********

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
let url = "https://job.me88.top/data/add_backlist.php"
  
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

$url = "https://job.me88.top/data/add_backlist.php";
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

    var url = 'https://job.me88.top/data/add_backlist.php';
    $.post(url, {"data": JSON.stringify(companies)}, function(data){

        console.log(data.msg)
    }, 'json');
```

- Dart & Flutter

```dart
import 'dart:convert';
import 'dart:io';

try {        
        var companies = [
        {
          'name': '南京原谷信息科技有限公司',
          'type': '不详',
          'province': '江苏省',
          'city': '南京市',
          'address': '不详',
          'issue': '工资不写入劳动合同，扣发工资',
          'detail': '工资不写入劳动合同，扣发工资'
        },
        {
           'name': '南京橘子星球网络科技有限公司',
           'type': '不详',
            'province': '江苏省',
            'city': '南京市',
           'address': '不详',
           'issue': '恶意拖欠工资',
           'detail': '恶意拖欠工资'
        }
      ];

      var jsonstring = jsonEncode(companies);
      var httpClient = new HttpClient();
      var request = await httpClient.postUrl(Uri.https('blacklist.me99.cc', '/data/add_backlist.php', {'data':jsonstring}));
      var response = await request.close();
      if (response.statusCode == HttpStatus.ok) {

        var jsonResult = await response.transform(Utf8Decoder()).join();
        Map mapResult = jsonDecode(jsonResult);
        print(mapResult['msg']);
      } 
    } catch (exception) {
      print(exception);
    }
```