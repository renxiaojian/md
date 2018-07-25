> 首先看一个判断题：null和undefined 是否相等

	console.log(null==undefined)	//true
	console.log(null===undefined)	//false

> 观察可以发现：null和undefined 两者相等，但是当两者做全等比较时，两者又不等。

## Undefined类型

只有一个值 `undefined` ，声明变量未初始化时，这个变量的值就是 `undefined`。

对未初始化和未声明的变量执行 `typeof` 操作符都返回了 `undefined`。

实际上，`undefined` 值是派生自 `null`值的，ECMAScript标准规定对二者进行相等性测试要返回true。

## Null类型

只有一个值 `null` ,即“空值”，代表一个空对象指针。使用 `typeof` 操作符运算得到 “object”。

## 最初设计

	console.log(Number(null))		// 0
	console.log(Number(undefined))	// NaN

> null是一个表示"无"的对象，转为数值时为 `0`；undefined是一个表示"无"的原始值，转为数值时为`NaN`。

## 典型用法

> `null` 表示"没有对象"，即该处不应该有值。

1.作为函数的参数，表示该函数的参数不是对象。

2.作为对象原型链的终点。

> `undefined` 表示"缺少值"，就是此处应该有一个值，但是还没有定义。

1.变量被声明了，但没有赋值时，就等于undefined。

2.调用函数时，应该提供的参数没有提供，该参数等于undefined。

3.对象没有赋值的属性，该属性的值为undefined。

4.函数没有返回值时，默认返回undefined。

> 参考资料：阮一峰的网络日志 [undefined与null的区别](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html?utm_source=tuicool&utm_medium=referral)