# ES6

## 知识点

### 1.var let const的各自特点

var：

​	1.函数作用域，区别if代码块。

​	2.函数作用域内部声明的变量, 外部无法使用，声明在外边，则为全局变量。

​	3.允许修改，在内在逻辑复杂的js中，被修改后不容易发现bug，难以定位。

​	4.可以重复声明

let：

​	1.块级作用域

​	2.不可以重复声明，全局声明和局部声明不算重复声明

​	3.可以修改值	

const：

​	1.块级作用域

​	2.不可以重复声明，全局声明和局部声明不算重复声明

​	3.不可以修改 --- 常量和引用对象的指针

​	4.但是可以对象中的值，也可以使用Object.freeze(person)强制该对象中的值不可以修改，这是es5的语法



用法区分：

```vue
for (var i=0;i<10;i++) {
	console.log(i)
    setTimeout(function(){
		console.log(`i:${i}`)
    },1000)                   
}
输出 1 2 3 4 5 6 7 8 9 10(10次)

                       
for (let i=0;i<10;i++) {
	console.log(i)
    setTimeout(function(){
		console.log(`i:${i}`)
    },1000)                   
}
输出 1 2 3 4 5 6 7 8 9 1 2 3 4 5 6 7 8 9
理解：因为let是块级作用域，每经过一次循环，i都不一样，内存指针指向的地方都不一向。而var这样写是全局变量，且因是1s后，var都是指向同一个地方，所以打印出10个相同的数字，cpu早已把console.log(i)10次打印执行完毕

猜测：js内部每次块级作用域 都会划分出小块内存，10个let会存于不通的内存块中。而var对于非函数作用与都显示在同一块内存中				
```

```vue
对于变量私有化
es5 
（function () {
	var name = 'jelly';
	console.log(name);
}）();

es6
{
	const name = 'tom'
}
```



补充概念：

​	变量提升，var会将变量提升至作用域顶部，所以以下会出现undefined的情况，不会出现referenceError

```vue
console.log(color)
var color = 'yellow'
```

​	let也有变量提升的概念，但是他还存在一个概念临时死区Temporal Dead Zone （TDZ），所以以下会输出referenceError的错误

```vue
console.log(color)
let color = 'yellow'
```



### 2.Arrow Function 箭头函数

1.命名函数较匿名函数的区别

​	命名函数一般用于 解除事件绑定 和 递归



2. 匿名函数的规则
   1. 无参 加 括号
   2. 有一个参数 可不用加括号
   3. 有多个参数中间用 逗号   ， 分隔

举例：

```vue
显示返回
const numbers = [5,6,13,0,1,18,23]
const double = numbers.map(() => {
	return 'hello'
})	
const double = numbers.map(number => {
	return number * 2
})
const double = numbers.map((number, i) => {
	return `${i}: ${number * 2}` // 把需要传递变量的地方 用大括号包裹起来
})	
隐式返回
const double = numbers.map(number => number * 2)

将箭头函数赋值给变量
const greet = name => {alert{`hello ${name}`}}
greet（'jelly'）
```



2.箭头函数的this

​	箭头函数没有自己的箭头函数的this是继承父级作用域中的对象

```vue
const Jelly = {
	name: 'Jelly'，
	hobbies：['Coding'，'Sleeping'，'Reading']，
    printHobbies：function() { // 动态指定，动态作用域
      this.hobbies.map(function(hobby) {//map的回调函数 所以是独立函数 指向window，											global(全局对象) 或	者严格模式中undefined
      	console.log(`${this.name} loves ${hobby}`)
      })
    }
}

const Jelly = {
	name: 'Jelly'，
	hobbies：['Coding'，'Sleeping'，'Reading']，
    printHobbies：function() { // 在定义的时候就被指定了，不会因调用方法的改变而改变
      this.hobbies.map(hobby => {
          console.log(`${this.name} loves ${hobby}`)
      })
    }
}

Jelly.printHobbies()

打印结果：
1.	loves Coding
	。。。

2.	Jelly loves Coding
	。。。

```



补充知识

1.javascript中apply、call和bind的区别

​	在JS中，这三者都是用来改变函数的this对象的指向的，他们有什么样的区别呢



1、都是用来改变函数的this对象的指向的。
2、第一个参数都是this要指向的对象。
3、都可以利用后续参数传参。
那么他们的区别在哪里的，先看一个例子。

1. ​                var xw = {
2. ​                        name : "小王",
3. ​                        gender : "男",
4. ​                        age : 24,
5. ​                        say : function() {
6. ​                                alert(this.name + " , " + this.gender + " ,今年" + this.age);                                
7. ​                        }
8. ​                }
9. ​
10. ​                var xh = {
11. ​                        name : "小红",
12. ​                        gender : "女",
13. ​                        age : 18
14. ​                }
15. ​
16. ​                xw.say();

