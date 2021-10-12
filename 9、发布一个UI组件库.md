### 1.在本地创建项目目录

### 2.在 GitHub 上创建仓库，并在本地关联远程仓库，用于保存项目。

### 3.添加开源许可证 - 如何选择开源许可证？


在 GitHub 对应的仓库根目录下新增文件，输入 LICENSE ，出现增加许可证的选项，点击后选择对应许可证即可：

### 4.本地项目目录下运行 npm init - 创建 package.json

### 5.本地项目目录下运行 npm i vue - 添加 vue

### 6.写自己的组件。。。。略

### 7.设置入口文件
在 package.json 中添加入口文件 "main": "index.js",，在入口文件中引入并导出需要打包发布的组件：

```
import Button from './src/Button.vue'
import ButtonGroup from './src/buttonGroup.vue'
import Icon from './src/Icon.vue'

export {Button,ButtonGroup,Icon}
```
### 8.发布到npm
在 npmjs注册一个账号并在邮箱中确认注册信息
在项目根目录的命令行中输入 npm adduser，根据提示填入账号密码邮箱
使用命令 npm publish 发布
注意：如果错误提示里面含有 https://registry.npm.taobao.org 则说明你的 npm 源目前为淘宝源，需要更换为 npm 官方源

可以直接安装 nrm 对 npm源 进行管理: npm install -g nrm

输入 nrm ls 可以看到目前的 npm 源；输入 nrm use npm 切换到 npm 源。


### 参考

[参考element-ui源码](https://github.com/ElemeFE/element/blob/dev/packages/alert/index.js)

