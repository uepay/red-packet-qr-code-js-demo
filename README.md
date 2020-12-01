# red-packet-qr-code-js-demo
##### Uepay钱支付案例
##### 开发环境：HTML + JS
##### uepa钱包SDK：uepay_jssdk.js

## 安装
1. git clone 代码到本地
2. 将html文件拖到浏览器或者部署到服务器

## 实例使用方法
步骤：1、app扫描H5 URL 生产的二维码。
2、进入H5页面，点击“在线支付”按钮。

分别执行以下命令
1. `git clone https://github.com/uepay/red-packet-qr-code-js-demo.git`

## 文件目录结构
```
index.html     --- sdk调用例子（判断是否为uepay内核后直接唤醒支付）
index.tp.html    --- sdk调用例子（输入金额点击支付，判断是否为uepay内核后直接唤醒支付）
uepay-1.2.0.js    --- uepay钱包支付SDK
README.md    --- 说明文档
```

## 注意：必須在UePay錢包內置瀏覽器（WebView）中使用。

## uepay钱包接口
下载相应的文件，将uepay-1.2.0.js文件放在项目下，便于引用 ```<script type="text/javascript" src="./uepay_jssdk.js"></script>```

1、获取版本号
```
const agent = UePayJsApi.getUserAgent();    // 获取当前浏览代理头
var serverSide = agent.UePay;      // 服務端版本
var clientSide = agent.UePayClient;    // 客戶端版本
```

2、判断当前是否为钱包内核
```
const isUePay = UePayJsApi.isUePayApp();    // true为UePay钱包内核，false为非UePay钱包内核
```

 ```
 
 4、喚醒APP支付功能。

        UePayJsApi.payment({
            "appId": "", 分配给商户的
            "timeStamp": '',时间戳
            "nonceStr": "", 由服务器生产的随机串,用于验证前后端交互的一致性
            "prepayid": "", 预支付订单的传递订单号
            "signType": "",签名散列算法，现在固定为'MD5'
            "paySign": "",验签参数
            callback: function (res) {
               支付结果回调函数，支付成功res返回{'ret_code':'00','ret_msg':'success'}JOSN字符串，支付失败res返回{'ret_code':'01','ret_msg':'failed'},
               取消支付res返回{'ret_code':'02','ret_msg':'cancel'}JOSN字符串。
            }



 5、用於關閉當前瀏覽器（WebView）窗口

        UePayJsApi.closeWindow({
            callback: function (res) {
               // 成功
            }
 
        })


6、獲取用戶當前的位置信息

         UePayJsApi.getLocation({
            "type": "", // 默认为wgs84的gps坐标
            callback: function (res) {
              {'latitude':'表示纬度，浮点数，范围为90 ~ -90','longitude':'表示经度，浮点数，范围为180 ~ -180'，'speed','表示速度，以米/每秒计','accuracy':'表示位置精度'}JOSN字符串
             
            }

        })

7.打開第三方地圖軟件，進行導航路徑規劃。目前包含：高德地圖、百度地圖、騰訊地圖。

        UePayJsApi.openLocation({
            "latitude": "",     // (必填)纬度，浮点数，范围为90 ~ -90
            "longitude": "",     // (必填)经度，浮点数，范围为180 ~ -180。
            "name": "",      // (必填)位置名称
            "address": "" ,  // (可选)地址详细说明
            callback: function (res) {
             //成功
             
            }

        })


8.UePay錢包APP的掃一掃功能

        UePayJsApi.scanCode({
            "needResult": 0 必填)默认为0，扫描结果由UePay处理，1 则直接返回扫描结
            callback: function (res) {
             //成功
             
            }

        }) 