本身没什么好说的，显示的肯定是小王 ， 男 ， 今年24。
那么如何用xw的say方法来显示xh的数据呢。

对于call可以这样：

1. xw.say.call(xh);



对于apply可以这样：

1. xw.say.apply(xh);



而对于bind来说需要这样：

1. xw.say.bind(xh)();



如果直接写xw.say.bind(xh)是不会有任何结果的，看到区别了吗？call和apply都是对函数的直接调用，而bind方法返回的仍然是一个函数，因此后面还需要()来进行调用才可以。
那么call和apply有什么区别呢？我们把例子稍微改写一下。

1. ​                var xw = {
2. ​                        name : "小王",
3. ​                        gender : "男",
4. ​                        age : 24,
5. ​                        say : function(school,grade) {
6. ​                                alert(this.name + " , " + this.gender + " ,今年" + this.age + " ,在" + school + "上" + grade);                                
7. ​                        }
8. ​                }
9. ​                var xh = {
10. ​                        name : "小红",
11. ​                        gender : "女",
12. ​                        age : 18
13. ​                }

可以看到say方法多了两个参数，我们通过call/apply的参数进行传参。

对于call来说是这样的

1. xw.say.call(xh,"实验小学","六年级");       



而对于apply来说是这样的

1. xw.say.apply(xh,["实验小学","六年级"]);



看到区别了吗，call后面的参数与say方法中是一一对应的，而apply的第二个参数是一个数组，数组中的元素是和say方法中一一对应的，这就是两者最大的区别。

那么bind怎么传参呢？它可以像call那样传参。

1. xw.say.bind(xh,"实验小学","六年级")();



但是由于bind返回的仍然是一个函数，所以我们还可以在调用的时候再进行传参。

1. xw.say.bind(xh)("实验小学","六年级");




默认值


```vue
ES5
function multiply (a,b) {
	a = a || 5  // 使用默认值  不能这样写const a = a || 5
	b = b || 3
	return a * b
}

ES6
function multiply (a = 5, b = 3) {
	return a * b
}

multiply（）   15
multiply（3）   9
multiply（，2）   Unexpected token，
multiply（undefined，2）   10
multiply（null，2）   0
```



箭头函数的注意事项

```vue
// 1.作为构造函数，一个方法需要需要绑定到对象
const Person = (name，points) => { // 箭头函数做构造函数时，是不存在this绑定的
	this.name = name
	this.points = points
}

const Jelly = new person（'jelly'， 5）
// 创建一个对象总共有四个步骤	1.生成一个新的对象  2.把构造函数中的this指向新生成的对象
// 3.把新生成的对象绑定到原型对象上  4.返回新生成的对象

上面构造函数应该用原来的ES5方法
const Person = function(name，points){
	this.name = name
	this.points = points
}
// 给person原型上绑定一个新的方法
Person.prototype.updatePoints = () => { ES6 箭头函数
	console.log（this） // window
	this.points ++；
	console.log(this.points)
}

Person.prototype.updatePoints = function() { ES5 普通方法 会绑定this
	this.points ++；
	console.log(this.points) 6
}
```

总结一： 箭头函数不会绑定this

```vue
// 2. 当你真的需要this的时候
const button = document.querySelector('.zoom')
button.addEvenListener('click', () => {
	this.classList.add('in') // 不能添加 元素.classList
})
button.addEvenListener('click', function(){
	this.classList.add('in') // 添加元素成功
    setTimeout(() => { // setTimeout 是window自带的方法
		this.classList.reomve('in') // 移除元素成功
    },2000)
})
button.addEvenListener('click', function(){
	this.classList.add('in') // 添加元素成功
    setTimeout( function() { // setTimeout 是window自带的方法
		this.classList.reomve('in') // 移除元素失败且报错，因为这里的this指代的是window，
    },2000)
})
```

```vue
// 3.需要使用arguments对象 
// 箭头函数是没有arguments这个对象的
const sum = () => {
	return Array.from(arguments).reduce((prevSum, value) => prevSum + value, 0)
}
// 正确用法
const sum = function（） {
	return Array.from(arguments).reduce((prevSum, value) => prevSum + value, 0)
}
sum（1,2,3） 输出结果： 6
Array.from(arguments) 将一个数组对象 转换成一个真正的数组
// args 是一个真正的数组
const sum = （...args） {
	return args.reduce((prevSum, value) => prevSum + value, 0)
}
```



### ES6字符串新增的方法

1.startwith（）     endsWith()

```vue
const id = '51030019800730366x'
cosnt fan = 'I love Laravist'

id.startsWith('51')  true
id.startsWith('1980',6) true  // 区分大小写

fan.endsWith('love',6) true   // 
```

2.includes()  //  返回true or false

