# alipay-node-sdk 

> 支付宝新版App支付nodejs版sdk.

**Examples**


```js
var path = require('path');
var Alipay = require('../lib/alipay');

var outTradeId = Date.now().toString();


var ali = new Alipay({
    appId: '2016080300159077',
    notifyUrl: 'http://www.xxx.com/callback/alipay',
    rsaPrivate: path.resolve('./pem/sandbox_iobox_private.pem'),
    rsaPublic: path.resolve('./pem/sandbox_ali_public.pem'),
    sandbox: true,
    signType: 'RSA'
});

//生成支付参数供客户端使用
var params = ali.pay({
    subject: '测试商品',
    body: '测试商品描述',
    outTradeId: outTradeId,
    timeout: '10m',
    amount: '10.00',
    goodsType: '0'
});
console.log(params);



//查询交易状态
ali.query({
    outTradeId: outTradeId
}).then(function (ret) {
    console.log("***** ret.body=" + body);
    
    //签名校验
    var ok = ali.signVerify(ret.json());
});

//统一收单交易关闭接口
ali.close({
    outTradeId: outTradeId
}).then(function (ret) {
    console.log("***** ret.body=" + body);
});

//统一收单交易退款接口
ali.refund({
    outTradeId: outTradeId,
    operatorId: 'XX001',
    refundAmount: '2.01',
    refundReason: '退款'
}).then(function (ret) {
    console.log("***** ret.body=" + body);
});

//查询对账单下载地址
ali.billDownloadUrlQuery({
    billType: 'trade',
    billDate: '2017-03'
}).then(function (ret) {
    console.log("***** ret.body=" + body);
});

```


## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i alipay-node-sdk --save
```

