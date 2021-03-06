# python学习-Task01 变量、运算符、数据类型及位运算

###### 时间：2020.07.20-2020.07.22

## 2 变量、运算符与数据类型

### 2.1 注释

+ `#`表示注释，作用于**单行**。

+ `''' '''`或者`""" """`表示注释，作用于**跨行区间**，添加在区间开始和结束即可。

### 2.2 运算符

+ 算数运算符

  `+`加 `-`减 `*`乘 `/`除 `//`整除 `%`取余 `**`幂

+ 比较运算符

  `>``>=``<``<=``==``!=`分别表示“大于”“大于等于”“小于”“小于等于”“等于”“不等于”
+ 逻辑运算符
  `and` 与 `or` 或 `not` 非
+ 位运算符
  `~` 按位取反 `&` 按位与 `|`按位或 `^` 按位异或 `<<` 左移 `>>` 右移
+ 三元运算符
 【例子】

```python
x,y=2,3 #向x,y赋值
small=x if x<y else y #向small赋值x,y中的较小者
print(small) #2
```

+ 其他运算符

`is` 是`is not`不是 `in`存在 `not in` 不存在 

其中`is``is not`对比的是两个变量的**内存地址**，区别于`==``!=`对比的两个变量的**值**。

+ 运算符的优先级

1. 一元高于二元；
2. 算数运算>移位运算>普通位运算；
3. 逻辑运算最低。

### 2.3 变量与赋值

+ 变量需赋值；
+ 变量名可包括**字母、数字、下划线**，但不能以数字开头；
+ 变量名大小写不同。

### 2.4 数据类型与转换

- `int`整型、`float`浮点型、`bool`布尔型为**基本类型**；
- 字符、元组、列表、字典和集合为**容器类型**；
- `type(a)`可以查看变量`a`的数据类型，**不考虑继承关系**，考虑继承关系的需要`isinstance(a)`；
- 对象-object、属性-attribute、参数-argument；
- `bool(x)`中，`x`为空则是`False`,否则为`True`；
- 转换为整型`int(x,base=10)`,**浮点型数据直接去掉小数点后**;
- 转换为字符串`str(object='')`；
- 转换为浮点型`float(x)`;

### 2.5 print()函数

函数完整形式为`print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)`

+ 将对象以字符串的形式输出到流媒体文件file中；
+ `sep`实现分隔符，可加入输出多个参数时的分隔字符；
+ `end`是输出结束时的字符，默认为换行符；
+ `file`定义输出文件，可重新定义其他文件；
+ `flush`表示立即把内容输出到流文件，不做缓存；



## 3 位运算

### 3.1 原码、反码和补码

+ 二进制有**原码、反码和补码**三种表示形式，计算机内部使用**补码**表示；
+ 二进制的最高位为**符号位**，0表示正数，1表示负数；
+ 正数的三码均相同，负数的反码在其原码的基础上取反，负数的补码在其反码的基础上加1；

### 3.2-3.5 按位非、与、或、异或操作

二进制表示下，数据按照对应位置进行逻辑运算。

### 3.6-3.7 按位左移、右移操作

+ `num<<i`表示将`num`的二进制表示向左移动`i`位所得的值，可简单地理解为乘以`2**i`；
+ `num>>i`表示将`num`的二进制表示向右移动`i`位所得的值，可简单地理解为除以`2**i`，奇数时`-1`再除；

### 3.8 利用位运算实现快速计算

+ 快速交换两个数（异或满足交换和结合定律，与自身异或为0，与0异或等于自身）。

```python
a^=b #a先于b异或
b^=a #b与a和b异或，此时b等于原来的a
a^=b #a等于原来的b
```

+ `a&(-a)`可根据得到的1或2判断`a`的奇偶。

### 3.9 利用位运算实现整数集合

+ 一个数的二进制可以用来表示一个集合（1表示在集合中，0表示不在集合中），这样能大大节省集合的储存空间，比如集合`{1,3,4,8}`可表示为`0100011010`进而利用位运算来操作集合。

1. 集合中元素

```
a | (1<<i) #把i插入集合中
a & ~(1<<i) #把i从集合中删除
a & (1<<i) #判断i是否在集合中
```

2. 集合之间

```
~a #a的补
a & b #a交b
a | b #a并b
a & (-b) #a差b
```

+ python中整型以其补码的形式存储，如果`bin`一个负数，你会发现输出的是其原码的二进制加上符号，而不是我们理解的负数的补码形式；
+ python中可通过与十六进制数`0xffffffff`进行按位与操作后再进行`bin()`可得到负数的补码。



## Task01 练习题 

**题目：leetcode 136 只出现一次的数字（位运算方法）**

给定一个非空整数数组，除了一个元素出现一次，其余元素均出现两次，请找出这个元素。

**思路：数组集合利用二进制表示，位运算中的异或操作可使相同元素操作后变成0，只保留单个出现的元素。**

**算法实现：**

```
arr = input("plz input a int list:") #提示输入集合
n = [int(n) for n in arr.split()] #确定集合元素个数

for i in range(len(n)): #集合的按位异或操作寻找
   num ^= n[i]
   
print(num) #输出显示单个出现的元素
```

