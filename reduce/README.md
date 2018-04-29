# 强大的reduce

数组的reduce方法用途很广。它一般被用来把数组中每一项规约到单个值。但是你可以利用它做更多的事。

## 使用reduce同时实现map和filter

假设现在有一个数列，你希望更新它的每一项（map的功能）然后筛选出一部分（filter的功能）。如果是先使用map然后filter的话，你需要遍历这个数组两次。

在下面的代码中，我们将数列中的值翻倍，然后挑选出那些大于50的数。有注意到我们是如何非常高效地使用reduce来同时完成map和filter方法的吗？


```js
const numbers = [10, 20, 30, 40];

const doubledOver50 = numbers.reduce((finalList, num) => {

  num = num * 2;

  if(num > 50) {
    finalList.push(num);
  }
  return finalList;
},[]);
doubledOver50;// [60, 80]
```

如果你认真阅读了上面的代码，你应该能理解reduce是可以取代map和filter的。

## 使用reduce匹配圆括号

reduce的另外一个用途是能够匹配给定字符串中的圆括号。对于一个含有圆括号的字符串，我们需要知道 (和 )的数量是否一致，并且 (是否出现在 )之前。

下面的代码中我们使用reduce可以轻松地解决这个问题。我们只需要先声明一个 counter变量，初值为0。在遇到 (时counter加一，遇到 )时counter减一。如果左右括号数目匹配，那最终结果为0。

```js
// Returns 0 if balanced.
const isParensBalanced = (str) => {
  return str.split('').reduce((counter, char) => {
    if(counter < 0) { //matched ")" before "("
      return counter;
    } else if(char === '(') {
      return ++counter;
    } else if(char === ')') {
      return --counter;
    }  else { //matched some other char
      return counter;
    }

  }, 0); //<-- starting value of the counter
}

isParensBalanced('(())')// 0 <-- balanced

isParensBalanced('(asdfds)')//0 <-- balanced

isParensBalanced('(()') // 1 <-- not balanced

isParensBalanced(')(') // -1 <-- not balanced
```

## 统计数组中相同项的个数

很多时候，你希望统计数组中重复出现项的个数然后用一个对象表示。那么你可以使用reduce方法处理这个数组。

下面的代码将统计每一种车的数目然后把总数用一个对象表示。

```js
var cars = ['BMW','Benz', 'Benz', 'Tesla', 'BMW', 'Toyota'];
var carsObj = cars.reduce(function (obj, name) {
   obj[name] = obj[name] ? ++obj[name] : 1;
  return obj;
}, {});
carsObj; // => { BMW: 2, Benz: 2, Tesla: 1, Toyota: 1 }
```

reduce的其他用处实在是太多了，我建议你阅读MDN的相关代码示例。