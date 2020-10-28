<!--
 * @Author: Li Zhiliang
 * @Date: 2019-09-03 16:44:00
 * @LastEditors: Li Zhiliang
 * @LastEditTime: 2020-09-30 14:51:05
 * @FilePath: /ScorpioBook/functional/regular.md
-->
## 常用的正则校验 

```js
// 匹配邮箱
let reg = /^([a-zA-Z]|[0-9])(\w|\-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/;

// (新)匹配手机号
// let reg = /^1[0-9]{10}$/;

// (旧)匹配手机号
let reg = /^1(3|4|5|7|8)[0-9]{9}$/;

// 匹配8-16位数字和字母密码的正则表达式
let reg = /^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{8,16}$/;

// 匹配国内电话号码 0510-4305211
// let reg = /\d{3}-\d{8}|\d{4}-\d{7}/;

// 匹配身份证号码
let reg=/(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/;

// 匹配腾讯QQ号
let reg = /[1-9][0-9]{4,}/;

// 匹配ip地址
let reg = /\d+\.\d+\.\d+\.\d+/;

// 匹配中文
let reg = /^[\u4e00-\u9fa5]*$/;
```