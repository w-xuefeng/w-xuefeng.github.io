---
title: 如何申请 iOS 证书
date: 2020-05-20 13:14:00
categories: 技术贴 | iOS 开发
tags: iOS
thumbnail: https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/thumbnail.png
---

## 一、账号类型与名词解释

首先我们来认识一下苹果开发者账号类型和几个专业名词：

- 苹果开发者账号类型：

	- $99/年 (可上架 App Store)
		- 个人版
		- 公司版 (可创建团队添加开发成员)

	- $299/年 企业版 (不可上架 App Store, 可创建团队添加开发成员）


- 专业名词：

	- 钥匙串文件
	- 证书
		- 软件 （Software）
			- 开发证书
			- 发布证书
			- In House 发布证书
		- 服务 （Service）
			- 开发推送证书 (Sandbox)
			- 发布推送证书 (Sandbox & Production)
		- 导出副本
			- P12 证书 （Keychain）
	- 应用 ID （bundleID）
	- 应用描述配置文件


| 名词 | 解释 | 对应英文 | 文件后缀名 |
| - | - | - | - |
| 钥匙串文件 | 申请证书所需的密钥文件 | Certificate Signing Request | .certSigningRequest |
| 开发证书 | 让开发者使用的设备有真机调试的权限 | Certificate -> Software -> iOS App Development | .cer |
| 开发推送证书 | 让开发者使用的设备有真机调试推送功能的权限 | Certificate -> Service -> Apple Push Notification service SSL (Sandbox) | .cer |
| 发布证书 | 让开发者有发布 App 的权限，可以上架 App Store | Certificate ->  Software -> iOS App Distribution (App Store Ad Hoc)| .cer |
| 发布推送证书 | 让开发者有 “上架APP” 推送功能的权限 | Certificate -> Service ->  Apple Push Notification service SSL (Sandbox & Production)   | .cer |
| In House 发布证书 | 只有 $299/年 的开发者账号才能申请，让开发者有发布 App 的权限，不可以上架 App Store，无需通过苹果审核，任何设备都可以安装 App | Certificate -> Software ->  In House and Ad Hoc | .cer |
| P12 证书 | 让第三方开发工具或平台有开发、调试、打包的权限，有时也叫 Keychain | 无 | .p12 |
| 应用 ID | 项目包名，即 bundleID | Identifiers  | 字符串，非文件 |
| 应用描述配置文件 | 让开发者的项目能有真机调试，发布的权限 | Profiles | .mobileprovision |

证书 和 P12 证书的区别：

| 项目 | 证书 | P12 证书 |
| - | - | - |
| 后缀名 | .cer | .p12 |
| 图标表示 | 蓝色边框和字体 | 黑灰色边框和字体 |
| 所含密钥 | 公钥 | 公钥和私钥 |
| 使用者 | 开发者，项目创建者，`Xcode` | 第三方开发工具或平台，如`lbuilder`、`phonegap`、`HBuilder`、`AppCan`、`APICloud` |
| 来源 | 通过钥匙串文件在苹果开发者官网申请生成 | 由证书导出 |


## 二、申请流程

然后我们梳理一下申请流程，我们需要用到的设备是一台可以联网的 Mac，执行以下步骤

- 1 创建钥匙串文件
- 2 申请证书 （需要上一步钥匙串文件）
- 3 创建应用 ID （如果已创建则可以跳过）
- 4 添加调试设备
- 5 创建应用描述文件 （需要证书和上一步的应用 ID）
- 6 导出 P12 证书 （需要证书和密钥）

确保 步骤1 和 步骤6 在同一台 Mac 上进行，否则将无法导出 P12 证书

如果我们是第一次申请证书，那么 步骤1 到 步骤6 都要执行一遍

如果我们之前申请过证书，那么只要我们在之前申请证书的设备上执行 步骤3 到 步骤6 即可，如果应用 ID 已经创建，则可以跳过 步骤3

如果申请发布证书或 In House 类型证书，或者测试设备已经添加过了，则可以跳过 步骤 4

申请推送证书只需要执行 步骤1、步骤2 和 步骤6 即可


接下来我们就开始吧。

### 1. 创建钥匙串文件

在 Mac 上 打开 “钥匙串访问” 程序，一般在 `其他` 中，找不到的话可以在右上角搜索

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/0.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

然后点击右上方钥匙串访问栏->证书助理->从证书颁发机构请求证书…

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/0-1.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

填写一个邮箱地址，选择 “存储到磁盘”，点击继续

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/0-2.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

文件名称为 `CertificateSigningRequest.certSigningRequest`，选择保存位置，点击 “存储” 保存到指定路径下，钥匙串文件就创建完成了。

<div style="width: 100%;display: flex;justify-content: center;flex-wrap: wrap;">
	<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/0-3.png" style="display:block;margin:0 10px">
	<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/0-4.png" style="display:block;margin:0 10px">
</div>

### 2. 申请证书

登录 苹果开发者网站 `https://developer.apple.com`, 点击 `Account`

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-0.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

输入 苹果开发者帐号和密码 登录

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-1.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

在左侧菜单栏中或者中间内容区域点击 `Certificates, Identifiers & Profiles` 进入 “证书、ID、描述文件” 管理

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-2.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

在证书管理页面，可以看到所有已经申请的证书及描述文件；在 `Certificates`栏目下点击页面的加号来创建一个新的证书：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-3.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">


如果我们要申请 APP 开发证书，则在 `Software` 栏下选中我们要申请的证书类型， 

- 如果我们的账号类型是 **$99/年**,

	- 如果我们是 **Xcode** 原生开发，则选择对应的 开发证书 `Apple Development` 或发布证书 `Apple Distribution`
	- 否则我们 开发证书选择 `iOS App Development` , 发布证书选择 `iOS Distribution (App Store and Ad Hoc)`

- 如果我们的账号类型是 **$299/年**,

	- 选择 **In House and Ad Hoc**


<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-4-software.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

如果我们要申请 推送服务 证书，则在 `Service` 栏下选中我们要申请的证书类型

- 开发推送证书选择 `Apple Push Notification service SSL (Sandbox)`
- 发布推送证书选择 `Apple Push Notification service SSL (Sandbox & Production)`

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-4-serveice.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

然后点击 `Continue`：


接下来需要用到 步骤1 生成的证书请求文件，也就是钥匙串文件，点击 `Choose File...` 选择刚刚保存到本地的 `CertificateSigningRequest.certSigningRequest` 文件，点击 `Continue` 生成证书文件：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-5.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

生成证书后选择 `Download` 将证书下到本地：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/1-6.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

### 3. 创建应用 ID （App ID，Bundle ID）

选择页面的 `Identifiers` 可查看到已申请的所有 App 应用标识，点击页面上的加号来创建一个新的应用标识：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/3-0.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

选择标识类型为 `App IDs`，然后点击 `Continue`

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/3-1.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

平台选择 `iOS，tvOS，watchOS`，Bundle ID 选择 `Explicit`，在 `Description`中填写描述，然后填写 `Bundle ID`，`Bundle ID` 要保持唯一性，建议填写反域名加应用标识的格式 如：`com.xxx.myappname`， 然后点击 `Continue`

注意：在第三方开发平台中 App 提交云端打包时界面上的 AppID 栏或者在证书配置里填写的就是这个 `Bundle ID`

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/3-2.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

接下来需要选择应用需要使用的服务（如需要使用到消息推送功能，则选择`Push Notifications`），然后点击 `Continue`
注意：如果 App 要上架 App Store, 用不到的服务一定不要勾选，以免响应审核

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/3-3.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">


确认后选择提交，回到 `identifiers` 页面即可看到刚创建的应用 ID：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/3-4.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">


至此，应用 ID 已经创建完毕。


### 4. 添加调试设备

开发描述文件必须绑定调试设备，只有授权的设备才可以直接安装 App，所以在申请开发描述文件之前，先添加调试的设备，如果已经添加设备，可跳过此步骤。
在证书管理页面选择 `Devices`，可查看到已添加的所有设备信息，点击页面上的加号来添加一个新设备：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/4-0.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">


填写设备名称 和 UDID（设备标识）：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/4-1.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">


获取设备UDID方法，将设备连接到电脑，启动 iTunes，点击此区域可切换显示设备的 UDID，右键选择复制，输入完成后，点击 `Continue` 继续完成添加即可；

接下来继续申请描述文件

### 5. 创建应用描述文件

在证书管理页面选择 `Profile`，可查看到已申请的所有描述文件，点击页面上的加号来添加一个新的描述文件：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-0.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

选择我们要创建的描述文件类型，

- 如果我们的账号类型是 **$99/年**,

	- 如果我们要创建**开发描述文件**，则在 `Development` 栏下选中 `iOS App Development`

	- 如果我们要创建**发布描述文件**，则在 `Distribution`栏下选中 `App Store`


- 如果我们的账号类型是 **$299/年**,

	- 在 `Distribution`栏下选择 **In House**


点击`Continue`按钮：

<div style="width: 100%;display: flex;justify-content: center;flex-wrap: wrap;">
	<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-1.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">
	<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-1-inhouse.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">
</div>

这里要选择 步骤3 创建的 应用 ID （App ID，Bundle ID），点击`Continue`：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-2.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

接下来选择需要绑定的证书，也就是 步骤2 申请的证书， 点击`Continue`：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-3.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

2020 年之后，需要在创建 应用 ID （App ID，Bundle ID） 的时候关联证书，创建 描述文件 的时候只需要选择要关联的应用 ID （App ID，Bundle ID）即可，无需再绑定证书

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-3-nocer.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

如果要创建的是开发描述文件，则要选择授权调试设备，这里建议直接勾选 `Select All`，点击 `Continue`：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-4.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

输入描述文件的名称, 点击 `Generate` 生成描述文件：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-5.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

点击 `Download` 下载保存开发描述文件（文件后缀为 .mobileprovision）

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/5-6.png" width="50%" style="display:block;margin:0 auto;min-width: 280px">

至此，对应的描述文件（.mobileprovision) 创建完成;


