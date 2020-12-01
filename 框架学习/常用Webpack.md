# Webpack 学习

1. 拆分和merge
2. ES6  ['bable loader']
3. 启动本地服务
4. 处理样式
5. 处理图片

## 多入口

1. entry 

2. ``` javascript
    entry: {
           index: path.join(srcPath, 'index.js'),
           other: path.join(srcPath, 'other.js')
       },
   ```

3. output[name[contentHas]

```javascript
  output: {
        // filename: 'bundle.[contentHash:8].js',  // 打包代码时，加上 hash 戳
        filename: '[name].[contentHash:8].js', // name 即多入口时 entry 的 key
        path: distPath,
        // publicPath: 'http://cdn.abc.com'  // 修改所有静态文件 url 的前缀（如 cdn 域名），这里暂时用不到
    },
```



1. HtmlWebpaclPlugin
   1. Chunks:['other']

## 抽离CSS

MiniCssExtractPlugin， 不使用style Loader => miniCssEtractPlugin

``` javascript
  new MiniCssExtractPlugin({
            filename: 'css/main.[contentHash:8].css'
        })
```

压缩文件

``` javascript
 optimization: {
        // 压缩 css
        minimizer: [new TerserJSPlugin({}), new OptimizeCSSAssetsPlugin({})],
    }
```

### 抽离公共代码

- Chunks 一段代码

```javascript
splitChunks: {
            chunks: 'all',
            /**
             * initial 入口 chunk，对于异步导入的文件不处理
                async 异步 chunk，只对异步导入的文件处理
                all 全部 chunk
             */

            // 缓存分组
            cacheGroups: {
                // 第三方模块
                vendor: {
                    name: 'vendor', // chunk 名称
                    priority: 1, // 权限更高，优先抽离，重要！！！
                    test: /node_modules/,
                    minSize: 0,  // 大小限制
                    minChunks: 1  // 最少复用过几次
                },

                // 公共的模块
                common: {
                    name: 'common', // chunk 名称
                    priority: 0, // 优先级
                    minSize: 0,  // 公共模块的大小限制
                    minChunks: 2  // 公共模块最少复用过几次
                }
            }
        }
```

```javascript
    // 多入口 - 生成 index.html
        new HtmlWebpackPlugin({
            template: path.join(srcPath, 'index.html'),
            filename: 'index.html',
            // chunks 表示该页面要引用哪些 chunk （即上面的 index 和 other），默认全部引用
            chunks: ['index', 'vendor', 'common']  // 要考虑代码分割
        }),
        // 多入口 - 生成 other.html
        new HtmlWebpackPlugin({
            template: path.join(srcPath, 'other.html'),
            filename: 'other.html',
            chunks: ['other', 'common']  // 考虑代码分割
        })
```

## 懒加载

 默认支持

Module, chunk, bundle

- Module - 各个源码文件，webpack 一切皆模块
- chunk - 多模块合并成的， 如 entry, import(), spliteChunk
- Bundle - 最终的输出文件



### Webpack 性能优化

- 优化babel - loader
- Ignore Plugin
- noParse
- happyPack
- ParallelUglifyPlugin
- 热更新
- DLLPlugin



1. 优化babel -loader

``` javascript
{
  test:/\.js$/,
  use:['babel-loader?cachDirctory']// 开启缓存
  include: path.resolve(__dirname, 'src');
}
```

2. ignorePlugin 插件 去掉不用引入

``` javascript
 // 忽略 moment 下的 /locale 目录
       new webpack.IgnorePlugin(/\.\/locale/, /moment/),
```

3. happyPack 多进程打包
   1. JS 单线程，开启多进程打包
   2. 提高构建速度（特别是多核CPU）

4. 热更新

   ``` javascript
   const HotModuleReplacementPlugin = require('webpack/lib/HotModuleReplacementPlugin');
   ```

5. Dllplugin
   1. 一般针对稳定的版本
   2. 构建一次，不用重复打包
   3. Dllplugin - 打包出 dll文件
   4. DllReferencesPlugin - 使用dll 文件

优化

1. 小图片base64编码 （url loader）

2. 提取公共代码 (splite , splitChunks {cacheGroups})

3. Bundle 加hash [contentHash:8]

4. ignorePlugin

5. 懒加载

6. 使用CND加速

7. Tree shaking 

   1. 使用purifyCSS
   2. JS 默认开启

8. Scope Hositing

   1. 代码体积更小
   2. 创建函数作用域

   ```javascript
   new webpack.optimize.ModuleConcatenationPlugin()
   
   ```



### Babel

1. 环境搭建 & 基本配置
2. Babel-polyfill
3. Babel-runtime



## WebPack 

1. 基本配置
2. 高级配置
3. 优化代码
4. 构建流程概述
5. 优化打包流程
6. Babel

### 基本配置

1. 拆分配置和merge
2. 启动本地服务
3. 处理Es6
4. 处理样式
5. 处理图片

高级配置

1. 多入口
2. 抽离css 文件
3. 抽离公共代码
4. 懒加载
5. 处理JSX
6. 处理Vue

产出代码

1. 小图片base64
2. Bundle + has
3. 懒加载
4. 提取公共代码
5. 使用CDN加速
6. ignorePlugin
7. 使用production
8. Scope Hositing
