# 一、开发者基本知识
苹果开发者官网：https://developer.apple.com/account/ ，个人账号688人民币一年，另外还有公司账号和企业账号，可以自行了解。本次介绍基于个人账号。 上架App或游戏需要先申请证书，申请证书需要涉及到下面的相关术语：

## 1. Certification和p12(证书)
证书是对电脑开发资格的认证，每个开发者帐号有一套，分为两种：

Developer Certification(开发证书)：用于开发测试；
Distribution Certification(发布证书)：用于打包测试ipa或者Appstore的安装包；
.cer是苹果的默认证书，在XCode开发打包可以使用，如果在lbuilder、phonegap、HBuilder、AppCan、APICloud这些跨平台开发工具打包，就需要用到p12文件。 或者多人开发的时候，本机用.cer，其他人用p12证书。

.cer证书仅包含公钥，.p12证书可能既包含公钥也包含私钥，这就是他们的区别，除开XCode开发工具，其他都需要用p12才能打包。

## 2. Identifiers(AppID、应用id)
app的标识，例如app的名字描述，包名

## 3. Devices(设备)
设备列表，表示当app安装调试的时候可以安装在这些机器上面，设备使用udid进行唯一判断，创建描述文件(Profiles)的时候需要选择设备。

## 4. Profiles(描述文件)
这个文件用来描述App IDs、证书和设备之间的关系，我们一般只用到Development、App Store和Ad Hoc三种，Development和Ad Hoc类型的需要指定可以运行在哪些Devices上，而App Store类型的不需要。

授权文件分为两种，对应相应的证书使用：

Developer Provisioning Profile(开发描述文件)：在装有开发证书或副本的电脑上使用，开发人员选择该描述文件通过电脑将程序安装到授权文件记录的设备中，即可进行真机测试，一般是开发自己做调试的时候用。
Distribution Provisioning Profile(发布描述文件)：在装有发布证书的电脑上（即配置证书的电脑，只有一台）制做测试版和发布版的程序。
AppStore发布版： 发布到AppStore上的程序文件，一般是测试完毕之后打AppStore包用；
AdHoc测试版：在发布之前交给测试人员可同步到设备上的程序文件，一般是打包给内测的时候用，只有描述文件里面包含了UDID对应的设备才能安装上。

# 二、创建Certification(证书)

