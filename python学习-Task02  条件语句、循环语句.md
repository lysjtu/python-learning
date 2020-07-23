# python学习-Task02  条件语句、循环语句

###### 时间：2020.07.23

## 4 条件语句

+ 主要由`if`语句来表示条件判断，`if-else`语句可执行两种不同情况下的语句，`if-elif-else`语句可以实现多种不同条件的判断和语句执行；
+ `if`语句**支持嵌套**，注意缩进来表示正确的条件判断结构；
+ `assert`关键词可在条件判断为`False`时终止运行并提示`AssertionError`。

【示例】

```
#判断hi大于5时输出good,小于2时输出bad
hi=4
if hi>2:
  if hi >5:
    print('good!')
else:
  print('bad')
```

```
temp=input('plz input your score:')#提示输入成绩
source=int(temp)
if 100>=source>=90:#成绩在90-100之间等级为A
  print('your level is A.')
elif 90>source>=80:#成绩在80-90之间等级为B
  print('your level is B.')
elif 80>source>=60:#成绩在60-80之间等级为C
  print('your level is C.')
else:#其他情况等级为D
  print('your level is D.')
```

## 5 循环语句

+ `while`循环语句根据**布尔表达式的判断**进行循环并执行相应的代码块，直至布尔表达式的值为假；
+ `while-else`语句在布尔表达式的值为假时执行`else`后的代码块，如果`while`循环中存在`break`强制跳出语句则不执行`else`后代码块；
+ `for`循环语句根据**序列遍历**进行循环并执行相应的代码块，这些序列可包括`str,list,turple,dict`等;
+ `for-else`语句同`while-else`语句；
+ `range([start,] stop[,step=1])`函数包括三个参数，起始点和步长可省略时默认为1；
+ `enumerate(sequence,[start=0])`函数为枚举函数，起始点可省略,返回值**包括枚举索引**；

【示例】

```
seasons = ['spring','summer','fall','winter'] #定义季节集合
lst = list(enumerate(seasons)) #枚举季节
print(lst) #输出枚举结果
#[(0,'spring'),(1,'summer'),(2,'fall'),(3,'winter')]
```

+ `break`语句**跳出整个循环**，进入下一个代码块的执行，`continue`语句**跳出当前循环**，进入下一个循环的执行；
+ `pass`语句可占位保证代码正确性和完整性；
+ 循环可直接应用在**列表、元组、字典和集合推导式**中；

```
#列表推导式
x = [i**2 for i in range(1,10)]
print(x)
#[1,4,9,16,25,36,49,64,81]

#元组推导式
a = (x for x in range(10))
print(a)
#<generator object<genexpr> at 0x0000025BE511cc48>
print(tuple(a))
#(0,1,2,3,4,5,6,7,8,9)

#字典推导式
b = {i:i%2==0 for i in range(10) if i%3==0}
print(b)
#{0:True, 3:False, 6:True, 9:False}

#集合推导式
c = {i for i in [1,2,3,4,5,5,6,4,3,2,1]}
print(c)
#{1,2,3,4,5,6}
```

## Task02 练习题

1. 找出1500-2700之间可同时被7和5整除的数字。

```
x=[i for i in range(1500,2700)  if i%7==0 and i%5==0]
print(x)
#[1505, 1540, 1575, 1610, 1645, 1680, 1715, 1750, 1785, 1820, 1855, 1890, 1925, 1960, 1995, 2030, 2065, 2100, 2135, 2170, 2205, 2240, 2275, 2310, 2345, 2380, 2415, 2450, 2485, 2520, 2555, 2590, 2625, 2660, 2695]
```

2. 龟兔赛跑游戏

```
v1,v2,t,s,l = input("输入兔子的速度v1,乌龟的速度v2,领先可休息最短距离t,领先时休息时间s以及赛道长度l: ").split(" ")
v1 = int(v1)
v2 = int(v2)
t = int(t)
s = int(s)
l = int(l)
r_cd = t_cd = 0 #兔子和乌龟的跑过距离
tmp = 0 #兔子的休息时间
flag = False
time = 0
while True:
    time+=1
    if r_cd - t_cd >= t and flag == False:
        flag = True #兔子开始一轮休息
        tmp = 0 #开始计时
    if flag == True:
        t_cd += v2
        tmp += 1
    else:
        t_cd += v2
        r_cd += v1
    if tmp == s:#兔子这轮休息完毕
        tmp = 0
        flag  = False
    if t_cd >= l or r_cd >= l:
        if t_cd >= l and r_cd < l:
            print("T\n",time)
            break
        elif t_cd == r_cd:
            print("D\n",time)
            break
        elif t_cd < l and r_cd >= l:
            print("R\n",time)
            break
        else:
            print("error")
            break


#输入v1=兔子的速度 v2=乌龟的速度 t=领先t米（包含） s=休息s秒 l=赛道长度 6 2 8 10 600
D
300
```

