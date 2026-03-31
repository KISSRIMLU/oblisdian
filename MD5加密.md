## 场景：防止数据库明文密码意外泄漏。

## 性质：单向无反函数、无密钥、可碰撞、不安全。
java工具类
```java
password = DigestUtils.md5DigestAsHex(password.getBytes());
```
![](assets/MD5加密/file-20260331085208727.png)