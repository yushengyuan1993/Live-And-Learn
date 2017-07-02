# JavaScript 创建对象的几种常见的方式
### 1. 基础方式：
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
### 2. 工厂模式（可能是最常用的一种方式）
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
> 看的出来，和第一种方法相比，工厂模式的优点就显而易见了，没错就是“多态”。
