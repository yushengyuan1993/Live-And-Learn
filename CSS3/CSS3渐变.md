## CSS3 渐变 (Gradients)
> ### CSS3 定义了两种类型的渐变（gradients）：
1. 线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
2. 径向渐变（Radial Gradients）- 由它们的中心定义
#### 注意： IE 9 及之前的版本不支持渐变。
> ### 线性渐变：
- `background: linear-gradient(direction, color-stop1, color-stop2, ...);`
#### 1. 线性渐变 - 从上到下（默认情况下）:
```
.box {
  background: -webkit-linear-gradient(red, blue);   /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(red, blue);        /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(red, blue);      /* Firefox 3.6 - 15 */
  background: linear-gradient(red, blue);           /* 标准的语法(必须放在最后) */
}
```
> 效果图 ![效果图](./pictures/渐变1.png)
#### 2. 线性渐变 - 从左到右
```
.box {
    height: 50px;
    background: -webkit-linear-gradient(left, red , blue);  /* Safari 5.1 - 6.0 */
    background: -o-linear-gradient(right, red, blue);       /* Opera 11.1 - 12.0 */
    background: -moz-linear-gradient(right, red, blue);     /* Firefox 3.6 - 15 */
    background: linear-gradient(to right, red , blue);      /* 标准的语法（必须放在最后） */
}
```
> 效果图 ![效果图](./pictures/渐变2.png)
#### 3. 重复的线性渐变
```
.box {
    height: 100px;
    width: 100px;
    background: -webkit-repeating-linear-gradient(red, yellow 10%, green 20%);  /* Safari 5.1 - 6.0 */
    background: -o-repeating-linear-gradient(red, yellow 10%, green 20%);       /* Opera 11.1 - 12.0 */
    background: -moz-repeating-linear-gradient(red, yellow 10%, green 20%);     /* Firefox 3.6 - 15 */
    background: repeating-linear-gradient(red, yellow 10%, green 20%);          /* 标准的语法（必须放在最后） */
}
```
> 效果图 ![效果图](./pictures/渐变3.png)
#### 4. 线性渐变进阶
```
.box{
    height: 100px;
    width: 100px;
    background: -webkit-linear-gradient(0deg,#FF0000 0%,#00FF00 50%,#0000FF 100%);
    background: -o-linear-gradient(0deg,#FF0000 0%,#00FF00 50%,#0000FF 100%);
    background: -moz-linear-gradient(0deg,#FF0000 0%,#00FF00 50%,#0000FF 100%);
    background: linear-gradient(0deg,#FF0000 0%,#00FF00 50%,#0000FF 100%);
}
```
> 效果图 ![效果图](./pictures/0deg.png)

> 没错，就是通过角度来空值渐变的起始位置：
- 45deg 效果图 ![效果图](./pictures/45deg.png)
- 90deg 效果图 ![效果图](./pictures/90deg.png)
- 135deg 效果图 ![效果图](./pictures/135deg.png)

*由此，我们知道了起始可以通过角度来获得我们想要的线性渐变的各种效果了，这基本能满足我们大多数的需求了。*
> 径向渐变
- `background: radial-gradient(center, shape size, start-color, ..., last-color);`
1. 径向渐变由它的中心定义。
2. 为了创建一个径向渐变，你也必须至少定义两种颜色结点。颜色结点即你想要呈现平稳过渡的颜色。同时，你也可以指定渐变的中心、形状（原型或椭圆形）、大小。默认情况下，渐变的中心是 center（表示在中心点），渐变的形状是 ellipse（表示椭圆形），渐变的大小是 farthest-corner（表示到最远的角落）。
#### 1. 普通的径向渐变
```
.box {
    height: 100px;
    width: 100px;
    background: -webkit-radial-gradient(red, green, blue);  /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(red, green, blue);       /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(red, green, blue);     /* Firefox 3.6 - 15 */
    background: radial-gradient(red, green, blue);          /* 标准的语法（必须放在最后） */
}
```
- 效果图 ![效果图](./pictures/径向渐变1.png)
#### 2. 不均匀的径向渐变
```
.box {
  background: -webkit-radial-gradient(red 5%, green 15%, blue 60%);     /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(red 5%, green 15%, blue 60%);          /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(red 5%, green 15%, blue 60%);        /* Firefox 3.6 - 15 */
  background: radial-gradient(red 5%, green 15%, blue 60%);             /* 标准的语法 */
}
```
- 效果图 ![效果图](./pictures/径向渐变2.png)
> **径向渐变容器如果不为正方形，则渐变区域会默认呈现为椭圆，若为正方形，则会呈现为正方形。**
#### 3.不同尺寸的径向渐变
- closest-side
- farthest-side
- closest-corner
- farthest-corner
```
.box {
    background: -webkit-radial-gradient(70% 50%, closest-side,red,green,blue);     /* Safari 5.1 - 6.0 */
    background: -o-radial-gradient(70% 50%, closest-side,red,green,blue);          /* Opera 11.6 - 12.0 */
    background: -moz-radial-gradient(70% 50%, closest-side,red,green,blue);        /* Firefox 3.6 - 15 */
    background: radial-gradient(70% 50%, closest-side,red,green,blue);             /* 标准的语法（必须放在最后） */
}
```
- 效果图 ![效果图](./pictures/径向渐变3.png)
1.  从上面的效果图中可以看出径向渐变的渐变原点的作用
2. 通过设置尺寸属性可以改变其大小
#### 4.重复的径向渐变
```
.box {
    height: 100px;
    width: 100px;
    background: -webkit-repeating-radial-gradient(red, yellow 10%, green 15%);  /* Safari 5.1 - 6.0 */
    background: -o-repeating-radial-gradient(red, yellow 10%, green 15%);       /* Opera 11.6 - 12.0 */
    background: -moz-repeating-radial-gradient(red, yellow 10%, green 15%);     /* Firefox 3.6 - 15 */
    background: repeating-radial-gradient(red, yellow 10%, green 15%);          /* 标准的语法（必须放在最后） */
}
```
- 效果图 ![效果图](./pictures/径向渐变4.png)
