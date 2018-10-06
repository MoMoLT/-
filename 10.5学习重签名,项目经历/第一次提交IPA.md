#第一次提交IPA
---
---
##1.用xcode编译，进行真机测试项目
- 打开入手的项目
- 要了解，xcode是打开.xcodeproj后缀名工程文件
- 在终端先进入该项目下，输入查找命令
`find . -name "*.xcodeproj"`
- 找到文件，然后打开，编译好安装到真机上使用，体验各种功能，发现是否有错误（一般不会有错）



##2.混淆操作 m_r

- 用`node $m_r 工程路径`    这指令进行自动混淆操作
- 注意：混淆指令会自动设置一些参数，如compiler for C/C++/Objective-C要设置为几维混淆编译器， 去掉armv7等
- 混淆包还需要静态库，静态库的创建：在`.../haoyue/tool/reviewWorkSpace/lotsofLib` 这个文件夹中，先创建`目标`文件夹，然后把`静态库压缩包`解压出的一个文件夹，放进`目标`文件夹中

- addr命令是在资源包里添加垃圾文件，rcg命令是在各个代码文件加入垃圾文件，用node $m_r xxx指令自动集合了上面的命令


##3.真机测试混淆工程
- 打开混淆后的工程，在真机上进行测试，对比加入混淆前后两次运行时候的效果。
- 有些地方比原app慢，没关系，而出现卡死，闪退， 部分功能失效等问题，需要慢慢修改问题。<br/>
- 使用混淆日志，慢慢修改找错误。


##4.导出IPA包

- 用Xocde  `Product`-->`Archive`编译后，导出ipa包。
- 如果`Archive`是灰色的，选择运行键右边第四个那个按钮，出现下拉表，有虚拟机和真机选项，选择`Generic iOS Device`
- 进入导出界面时，不勾选`Upload your app's symbols to receive symbolicated reports from Apple`,这是是加入反馈什么的，会把ipa包体加大
- 导出包如果遇到问题，那是配置文件与证书不匹配

##5.混淆IPA包 resign

- 第五步导出的包，不只有ipa包，但上传只上传ipa包
- 进入终端，用cd指令，进入导出包
- 在导出包目录下，用resign指令混淆ipa包，`[resign ./ -num 3333]`或`[resign]`，参数会默认调用的。
- 打开ipa解压文件Payload，可能要修改一些问题，如找到app下的info.plist，修改权限问题，内部版本号等，外部版本号绝对不能动！！！
- 然后压缩文件`Payload, zip -r xxx.ipa. Payload/`	前面是你要压缩成ipa的包名

##6.重签名 fastlane, iReSign

- 有两种方式：fastlane命令和iReSign工具

> fastlane

- 进入导入包
- `fastlane sigh resign`
- 然后输入证书的密钥
- 重签名成功

>iReSign

- 由于fastlane重签名方法在上传IPA包操作时，可能出现`error 99046`错误， 用这个工具可以解决
- 终端输入codesign --display --entitlements - ipa的解压文件/xxx.app
- 得到几行xml格式代码，创建文件，把代码复制进去
- iReSign界面填写
	- 第一行		`混淆的ipa包`
	- 第二行		resign混淆后，导出包目录下生成的`配置文件`
	- 第三行		`xml代码文件`
	- 第四行		不填写
	- 第五行		与第二行配置文件对应的`证书`
- 注意，如果新配置文件绑定的工程ID与工程ID不符合，那么需要去info.plist修改工程唯一ID

##8.上传IPA包
- 左上角的苹果标识旁的`Xcode`-->`Open Developer Tool`-->`Application Loader`
- 输入客户给的开发者账号，登陆进去
- 选择重签名后的IPA包，进行上传即可


##知识储备
- ios的[签名](https://www.jianshu.com/p/efa64438ef49)，[重签名](https://www.jianshu.com/p/ac5ce7e2bb53?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)
- [entitlements.plist是什么？](https://blog.csdn.net/yst19910702/article/details/72472325)
- info.plist参数， 了解其中的[权限参数](https://www.jianshu.com/p/f0e9cbcef036)
- [Xcode的General设置](https://www.jianshu.com/p/e2c76cb6f6e8)中的Version, Build参数
- Xcode的Build Setting参数
- 简单认识一下游戏引擎：coco3, unity...


##解决问题
- entitlements.plist是什么？

>答：权限配置文件，一些要开启的app功能需要该配置文件。即功能要授予权限。

- ios签名, 重签名

>答：看我写的重签名学习.txt吧，再看看链接



