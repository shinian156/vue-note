### NPM介绍
NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：

+ 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
+ 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
+ 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

```
//检测是否安装成功
npm -v

//使用npm命令安装模块
npm install <Module Name>
// 缩写
npm i <Module Name>
```

### 全局安装与本地安装

```
npm i koa      //本地安装
```
+ 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
+ 可以通过 require() 来引入本地安装的包。

```
npm i koa -g   //全局安装
```

+ 将安装包放在 /usr/local 下或者你 node 的安装目录。
+ 可以直接在命令行里使用。

npm install -save moduleName # -save 的意思是将模块安装到项目目录下，并在package文件的dependencies节点写入依赖。
 
npm install -save-dev moduleName # -save-dev 的意思是将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖。

### 查看安装信息
查看所有全局安装的模块

```
npm list -g
```

如果要查看某个模块的版本号，可以使用命令如下：
```
npm list koa -g
```

### 使用 package.json
package.json 位于模块的目录下，用于定义包的属性。

Package.json 属性说明
+ name - 包名。
+ version - 包的版本号。
+ description - 包的描述。
+ homepage - 包的官网 url 。
+ author - 包的作者姓名。
+ contributors - 包的其他贡献者姓名。
+ dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
+ repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
+ main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。
+ keywords - 关键字

### 卸载模块
我们可以使用以下命令来卸载 Node.js 模块。

```
npm uninstall koa
```
卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：

```
npm ls
```

### 更新模块

```
npm update koa
```
### 搜索模块

```
npm search express
```

### 创建模块
创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

```
npm init
快速创建
npm init -y
```

### 在 npm 资源库中注册用户（使用邮箱注册）：

```
npm adduser

Username: "用户名"
Password: "密码"
Email: (this IS public) "邮箱"
```
### 发布模块
```
npm publish
```

### 容易混乱的几个安装
<!-- 原文地址：https://www.cnblogs.com/limitcode/p/7906447.html -->
```
npm install moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -g moduleName 命令
1. 安装模块到全局，不会在项目node_modules目录中保存模块包。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -save moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入dependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，会自动下载模块到node_modules目录中。

npm install -save-dev moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入devDependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中。


```
### 总结
devDependencies 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩css、js的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 -save-dev 的形式安装。像 express 这些模块是项目运行必备的，应该安装在 dependencies 节点下，所以我们应该使用 -save 的形式安装。