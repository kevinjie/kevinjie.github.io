# call、apply和bind的实现

#javascript
## call

```js
Function.prototype.newCall = function(context, ...parameter) {
  if (typeof context === 'object') {
    context = context || window
  } else {
    context = Object.create(null)
  }

  const fn = Symbol()

  context[fn] = this
  const result = context[fn](...parameter)

  delete context[fn]

  return result
}
```

## apply

```js
Function.prototype.newApply = function(context, parameter) {
  if (typeof context === 'object') {
    context = context || window
  } else {
    context = Object.create(null)
  }

  const fn = Symbol()

  context[fn] = this
  const result = context[fn](...parameter)

  delete context[fn]

  return result
}
```

## bind

```js
Function.prototype.newBind = function(context, ...initArgs) {
  const self = this
  return function(...finallyArgs) {
    return self.call(context, ...initArgs, ...finallyArgs)
  }
}
```