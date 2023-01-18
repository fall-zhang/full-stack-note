> Create by **fall** on: 18 Jan 2023
> Recently revised in: 18 Jan 2023

## crypto

crypto 负责加密解密

前端使用 encrypted = encrypt(password+key)，后端使用  password = decrypt(encrypted +key) 

**对称加密算法**

前端通过 key 和 password进行加密后，后端通过 key，解密前端内容

```js
const CryptoJS = require('crypto-js')
const key = CryptoJS.enc.Utf8.parse("1234123412ABCDEF");  // 十六位十六进制数作为密钥，当然也可以选其它内容作为密钥
const iv = CryptoJS.enc.Utf8.parse('ABCDEF1234123412');   // 十六位十六进制数作为密钥偏移量
// 加密方法
function passwordEncrypt(word) {
  let srcs = CryptoJS.enc.Utf8.parse(word);
  let encrypted = CryptoJS.AES.encrypt(srcs, key, { iv: iv, mode: CryptoJS.mode.CBC, padding: CryptoJS.pad.Pkcs7 });
  return encrypted.ciphertext.toString().toUpperCase();
}
//解密方法
function passwordDecrypt(word) {
  let encryptedHexStr = CryptoJS.enc.Hex.parse(word);
  let srcs = CryptoJS.enc.Base64.stringify(encryptedHexStr);
  let decrypt = CryptoJS.AES.decrypt(srcs, key, { iv: iv, mode: CryptoJS.mode.CBC, padding: CryptoJS.pad.Pkcs7 });
  let decryptedStr = decrypt.toString(CryptoJS.enc.Utf8);
  return decryptedStr.toString();
}
export default {
  Encrypt,
  Decrypt,
}
```

```js
const CryptoJS = require('crypto-js');
const desKey = CryptoJS.enc.Utf8.parse("11");
// DES加密方法
function desEncrypt(message) {
  let encrypted = CryptoJS.DES.encrypt(message, desKey, {
    mode: CryptoJS.mode.ECB,
    padding: CryptoJS.pad.Pkcs7
  });
  return encrypted.toString();
}
//DES解密方法
function desDecrypt(ciphertext) {
  if(ciphertext===""||ciphertext===null||ciphertext===undefined){
    return "";
  }
  if(typeof(ciphertext)!="string"){
    ciphertext=ciphertext.toString();
  }
  var decrypted = CryptoJS.DES.decrypt({
    ciphertext: CryptoJS.enc.Base64.parse(ciphertext)
  }, desKey, {
    mode: CryptoJS.mode.ECB,
    padding: CryptoJS.pad.Pkcs7
  });
  return decrypted.toString(CryptoJS.enc.Utf8);
}
export default {
  desEncrypt,
  desDecrypt
}
```



## 参考文章

| 作者 | 链接 |
| ---- | ---- |
|      |      |

