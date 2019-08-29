# 微信小程序转支付宝小程序 #

原仓库：[https://github.com/foxitdog/wx2ali](https://github.com/foxitdog/wx2ali)，把原来仓库的Java版本去掉，更换了一些规则，修复了bug，详情见1.19日志，新开仓库是为了方便后面维护一个node版本，因为原作者的版本包含了Java版本，很容易混淆，造成维护麻烦。为了方便，我新增了一个npm包wxapp2ali。使用时把原仓库的wx2ali改为wxapp2ali。

###说明：###
	这是一个将微信小程序中的大多数与支付宝小程序功能相关，格式相似的api与属性转化为支付包小程序的格式
	其中包含了json、js、wxml的转换，但是转换只是治标并不治本，所以转化结束的源码中的一些错误还是需要靠自己进行解决。
	该程序可以给你的代码迁移省下一部分的精力。
## 环境配置： ##
	node.js
## 安装 ##
	npm i wxapp2ali -g

## 使用 ##
**如果是旧版本请命令行中输入npm update wxapp2ali -g进行更新**

1. 	复制微信小程序的源码一份；
1. 	wxapp2ali --getConfig获取配置文件路径 按照需要修改配置并保存
1.  wxapp2ali --start
1. 	等待处理完成。
1. 或者可以通过 wxapp2ali --path path路径   开始转换


![](https://github.com/foxitdog/wx2ali/blob/master/img/usage.gif)

	
	
## 注意事项 ##

<b style="color:red">因为是用正则表达式进行转换，所以已经转换过的文件请不要进行二次转换，防止发生不必要的麻烦。

多发生在js文件中。</b>

## 文件: ##
	node
	  --wxapp2ali.txt //配置
 	  --package.json
	  --index.js //源码
	  lib
        --JSApiPropReplace.js //api属性替换
		
[点击进入github](https://github.com/kujian/wxapp2ali "wx2ali转换")

## 转换原则: ##

1. 从wxmp（微信小程序）转成antmp（支付宝小程序）
2. <b style="color:red">wxmp有而antmp没有的属性、接口 不进行转换	</b>
3. <b style="color:red">antmp有而wxmp没有的属性、接口 不进行转换	</b>
4. wxmp中的接口、属性与antmp中的接口、属性 如果<b style="color:red">功能相同而名称不同</b>的则<b style="color:red">进行转换</b>
5. 所有文件大体都有正则表达式进行转换
6. js文件有进行过ast转换 可以转换到方法名称

## 更新: ##

	v1.1.9
		fix:修复转换绑定事件时会默认把事件名也一起转换了，例如 ```bindchage = "bindchange"```转换后是 ```onChange = "onChange"```，这是错误的，转换只需要转换前面的bindchange，后面的还是保留的。修复后转换为 ```onChange = "bindchange"
		fix:import导入时会文件类型同时也要调整。
	v1.1.8
		fix:修复scroll-view组件事件匹配
		fix:修复只匹配绑定事件，不匹配其他函数
		新增匹配wxml中的include和import
	v1.1.7
		解决babel-plugin-transform-object-rest-spread插件未找到问题
		https://github.com/foxitdog/wx2ali/issues/9
	v1.1.6
		解决：转换es6扩展运算符出错
	v1.1.5
		修复wxss文件中会import wxss文件，这个没有被转换	https://github.com/foxitdog/wx2ali/issues/4
		将require类型的导入替换成import类型的导入
		将module.exports类型的导出替换成export default 类型的导出 https://github.com/foxitdog/wx2ali/issues/2
	------------------------
	v1.1.4
		wx2ali.txt规则修改
		修复多匹配问题 https://github.com/foxitdog/wx2ali/issues/3
	------------------------
	v1.1.3
		wx2ali.txt规则增加
		axml文件转换更为彻底
	------------------------
	v1.1.2
		wx2ali.txt规则增加
		js文件的转换更为彻底
		待完成的工作：
			axml文件的转换
	------------------------
	v1.1.1
		添加js文件api中的差异转换
	------------------------
	v1.0.2
		添加json文件转换
		添加js文件简单转换
		添加axml文件简单的转换

	
