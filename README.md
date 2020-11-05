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
uepay_jssdk.js    --- uepay钱包支付SDK
README.md    --- 说明文档
```

## uepay钱包接口
下载相应的文件，将uepay_jssdk.js文件放在项目下，便于引用 ```<script type="text/javascript" src="./uepay_jssdk.js"></script>```

1、获取版本号
```
const agent = UePay.getUserAgent();    // 获取当前浏览代理头
var serverSide = agent.UePay;      // 服務端版本
var clientSide = agent.UePayClient;    // 客戶端版本
```

2、判断当前是否为钱包内核
```
const isUePay = UePay.isUePayApp();    // true为UePay钱包内核，false为非UePay钱包内核
```

3、异步方法用于注册被监听的全局文件准备就绪事件
```
const isUePay = UePay.onReady();
/**
 * (uePay) => {
 *     uePay && uePay.payment();
 * }
 */
 ```
 
 4、实例化UePayJsApi并发起支付
 ```
var paySdk = UePay.build(function(res) {});
paySdk.payment(req);
paySdk.getCurrentLocation(req);   獲取當前地址， req默認為{type: 'wgs84'}
paySdk.sendShareReq(req);         用於喚醒原生APP的分享功能，目前包括：微信對話和微信朋友圈 
paySdk.closeWindow(req);          關閉內置瀏覽器窗口
paySdk.openLocation(req);         打開地圖
paySdk.scanCode(req);             (必填)默认为0，扫描结果由UePay处理，当needResult 为 1 时，扫码返回的结果

```
build里面参数为支付结果回调函数，支付成功res返回{'ret_code':'complete','ret_msg':'successful'}JOSN字符串，支付失败res返回{'ret_code':'fail','ret_msg':'cancel'}JOSN字符串。


 `req`为支付信息参数对象時，结果为appId（分配给商户的）、timeStamp（时间戳）、nonceStr（由服务器生产的随机串，用于验证前后端交互的一致性）、prepayid（预支付订单的传递订单号）、signType（签名散列算法，现在固定为'MD5'）、paySign（验签参数）

`req`为微信分享參數對象時，结果为isFriend（false:为聊天列表，true:为朋友圈）、type（1:为普通链接方式，image为链接的头像，2:为大图分享方式，image为大图的链接）、content（內容描述）、title(標題)、image（分享鏈接縮略圖）、platform（"wechat" 分享平台（目前只支持微信））

`req`为打開地圖時，结果为 latitude((必填)纬度，浮点数，范围为90 ~ -90)、longitude((必填)经度，浮点数，范围为180 ~ -180)、name（(必填)位置名称）、address（(可选)地址详细说明）
