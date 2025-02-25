## :world_map: 使用教程

【拉库】

    ql repo https://github.com/Yiov/wool.git "" "COOKIE"

## :loudspeaker: 关于小号

建议：玩毛不要用自己常用手机，不然垃圾短信一堆

* 移动：和多号app（5元/月）
* 联通：沃小号app（5元/月）
* 联通&腾讯：微小号（小程序 10元/月）
* 联通&阿里：阿里小号app（已下线，续期的可以继续用）
* 电信：天翼小号app（已下线）


## :gear: 在线请求头转JSON

我把我已知的都列举出来了，也欢迎投更好用的

* [ToolTT](https://tooltt.com/header2json/)「好像不好用了」

* [uutool](https://uutool.cn/header2json/)

* [wejson](https://wejson.cn/header2json/)




## :fire: 2022-3-18更新


### 海尔智家 haier.js

cron 未知

<details>
<summary>食用步骤：</summary>
<br />
海尔智家app-手机号登录-设置登录密码-退出登录，然后选择密码登录，抓POST包

https://zj.haier.net/oauthserver/account/v2/login

请求头转换成json格式才可以用

    export haierhd='{"appVersion":"7.9.0"***"okhttp/4.9.3"}'

body复制出来就可以了

    export haierbody='{"username":***"phoneType":"Mi 10"}'

</details>

    // 2022-3-18根据脚本完成任务来看，还没发现是做的啥任务



## 2022-3-17更新


### 源火星球 yhxq.js

cron 13 0-23/4 * * *

<details>
<summary>食用步骤：</summary>
<br />
注册好后下载app并登录

地址：http://reg.yuanhuoxingqiu.com/

抓get包，登录app即可获取数据，只有Authorization值就行,删掉Bearer和空格，只要纯数字的组合

http://api.yuanhuojisuban.com/user/account

由于依赖每次拉库会被覆盖，请在脚本同目录手动新建空白文件`raw_master_yhxq_variable.js`

复制下列内容，删掉括号和中文字符，填上token和UA变量后，保存即可

```
module.exports = {"code":200,"yhxq_variable_data":{
    "config":[{
        "url":"https://gitee.com/soy-tool/app-script/raw/master/app_yhxq.js",
        "update":false,
        "notice":true
    }],
    "user_data":[{
        "token":"请求头上的Authorization值",
        "Withdrawal":false,
        "Withdrawal_Time":8,
        "Feed":false,
        "UA":"请求头的User-Agent值选填"
    }
    
]}}
```

</details>

    // 2022-3-17新增了依赖文件,请重新配置




### 快手极速版 ksjsb.js (leaf版)

cron 38 7-22 * * * (每天15次)

<details>
<summary>食用步骤：</summary>
<br />
抓POST包，进入积分换好礼页面即可获取数据，只要有Cookie就行

https://api.kuaishouzt.com/rest/zt/appsupport/yoda/accelerate/info

把Cookie中的kuaishou.api_st复制出来，包括分号，多账号换行隔开

    export ksjsbCookie='kuaishou.api_st=***;'

默认每天0点自动兑换金币，15点提现，要改的话把提现时间填到变量，不想提现设置成99

    export ksjsbWithdrawTime='15'

默认从高到低提现，固定金额用以下变量

    export ksjsbCash='100'

默认提现时间会触发通知，可以把ksjsbNotify设置成2，每次运行都通知；为0，则不通知

    export ksjsbNotify='0'

</details>

    // 2022-3-17修复绑定提现问题，抽奖无金币也能看视频bug，减低黑号风险



### 快手 ks.js

cron 22 10-20 * * *

<details>
<summary>食用步骤：</summary>
<br />
普通版的快手，非极速版，CK可以通用

注意现在多一个did的设备参数，必填！多账户@隔开

> 由于我IOS端找不到入口，我就用的极速版抓的CK里提取了did数值，粘贴在后面，任务一样跑

    export ksCookie='kuaishou.api_st=***;did=***;'

默认每天0点自动兑换金币，14点提现，不想提现设置成99

    export ksWithdrawTime='14'

默认提现2块，要改的话把提现金额填到变量。如提现失败，手动接验证码提现一次，自动检测绑定了微信还是支付宝提现账号，都绑定了的话默认提现到支付宝

>手动提现入口：头像-更多-我的钱包-天降红包提现，默认从高到低提现，固定金额用以下变量

    export ksCash='100'

默认提现时间会触发通知，可以把ksjsbNotify设置成2，每次运行都通知；为0，则不通知

    export ksNotify='0'

</details>

    // 2022-3-9 修复不做直播任务，更换提现接口





## 2022-3-12更新


### 酷狗音乐 kgyy.js（安卓）

cron 一天一次即可

<details>
<summary>食用步骤：</summary>
<br />
抓GET包，我的-任务中心，需带有token、uuid、mid、userid、dfid的整段链接

https://gateway.kugou.com/mstc/musicsymbol/v1/user/info?userid=***"

    export kgyy="https://gateway.kugou.com/mstc/musicsymbol/v1/user/info?userid=***"

</details>

    // 2022-3-12 每天7毛






## 2022-3-6更新

心态好一点，别总觉得毛小，抖音/快手大公司也没让人薅的飞起啊，毛小可以账号多啊，只要你爱折腾，别老等着喂饭




### ~趣躺赚 wx_qtz.js~

cron 一天3-4次

<details>
<summary>食用步骤：</summary>
<br />
微信小程序，新人直领0.3

抓POST包，只要请求头包含openid、userToken、userKey、apmat的值，参考链接

https://wx.17u.cn/platformflowpool/homepage/info

复制全部请求头，使用顶部链接把请求头转换成json格式

    export qtzhd='{"Host":"wx.17u.cn",***"html"}'

</details>

    //报错了，有点难修







### 饿了么吃货豆 elm.js

Cron 5 12,18 * * * 

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进APP-我的-赚吃货豆，即可获取数据

https://h5.ele.me/svip/task-list

只要cookie，不要cookie2，复制出来包括分号，多账户@隔开

    export elmck='SID=***'


说明：以上数据由IOS设备抓取，安卓机用Alook浏览器或者用M浏览器，UA设置为

    Mozilla/5.0 (iPhone; CPU iPhone OS 8_3 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12F70 Safari/600.1.4


然后打开h5.ele.me，手机号+验证码登录后，抓的ck就可以用了。第一个参数是__wpk******，最后一个参数是x5check_ele=******

</details>

    // 2022-3-6修复报错




### 微娱推客 wytk.js

cron 26/5 10,13 * * *(一天12-15次)

<details>
<summary>食用步骤：</summary>
<br />
微信打开注册，然后根据提示下载安装并登陆

https://lm.wy.run/index/user/wechatLogin

抓POST包，签到即可获取toekn值

> 我的-设置-复制appkey-返回 活动-立即签到-保存图片-微信扫码 登陆-签到-输入appkey-再次点签到，等视频完结即可

https://lm.wy.run/api/sign/index


    export soy_wytk_data="token&UA"

</details>

    // 2022-3-6有可能活不久，不清楚，我放弃了

    // 现在分红只有靠积分，添加客服wwy6762拉群卖积分，而积分交易需要2元实名认证，一不小心就反撸





## 2022-3-2更新

有点忙，几天没看了，又来整理下，撸个毛还要学很多





### 渤海宣传员 wx_bhxcy.js

cron 40 10 * * *

<details>
<summary>食用步骤：</summary>
<br />
微信小程序，需要注册，电子账户看你们，反正我不注册

抓POST包，点天天签到 最高领88元红包，拆，即可获取数据

https://api.yd.ihaoqu.com/?r=api2&apiAction=SignIn

    export bhxcytoken='uid=***&token=***&signure=***'

</details>

    //2022-3-2签到兑换京东E卡




### 康师傅畅饮社wx_ksfcys.js

cron 42 9,18 * * *

<details>
<summary>食用步骤：</summary>
<br />
微信小程序，注册送200积分

抓GET包，点我的即可获取数据，多账号@隔开

https://club.biqr.cn/api/member/getMemberInfo

    export ksfcysToken='***'

默认不会抽奖，如果需要50积分抽奖，请设置变量ksfcysDraw为true

    export ksfcysDraw="true"

</details>

    // 2022-3-2积分可换E卡，重进小程序有可能会挤掉线，请重新抓








## 2022-2-22更新



### 悟空浏览器 wkllq.js

cron 0-59/15 0-1,6-15,19-23 * * *

<details>
<summary>食用步骤：</summary>
<br />
打开app，即可抓取数据，没有这条的任意host里有值也可

https://api5-normal-lf.toutiaoapi.com/ugc/business_alliance/user_info/

我们需要3个值device_id、x-tt-token、sessionid

> 现在不是用export变量的了，需要添加soy_variable_data.js依赖

在wkllq.js脚本同目录新建soy_variable_data.js文件，把下面的代码粘贴进去

```
module.exports = {"code":200, 
"variable_data":{ 
"wkllq":[{ //悟空浏览器
    "device_id":"409***", //链接上找device_id值
    "x-tt-token":"00b***-1.0.1", //请求头的值
    "sessionid":"b9c***"} //请求头cookie上的值
]
}}
```
修改成自己的变量保存，就可以跑脚本了

多账号模板演示，英文逗号,后跟一个{}里面填数据

```
module.exports = {"code":200, 
"variable_data":{ 
"wkllq":[{ //悟空浏览器
    "device_id":"账号1的device_id值",
    "x-tt-token":"账号1的x-tt-token值",
    "sessionid":"账号1的sessionid值"},{
    "device_id":"账号2的device_id值",
    "x-tt-token":"账号2的x-tt-token值",
    "sessionid":"账号2的sessionid值"} 
]
}}
```

</details>

    //2022-2-22更新：-

    另：脚本默认跑作者邀请码,如果不想就自行去绑定邀请码后在跑脚本



### 快音 kyin.js

cron 0-59/10 6-20 * * *

<details>
<summary>食用步骤：</summary>
<br />

退出登录-开抓包-微信登录成功后即可获取数据
https://api.kaixinyf.cn/passport/UnionLogin

> device-id值在请求头里面找

> access-token值和refresh_token值在响应的set-cookie里面找，注意只要token的value值

同样的需要同目录有soy_variable_data.js文件，代码参考如下

```
module.exports = {"code":200, 
"variable_data":{ 
"wkllq":[//这里是悟空浏览器的数据，自己别删了
],
"kyin":[//快音
"device-id值&access-token值&refresh_token值",//这是第1个账号
"",//多账号逗号换行
] 
```
</details>

    //2022-2-22更新：报错的重新拉


### 腾讯自选股 txstock.js

cron 35 11,16 * * *

<details>
<summary>食用步骤：</summary>
<br />
注意：APP和公众号都要抓，多账号用#隔开


APP-头像-右上角金币-获取金币，抓get包

https://wzq.tenpay.com/cgi-bin/activity_task_daily.fcgi?


抓到的连接填在下方

    export TxStockAppUrl='https://wzq.ten....#https://wzq.ten....'


请求头header，转换一下格式 https://tooltt.com/header2json/

    export TxStockAppHeader='{"Host":"...","Accept":"..."}#{"Host":"...","Accept":"..."}'



自选股公众号-右下角好福利-福利中心，抓get包

https://wzq.tenpay.com/cgi-bin/activity_task_daily.fcgi?

请求头header，转换一下格式 https://tooltt.com/header2json/

    export TxStockWxHeader='{"Host":"...","Accept":"..."}#{"Host":"...","Accept":"..."}'



提现变量，0代表不提现，1代表提现1元，5代表提现5元

    export TxStockCash='1'

新手变量，0代表不做新手任务，1代表做新手任务

    export TxStockNewbie='1'

分享变量，0代表不做分享互助，1代表做分享互助

    export TxStockHelp='0'

互助变量，0代表不帮助其他用户，否则填用户，用@或者#隔开

    export TxStockHelpOrder='0'


</details>

    // 新增一个新版的，老版能跑的请禁用！！！
    新抓包的用new版，不然可能报错，老版的不用管






## 2022-1-12更新


### 九章头条 jztt.js

Cron 15 0,6-23 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进app-任务，抓取token值

https://api.st615.com/v2/user/info

    export jzttToken="***"

自定义阅读次数，默认每次阅读3篇文章

    export jzttReadNum="***"

提现金额，按门槛自动提现，从大到小，默认顺序5元，2元和0.3元

    export jzttWithdrawLimit="***"

</details>

    // 2022-1-12更新：修复文章、提现


### 滴滴果园 dd_fruit.js

cron 10 0,8,12,18 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进app-5天种水果，浇一次水，搜water

把请求主题中的 token 值复制出来，多账户用,号(英文)隔开

    export DD_TOKEN='token1,token2'

拉库了的记得把dd_cookie.js从运行列表中禁用

</details>

    // 2022-1-12更新：新增转盘抽奖，自动使用背包道具


### 滴滴果园自动收水 dd_bucketWater.js

cron */30 * * * *

用上面的token即可




## 2022-1-8更新


### 闪辆 sl.js

cron 5 0 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进app-来玩获取url即可

https://newvideo.autohome.com.cn/openapi/activity-api/switch/get_user_switch_info

    export slurl="https://newvideo.autohome.com.cn/openapi/activity-api/switch/get_user_switch_info?_appid=***"

</details>

    // 不知道是我黑号了，看视频没有加积分，手动可以







## 2022-1-3更新



### 快手极速版 ks_js.js

Cron 11 8 * * *（一天一次即可，仅供参考）

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进app-点红包进去，获取Cookie

https://nebula.kuaishou.com/rest/n/nebula/activity/earn/overview/basicInfo

    export kshd="Cookie1@Cookie2"

0为不自动提现,0.3为提现3毛，默认自动提现3元

    export kscash="3"

提现时间变量，默认20点提现和金币兑换

    export kstxtime=""

通知变量，默认开启，2为关闭通知

    export kstz=""

</details>

    // 2022-1-3更新：修复报错bug 注意：不刷视频，只挂脚本容易黑号！




### 高佣金(更名：佣金帝) gyj.js

cron 随意，一天一次即可

<details>
<summary>食用步骤：</summary>
<br />
抓包，进APP-签到赚钱，即可获取

https://client.atomsh.com/e00-bee-client/client/act/getGoldCount

复制token值，添加到环境变量
    
    export gyjhd='token1@token2@token3'

</details>

    // 记得金币要手动去商城兑换，然后再提现




## 2021-12-28更新


### 中青看点 新增 看看赚肥皂版 zq_kkz_fz.js

教程在文件内，注意CryptoJS.js文件是依赖文件，别删了，禁用就行






## 2021-12-26更新


### 链萌优选 小程序 wx_lmyx.js

cron 3 0,9,17 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓token和version值，打开APP即可获取，多账户@隔开

https://www.lmyx.shop/web/index.php?store_id=1&r=api/user/index&access_token=***&_version=2.8.9&_platform=wx

    export soy_lmyx_data="token值&2.8.9&支付宝名&支付宝账号&UA"

不开小号给大号送通行证，分红很少，提现基本不够，可以先只使用前2个变量跑，金额多了再加变量上去

</details>

    // 202-12-26新增：提现变量，需要提供ZFB信息





## 2021-12月


### 中国联通 Chinaunicom.js

Cron 5 9,11,18 * * *

<details>
<summary>食用步骤：</summary>
<br />

功能：签到，签到任务，多账号用 @ 分隔

    export ltphone="" #手机号

    export ltpwd="" #登录6位密码

</details>

    // 跑的是app的任务，我至今未打开





### 得间小说 djxs.js

Cron 0 6-23 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进app-福利-看视频，获取数据

https://dj.palmestore.com/zycl/gold/receive


    export djxsCookie='Cookie1@Cookie2'

    export djxsReferer='Referer1@Referer2'

</details>

    // 提现比较蛋疼，需要同时满足当日阅读120分钟、签到10天、看视频3次






### 返利购(更名：利淘优选) flg.js

cron 0,30 8 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓POST包，进APP-我的-签到，即可获取数据

https://api.flgflg.com/htmmall/api/gold/finishedVideoNum

    export flgReferer='抓取的Referer1@抓取的Referer2'

</details>

    // 是我玩过返利内最良心送钱的app



### 返利好省 flhs.js

cron 0 8-23 * * *

<details>
<summary>食用步骤：</summary>
<br />
抓包，进APP-现金福利，即可获取

https://api.uutequan.com/v1/welfare/page

随便哪一个Cookie应该都行


    export flhsCookie='Cookie1@Cookie2'

</details>

    // 扣就一个字





### 机场签到 jcCheck.js

cron 随意，一天一次即可

请第1次拉完库，复制一份到scripts目录，不然每次都会覆盖！

例：
在Yiov_wool/jcCheck.js，复制粘贴到scripts目录，青龙task jcCheck.js，原本的禁用






### 快手果园 ks_fruit.js

Cron 随意，一天一次

<details>
<summary>食用步骤：</summary>
<br />
抓get包，进app-左上角三横-快手果园，获取Cookie

https://ug-fission.kuaishou.com/rest/n/darwin/orchard/water/watering

    export KS_COOKIE='client_key=***;did=***;kuaishou.api_st=***;ud=***;ver=***;'

</details>

    // 默认会助力作者，介意勿玩，代码加密的




### 美团赚米粒 meituan.js

Cron 5 11 * * *

<details>
<summary>食用步骤：</summary>
<br />
进美团官网：https://www.meituan.com

F12审查元素-登录账号-工作台选 网络，找到www.meituan.com的封包，Cookie中找到token值，复制出来

    export mtTk='这里填token值，不带分号'

可关闭神券膨胀，不想关，删除变量

    export sjpz="false"

</details>

    // 米粒有啥用，我还没进app看过





### NTF博物馆

Cron 45 18 * * *

<details>
<summary>食用步骤：</summary>
<br />

下载：http://nftwatches.net

登录APP即可获取token

http://service.nftbwg.net/home/view

视频code2，需要点门票收益获取，广告一直会加载出问题，反复进，有个60几秒的广告就是了

http://mobads.baidu.com/cpro/ui/mads.php?code2=***

注意:提示视频缓存失败，抓不到code值，关掉APP重来。即便抓到了，也不一定能完成,app自身的原因

    export soy_NFT_data="token&视频code2的值"

</details>

    // token有效期好像只有半月，还是几周的，失效记得抓，攒够200万就可以提现了





### 沃邮箱 公众号 wx_wyx.js

cron 11 10 * * *

<details>
<summary>食用步骤：</summary>
<br />
关注公众号:联通沃邮箱-进入邮箱，不知道密码的重置

重置密码：https://user.mail.wo.cn/m/reset?mobile


抓Get包，福利中心-签到领话费，多账号@隔开

https://nyan.mail.wo.cn/cn/sign/index/index?mobile=***&userName=&openId=***

    export soy_wyx_data="手机号#密码#抓包链接https://nyan.mail.wo.cn/cn/sign/index/index?mobile=***&userName=&openId=***"
    
    export soy_wyx_UA="Mozilla/5.0***"

</details>

    // 目前公众号系统在维护，跑不动




### 小米刷步 xmsb.py

cron 随意，一天一次即可

<details>
<summary>食用步骤：</summary>
<br />
请第1次拉完库，复制一份到scripts目录，不然每次都会覆盖！

例：
在Yiov_wool/xmsb.py，复制粘贴到scripts目录，青龙task xmsb.py，原本的禁用


### 注册好小米运动账号，绑定第三方微信

手动修改py里面的数据

账号user = "138****8888"

密码passwd = "******"

修改固定步数值，留空为随机步数

step = "23333"

修改随机范围步数值，与固定步数二选一改

step = str(random.randint(20000, 21000))

</details>

    // 推送通知好像是微信企业微信，我改过其他推送但也没成功，算了


### 萤石云视频 ysy.js

cron 随意，一天一次即可

<details>
<summary>食用步骤：</summary>
<br />
抓3个数据，重新登录！重新登录才可以抓到数据

https://api.ys7.com/v3/users/login/v2

把header转成JSON：https://tooltt.com/header2json/

    export ysyhd=''

body查看表单即可获取

    export ysybody='account=188********'


CK获取

https://api.ys7.com/v3/integral/yd/getUserOpenBoxCd

    export cookie='"ASG_DisplayName=***"'


提现body 查看表单获取数据

https://api.ys7.com/v3/integral/yd/pay

    export txbody='payCode=101006&receiverType=2&receiverId=2********'

</details>

    // 要攒到1块钱是个无比漫长的过程


### 亿享云 yxyapp.js


cron 随意，一天一次即可

<details>
<summary>食用步骤：</summary>
<br />
注册地址：https://ystzwz.com/h6/#/

就是个网页，没有APP的

    export yxyPhone='手机号#密码'

</details>

    // 不知道靠不靠谱，反正一直活着


## 晶彩看点 jckd

文件内有教程



## 水果天气 jctq

文件内有教程









## :email: 特别鸣谢:

* [@whyour](https://github.com/whyour/qinglong)「青龙」
* [@xl2101200](https://github.com/xl2101200/-/)「Tom」
* [@YaphetS0903](https://github.com/YaphetS0903/JStest)「YaphetS」
* [@WindFgg](https://github.com/WindFgg/QuantumultX_Conf/)「WindFgg」
* [@gossh520](https://gitee.com/gossh520/script/)「gossh520」
* [@LubooC](https://gitee.com/xiecoll/radish-script)「萝卜」
* [@leafxcy](https://github.com/leafxcy/JavaScript)「leaf」
* [@shaolin-kongfu](https://github.com/shaolin-kongfu/js_scripts)「少林大佬」
* [@liuqi6968](https://github.com/liuqi6968/-/)「liuqi6968」
* [@ziye888](https://github.com/ziye888/JavaScript)「ziye」
* [@soy](https://gitee.com/soy-tool/app-script)「soy」
* [@passerby-b](https://github.com/passerby-b/didi_fruit)「passerby-b」

