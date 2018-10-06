Target 工程
---
>* General	---通用选项（标识，签名，部署,icon,添加库，二进制文件）
>* Info		---通用选项（info.plist,支持的文件类型，导入导出UTIs, APP跳转)
>* ...


General
---
1: Identity	 --身份
> - display name:项目名称，默认就好
> - Bundle Identifier:包标识符，该ID是唯一的
> - Version:	外部版本号,用户能够看到
> - Build:	内部版本号，开发者自己看到，区分测试版用

2:Signing		--应用程序的签名，如果有开发者账号
3:Deployment Info	--部署信息
> - Deployment Target:	对象运行的版本号
> - Devicxes: 	支持的设备
> - Main Interface: 启动时加载的界面，如果纯代码编程，则需要设置为空，然后删除storyboard
> - Device Orientation: 应用支持的方向

