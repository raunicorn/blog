# JS不支持反向预查 囧

今天做一道题时遇到一个问题，题目如下：

完成一个 extractStr 函数，可以把一个字符串中所有的 : 到 . 的子串解析出来并且存放到一个数组当中，例如：
extractStr('My name is:Jerry. My age is:12.') // => ['Jerry', '12']
注意，: 和 . 之间不包含 : 和 .。也即是说，如果 ::abc..，则返回 ['abc']。

于是我写出如下答案：

```javascript
const extractStr = (str) => {
  let reg=/(?<=:)[^:]*?(?=\.)/g;
  return str.match(reg)||[];
}
```

结果提示我正则表达式不正确，找了很久原因发现JS竟然不支持反向预查，只好将答案改为如下代码：

```javascript
const extractStr = (str) => {
  let reg=/:[^:]*?(?=\.)/g;
  let result= str.match(reg)||[];
  return result.map(v=>v.replace(':',''));
}
```