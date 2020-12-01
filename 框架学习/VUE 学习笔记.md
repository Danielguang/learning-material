# VUE 学习笔记

打包 输出目录

 DIST

- cjs web pack 1 . browserfiy
- esm webpack 2+
- Umd 兼容 cjs 和 esm

## 测试环境

- 安装依赖

- 安装rollup npm i rollup -g

- 修改dev 脚本

- 执行 npm run dev命令

  ```javascript
  npm run dev
  ```

##  入口文件

/src/platforms/web/entry-runtime-with-compiler.js

扩展了 $mount 方法，处理template和el 选项，尝试编译

src/platforms/web/runtime/index.js

定义 $mount 方法，执行挂载mountComponent(this, el, hydrating) 方法

src/core/index.js

``` javascript
  initUse(Vue)
  initMixin(Vue)
  initExtend(Vue)
  initAssetRegisters(Vue)
```

src/core/instance/index.js

构造函数定义点

``` initMixin(Vue) // 实现了 _init 方法
stateMixin(Vue)

eventsMixin(Vue)

lifecycleMixin(Vue)

renderMixin(Vue)
initMixin(Vue) // 实现了 _init 方法
```

init 

``` javascript
		initLifecycle(vm)
    initEvents(vm)
    initRender(vm)
    callHook(vm, 'beforeCreate')
    initInjections(vm) // resolve injections before data/props
    initState(vm)
    initProvide(vm) // resolve provide after data/props
    callHook(vm, 'created')
```

## 数据响应式

src/core/instance/state.js

数据的初始化

initData()

判断重复，调用observe()

返回一个observer 对象实例

Observe src/core/observer/index.js

判断数据对象的类型，做相应处理



defineReactive

给 data 中每一个key 定义数据劫持
