### React 学习笔记

```javascript
cnpm init react-app ToDoList
```

```javascript
npx create-react-app mj-ts-template --template typescript // 创建typescript 项目
```



### 高阶特性 

1. 函数组件 （没有生命周期）
2. 非受控组件 （input type = file）
3. Portals ( 渲染到父组件)
4. Context
5. 异步组件 React.lazy React suspend



### 性能优化

1. SCU
2. pureComponent



函数编程

1. 一种编程范式
2. 纯函数
3. 不可变值



## 回顾vdom 和diff

- 只比较同一层级，不跨级比较
- tag 不相同，则直接删掉重建，不再深度比较
- tag 和 key， 两者都相同，则认为是相同节点，不再深度比较



## setState 和batchUpdate

1. setState 主流程

2. batchUpdate 机制
   1. 生命周期（和它调用的函数）
   2. React 中注册的事件（和它调用的函数）
   3. React可以管理入口
3. batchUpdate不能命中
   1. setTimeOut
   2. 自定义事件

3. transcation 机制



组件更新

1 setState(new State) => dirtyComponents

2. Patch(node)
   1. Reconcliiation 阶段 执行diff算法
   2. commit 阶段 - 将diff 结果渲染DOM中

React fiber

1. 将reconciliation 进行拆分
2. DOM 需要渲染的时候，暂停，空闲的时候恢复（windows.requestIdeCallback()）





### redux

```javascript
export const addToDoAsync = text =>{
  return (dispatch) =>{
    fetch(rul).then(res)=>{
      // 执行异步action
    }
  }
}
// create store thunk
import thunk from 'redux-thunk';
import {applyMiddleware} from 'redux';


const store = createStore(rootReducer, applyMiddleware(thunk))
```



### MiddleWare

![image-20201013233423409](/Users/zhaoguangyu/Library/Application Support/typora-user-images/image-20201013233423409.png)

``` javascript
let next = store.dispatch;
store.dispatch = function dispatchAndlog(action){
  console.log('dispathcing', action);
  next(action)
  console.log('next state');
}
```

 ![image-20201013233944655](/Users/zhaoguangyu/Library/Application Support/typora-user-images/image-20201013233944655.png)