# TokenPocket Protocol

#### Version：v1.0

该协议可以用于从网页和第三方App拉起TokenPocket钱包做授权 转账等操作

This protocol can be used to call TokenPocket do some actions from page or app。
****
### 使用场景（How to use）

#### 扫码拉起TokenPocket （Scan qrcode call TokenPocket）

#### 页面拉起 ( Call from web page )
- Scheme：tpoutside://pull.activity?param={}
~~~
转账示例，其他操作类似(Token transfer demo)

<a href='tpoutside://pull.activity?param={"Protocol":"TokenPocket","version":"v1.0","blockchain":"eos","from":"aaaaaa123451","to":"cbzfb4a5s5zv","amount":"0.0001","contract":"eosio.token","symbol":"EOS","precision":"4","action":"transfer","memo":"test transfer from page"}'>Open TokenPocket to transfer eos</a><br/>
~~~

#### 独立App拉起 ( Call from app )
第三方App可以拉起TokenPocket执行签名，转账等操作。TP sdk还支持内嵌钱包，可以实现对于特定操作，第三方App不需要拉起钱包，直接在应用内部完成，体验更为流畅，具体使用请参照：[https://github.com/TP-Lab/Mobile-SDK](https://github.com/TP-Lab/Mobile-SDK)

Third-party apps can execute signatures, transfers, and etc actions by pull up the TokenPocket. TP SDK also supports built-in wallets that can execute specific actions without leaving the app, which provides a better user experience. Please check it for the details:[https://github.com/TP-Lab/Mobile-SDK](https://github.com/TP-Lab/Mobile-SDK)


#### Dapp 浏览器打开url ( Call TokenPocket to open url with Dapp browser)
- Scheme:tpdapp://open?params={}
~~~
<a href='tpdapp://open?params={"url": "https://dapp.mytokenpocket.vip/referendum/index.html#/", "chain": "EOS", "source":"xxx"}'>Open url with TokenPocket</a>
~~~
****

### 通用操作（common actions）
- [1 授权登陆 （Login）](#Login)
- [2 转账 （Token transfer）](#Transfer)
- [3 PushTransaction](#PushTransaction)
- [4 签名（Sign）](#Sign)
- [5 Dapp 浏览器打开url （Dapp browser open url）](#DappBrowser)
### 内置钱包操作
- [1 初始化SDK（init sdk）](#initSDK)
- [2 设置节点信息（set blockchain info）](#setBlockChain)
- [3 设置插件信息（set pulugin info）](#Auth)
- [4 设置加密seed（set seed to protect data）](#setSeed)
- [5 修改加密seed（modify seed）](#modifySeed)
- [6 获取已授权账号信息（get authed accounts）](#getAccounts)
- [7 检查权限是否存在（check permission bind to account）](#isPermExist)
- [8 检查权限是否link到action（check action bind to permission）](#isPermLinkAction)
- [9 清除本地授权（clearAuth）](#clearAuth)


#### <a name='Login'></a> Login

- Parameters
~~~
{
    protocol  string   //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    blockchain  string   // wallet type(eos bos eth moac )
    wallet      string   // account name
    action      string   // neccessary here is login
    actionId    string   // optional   
    callbackUrl string   // optional
    expired     string   //expire time in seconds
    memo      string   // optional
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
    expired     string   // expire time in seconds
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

#### <a name='DappBrowser'></a>Dapp 浏览器打开url (Dapp browser open url)
- Parameters
~~~
"url": "https://dapp.mytokenpocket.vip/referendum/index.html#/",
"chain": "EOS", 
"source":"xxx"
~~~

#### <a name='initSDK'></a>初始化sdk (Init SDK)
~~~
TPManager.initSDK(Context context);
~~~

#### <a name='setBlockChain'></a>设置blockchain 信息 (Set blockchain info)
~~~
TPManager.getInstance().setBlockChain(Context context, NetTypeEnum netType, String nodeUrl);
~~~

#### <a name='setAppPluginNode'></a>设置插件信息 (Set plugin info)
~~~
TPManager.getInstance().setAppPluginNode(Context context, String pluginUrl);
~~~

#### <a name='setSeed'></a>设置seed (Set seed to protect data)
~~~
TPManager.getInstance().setSeed(Context context, String seed)
~~~

#### <a name='modifySeed'></a>修改seed (Modify seed)

~~~
TPManager.getInstance().modifySeed(Context context, String oldSeed, String newSeed)；
~~~

#### <a name='getAccounts'></a>获取已授权账号信息（get authed accounts
~~~
TPManager.getInstance().getAccounts(Context context)；
~~~

#### <a name='isPermExisted'></a>检查权限是否存在（check permission bind to account）
~~~
TPManager.getInstance()isPermExisted(Context context, String account, String perm, final TPListener listener);
~~~

#### <a name='isPermLinkAction'></a>检查权限是否link到action（check action bind to permission)
~~~
TPManager.getInstance().isPermiLinkAction(Context context, String account, String perm, List<Permission.LinkAction> actions,
                                  final TPListener listener);
~~~

#### <a name='clearAuth'></a>清除本地授权（clearAuth）
~~~
TPManager.getInstance().clearAuth(Context context, String account);
~~~

