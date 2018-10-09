###由于小程序不支持cookie
```js
	wx.request({
      url: 'http://47.106.221.157:8080/doLogin?userName=20177720165&password=123456',
      method: 'GET',
      success(res) {
        wx.setStorageSync("sessionId", [...res.header["Set-Cookie"].split(';')][0]);//获取cookie并存储起来
        console.log(res.header);
        wx.request({
          url: 'http://47.106.221.157:8080/book/out/17',
          header: {
             'cookie': wx.getStorageSync("sessionId")
            },//在请求头上使用cookie
          success(res){
            console.log(res,"1");
          },
          fail(rej){
            console.log(rej);
          }
        })
      }	

```