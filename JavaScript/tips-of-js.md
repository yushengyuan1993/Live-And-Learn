# 一些关于JS的小技巧
### 1. 获取json的 "key" 值
> `var obj = { name: "naruto", age: 23, dad: "minato"}`
1. 使用 `for in` 来循环 :
```
for (var key in obj){
    console.log(key) // 依次输出 "name", "age", "dad"
}
```
- 这种方法比较常见，相信大家看到这个问题时第一时间都会想到吧，但是我要介绍的是下面这个更简单的方法。
2. 使用 `Object.keys()` 来获取 :
```
- console.log( Object.keys(obj) ) // 输出一个数组 ["name", "age", "dad"]
- 所以, 当我们需要某个key值时可以从当前数组中取得。
```
<hr>
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
