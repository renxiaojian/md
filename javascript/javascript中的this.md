## 普通函数调用

	function person(){
		// "use strict";
		this.name = 'Jim';
		console.log(this);
		console.log(this.name);
	}
	person();	//输出 window Jim

- 默认绑定规则：this绑定给window。`person() ==> window.person()`
- 在严格模式下，默认绑定规则会把 `this` 绑定 `undefined` 上

## 作为对象方法调用

	var name = 'Jim';
	var personA = {
		name:'Json',
		showName:function(){
			console.log(this.name);
		}
	}
	var personB = {
		name:'Lucy',
		showName:personA.showName
	}
	var personC = {
		name:'jian',
		showName:function(){
			var fun = personA.showName;
			fun();
		}
	}
	personA.showName();		//	Json	this指向personA对象
	var showNameA = personA.showName;
	showNameA();			//	Jim		this指向window对象
	personB.showName();		//	Lucy
	this关键字虽然在personA.showName中声明,但运行的时候是personB.showName,所以this指向personB.showName行数的当前对象，故最后执行输出的是Lucy.
	personC.showName();		//  Jim		this指向window对象
- 一般而言，在Javascript中，this指向函数执行时的当前对象。
- 当没有明确的执行时的当前对象时，this指向全局对象window。(也能理解成showNameA是window对象下的方法，所以执行时的当前对象时window。但局部变量引用的函数上，却无法这么解释)
- 值得注意，该关键字在Javascript中和执行环境，而非声明环境有关。

## 作为构造函数来调用(new关键字)
	
	function Person(name){
		this.name = name;
	}
	var personA = Person("Jim");
	console.log(personA.name);		// undefined
	console.log(window.name);		// Jim
	var personB = new Person("Lucy");
	console.log(personB.name);		// Lucy
- 没有new关键字，相当于普通函数调用，`this` 指向window
- new关键字后的构造函数中的this指向用该构造函数构造出来的新对象

## call/apply方法的调用

> apply和call能够强制改变函数执行时的当前对象，让this指向其他对象。(apply和call较为类似)

	var name = "window";
    
	var someone = {
	    name: "Bob",
	    showName: function(){
	        alert(this.name);
	    }
	};
	
	var other = {
	    name: "Tom"
	};    
	
	someone.showName.apply();    		//window
	someone.showName.apply(other);    	//Tom

- apply用于改变函数执行时的当前对象，当无参数时，当前对象为window，有参数时当前对象为该参数。

## bind()方法

	var name="window";
    function Person(name){
        this.name=name;
        this.sayName=function(){
            setTimeout(function(){
                console.log("my name is "+this.name);
            },50)
        }
    }
    var person=new Person("Jim");
    person.sayName();			// my name is window	setTimeout()==>window.setTimeout()

那么如何才能输出"my name is Jim"呢？

	var name="window";
    function Person(name){
        this.name=name;
        this.sayName=function(){
            setTimeout(function(){
                console.log("my name is "+this.name);
            }.bind(this),50)
        }
    }
    var person=new Person("Jim");
    person.sayName();			// Jim

- 或者 `_this = this` 保存this指向

## Eval函数

>对于eval函数，其执行时候似乎没有指定当前对象，但实际上其this并非指向window，因为该函数执行时的作用域是当前作用域，即等同于在该行将里面的代码填进去。

	var name="window";
    var person={
        name:"Jim",
        showName:function(){
            eval("console.log(this.name)");
        }
    }
    person.showName();  // Jim
    var a=person.showName;
    a();				//	window

## 箭头函数

>es6里面this指向固定化，始终指向外部对象，因为箭头函数没有this,因此它自身不能进行new实例化,同时也不能使用call, apply, bind等方法来改变this的指向

	function Timer() {
        this.seconds = 0;
        setInterval( () => this.seconds ++, 1000);
    } 
    var timer = new Timer();
    setTimeout( () => console.log(timer.seconds), 3100);
	//	3

- 在构造函数内部的setInterval()内的回调函数，this始终指向实例化的对象，并获取实例化对象的seconds的属性,每1s这个属性的值都会增加1。否则最后在3s后执行setTimeOut()函数执行后输出的是0