```
fan.includes('Laravist') true  代替indexOf
fan.includes('Laravist', 10) false // 从第10位开始查询是否包含该字符串
```

3.repeat()   // 字符串重复几次，参数是重复的次数 



### 模板字符串

#### 通识

1.ES6中用反引号 和 ${} 来写字符串和变量

2.可以用反引号写html语言

3.${funcionName(Jelly)} 可以调用函数

#### 标签模板字符串 Tagged Template Strings

```vue
function highlight(strings,...values) {
	debugger;  // 开启debug模式
}
```

```vue
function highlight(strings,...values) { // ... values 是剩余数组的参数集合
	const highlighted = values.map(value => `<span class="highlight">${vlaue}</span>`)
	let str = ''
	strings.forEach((string,i) => str += `${string}${highlighted[i]}`|| '') 
	return str
}
// 或者使用reduce方法
function highlight(strings,...values) { // ... values 是剩余数组的参数集合
	const highlighted = values.map(value => `<span class="highlight">${vlaue}</span>`)
	
	return strings.reduce((total,current,i) => `${total}${curr}${highlighted[i] || ''}`, '')
}
const user = 'Mary'；
const topic = 'Learn to use markdown'；
// 在模板标签前添加字符串可以 使用js对模板变量进行改变
const sentence = highlight `${user} has commented on your topic ${topic}`；
```

#### 转义标签

```vue
// 为了防止xss攻击，我们需要对用户的输入进行过滤
使用开源项目 dompurfiy
function sanitize (strings,...values) {
	cosnt dirty = strings.reduce((prev,curr,i)=> `${prev}${curr}${values}[i] || ''}`，'')
	return DOMPurify.sanitize(dirty)
}
```



### 对象解构

```vue
const Tom = {
	name: 'Tom Jones'，
	age：25，
	family： {
		mother：'Norah'，
		father：'Richard',
		brotheer: 'Howard'
	}
}

cosnt { father: f, mother, brother: b, sister= 'have no sister'} = Tom.family
console.log(f)
console.log(mother)
console.log(b)
console.log(sister) // 被解构对象中没有的属性值，将会使用默认值（只有当值为undefined时）
```



### 数组

1.解构

```
const numbers = ['one','two','three','four']
const ['one',...others] = numbers
const ['one', ,'three'] = numbers
...Others rest参数

交换数据
let a = 10
let b = 20
[a,b] = [b,a]  // 交换变量的值
```

2.循环

for  循环繁琐

 forEach 不能打断

for  in 循环

```vue
for (let index in fruits) { // index的下标
	console.log(fruits[index])
} // 会打印出非数组中的非数字东西
```

for of 循环

```vue
for (let fruit of fruits) {
	优点： 1.可以跳出当前的循环
	       2. 只打印出数组的数字
			3.且不是下标，是数组中的值
}
```



3.for of使用示例

```vue
const fruits = ['Apple','Banana','Orange','Mango']
for (let [index,fruit] of fruits.entries() ) { // object暂不支持
	console.log(fruit) // iterator内置next方法 
}
```

```vue
function sum() {
	let total = 0
	for (let num of arguments) {
		total = total + num
	}
	console.log(total)
	return total
}
sum(10,23,324,435,34,12)
```

```vue
// 遍历字符串
let name = 'Laravist'
for (let char of name) {
	console.log(char)
}
```

```vue
// 也可以遍历nodelist
for （let li of lis）{
	li.addEventListener('click', function() {
		this.classList.toggle('completed')
	})
}
```



Es5数组的方法

Array的map方法



es6数组的新方法

1.Array.from()  将类数组对象转换成数组对象

```vue
<ul>
	<li></li>
	<li></li>
	<li></li>
</ul>

const todos = document.querySelectorAll('li')
cosnt names = Array.from(todos, todo => todo.textContent)
```

2.Array.of()

3.find // 返回符合条件的元素

```vue
const bananas = inventory.find((element, index, array))
```

4.findIndex()  // 返回符合条件元素的下标

```vue
cosnt bananasIndex = inventory.findIndex((element, index, array)) 
```

5.some //  某一元素的存量符合条件，返回true，false

```vue
cosnt isEnough = inventory.find(fruit => fruit.quanity > 0) 
```

6.every（）

​	// 只有所有元素符合条件，就会返回true和false



### 剩余参数

```vue
function sum (...numbers) {
	return numbers.reduce(....)
}
```



### 扩展运算符 Spread Operator Intro

```vue
const youngers = ['George']
const olders = ['James']

let members = [...youngers,'Mary',...olders]
// 扩展运算符会将可遍历对象扩展成新的参数序列，具有与被选择对象不一样的内存位置
const currentMembers = [...members]
```

 

