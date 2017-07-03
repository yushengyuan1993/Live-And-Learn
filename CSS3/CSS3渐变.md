# CSS3 渐变 (Gradients)
> ### CSS3 定义了两种类型的渐变（gradients）：
1. 线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
2. 径向渐变（Radial Gradients）- 由它们的中心定义
> ### 注意： IE 9 及之前的版本不支持渐变。
> ### 语法：
- `background: linear-gradient(direction, color-stop1, color-stop2, ...);`
1. 线性渐变 - 从上到下（默认情况下）:
```
.box {
  background: -webkit-linear-gradient(red, blue);   /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(red, blue);        /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(red, blue);      /* Firefox 3.6 - 15 */
  background: linear-gradient(red, blue);           /* 标准的语法(必须放在最后) */
}
```
> 效果图 ![效果图](./pictures/渐变1.png)
2. 线性渐变 - 从左到右
```
.box {
    height: 50px;
    background: -webkit-linear-gradient(left, red , blue); /* Safari 5.1 - 6.0 */
    background: -o-linear-gradient(right, red, blue); /* Opera 11.1 - 12.0 */
    background: -moz-linear-gradient(right, red, blue); /* Firefox 3.6 - 15 */
    background: linear-gradient(to right, red , blue); /* 标准的语法（必须放在最后） */
}
```
> 效果图 ![效果图](./pictures/渐变2.png)
