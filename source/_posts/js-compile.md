---
title: javaScripte预编译
date: 2019-04-13 14:09:51
tag:  javaScript
---

##js预编译
###预编译过程 发生在函数执行的前一刻
步骤：</br>

1. 创建AO对象 activation object(执行期上下文as作用域)
2. 找形参和变量声明，将变量和形参名作为AO的属性名,值为undefined
3. 将实参和形参统一
4. 在函数体里找函数声明,把函数名当属性，值为函数体


## 例子讲解

代码：

```
 <script>    
        function fn(a){
            console.log(a)   //func
            var a = 123;
            console.log(a)   // 123

            function a(){}
            console.log(a)  //123

            var b = function(){}
            console.log(b)     // func
            function d(){}
        }

        fn(1)
    </script>

```

编译过程

1. 创建AO对象   
	
	```	
	AO={
	
	}
 	```
2. 找形参和变量声明,并复制undefined 有形参a 及变量 a,b
	
	```
	AO={
		a: undefined
		b: undefined
	}
	```
3. 将实参和形参统一

	```

	AO={
		a: 1
		b: undefined
	}

	```

4. 在函数体里找函数声明 有a d

	```
	AO={
		a: function a(){}
		b: undefined
		d: function d(){}
	}
	```
 所以打印结果为
 function 123 123  function

 
 