创建App第一步就是创建证书
![image](https://github.com/Ernestanior/ios-/assets/36638557/74c73cc3-90df-40b2-bb82-8ffc619855a2)


创建证书之前需要现在Mac电脑上面申请certSigningRequest(CSR)文件，打开钥匙串访问程序 - 证书助理 - 从证书颁发机构请求证书
![image](https://github.com/Ernestanior/ios-/assets/36638557/67bb60da-e59c-48f5-9dc9-e019f6e84668)

输入下面两项，保存证书文件到电脑。
![image](https://github.com/Ernestanior/ios-/assets/36638557/ab1f3b39-544a-45b5-877e-5b0adc93ba43)


打开网站，开始申请证书
![image](https://github.com/Ernestanior/ios-/assets/36638557/1f2fbc96-9210-4a7a-ae07-44df39072302)


选择Apple Develpment,continue
![image](https://github.com/Ernestanior/ios-/assets/36638557/89373af1-81ba-45dc-9c8e-183b3a91f646)


Choose File选择刚刚创建的文件
![image](https://github.com/Ernestanior/ios-/assets/36638557/4d36dab9-8abd-46f6-88c4-4a8dc31aa9bf)


确定信息，Download下载证书
![image](https://github.com/Ernestanior/ios-/assets/36638557/620984ee-9f39-48d2-bc8e-ed653419b248)


接着重复刚刚的步骤创建一个Apple Distribution证书。 iOS Distribution和Apple Distribution区别是，Apple Distribution是新的，只支持XCode11以及之后的版本的XCode，但是它支持m1的macOS。现在创建Apple Distribution。

这时候已经下载了两个证书，双击证书，导入到电脑，两个都要。

# 三、创建Identifiers
打开网站：https://developer.apple.com/account/resources/identifiers/list/bundleId
![image](https://github.com/Ernestanior/ios-/assets/36638557/dc1cfbe6-ee82-4dfd-9d7a-42244f862ab3)


选择App IDs，Continue
![image](https://github.com/Ernestanior/ios-/assets/36638557/ad0aa2fd-d3c7-4287-8a5f-968f663d1e55)


选择App
![image](https://github.com/Ernestanior/ios-/assets/36638557/6a20e623-132a-42c2-98d4-21db19bb97fa)



输入名字描述(注意不能中文)，包名(一般是com.xxxx.xxxx)，选择app里面需要的服务(这个可以后面编辑)。
![image](https://github.com/Ernestanior/ios-/assets/36638557/d3a8763a-4a6d-4bcb-b506-fcedfcac5f2a)


continue之后Resister，然后你会在Idntifiers列表里面看到你创建的Identifier


四、添加测试设备Devices
在打包的时候需要运行到手机上，然后运行的手机需要在开发者网站添加
![image](https://github.com/Ernestanior/ios-/assets/36638557/a874fa96-f6ad-40d2-836d-f4272b7aa567)

输入对应的信息（注意这里需要获取设备的udid，获取方法看下面）
![image](https://github.com/Ernestanior/ios-/assets/36638557/fa9f7bf6-4118-4897-a415-2c8eec5c967f)


获取设备的udid
方法1（电脑）: 电脑连接手机(手机弹窗选择信任)，打开XCode，菜单栏Window-Devices and Simulates-就可以看到对应的udid
![image](https://github.com/Ernestanior/ios-/assets/36638557/8ed1813d-51c1-48e3-880f-15c792ab9d97)

方法2（电脑）: 打开访达Fidler，位置栏目点击手机，手机名字下面的信息，即可看到udid，右键即可复制
![image](https://github.com/Ernestanior/ios-/assets/36638557/124f9eb5-a1ec-4838-baae-239b0168e432)


方法3（手机）: 手机打开蒲公英网址 https://www.pgyer.com/tools/udid ,根据提示操作

确定之后确定信息点击Register即可在Devices列表里面看到刚刚创建的手机
五、创建描述文件(Profiles)
打开https://developer.apple.com/account/resources/profiles/list
![image](https://github.com/Ernestanior/ios-/assets/36638557/6beadae8-33c3-4921-a23a-339357763e76)


首先创建开发证书(开发证书类型为iOS Development)，开发调试的时候使用这个证书
![image](https://github.com/Ernestanior/ios-/assets/36638557/d332c4ea-9e9b-46e9-aa00-b33511147581)


Continue之后选择之前创建的Identifiers，即AppID
![image](https://github.com/Ernestanior/ios-/assets/36638557/08c5e90e-7b69-4b1b-8735-96bc16eeaf61)


Continue之后选择之前创建的Development开发证书
![image](https://github.com/Ernestanior/ios-/assets/36638557/881d2c30-9e41-4c09-987d-c0f36a35e40d)


Continue之后选择测试设备（这些设备就是Deevics设备列表的设备）
![image](https://github.com/Ernestanior/ios-/assets/36638557/5e0f6b06-4f29-43fe-8108-abc2fa8be6d1)


之后输入描述文件的名字，我一般取名是 项目名+证书类型，例如Project3_Development
![image](https://github.com/Ernestanior/ios-/assets/36638557/b34b681a-9711-4ee3-abf2-5f0e3271c845)


生成之后Download下来，文件的后缀名是mobileprovision

重复上面的步骤，再创建一个AdHoc的描述文件 (打包测试使用)

再次重复上面的步骤，再创建一个AppStore的描述文件**(打包上架AppStore使用)**

三个描述文件下载下来：
![image](https://github.com/Ernestanior/ios-/assets/36638557/b0cd1702-ddab-4d89-a0a1-fcfe95bd9f95)


六、导入使用
在XCode里面新建项目，点击项目 - TARGETS下面的项目 - Siging & Capabilities - Provisioning Profile - 点开选择Import Profile，导入你下载的3个描述文件
![image](https://github.com/Ernestanior/ios-/assets/36638557/9cf49523-3651-48c1-9d7c-4aabbe60ffd7)


这就能正常开发使用了
————————————————
版权声明：本文为CSDN博主「KeepStudya」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/niubitianping/article/details/113137555
