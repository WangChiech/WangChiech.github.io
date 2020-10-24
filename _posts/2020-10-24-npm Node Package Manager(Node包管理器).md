---
layout: post
title: "npm"
subtitle: ''
author: "WangChiech"
header-style: text
tags:
  - 工程化
---

## npm Node Package Manager(Node包管理器)

1. npm是node默认的模块管理器（包管理工具）,用来安装和管理node模块

2. https://www.npmjs.com/（类似Appstore）
   1. 模块都会提交到这个网站，安装一个模块也是从这个网站上下载并安装
   2. 通过npm我们可以自动下载并安装包、升级安装包、卸载安装包
   3. https://www.npmjs.com.cn/   npm中文文档
   4. 全世界的开发者都会选择把项目放在这个网站中，大家都可以通过npm去下载使用，并且我们也可以往上面提交项目

###  安装npm

1. 安装nodejs环境（node环境自带npm）

 https://nodejs.org/en/download/   下载node

2. 打开命令输入框

   注意：最好用管理员的身份运行，不然安装模块的时候可能会报错！！！

   （是管理员的身份运行的话cmd框的标题上会显示一个管理员）

3. 输入`node -v`以及`npm -v`能够输出版本号就证明安装成功了

### npm安装模块

1. 安装前要确认的事件
   - 命令提示符窗口必需是管理员身份打开的
   - 命令提示符里显示的路径是你要安装的路径
   - 当前文件里必需有一个package.json文件

2. 步骤
   - 如果没有package.json文件，输命令：`npm init`，然后一路回车（或者`npm init -y`）
   - `npm install` 模块名

3. `npm install `命令

   - 全局安装

     1. 将一个模块安装到全局中，在这个电脑上所有项目都可以用

        - 查看全局路径：`npm root -g`

        - 修改全局路径：`npm config set prefix '目录'`

          windows下： C:\Users\kaivon\AppData\Roaming\npm\node_modules

          mac下：/usr/local/lib/node_modules

     2. 适用于安装工具模块

     3. 命令

        - npm install -g 模块名
        - npm install -global 模块名

   - 本地安装

     1. 将一个模块安装到当前目录的node_modules子目录里，然后只有在当前目录和它的子目录之中才能使用这个模块
     2. 命令
        - npm install 模块名
     3. 安装模块的固定版本
        - 命令：npm install 模块名@0.1.1
     4. 设置模块安装时的依赖
        - npm install 模块名 --save   模块名将被添加到dependencies
        - npm install 模块名 --save-dev 模块名将被添加到devDependencies(简写：npm install 模块名 -D)
        - npm install 模块名 --save-optional  模块名将被添加到optionalDependencies

4. 淘宝镜像
   - npm的服务器在国外，我们安装东西的时候会非常的慢，建议大家安装一个淘宝镜像
   - 淘宝镜像官网https://npm.taobao.org/
   - 安装淘宝镜像命令：npm install -g cnpm --registry=https://registry.npm.taobao.org
   - 安装淘宝镜像后，所有的npm命令可以换成cnpm
   - 但是如果发布的话，还得用npm

5. 注意

   > 安装的一个模块如果有依赖其它的模块，它会自动安装
   > 一旦安装了某个模块，就可以在代码中用require命令调用这个模块
   > var backbone=require('backbone');
   > console.log(backbone.VERSION);

### npm 常用命令

[npm所有命令](https://docs.npmjs.com/)
[npm所有命令（中文的）](https://www.npmjs.com.cn/)

```bash
npm init					新建一个package
npm -version或者npm -v	  查看npm的版本号
npm help或者npm -h		  npm的所有命令列表
npm -l					各个命令的简单用法
npm config list			提供npm的安装信息
npm install 模块名			安装模块
npm update	 模块名			升级模块
npm update -g 模块名		升级全局安装的模块
npm uninstall 模块名		卸载模块
npm uninstall -g 模块名		卸载全局安装的模块
npm list					列出当前目录安装的所有模块
npm -g list				列出全局安装的模块（这里有问题，会报错）
npm search 模块名			搜索模块（与在npm官网搜索是一样的）
npm publish 				发布模块
npm unpublish	模块名 --force		删除已发布模块**
```

### npm publish

`npm publish` 发布步骤:

1. 注册或者登录一个用户
   - npm adduser
   - 输入用户名
   - 输入密码
   - 输入邮箱
     - 然后就上传数据，上传完了就表示注册完了
     - 上传完了，会给你的邮箱发一封邮件
     - 然后在命令行里给你提示一个地址
2. 登录（如果你已经有用户名跟密码了，那就不用adduser）
   - npm login
   - 登录后可以npm whoami看一下自己的用户名
3. 新建package
   - npm init
   - 然后在package里输入一些信息
4. 新建一个Readme.md文件
5. npm publish
   (如果更新了，需要把package里的版本号更新一下，不然报错

)

### package.json

package.json		包描述文件，用来描述包的信
	package name		包的名字
	version			包的版本号
		版本号：主版本号.次版本号.build号
			1、^		兼容版本
			2、~		最新版本
			2、*		所有版本
			6、a-b	两个版本间的版本
	description		包的描述
	entry point		入口文件
	main				入口文件
	test command		测试命令（系统要对你的
	git repository	git地址
	keywords			关键字（别人能搜到你，
	author			作者名字
	license			授权（一般回车就行）
	dependencies		项目运行依赖包（在包的名字后加上 --save）
	devDependencies	项目开发依赖包（在包的名字后加上 --save-dev）
	scripts			可以通过命令运行的js文件
		npm start		运行js
		npm stop			停止运行js
		npm restart		重启js
		npm test			测试js
		注意：这些命令后面的值为"node 文件名.js
	homepage			包的官网url
	contributors		包的其他贡献者姓名