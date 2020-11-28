# wxmp-rsa

### 1、简介
前端rsa加解密工具。
+ 基于插件[jsencrypt](https://github.com/travist/jsencrypt)修改扩展功能。
+ 兼容微信小程序环境，54kb左右的大小，节省空间。
+ 支持超长文本加解密。
+ 支持中文字符的加解密。

### 2、安装
```
npm i wxmp-rsa -S
```

### 3、使用方式
```js
import { JSEncrypt } from 'wxmp-rsa'

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

const myEncrypt = new JSEncrypt()
myEncrypt.setPublicKey(publicKey)
myEncrypt.setPrivateKey(privateKey)

const cryptStr = myEncrypt.encryptLong(str)
console.log('加密后的结果：', cryptStr)

const originalStr = myEncrypt.decryptLong(cryptStr)
console.log('解密后的原始数据：', originalStr)
```
其他api参考jsencrypt插件：https://github.com/travist/jsencrypt

### 4、注意事项
+ 填空方式默认`pkcs1`，目前暂不支持其它填空方式。
+ 已知偶现的会有加密异常的问题，把加密异常后的结果解密后得到的字符串后半段是重复的，这是插件jsencrypt本身的bug，但目前不清楚具体原因，发生概率大概1%左右。
我这里在内部做了处理，当设置了私钥后就能自动处理这个问题，但前提是通过setPrivateKey设置了私钥，否则不会生效。
+ 此插件更推荐给微信小程序端使用，因为小程序主包大小有2mb的限制，其他插件动辄四五百kb的大小实在不适合，而此插件压缩后大小54kb左右，占用空间很小。
如果是非小程序端环境，由于上述bug的原因还是推荐用其他插件吧（例如node-rsa）。

