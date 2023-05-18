## VScode中uniapp开发微信小程序配置与操作

VSCode开发uni-app的体验优势和插件推荐图

[VSCode开发uni-app教程（掘金社区版）]: https://juejin.cn/post/7090532271257714695#comment

![VSCode开发uni-app.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/28309fd5d44343bdb154011a82612a29~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

#### 简述

- 增强`pages.json`和`manifest.json`开发体验（语法提示、颜色块、写注释）
- 一键创建页面、组件、分包
- 完善的`API`，组件，uni.scss 变量提示
- 条件编译注释高亮

基于以上的目的和优势，**VSCode与HBuiderX开发uni-app最大的不同在于VSCode只能通过脚手架的方式创建项目**，无法实现HBuiderX的一键生成uni-app项目，两种方式各有利弊。

同时由于采用VSCode脚手架的方式创建项目对于DCloud插件市场的支持便不如HBuderX一样可以一键导入，只能通过手动方式导入，**如果插件支持npm则通过npm的方式引入，如不支持npm则可以通过下载zip压缩包的方式导入**



#### 初始化项目

[通过脚手架初始化uniapp项目]: https://uniapp.dcloud.net.cn/quickstart-cli.html#install-vue-cli

#### pages.json和manifest.json报红处理

原因：在Json文件中不能写注释导致的，所以针对这两个json文件需要特殊处理

**解决方案**：把`pages.json`和`manifest.json`这两个文件关联到`jsonc`中，然后就以写注释了。在设置中打开`settings.json`

```json
"files.associations": {
    "pages.json": "jsonc",
    "manifest.json": "jsonc"
}
```

#### 一、Vscode中相关插件安装

1. Vue2用vuter、Vue3用volar：vue框架开发利器
2. **uni-app-snippets**： uniapp基本能力代码片段 或者直接安装uni-helper
3. **uni-app-schemas**： 校验 uni-app 中的 androidPrivacy.json、pages.json 和 manifest.json 格式
4. **uni-create-view**： 快速创建 uniapp 视图与组件
5. **Path Intellisense**： 文件路径提示
6. **SCSS IntelliSense**： Scss变量提示
7. **Better Comments**： 代码注释高亮，主要便于uniapp在不同端的注释代码清晰显示，但是在volar下无效
8. **image preview**： 图片预览
9. **Vue Peek**: 快速跳转到组件、模块定义的文件
10. **Vue VSCode Snippets**： Vue代码片段生成
11. vue-helper、CSS Peek、vscode-elm-jump：代码定义跳转

#### 二、运行、发布项目

对应的命令在`package.json`，中，可以自行查看。

- npm run dev:%PLATFORM%
- npm run build:%PLATFORM%

比如：运行至微信小程序的命令：`npm run dev:mp-weixin`

VSCode与HBuiderx关于联调的区别，VSCode不会自动在微信开发者工具中导入项目并打开，所以需要手动导入，但是只需要导入一次即可，后续可以直接打开微信开发者工具使用。

**VSCode开发时需要在manifest.json文件中配置微信小程序的appid，否则运行时会报错**

##### 项目运行

将通过命令打包后的项目导入微信开发者工具中，后续就可以在微信开发者工具中进行项目的运发、编译等

#### 关于uni-app的Vue2和Vue3版本的差异

具体的项目创建可参考初始化中的官网链接

Vue2和Vue3的主要区别在于，Vue3采用的vite进行的初始化，同时Vue3版本中默认不安装API语法提示依赖，需要通过手动方式进行安装

```shell
npm i @dcloudio/types miniprogram-api-typings mini-types -D
```

Vue3版本脚手架安装时可能会访问官方仓库失败的情况，可以进行相关文件的更新

```shell
npx @dcloudio/uvm
```