```vue
span 是内联元素
transition：transform 0.25s  针对transform属性
transform： translateY（-20px） rotate（10deg） scale（2）

[...word].map(letter => `<span>${letter}</span>`).join('') 将数组中的逗号去电
element.innerHTML = ... 
```



slice方法如果只传入第一个参数（索引），则意味 这个下标的元素一直所以到数组最后的元素

 

```vue
concat 会生成新的数组 所以使用可扩展运算符
cosnt fruit =['apple','bananas','pear']
const newFruit = ['orange','mongo']

fruit.push.apply(fruit, newFruit) // apply方法第二个参数是数组
fruit.push（...newFruit）

const dateFields= [2017,5,6]
new date(year,month,day)
new date(...dateFields) // 扩展运算符对多参数构造变量非常有利
```



### 对象字面量的拓展

```vue
const Laravist = { // 简写
	name,
	age,
	birthday，
	greet （）{ // 方法的简写
	}
} 


userIds[`user-${++id}`] = id
userIds[`user-${++id}`] = id
userIds[`user-${++id}`] = id

等价于	cosnt userIds={
	[`user-${++id}`] = id
	[`user-${++id}`] = id
	[`user-${++id}`] = id
} 

const values = {
	[keys.shift()]: values.shift(),
	[keys.shift()]: values.shift(),
	[keys.shift()]: values.shift(),
}
```



### promise

承诺

```vue
自己编写一个promise

成功数据reslove，失败数据reject

// 链式调用
getRepoById(1)
.then(repo => {
	return comboundOwner(repo)
})
.then(repo => {
	console.log(repo)
})
.catch(err => { // 只要上面发生错误就进入这个回调
	console.log(err)
})

// 如果全部成果机会调用then方法
Promise.all([usersPromise,moviePromise])
.then(responses => {
	const [users, movie] = responses
	console.log(users)
	console.log(movie)
})
.catch(err => {
	console.error(err)
})

// 由第一个返回的promise决定
Promise.race([usersPromise,moviePromise])
.then(responses => {
	console.log(responses)
})
.catch(err => {
	console.error(err)
})
```



### symbol

javaScript的第七种数据结构

```javascript
const peter = Symbol('peter')  // 括号里的是描述，symbol唯一性
const student = Symbol('student')

peter = student // false

symbol不可以遍历

object.getOwnPropertySymbols(classRoom).map(symbol => classRoom[symbol])
[] 代表计算属性

symbol的用法  可已经在方法内部定义私有属性
```



### ES6 Modules

将全局变量变成局部变量

```javascript
const apiKey = 'abc123'

// 两种导出方式
1.默认导出 一个模块只可以有一个默认导出  在别的模块使用可以将命名随意更改
export default apiKey；

2.命名导出
export const age = '12
别的模块引用不能随意更改
```



### Babel

将es6的语法转换成es5的语法

babel的官网babeljs.io



polyfill 将一些新加的方式补充到老旧的浏览器中



### Prototyal  Inheritance Review

js函数是一个对象，任何对象都会占据内存

```vue
function User (name, email) {
 	this.name = name
	this.email = email
}
// 可重新改写， 可新增
User.prototype.info = function() {
	console.log(``)
}
```



```javascript
1.类的声明 （特殊的函数）
	函数存在函数提升，可以在未声明之前使用它， 而类不可以
    class User {
      constructor（） { // 构造函数
        
      }

      info （） {
		console.log()
      }	

	  // 静态方法   只能在类上使用  而不能在实例上使用
      static description() {
		
      }	

      set github（value）{
		this.githubName = name // 类中定义属性 不需要使用let，cosnt，var
      }

	  get github(value) {
      	return `https://github.com/${this.githubName}`
      }
    }

    2. const user = class {
      
    }
```



继承类

```javascript
class Animal {
  constructor（name） {
    this.name = name
    this.belly = []
  }
	
  eat (food) {
	this.belly.push(food)
  } 
	
  speak () {
	console.log(`HI`)
  }	
}

class Dog extends Animal {
  constructor(name,age) {
    super（name）
    this.age = age
  }
  
  bark () {
    console.log()
  }
  
  // es6的子类会覆盖父类 中的 方法
  speak () {
    console.log（`Bark bark！HI`）
  }
}

const lucky = new Dog ('lucky', 2)
```



#####识别es5中类的继承，不要求掌握

```javascript
// 定义个函数，dog函数和对象二象性
function Dog (name, age) {
  // 将animal的构造函数赋给this
  Animal.call(this, name, age) {
    this.name = name
    this.age = age 
  }
} 
// 先将dog的原型声明为一种animal
Dog.prototype = new Animal()
// 再讲animal的构造函数借给dog使用
Dog.prototype.constructor = Dog
```



### 扩展内建对象数组

```js
p44 重新学习 没听懂
```



### 遍历器iterator

```vue

```



### Proxy

帮助我们重写对象的方法

```javascript

```

