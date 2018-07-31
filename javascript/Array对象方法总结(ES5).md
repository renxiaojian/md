## ES5数组方法

### isArray()

> 判断对象是否为数组。（它可以弥补typeof运算符的不足）

	var a = [1,2,3];
	typeof a			//"object"
	Array.isArray(a)	// true

### valueOf()

> 返回数组对象的原始值

	var a = [1,2,3];
	a.valueOf()		//[1,2,3]

### toString()

> 返回数组的字符串形式

	var a = [1,2,3];
	a.toString()	//"1,2,3"
	
	var b = [1,2,3,[4,5,6]]
	b.toString();	//"1,2,3,4,5,6"

### push()

> 可向数组的末尾添加一个或多个元素，并返回新的长度。注意，该方法会改变原数组。

	var a = ['a'];
	a.push(1)		//	2
	a.push('b')		//	3
	a.push(true,{})	//	5
	a				// ['a',1,'b',true,{}]

### pop()

> 用于删除数组的最后一个元素并返回删除的元素。注意，该方法会改变原数组。

	var a = ['a','b','c'];
	a.pop()		// 'c'
	a			// ['a','b']
注：对空数组使用pop方法，不会报错，而是返回undefined。

### shift()

> 用于把数组的第一个元素从其中删除，并返回第一个元素的值。注意，该方法会改变原数组。

	var a = ['a','b','c'];
	a.shift()		//	'a'
	a				//	['b','c']

### unshift()

> 可向数组的开头添加一个或更多元素，并返回新的长度。注意，该方法会改变原数组。

	var arr = ['c','d'];
	arr.unshift('a','b')	//	4
	arr						//['a','b','c','d']

### concat()

> 用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

	[1, 2, 3].concat(4, 5, 6)	// [1, 2, 3, 4, 5, 6]
	
	// 等同于
	[1, 2, 3].concat(4, [5, 6])
	[1, 2, 3].concat([4], [5, 6])

> concat方法也可以用于将对象合并为数组。

	[].concat({a: 1}, {b: 2})	// [{ a: 1 }, { b: 2 }]
	[].concat({a: 1}, [2])		// [{a: 1}, 2]
	[2].concat({a: 1})			// [2, {a: 1}]

### reverse()

> 用于颠倒数组中元素的顺序，返回改变后的数组。注意，该方法将改变原数组。

	var a = ['a', 'b', 'c'];
	a.reverse() // ["c", "b", "a"]
	a // ["c", "b", "a"]

### join()

> 以参数作为分隔符，将所有数组成员组成一个字符串返回。如果不提供参数，默认用逗号分隔。

	var a = [1, 2, 3, 4];
	
	a.join(' ') 		// '1 2 3 4'
	a.join(' | ') 		// "1 | 2 | 3 | 4"
	a.join() 			// "1,2,3,4"

---

### slice()

> 方法用于提取原数组的一部分，返回一个新数组，原数组不变。

	// 格式
	arr.slice(start_index, end_index);

	// 用法
	var a = ['a', 'b', 'c'];
	
	a.slice(0) 		// ["a", "b", "c"]
	a.slice(1) 		// ["b", "c"]
	a.slice(1, 2) 	// ["b"]
	a.slice(2, 6) 	// ["c"]
	a.slice() 		// ["a", "b", "c"] 相当于复制数组

> 如果slice方法的参数是负数，则表示倒数计算的位置。

	var a = ['a', 'b', 'c'];
	a.slice(-2) 	// ["b", "c"]
	a.slice(-2, -1) // ["b"]
> 如果参数值大于数组成员的个数，或者第二个参数小于第一个参数，则返回空数组。

	var a = ['a', 'b', 'c'];
	a.slice(4) 		// []
	a.slice(2, 1) 	// []

### splice()

> 用于插入、删除或替换数组的元素。返回值是被删除的元素。注意，该方法会改变原数组。
> splice的第一个参数是删除的起始位置，第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素。

	//格式
	array.splice(index,howmany,item1,.....,itemX)

	var a = ['a', 'b', 'c', 'd', 'e', 'f'];
	a.splice(4, 2) 		// ["e", "f"]
	a 					// ["a", "b", "c", "d"]

	从倒数第四个位置c开始删除两个成员。
	var a = ['a', 'b', 'c', 'd', 'e', 'f'];
	a.splice(-4, 2) 	// ["c", "d"]

