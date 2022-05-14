# typeof 和 instanceof的原理


- typeof的原理：适合用于判断基本数据类型string，number，boolean，Symbol，null，undefinedjs在底层存储变量时，会在变量的机器码的低位1~3位存储其类型信息
```
	* 000：对象
	* 010：浮点数
	* 100：字符串
	* 110：布尔值
	* 1：整数
	* 0：null
	* -2^30：undefined
```

为了更加准确的判断数据类型，可以使用Object.prototype.toString判断

- instanceof的原理：判断右边变量的prototype是否在左边变量的原型链

```js
function new_instance_of(leftVaule, rightVaule) {
    let rightProto = rightVaule.prototype; // 取右表达式的 prototype 值
    leftVaule = leftVaule.__proto__; // 取左表达式的__proto__值
    while (true) {
        if (leftVaule === null) {
            return false;
        }
        if (leftVaule === rightProto) {
            return true;
        }
        leftVaule = leftVaule.__proto__
    }
}
```
