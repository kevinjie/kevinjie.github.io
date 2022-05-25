# 偏函数、柯里化、compose和pipe

#javascript #partial #curry #compose #pipe

## partial

> 将接收n个参数的函数转换为接收n-x个参数的函数

```js
function partial(fn, ...initArgs) {
  return function(...finallyArgs) {
    return fn.apply(this, [...initArgs, ...finallyArgs])
  }
}
```
## curry

> 将接收n个参数的函数转换为n个接收一元参数的函数

```js
function curry(func) {
  return curried(...args) {
    if (func.length <= args.length) {
      return func.apply(this, args)
    } else {
      return function(...newArgs) {
        return curried.apply(this, [...args, ...newArgs])
      }
    }
  }
}
```
## compose

> 可以接收任意数量的参数，参数都是函数，函数的执行顺序是**从右到左**，初始函数在最右边，可以接收多元参数，其他函数只能接收一元参数

```js
const compose = (...funcs) => (...args) => funcs.reduceRight((prev, next) => {
  return Array.isArray(prev) ? next.apply(null, prev) : next.call(null, prev)
}, args)
```

## pipe

> 可以接收任意数量的参数，参数都是函数，函数的执行顺序是**从左到右**，初始函数在最左边，可以接收多元参数，其他函数只能接收一元参数

```js
const pipe = (...funcs) => (...args) => funcs.reduce((prev, next) => {
  return Array.isArray(prev) ? next.apply(null, prev) : next.call(null, prev)
}, args)
```