### 6. 导出 P12 证书


双击 步骤2 下载的证书, 打开证书将其安装到钥匙串，若弹出安装提示，选择安装到`登录`，在钥匙串中找到安装的证书

若提示此证书是由未知颁发机构签名的

请下载` Apple Worldwide Developer Relations Certification Authority`证书进行安装

地址[http://developer.apple.com/certificationauthority/AppleWWDRCA.cer](http://developer.apple.com/certificationauthority/AppleWWDRCA.cer)

在左边选择 `登录` 和 `我的证书`，找到证书，在证书上面点击鼠标右键，然后在菜单中选择导出证书，如图：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/6-0.png" style="display:block;margin:0 auto;min-width: 280px">

在弹出页面中指定证书名，点击存储，然后输入证书密码（此密码在第三方开发平台页面输入），点击好，生成 p12 格式证书。

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/how-to-request-the-ios-certificate/6-1.png" style="display:block;margin:0 auto;min-width: 280px">

至此，我们现在 有了 

- 1. 钥匙串文件
- 2. 证书（或推送证书），分**[开发，发布，In House]**类型
- 3. 应用 ID （Bundle ID）
- 4. 证书导出的 P12证书（或推送证书导出的 推送P12证书），分**[开发，发布，In House]**类型
- 5. 应用描述文件，分**[开发，发布，In House]**类型

一般第三方平台所需要的是 `证书导出的 P12证书` 和 `应用描述文件`，同时需要填写 `应用 ID` 和导出 P12 证书时设置的密码。


### 参考资料
- [苹果开发者账号的区别，发布方式In-House和Ad Hoc区别](https://blog.csdn.net/weixin_34408717/article/details/90338084?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-2)
- [iOS证书(.p12)和描述文件(.mobileprovision)申请](https://ask.dcloud.net.cn/article/152)
- [iOS证书及描述文件制作流程](https://docs.apicloud.com/Dev-Guide/iOS-License-Application-Guidance#2)