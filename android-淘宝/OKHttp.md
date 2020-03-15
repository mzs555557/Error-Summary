###  网络连接 java.net.UnknownServiceException: CLEARTEXT communication ** not permitted by network security policy
- 改用 https
- targetSdkVersion 改为 27以下
- 在res的xml目录下,定义一个新的xml文件,内容:
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```
- 在 manifest中 添加
```xml
<application
...
 android:networkSecurityConfig="@xml/network_security_config"
...
/>
```

