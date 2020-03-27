参考地址：https://segmentfault.com/a/1190000006178770

### 使用webpack构建本地服务器 ###

想不想让你的浏览器监听你的代码的修改，并自动刷新显示修改后的结果，其实Webpack提供一个可选的本地开发服务器，这个本地服务器基于node.js构建，可以实现你想要的这些功能，不过它是一个单独的组件，在webpack中进行配置之前需要单独安装它作为项目依赖
```
npm install --save-dev webpack-dev-server
```
devserver作为webpack配置选项中的一项，以下是它的一些配置选项，更多配置可参考这里

devserver的配置选项	功能描述

contentBase	默认webpack-dev-server会为根文件夹提供本地服务器，如果想为另外一个目录下的文件提供本地服务器，应该在这里设置其所在目录（本例设置到“public"目录）

port	设置默认监听端口，如果省略，默认为”8080“

inline	设置为true，当源文件改变时会自动刷新页面

historyApiFallback	在开发单页应用时非常有用，它依赖于HTML5 history API，如果设置为true，所有的跳转将指向index.html

把这些命令加到webpack的配置文件中，现在的配置文件webpack.config.js如下所示

```
module.exports = {
  devtool: 'eval-source-map',

  entry:  __dirname + "/app/main.js",
  output: {
    path: __dirname + "/public",
    filename: "bundle.js"
  },

  devServer: {
    contentBase: "./public",//本地服务器所加载的页面所在的目录
    historyApiFallback: true,//不跳转
    inline: true//实时刷新
  } 
}
```
在package.json中的scripts对象中添加如下命令，用以开启本地服务器：

```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack",
    "server": "webpack-dev-server --open"
  },
```
在终端中输入npm run server即可在本地的8080端口查看结果


