# Webpack

Webpack[官网](https://www.webpackjs.com/)

## Webpack安装

安装webpack npm i Webpack Webpack- cli -D

查看webpck版本 npx webpack -v

npx webpack 文件名 打包文件

## Webpack操作

1.可以解析文件之间的依赖关系(ESModeule/CommonJS) 进行打包

2.webpack 可以解析node代码

3.webpack 可以压缩代码

## Webpack 配置

webpack.comfig.js文件 在node环境进行配置运行，在有这个文件的情况中可以进行指令修改

```js
const path = require('path')
module.exports = {
	mode:'development',//打包的代码后在开发环境中 打包后的代码不会被压缩
    entry:'./index.js',//打包的文件
    output:{ //打包后文件的输入的地址
        path:path.join(__dirname,'dist') //path必须是个绝对路径
    },
    //处理非js文件的配置
    module:{
        rule:[
            {
            	test:/\.gif$/, //匹配道gif结尾
            	use:['url-loader']
        	}
        ]
    }
    
}
```

package 文件可以修改webpack指令

```

```

