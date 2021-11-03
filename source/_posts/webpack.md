---
title: 'Webpack'
date: 2019-10-21 09:55:18
tags: [Webpack]
published: true
hideInList: false
feature: 
---
[从WebPack 4.X 到 Vue-Cli 3.X 一篇就够](https://juejin.im/post/5dab320851882565f7660c5e)
```js
/* 
    在这个文件中设置我们自定义的打包规则
        1. 所有的规则都写在module.exports={}中
*/
let path = require('path');
let HtmlWebpackPlugin = require('html-webpack-plugin');
let MiniCssExtractPlugin = require('mini-css-extract-plugin'), //把css单独分离出来
    OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin'), //压缩css
    UglifyjsWebpackPlugin = require('uglifyjs-webpack-plugin'); //压缩js
let webpack = require('webpack');
//导入进来的插件都是一个类  new HtmlWebpackPlugin({});

module.exports = {
    //配置优化规则
    optimization: {
        //设置压缩方式
        minimizer: [
            //压缩css  (产生问题：JS压缩不在执行自己默认的压缩方式了，也走的是这个插件，从而导致无法压缩，所以必须设置JS的压缩方式)
            new OptimizeCssAssetsWebpackPlugin(),
            //压缩js
            new UglifyjsWebpackPlugin({
                cache: true, //是否使用缓存
                parallel: true, //是否是兵法编译
                sourceMap: true, //启动源码映射（方便调试）
            })
        ]
    },
    //配置环境 开发环境development  生产环境production(默认)
    mode: 'production',
    //入口
    entry: ['@babel/polyfill', './src/index-my.js'],
    //出口
    output: {
        //输出文件的文件名
        //bundle.min.[hash].js 让每一次生成的文件名都带着hash值
        filename: 'bundle.min.js',
        // filename: 'bundle.min.[hash].js',
        //输出的目录必须是绝对路径,__dirname当前目录
        path: path.resolve(__dirname, 'dist'),
        publicPath: './' //给编译后引入资源地址前面设置的前缀
    },
    //关于webpack-dev-server的一些配置  执行命令：webpack-dev-server --config xxx.js (特点：服务启动后，默认是不关闭的，当我们修改src中的源文件，他会自动进行编译，然后自动刷新浏览器,类似于vscode中的Live Server插件，实时刷新)
    devServer: {
        //创建服务指定的端口号
        port: 3000,
        //显示打包编译进度
        progress: true,
        //指定当前服务处理资源的目录
        contentBase: './dist',
        //编译完成后，自动打开浏览器
        open: true
    },
    //使用插件 (数组)
    plugins: [
        new HtmlWebpackPlugin({
            //不指定模版会按照默认模版创建一个html页面，当然真实项目中一般都是把自己写好的html进行编译
            template: './src/index.html',
            //输出的文件名
            filename: 'index.html',
            //让我们引入js后面加上hash戳（清除缓存）,但是真实项目中我们一般都是每一次编译生成不同的js文件引入
            hash: true,
            //控制压缩
            minify: {
                collapseWhitespace: true,
                removeComments: true,
                removeAttributeQuotes: true,
                removeEmptyAttributes: true
            }
        }),
        new MiniCssExtractPlugin({
            //指定输出的文件名
            filename: 'main.min.css'
        }),
        //在每个模块中都注入$
        new webpack.ProvidePlugin({
            '$': 'jquery'
        }),
    ],
    //使用加载器loader处理规则
    module: {
        rules: [{
            //基于正则匹配处理哪些文件
            test: /\.(css|less)$/,
            //使用哪一个加载器，控制使用的loader（有顺序的：从右到左执行）
            use: [
                // "style-loader", //把编译好的css插入到页面的head中（内嵌式）
                MiniCssExtractPlugin.loader, //使用插件中的loader代替style方式
                "css-loader", //编译解析@import/URL()这种语法
                // "postcss-loader",//设置前缀的加载器
                {
                    loader: "postcss-loader",
                    options: {
                        ident: 'postcss',
                        plugins: [
                            require('autoprefixer')
                        ]
                    }
                },
                {
                    loader: "less-loader", //编译less
                    options: {
                        //加载额外的配置
                    }
                }
            ]
        }, {
            test: /\.js$/,
            //处理编译JS的loader
            use: [{
                loader: 'babel-loader',
                options: {
                    //转换的语法预设（ES6->ES5)
                    presets: [
                        "@babel/preset-env"
                    ],
                    //=>基于插件处理ES6/ES7中CLASS的特殊语法
                    plugins: [
                        ["@babel/plugin-proposal-decorators", {
                            "legacy": true //处理装饰器
                        }],
                        ["@babel/plugin-proposal-class-properties", {
                            "loose": true //处理属性
                        }],
                        "@babel/plugin-transform-runtime"
                    ]
                }
            }],
            //设置编译时忽略的文件和指定编译目录
            include: path.resolve(__dirname, 'src'), //编译的
            exclude: /node_modules/ //忽略的·
        }, {
            //图片处理
            test: /\.(png|jpg|gif|jpeg|ico|webp|bpm)$/i,
            use: [{
                loader: 'url-loader',
                options: {
                    //只要图片小于200KB,在处理的时候直接base64
                    limit: 2 * 1024,
                    //控制打包后图片所在的目录
                    outputPath: 'images'
                }
            }]
        }, {
            //处理HTML文件中导入的img文件
            test: /\.(html|htm|xml)$/i,
            use: ['html-withimg-loader']
        }]
    }
}

```