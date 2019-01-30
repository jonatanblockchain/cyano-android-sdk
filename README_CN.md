# cyano-android-sdk-ONTID
cyano-android-sdk 帮助钱包集成ONTID相关功能

## 如何使用
将工程当作module导入到项目中

#### 添加权限
 
```
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
    <uses-permission android:name="android.permission.SYSTEM_OVERLAY_WINDOW" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
```

#### 注册activity
 
```
    <activity android:name="com.github.ont.connector.ontid.CreateOntIdActivity" />
    <activity android:name="com.github.ont.connector.ontid.ImportOntIdActivity" />
    <activity android:name="com.github.ont.connector.ontid.OntIdWebActivity" />
    <activity android:name="com.github.ont.connector.ontid.TestFrameActivity" />
    <activity android:name="com.github.ont.connector.ontid.ExportOntIdActivity" />
```

#### 添加ONT lib
* 将repositories的文件夹复制到工程中
* 在工程最外部的build.gradle添加
```
allprojects {
    repositories {
        flatDir {
            dirs '../repositories'
        }
    }
}
```
* 如果钱包需要集成，在对应build.gradle文件中添加
```
  implementation(name: 'ontolib-release', ext: 'aar')
```

#### 照片选择
在[build.gradle](https://github.com/ontio-cyano/cyano-android-sdk/blob/master/cyano_lib/build.gradle)修改图片选择库，当前使用得是matisse图片选择器

在[com.github.ont.connector.update.ImageUtil](https://github.com/ontio-cyano/cyano-android-sdk/blob/master/cyano_lib/src/main/java/com/github/ont/connector/update/ImageUtil.java)文件中修改对应的图片处理

#### 网络请求
在[build.gradle](https://github.com/ontio-cyano/cyano-android-sdk/blob/master/cyano_lib/build.gradle)修改网络框架，当前使用得是okhttp框架

在[com.github.ont.connector.update.NetUtil](https://github.com/ontio-cyano/cyano-android-sdk/blob/master/cyano_lib/src/main/java/com/github/ont/connector/update/NetUtil.java)文件中修改对应的网络请求

## 开始使用

#### 设置wallet file的存储路径
修改[Constant](https://github.com/ontio-cyano/cyano-android-sdk/blob/master/cyano_lib/src/main/java/com/github/ont/cyano/Constant.java)的WALLET_FILE字段，让ont sdk存储wallet file路径一致

#### 设置服务器的接收地址
修改[Constant](https://github.com/ontio-cyano/cyano-android-sdk/blob/master/cyano_lib/src/main/java/com/github/ont/cyano/Constant.java)的WALLET_RECEIVER_URL字段，认证后会返回[authenticationId](https://github.com/ontio-cyano/integration-docs/blob/master/%E9%92%B1%E5%8C%85%E5%AF%B9%E6%8E%A5-OntId%E8%AE%A4%E8%AF%81.md),需要提交到钱包服务器.

#### 启动
启动ONT ID界面，ONT ID的私钥，密码和ONT 默认钱包 钱包一致，在进入界面之前需要检查是否已创建好钱包。

ONT ID只允许创建一个

```
        String defaultAccountAddress = OntSdk.getInstance().getWalletMgr().getWallet().getDefaultAccountAddress();

        if (TextUtils.isEmpty(defaultAccountAddress)) {
        //TODO 未创建钱包的处理
        } else {
                    Intent intent = new Intent(baseActivity, TestFrameActivity.class);
                    startActivity(intent);
        }
```

## DEMO
[cyano-android](https://github.com/ontio-cyano/cyano-android)

## 版本
0.0.1