### Web 知识

#### 安全

- XSS 跨站请求攻击
  - 博客网站 发表博客，嵌入<script>, 获取cookie 发送到我的服务器
  - 脚本内容，获取cookie， 发送到我的服务器（服务器配合跨域）
  - 解决方法
    - 替换特殊字符串< => &lt；
- XSRF 跨站请求伪造
  - 正在购物，看中商品，产品id 是100
  - 付费接口x xx.com/pay?id=100
  - 发送邮件，但是邮件中隐藏一个<img src = xxx.con/pay?id=200 />
  - 使用post 接口，增加验证

#### http 协议

### Ajax

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'api',false);
xhr.onreadtstateChange
```

XHR.status

- 2xx - 表示成功处理
- 3xx - 重新定向
- 4xx 客户端请求错误
- 5XX 服务端错误