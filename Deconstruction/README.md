# 解构(Deconstruction)

## 对象解构

### 删除不需要的属性

有时候你不希望保留某些对象属性，也许是因为它们包含敏感信息或仅仅是太大了（just too big）。你可能会枚举整个对象然后删除它们，但实际上只需要简单的将这些无用属性赋值给变量，然后把想要保留的有用部分作为剩余参数就可以了。

下面的代码里，我们希望删除 _internal和 tooBig参数。我们可以把它们赋值给 internal和 tooBig变量，然后在 cleanObject中存储剩下的属性以备后用。

```js
let obj = {
  el1: '1',
  _internal:"secret",
  tooBig:{},
  el2: '2',
  el3: '3'
};
let {_internal, tooBig, ...cleanObject} = obj;
console.log(cleanObject); // {el1: '1', el2: '2', el3: '3'}
```

### 在函数参数中解构嵌套对象

在下面的代码中， engine是对象 car中嵌套的一个对象。如果我们对 engine的 vin属性感兴趣，使用解构赋值可以很轻松地得到它。

```js
var car = {
  model: 'bmw 2018',
  engine: {
    v6: true,
    turbo: true,
    vin: 12345
  }
}
const modelAndVIN = ({model, engine: {vin}}) => {
  console.log(`model: ${model} vin: ${vin}`);
}
modelAndVIN(car) // model: bmw 2018 vin: 12345
```

### 合并对象

```js
let obj1 = { a: 1, b: 2, c: 3 }
let obj2 = { b: 30, c:40, d: 50 }
let merged = {...obj1, ...obj2}
console.log(merged) // {a: 1, b: 30, c: 40, d: 50}
```

## 数组解构

有时候你会将函数返回的多个值放在一个数组里。我们可以使用数组解构来获取其中每一个值。

### 数值交换

```js
let param1 = 1;
let param2 = 2;
//swap and assign param1 & param2 each others values
[param1, param2] = [param2, param1];
console.log(param1) // 2
console.log(param2) // 1
```

### 接收函数返回的多个结果

在下面的代码中，我们从 /post中获取一个帖子，然后在 /comments中获取相关评论。由于我们使用的是 async/await，函数把返回值放在一个数组中。而我们使用数组解构后就可以把返回值直接赋给相应的变量。

```js
async function getFullPost(){
  return await Promise.all([
    fetch('/post'),
    fetch('/comments')
  ]);
}
const [post, comments] = getFullPost();
```