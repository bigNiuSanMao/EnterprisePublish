####	1、企业证书配置

	这个比较简单，忽略了。

####	2、打包成ipa包

	这个比较简单，忽略了。

####	3、企业发布APP

	要发布还必须有一个plist文件，在Xcode6之前会自动生成一个plist文件，但是Xcode6之后需要我们自己创建plist，文章最后提供一个plist模板，复制并重命名为plist后打开根据提示操作即可。
	
	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	<plist version="1.0">
	<dict>
		<key>items</key>
		<array>
			<dict>
				<key>assets</key>
				<array>
					<dict>
						<key>kind</key>
						<string>software-package</string>
						<key>url</key>
						<string>https://www.example.com/dwsoft/Clerk/Clerk.ipa（ipa包URL 必填）</string>
					</dict>
					<dict>
						<key>kind</key>
						<string>full-size-image</string>
						<key>needs-shine</key>
						<true/>
						<key>url</key>
						<string>https://www.example.com/dwsoft/Clerk/setup.png（下载时小图 非必填）</string>
					</dict>
					<dict>
						<key>kind</key>
						<string>display-image</string>
						<key>needs-shine</key>
						<true/>
						<key>url</key>
						<string>https://www.example.com/dwsoft/Clerk/setup.png（下载时小图 非必填）</string>
					</dict>
				</array>
				<key>metadata</key>
				<dict>
					<key>bundle-identifier</key>
					<string>cn.com.example.clerk（Bundle ID 必填）</string>
					<key>bundle-version</key>
					<string>1.0.0</string>
					<key>kind</key>
					<string>software</string>
					<key>副标题（非必填）</key>
					<string>应用名（必填）</string>
				</dict>
			</dict>
		</array>
	</dict>
	</plist>

那么plist放在哪里呢（即Safari打开plist的URL是多少呢）？苹果对plist存放地址有要求，必须是https的，如果没有https网站，我们可以把plist放在``https://git.oschina.net``。具体做法就是在上面创建一个项目（不能是私人的），然后将编辑好的plist传到项目，最后将plist的URL赋值下来，比如``https://git.oschina.net/waitwait/companytest/blob/master/MDDTest.plist``。然后我们在Safari中输入：``itms-services:///?action=download-manifest&url=https://git.oschina.net/waitwait/companytest/blob/master/MDDTest.plist``就可以安装了（一定要将红色字符串和蓝色URL一起输入）。

Safari操作的具体流程是：

 　　1 Safari解析我们输入的那一串字符串，找到plist文件

　　 2 根据plist文件里面提供的信息下载并安装ipa包，还会访问大小图标，大小图标在ipa包正在下载时显示，当下载完毕后显示程序自带的图标

　　下载安装后，如果想打开程序还需要在手机 设置->通用->描述文件与设备管理(不同系统可能名字不一样) 里面选择相应的证书信任后，方可打开程序。

　　
###	附件地址：

[https://github.com/yaoqi-github/EnterprisePublish/tree/master/dwsoft](https://github.com/yaoqi-github/EnterprisePublish/tree/master/dwsoft)