# wxmp-rsa

### 1、简介
前端rsa加解密工具。
+ 基于[jsencrypt](https://github.com/travist/jsencrypt)修改扩展功能。
+ 兼容小程序环境，压缩后60kb左右的大小，节省小程序空间。
+ 支持超长文本加解密。
+ 支持中文字符的加解密。

### 2、安装
```
npm i wxmp-rsa -S
```

### 3、使用方式
（小程序使用之前需先使用开发者工具[构建npm](https://developers.weixin.qq.com/miniprogram/dev/devtools/npm.html)）
```js
// 导入包
import WxmpRsa from 'wxmp-rsa'

// 实例化rsa
const rsa = new WxmpRsa()

// 定义待加密的字符串
const str = '{"name":"neo"}'
// 定义公钥
const publicKey = `
  -----BEGIN PUBLIC KEY-----
  MIGeMA0GCSqGSIb3DQEBAQUAA4GMADCBiAKBgFnWSUwsmGawhMJ30z6y5li2jcf1
  m7rPMZcwZOS3To8bk3OBaMGhVEc1F8GtJBbc1rn/HCLNL9zrCy21EefJON8tRFcY
  HnpseZSzh+349lIhS+MFw9x4JUddwSPDyxwha929cKzMuVoftu3CJ+kqDBVvxLk7
  iDBzUMqW3Kgehk2TAgMBAAE=
  -----END PUBLIC KEY-----
`
// 设置公钥
rsa.setPublicKey(publicKey)
// 加密
const cryptStr = rsa.encryptLong(str)
console.log('加密后的结果：', cryptStr)

// 定义私钥
const privateKey = `
-----BEGIN RSA PRIVATE KEY-----
MIICWgIBAAKBgFnWSUwsmGawhMJ30z6y5li2jcf1m7rPMZcwZOS3To8bk3OBaMGh
VEc1F8GtJBbc1rn/HCLNL9zrCy21EefJON8tRFcYHnpseZSzh+349lIhS+MFw9x4
JUddwSPDyxwha929cKzMuVoftu3CJ+kqDBVvxLk7iDBzUMqW3Kgehk2TAgMBAAEC
gYBRChPeyk/EOrHX912xLpLKLguh+LY9g1B50ScChzUvtTGDPZaxLQYoogVHKhfn
I9nzuOS5pBzsDX9tAO0hCQzqfHgqRjn+vEgm1Ui+f0E3BVRnhobcJKZpZqlvCBR5
Gu2+zlrY4SeGq3AuQSr/A5FiB5k0RgsvNycDTjqyg7TXGQJBAJoZ8Yr0zakxT1I8
lVqsFbeNPtt8FNG2UgIlIs9RL7aXhw+Y3sWtk/kbaOXafSofu0NcQYx4Km3M3kiP
lcNfTJ8CQQCVPcaRpu+mprRgHS6s76Z668NaFsjX04CUUa0kCrey+Nf/SJJ3BkRH
M7GllZWuI/RSXs/F5N38p5bfkn7QZqaNAkBy3dHJZW8DpgjdYOFnhAxwFK39BwGx
zHhWtv26kWbCcTKwsp+jtB4vunm3k+RmiN6aeGM35L6jt+kdJ0JYLmo7AkBJpRZb
wZj5D8Jqu3vQ8uGgPr9DsYKinkgQ6M0bv/4uXwWXf+Rmv7zpteSv5UTbjfp+uzKk
YO/6QWj+InhZto3xAkAOA0i702dLHm5elLWvht7UEYIDEW1+rYGdbthmJBvT9sZh
VKL954Y9hDzBWepjYsBiJnmIkgeladPnU5025/G/
-----END RSA PRIVATE KEY-----
`
// 设置私钥
rsa.setPrivateKey(privateKey)
// 解密
const originalStr = rsa.decryptLong(cryptStr)
console.log('解密后的原始数据：', originalStr)
```
其他api参考[jsencrypt](https://github.com/travist/jsencrypt)插件

### 4、注意事项
+ 填空方式默认`pkcs1`，目前暂不支持其它填空方式。

### 5、更新提示
+ 之前偶现的加密异常的问题已于v2.0.0+版本中修复。
+ 之前偶现的解密后部分中文乱码的问题已于v2.1.0+版本中修复。

### 6、测试对比
推荐两个第三方rsa工具，仅供参考。
+ 在线生成rsa公私钥：http://travistidwell.com/jsencrypt/demo/ （推荐1024长度的密钥）
+ 在线rsa加解密：http://www.toolzl.com/tools/testrsa.html （117超长加密，128超长解密）
