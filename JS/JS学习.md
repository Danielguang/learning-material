## 变量和类型计算





## 原型链

​	

![image-20201022113853195](/Users/zhaoguangyu/Library/Application Support/typora-user-images/image-20201022113853195.png)

### 闭包

函数定义的时候向上查找，而不是在函数执行的时候向上查找！！



### This

1. 作为普通函数
2. 使用 call, apply, bind
3. 作为对象方法被调用
4. 在c lass 方法中调用
5. 箭头函数

### JS原型链

```javascript
Function.prototype === Function.__proto__
```

### 前端存储

``` javascript
Document.cookie= 'a=300,b=400'
```

Cookie:

1. 4KB
2. http 请求时需要发送到服务端

Localstorage 和SessionStorage

- 最大 5M



### BOM(Browser Object Model)

- navigator
- screen
- location
- history

### DOM 操作

```javascript
const flag = Document.createDocumentFragment();
listNode.appendChild(frag);
```



### sort

- 会修改原函数
- 如果 `compareFunction(a, b)` 小于 0 ，那么 a 会被排列到 b 之前；
- 如果 `compareFunction(a, b)` 等于 0 ， a 和 b 的相对位置不变
- 如果 `compareFunction(a, b)` 大于 0 ， b 会被排列到 a 之前。



### 数字的格式化

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat

``` javascript
new Intl.NumberFormat("en-US", {

  style: "decimal",

  minimumFractionDigits: 2,

});
```



