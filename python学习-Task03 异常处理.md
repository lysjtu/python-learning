# python学习-Task03 异常处理

###### 时间：2020.07.24-2020.07.25

这一部分主要介绍了python在编译过程中的常见错误和警告，以及利用`try`语句检测错误。



## Task03 练习题

##### 题目：生成0-100之间的随机整数并根据提示猜测。

```
import random
x = random.randint(0,100)
print(x)
i = 0
print('猜测一个0-100之间的随机数字。')

while True:
    i+=1
    try:
        n = input('第%s次猜，请输入一个整型数字：'%i)
        nt =int(n)
    except ValueError:
        print('输入无效')
        n = int(input('第%s次猜，请输入一个整型数字：'%i))
    if n<x:
        print('太小')
    elif n > x:
        print('太大')
    else:
        print('恭喜你猜中了这个数为%f'%x)
        break
```