> 如果只是单纯地插入元素，splice方法的第二个参数可以设为0。

	var a = [1, 2, 3];

	a.splice(1, 0, 'a') 	// []
	a 					// [1, a, 2, 3]

### sort()

> 对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。

	var points = [40,100,1,5,25,10];
	points.sort(function(a,b){return a-b});
	//	1,5,10,25,40,100

	var points = [40,100,1,5,25,10];
	points.sort(function(a,b){return b-a});
	//	100,40,25,10,5,1

### *map()*

> 返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

> map方法接受一个函数作为参数。该函数调用时，map方法会将其传入三个参数，分别是当前成员、当前位置和数组本身。
	
	array.map(function(currentValue,index,arr))
	
	var numbers = [1, 2, 3];

	numbers.map(function (n) {
	  return n + 1;
	});							// [2, 3, 4]	
	numbers						// [1, 2, 3]
	
	[1, 2, 3].map(function(elem, index, arr) {
	  return elem * index;
	});							// [0, 2, 6]
- map() 不会对空数组进行检测。
- map() 不会改变原始数组。

### forEach()

> 方法与map方法很相似，也是遍历数组的所有成员，执行某种操作，但是forEach方法一般不返回值，只用来操作数据。如果需要有返回值，一般使用map方法。

	//格式
	array.forEach(function(currentValue, index, arr), thisValue)

	function log(element, index, array) {
	  console.log('[' + index + '] = ' + element);
	}
	
	[2, 5, 9].forEach(log);
	// [0] = 2
	// [1] = 5
	// [2] = 9

- forEach方法也可以接受第二个参数，用来绑定回调函数的this关键字。
- forEach方法无法中断执行，总是会将所有成员遍历完。如果希望符合某种条件时，就中断遍历，要使用for循环。
	
### *filter()*

> 创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。该方法不会改变原数组。

	[1, 2, 3, 4, 5].filter(function (elem) {
	  return (elem > 3);
	})
	// [4, 5]

### some()，every()

1.用来判断数组成员是否符合某种条件。

2.它们接受一个函数作为参数，所有数组成员依次执行该函数，返回一个布尔值。该函数接受三个参数，依次是当前位置的成员、当前位置的序号和整个数组。

3.不会对空数组进行检测,不会改变原始数组。

> some()

	var arr = [1, 2, 3, 4, 5];
	arr.some(function (elem, index, arr) {
	  return elem >= 3;
	});
	// true

- 如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测。
- 如果没有满足条件的元素，则返回false。

> every()

	var arr = [1, 2, 3, 4, 5];
	arr.every(function (elem, index, arr) {
	  return elem >= 3;
	});
	// false
- 如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。
- 如果所有元素都满足条件，则返回 true。

### reduce()，reduceRight()

> `reduce()` 将数组元素计算为一个值（从左到右）。

> `reduceRight()` 将数组元素计算为一个值（从右到左）。

这两个方法的第一个参数都是一个函数。该函数接受以下四个参数：

1.累积变量，默认为数组的第一个成员

2.当前变量，默认为数组的第二个成员

3.当前位置（从0开始）

4.原数组

	[1, 2, 3, 4, 5].reduce(function(x, y){
	  console.log(x, y)
	  return x + y;
	});
	// 1 2
	// 3 3
	// 6 4
	// 10 5
	//最后结果：15

> 利用reduce方法，可以写一个数组求和的sum方法。

	let arr = [234,234,34,34,12]
	Array.prototype.sum = function () {
	    return this.reduce(function (partial, value) {
	        return partial + value
	    })
	}
	console.log(arr.sum())  //584

> 如果要对累积变量指定初值，可以把它放在reduce方法和reduceRight方法的第二个参数。

	[1, 2, 3, 4, 5].reduce(function(x, y){
	  return x + y;
	}, 10);
	// 25

### indexOf()，lastIndexOf() 

> `indexOf()` 返回给定元素在数组中第一次出现的位置，如果没有出现则返回-1。

> `lastIndexOf()` 返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1。

	var a = ['a', 'b', 'c'];

	a.indexOf('b') // 1
	a.indexOf('y') // -1

> indexOf方法还可以接受第二个参数，表示搜索的开始位置。

	['a', 'b', 'c'].indexOf('a', 1) // -1