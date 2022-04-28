[TOC]


### 1. 数据类型


#### Number

JavaScript不区分整数和浮点数，统一用Number表示

#### 字符串

使用反引号表示多行字符串， 使用 ${name} 进行字符串动态填充
```
`你
好
呀`
```

#### 布尔值

#### 数组

indexOf, slice, push, pop, `unshift`, `shift`, sort, reverse, `splice`, concat, join

#### Map/Set

```
var m = new Map([['Michael', 95], ['Bob', 75]);

var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```

push, pop: 数据末尾操作

shift, unshift: 数据头部操作

splice: 截断数据，并填充

#### 对象


js 对象是一种无序的集合数据类型，它由若干键值对组成

```
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
'toString' in xiaoming; // true
xiaoming.hasOwnProperty('name'); // true
```

#### iterable

可以使用 `for ... of` 循环进行遍历

### 2. 循环

```
for(var i; i<arr.length; i++)

for(var i in a)   （一般使用 for var i of a 代替）

while(n > 10)

do{
    
}while(n < 10)

a.forEach(function(element, index, array){
    // element: 指向当前元素的值
    // index: 指向当前搜索 
    // array: 指向 Array 对象本身
})
```

### 3. 函数


#### 函数定义


arguments 在函数内指代所有参数

```
function foo(x) {
    console.log('x = ' + x); // 10
    for (var i=0; i<arguments.length; i++) {
        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
    }
}
foo(10, 20, 30);
```


rest参数， 可以获得额外的参数

```
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

```

#### 变量作用域

一般情况var创建的变量可以为全局或者函数内部的变量域，但是没有块级变量域，如for,while等

因此引入了let在for等地方创建块级变量

note:所有函数其实也都是全局变量域，挂靠在window下

#### 解构赋值

```
//数组解构-相应也要用[]
var arr =[1 , 2 ,3];
var[a ,b , c ] = arr;

//对象解构-相应用{}
var obj ={
name:"louis",
age:18,
number:"+123456789"
};
//解构得与对象的key同名，可以用:起别名,还可以对变量赋予默认值，如age,gender 
var {name:one , age = 21 , gender="man", location} = obj;
console.log(one);//"louis"
consoel.log(age);//18
consoel.log(gender);//man
console.log(location);//undefine
```

#### 高阶函数

map/reduce

```
var arr = ['1', '2', '3'];
var r;
r = arr.map(x=>parseInt(x));
```

filter

```
// 去除重复元素

r = arr.filter(function (element, index, self) {
    return self.indexOf(element) === index;
});

```

sort

```
// 无法理解的结果: (因为 sort 会将元素先转换成 String 在使用其 ASCII 码进行比较)
[10, 20, 1, 2].sort(); // [1, 10, 2, 20]
```

every 

find

findIndex

forEach


#### 闭包

换句话说，闭包就是携带状态（函数内部的局部变量）的函数。

```
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push(function () {
            return i * i;
        });
    }
    return arr;
}

var results = count();
var f1 = results[0];  
var f2 = results[1];
var f3 = results[2];

f1();  // 16
f2();  // 16
f3();  // 16
```

```
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push((function (n) {
            return function () {
                return n * n;
            }
        })(i));
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];

f1(); // 1
f2(); // 4
f3(); // 9
```

使用闭包创建一个累加器

```
function create_counter(initial) {
    var x = initial || 0;
    return {
        inc: function () {
            x += 1;
            return x;
        }
    }
}

var c2 = create_counter(10);
c2.inc(); // 11
c2.inc(); // 12
c2.inc(); // 13
```


#### 箭头函数


```
// 一个参数:
x => x*x

// 两个参数:
(x, y) => x * x + y * y

// 无参数:
() => 3.14

// 可变参数:
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}

// 返回对象:
x => ({ foo: x })
```


#### generator 生成器

一边循环一边计算的机制（懒加载）称为生成器, 具有状态而且懒加载的函数。

```
function* fib(max){
    var a=0, b=1, n=0;
    while(n < max){
        yield a;
        [a, b] = [b, a+b];
        n++;
    }
}

for i in fib(10){
    console.log(i)
}
```

#### JSON 

序列化 (对象 -> 字符串)

```
var xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '\"W3C\" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
};

var s = JSON.stringify(xiaoming);
```

反序列化 (字符串 -> 对象)

```
JSON.parse('[1,2,3,true]'); // [1, 2, 3, true]
```