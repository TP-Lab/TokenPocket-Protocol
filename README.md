# TokenPocket Protocol

#### Version：v1.0

该协议可以用户从网页和第三方App拉起TokenPocket钱包做授权 转账等操作

This protocol can be used to call TokenPocket do some actions from page or app。
****
### 使用场景（How to use）

#### 扫码拉起TokenPocket （Scan qrcode call TokenPocket）

#### 页面拉起 ( Call from web page )
~~~
转账示例，其他操作类似(Token transfer demo)

<a href='tpoutside://pull.activity?param={"Protocol":"TokenPocket","version":"v1.0","blockchain":"eos","from":"aaaaaa123451","to":"cbzfb4a5s5zv","amount":"0.0001","contract":"eosio.token","symbol":"EOS","precision":"4","action":"transfer","memo":"test transfer from page"}'>Open TokenPocket to transfer eos</a><br/>
~~~

#### 独立App拉起 Call from app
- [App 拉起钱包操作( Call from app )](https://github.com/TP-Lab/Mobile-SDK)
****

### 操作（actions）
- [1 授权登陆 （Login）](#Login)
- [2 转账 （Token transfer）](#Transfer)
- [3 PushTransaction](#PushTransaction)
- [4 签名（Sign）](#Sign)


#### <a name='Login'></a> Login

- Parameters
~~~
{
    protocol	string   //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    blockchain  string   // wallet type(eos bos eth moac )
    wallet      string   // account name
    action      string   // neccessary here is login
    actionId    string   // optional   
    callbackUrl string   // optional
    expired	    string   //expire time in seconds
    memo	    string   // optional
}
~~~

- Success return data
~~~
{
   "sign": "SIG_K1_KZL9eR4cCQCJHpYHbh44yGrDqu4w8hHzQwb1xTk4Mcd4czqpw4jJUgg9DnWXzE3r",
   "timestamp": "1546613919", //in seconds
   "wallet": "eoseoseosacc", //account name
   "ref": "TokenPocket",
   "action":"login",
   "actionId":"ljsdjljdljf-xjlsdjfkj" //actionId from dapp
   "publickey": "EOS2TtWv19a9eYEQYB8NbGCM28nQNngWP4UcSjVYqtEz6kF7yCnPX",
   "permissions": ["active", "owner"],
   "result": 1
}
~~~

Cancel return data
~~~
{
   "action":"login",
   "actionId":"ljsdjljdljf-xjlsdjfkj" 
   "result": 0
}
~~~


#### <a name='Transfer'></a>转账（Token transfer）

- Parameters
~~~
{
    protocol    string   //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    action      string   // neccessary here is transfer
    actionId    string   // optional
    blockchain  string   //wallet type(eos bos eth moac )
    from        string   // optional
    to          string   // neccessary
    amount      number   // neccessary
    contract    string   // neccessary
    symbol      string   // neccessary
    precision   number   // neccessary
    memo        string   //optional		     
    expired	    string   // expire time in seconds
}
~~~


- Success return data
~~~
"ref": "TokenPocket",
"txID": "588c6797534d09e8e0b149c06c11bfd6ca7b96f0d4bba87700fffe7a87b0d988",
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"action":"transfer",
"actionId":"ljsdljf-xljlsdjfl" //from dapp
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~

- Cancel return data
~~~
"action":"transfer",
"actionId":"ljsdljf-xljlsdjfl" //from dapp
"result": 0
~~~


#### <a name='PushTransaction'></a>PushTransaction
- Parameters
~~~
    protocol    string  //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    action      string   // neccessary here is pushTransaction
    actionId    string   // optional 
    blockchain  string   //wallet type(eos bos eth moac )
    actions     string   //actions data
    memo    string       //optional
~~~

- Success return data
~~~
"ref": "TokenPocket",
"txID": "588c6797534d09e8e0b149c06c11bfd6ca7b96f0d4bba87700fffe7a87b0d988",
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"action":"pushTransaction",
"actionId":"ljsdljf-xljlsdjfl" 
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~

- Cancel return data
~~~
"action":"pushTransaction",
"actionId":"ljsdljf-xljlsdjfl"
"result": 0
~~~

#### <a name='Sign'></a>签名(Sign) (only version 0.6.5 or higher support this api)
- Parameters
~~~
    protocol    string  //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    action      string   // neccessary here is sign
    actionId    string   // optional 
    blockchain  string   //wallet type(eos bos eth moac )
    message     string   //message to sign
    memo    string       //optional
~~~

- Success return data
~~~
"ref": "TokenPocket",
"sign": "SIG_K1_JXLSDFLJLSKDJFKJ", //signed data
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"action":"pushTransaction",
"actionId":"ljsdljf-xljlsdjfl" 
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~

- Cancel return data
~~~
"action":"sign",
"actionId":"ljsdljf-xljlsdjfl"
"result": 0
~~~
