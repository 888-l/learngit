# Python

### python turtle

python turtle是python的图形库，具有画图的功能

```python
import turtle    #调用turtle图形库
```

```python
turtle.showturtle()    #显示箭头
```

```python
turtle.write("文字")   #显示文字
```

```python
turtle.forward(300)   #向前移动
```

```python
turtle.color("color")  #改变颜色
```

```
turtle.left/rignt(角度)   #改变方向和角度
```

```
turtle.goto(0,0)  #前往特定坐标
```

```
turtle.width(10)  #调整线条宽度
```

```
turtle.circle(r)   #绘制半径为r的圆
```

```
turtle.penup()   #画笔离开画布，即不留下痕迹
```

```
turtle.pendown()  #画笔落下画布 
```

使用\或/连接较长的换行代码

### 对象的基本组成和内存

对象包括三个部分：

1、标识：唯一标识对象，通常对应于对象在计算机内存中的基础

2、类型：对象存储的”数据“类型

3、值：对象所储存的数据的信息

对象的本质：一个内存块，拥有特定的值、支持特定类型的操作

id（a）：a的地址

type（a）：类型

### 引用的本质

变量存储的就是变量的地址，变量通过地址引用了对象

![image-20240123204745306](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401232047347.png)

![image-20240123204727089](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401232047405.png)

![image-20240124174811204](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241748271.png)

### 变量的使用

![image-20240124181640689](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241816736.png)

### 常量的使用

python中不支持常量,是逻辑上的常量，可以修改

链式赋值x=y=100

系统数据赋值给对应相同个数的变量 例：a,b,c=1,2,3

实现互换 例如：a,b = b,a

### 内置数据类型

![image-20240124184323875](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241843969.png)

数字与基本运算符：

![image-20240124184539967](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241845045.png)

### 不同进制

![image-20240124185003073](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241850100.png)

### 自动转换

![image-20240124195234527](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241952559.png)

![image-20240124195026967](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401241950026.png)

### 时间表示

![image-20240124200440916](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401242004954.png)

### 布尔值的本质

![image-20240124214610110](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401242146203.png)

注：

```
bool("False")
```

其中字符串不为0，因此为True

逻辑运算符：

![image-20240124222635175](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401242226222.png)

按位运算符：

![image-20240124223250338](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401242232475.png)

增强赋值运算符：

![image-20240124223633636](https://888-l.oss-cn-guangzhou.aliyuncs.com/test/202401242236723.png)