# wx-jssdk-sign
微信网页开发，接入微信JS-SDK。
1.微信分享SDK
在需要调用JS接口的页面引入如下JS文件，（支持https）：http://res.wx.qq.com/open/js/jweixin-1.0.0.js 如需使用摇一摇周边功能，请引入 http://res.wx.qq.com/open/js/jweixin-1.1.0.js

获取access_token，access_token是公众号的全局唯一接口调用凭据，公众号调用各接口时都需使用access_token。

发送get请求，地址：https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET(APPID,APPSECRET 怎么来的在准备步骤已经说明)

获取jsapi_ticket，jsapi_ticket是公众号用于调用微信JS接口的临时票据。

发送get请求，地址：https://api.weixin.qq.com/cgi-bin/ticket/getticket?access_token=ACCESS_TOKEN&type=jsapi (ACCESS_TOKEN 第1步已经获取到了)

验证签名，算法请查看源文件。

调用

  wx.config({
    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
    appId: '', // 必填，公众号的唯一标识
    timestamp: , // 必填，生成签名的时间戳
    nonceStr: '', // 必填，生成签名的随机串
    signature: '',// 必填，签名，见附录1
    jsApiList: ['onMenuShareTimeline', 'onMenuShareAppMessage', 'onMenuShareQQ', 'onMenuShareWeibo', 'onMenuShareQZone'] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2
});
分享回调
wx.ready(function(){
    //分享到朋友圈
    wx.onMenuShareTimeline({
        title: shareInfo.title,
        link: shareInfo.link,
        imgUrl: shareInfo.imgUrl,
        success: function() {

        },
        cancel: function() {

        }
    });
    //分享给朋友
    wx.onMenuShareAppMessage({
        title: shareInfo.title,
        desc: shareInfo.desc,
        link: shareInfo.link,
        imgUrl: shareInfo.imgUrl,
        success: function() {

        },
        cancel: function() {

        }
    });
)}
