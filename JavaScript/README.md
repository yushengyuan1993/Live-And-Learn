# 一些关于JS的小技巧
### 1. 获取json的 "key" 值
> `var obj = { name: "naruto", age: 23, dad: "minato"}`
#### 1. 使用 `for in` 来循环 :
```
for (var key in obj){
    console.log(key) // 依次输出 "name", "age", "dad"
}
```
- 这种方法比较常见，相信大家看到这个问题时第一时间都会想到吧，但是我要介绍的是下面这个更简单的方法。
#### 2. 使用 `Object.keys()` 来获取 :
```
- console.log( Object.keys(obj) ) // 输出一个数组 ["name", "age", "dad"]
- 所以, 当我们需要某个key值时可以从当前数组中取得。
```
----
### 2. JavaScript 创建对象的几种常见的方式
#### 1. 原始方式：
* 对象字面量方式
```
var Hero = { 
    name: 'MasterYi',
    skill: 'AlphaStrike',
    todo: function () { alert(this.name); }
};
```
* Object构造函数方式
```
var Hero = new Object();

Hero.name = 'MasterYi';
Hero.skill = 'Q';
Hero.do = function(){
    return this.name + ' use ' + this.skill + ' kill ' + 'yasuo';
}

alert( Hero.skill );    // AlphaStrike
alert( Hero.do() );     // MasterYi use AlphaStrike kill yasuo
```
> 显然，当我们要创建批量的Hero1、Hero2……时，
每次都要敲很多代码，资深copypaster都吃不消！
然后就有了批量生产的工厂模式。
#### 2. 工厂模式
```
function heroObj(name, skill){
    var Hero = new Object();

    Hero.name = name;
    Hero.skill = skill;
    Hero.do = function(){
        return this.name + ' use ' + this.skill + ' kill ' + 'MasterYi';
    }

    return Hero;
}
var riven = heroObj('yasuo', 'R');
var ashe = heroObj('Caitlin', 'W');

alert(riven.skill);     // R
alert(ashe.do());       // Caitlin use W kill MasterYi
```
> 工厂模式就是批量化生产，简单调用就可以进入造人模式（啪啪啪……）。
 指定姓名年龄就可以造一堆小宝宝啦，解放双手。
 但是由于是工厂暗箱操作的，所以你不能识别这个对象到底是什么类型、
 是人还是狗傻傻分不清（instanceof 测试为 Object），
 另外每次造人时都要创建一个独立的temp对象，代码臃肿，你受得了？
#### 3. 构造函数
```
function HeroObj(name, skill){

    this.name = name;
    this.skill = skill;
    this.do = function(){
        return this.name + ' use ' + this.skill + ' kill ' + 'MasterYi';
    }

}

var riven = new heroObj('yasuo', 'R');
var ashe = new heroObj('Caitlin', 'W');

alert(riven.skill);     // R
alert(ashe.do());       // Caitlin use W kill MasterYi
```
> ECMAScript中的构造函数可以用来创建特定类型的对象。像Object和Array的原生的构造函数，在运行时会自动出现在执行环境中。此外，也可以创建自定义的构造函数，从而定义自定义对象类型的属性和方法。
#### 4. 原型模式
* 直接使用 prototype 属性
```
function Hero () {}
Hero.prototype.name = 'MasterYi';
Hero.prototype.skill = 'AlphaStrike';
Hero.prototype.do = function () { alert(this.name); };
```
* 字面量定义方式
```
function Hero () {}
Hero.prototype = {
    name: 'MasterYi',
    skill: 'AlphaStrike',
    sayName: function () { alert(this.name); }
};
var p1 = new Hero(); //name='MasterYi'
var p2 = new Hero(); //name='MasterYi'
```
> 这里需要注意的是原型属性和方法的共享，即所有实例中都只是引用原型中的属性方法，任何一个地方产生的改动会引起其他实例的变化。
#### 5. 混合模式
```
function Hero (name, skill) {
    this.name = name;
    this.skill = skill;
}
Hero.prototype = {
    skillLists: ['Q', 'W', 'E', 'R'];
    sayName: function () {
        alert(this.name);
    },
    do: function () {
        alert(this.name + ' use ' + this.skill + ' kill ' + 'MasterYi');
    }
};
var p1 = new Hero('yasuo', 'R');
var p2 = new Hero('ashe', 'w');
p1.sayName();   // yasuo
p1.skillLists;  // ['Q', 'W', 'E', 'R']
p2.do();        // ashe use w kill MasterYi
```
#### 6. 使用`class`关键字
```
class Hero {
    constructor(){
        this.name = 'MasterYi';
        this.skill = 'AlphaStrike';
    }
    do(enemy){
        alert(this.name + ' use ' +  this.skill + ' kill ' + enemy)
    }
}

let ashe = new Hero();
ashe.do('ashe');       // MasterYi use AlphaStrike kill ashe

class Yasuo extends Hero {
    constructor(){
        super()
        this.name = 'yasuo'
    }
}
let yasuo = new Yasuo();
yasuo.do('timor');      // yasuo use AlphaStrike kill timor
```
> 这里涉及到 `ES6` 里的新特性，想了解 `ES6` 中更多的新特性，大家可以去看看 [阮一峰](http://es6.ruanyifeng.com/) 老师的书。
----
### 3. JS实时监听文本域的变化
>  众所周知，使用 `onchange` 事件来监听文本域的变化是我们在开发中用到的最多的方法。但是， `onchange` 是在文本域失焦时才触发，有时候由于需求的原因，需要我们来实时监听文本域的变化，除了使用`keydown`和`keyup`外，我们还可以:
#### 1. 使用 `onpropertychange` 
```
<input type="text" id="txt">

$("#ysy").bind('input propertychange', function() {  
    console.log(new Date().getTime()); 
});
```
#### 2. 使用 `oninput` 
```
document.getElementById('txt').oninput = function(){
    console.log(this.value);
}
```
> 最后，总结一下`onchange, onpropertychange`和`oninput`之间的异同：
1. `onchange`事件与`onpropertychange`事件的区别：`onchange`事件在内容改变（两次内容有可能还是相等的）且失去焦点时触发；`onpropertychange`事件却是实时触发，即每增加或删除一个字符就会触发，通过js改变也会触发该事件，但是该事件IE专有。
2. `oninput`事件与`onpropertychange`事件的区别：`oninput`事件是IE之外的大多数浏览器支持的事件，在value改变时触发，实时的，即每增加或删除一个字符就会触发，然而通过js改变value时，却不会触发；`onpropertychange`事件是任何属性改变都会触发的，而`oninput`却只在value改变时触发，`oninput`要通过`addEventListener()`来注册，`onpropertychange`注册方式跟一般事件一样。（此处都是指在js中动态绑定事件，以实现内容与行为分离）>
3. `oninput`与`onpropertychange`失效的情况：  （1）`oninput`事件：a). 当脚本中改变value时，不会触发；b).从浏览器的自动下拉提示中选取时，不会触发。  （2）`onpropertychange`事件：当input设置为`disable=true`后，onpropertychange不会触发。
----
### 4. JavaScript类型检验
> 介绍一个简单有用的js类型检验的方法
```
function checkType(sth) {
    return Object.prototype.toString.call(o)
    .match(/(\w+)\]$/)[1]
    .toLowerCase();
}

checkType({})               // object
checkType([])               // array
checkType(function(){})     // function
checkType(1)                // number
checkType(+'3')             // number
checkType(3+'')             // string
```
### 5. JS中的数组
> #### 关于数组的一些认识
1. 使用构造器函数创建数组时:
```
let ary = new Array();
```
- 若参数只有一个，且为数字，`let ary1 = new Array(3)`，这是其实我们是在指定数组的长度的，即 `ary1.length === 3`。`ary1[0]`则为`undefined`;
- 当定义`let ary2 = new Array(1, 2)`时，此时`ary2 === [1, 2, 3]`;
2. JS中的数组定义非常的自由：
>> 看下面的例子：
```
let ary = [1, 2, 3];
ary[5] = 5;
console.log(ary);           // [1,2,3,undefined,undefined,5]
console.log(ary.length);    // 6
```
>> 再看：
```
let ary2 = [1, 2, 3, 4, 5];
ary2.length = 3;
console.log(ary2);      // [1, 2, 3]
```
> #### 常用的数组API
1. 万能方法 `splice()`
-  splice()方法允许我们对数组进行插入、替换和删除的功能。**splice方法返回一个有删除元素组成的新数组，没有删除时则返回一个空数组**，简直完美呀！
- `splice()`方法接受三个参数，**第一个**为开始索引，**第二个**为删除元素的位置，**第三个**为插入的元素，可以为第二个，当然也可省略（表示删除元素）。
- `splice()`方法会修改原数组！
- 通过以下三个demo了解一下具体的用法吧：
>> 插入:
```
let ary1 = ["first", "second", "third", "forth", "fifth"];
let ary2 = ary1.splice(1,0,"add1");
console.log(ary1);      [ 'first', 'add1', 'second', 'third', 'forth', 'fifth' ]
console.log(ary2);      [] 没有删除则放回一个空数组
```
>> 替换：
```
let ary1 = ["first", "second", "third", "forth", "fifth"];
let ary2 = ary1.splice(1,1,"replace");
console.log(ary1);      [ 'first', "replace, 'third', 'forth', 'fifth' ]
console.log(ary2);      ["second"] 返回被删除(即替换)的数组
```
>> 删除：
```
let ary1 = ["first", "second", "third", "forth", "fifth"];
let ary2 = ary1.splice(1,3);
console.log(ary1);      ["second", "third", "forth"]
console.log(ary2);      ["first", "fifth"]
```
2. `slice()` 方法
- `slice()` 方法可以接受两个参数(start, end)；
- `slice()` 方法可从已有的数组中返回选定的元素；
- `slice()` 方法可提取字符串的某个部分，并以新的字符串返回被提取的部分；
- `slice()` 方法**不会改变原始数组**，而是返回一个新数组。
>> demo1:
```
let ary = ["first", "second", "third", "forth", "fifth"];
console.log (ary.slice(1,2) );      // ["second"]
let ary1 = ary.slice(1,2);          // ["second"]
let ary2 = ary.slice(1,3);          // ["second", "third"]
console.log(ary);                   // ["first", "second", "third", "forth", "fifth"];
```
>> demo2:
```
let ary = ["first", "second", "third", "forth", "fifth"];
console.log(ary.slice(1,2));    // ["second"]
console.log(ary.slice(1,3));    // ["second", "third"]
console.log(ary));              // ["first", "second", "third", "forth", "fifth"];
```
>> demo3:
```
let ary = ["first", "second", "third", "forth", "fifth"];
let ary1 = ary.slice();     // ["first", "second", "third", "forth", "fifth"];
let ary2 = ary.slice(0);     // ["first", "second", "third", "forth", "fifth"];

ary === ary1;       // false
ary === ary2;       // false
ary1 === ary2;      // false
```
**看出来啥猫腻没，这不是深复制一个数据吗！**
