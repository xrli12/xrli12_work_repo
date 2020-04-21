搜集python的优质资料

1. python print() 里的逗号相当于空格
2. input('注释') 提供了交互，相当于C++里的cin>>,需要注意输入的数据格式是str，有时候可能需要用到数据转换
4. `/`的结果始终是浮点数，`//`被称为地板除，得到的是取整后的整数，`%`取余数的操作符可以关注一下

### Python数据类型

#### str

Path=r"D:\BaiduNetdiskDownload" 加r的原因是`r""`表示`""`内部的字符串默认不转义。

**格式化**

```python
print('Hi %s, your score is %d.'%('Bart',59))
```

常用占位符：

| 占位符 |   替换内容   |
| :----: | :----------: |
|   %d   |     整数     |
|   %f   |    浮点数    |
|   %s   |    字符串    |
|   %x   | 十六进制整数 |

**那么遇到字符串里有%就需要%%来转义**



![](https://www.liaoxuefeng.com/files/attachments/928817906446432/0)



#### List

```python
a=[] # 创建空列表
a=['Bob',23,3.14]
a[0]
a[-1]
a.append('Tom') # 一次只能append一个元素
a.insert(0,'Tom')# 指定位置插入元素
```

 ##### 删除

`Pop()`删除末尾元素

`pop(i)`删除指定位置元素

##### 替换

`list_name[i]=新元素`

##### 空列表

```python
l=[]
len(l)

##
0
```

空列表并不是None

##### 切片

```python
l[n1:n2]
l[n1:n2,k]
```

取[n1,n2)的元素

##### 列表生成式

> 运用列表生成式，可以快速生成list，可以通过一个list推导出另一个list，而代码却十分简洁。

```python
[f(x) for x in l (if 筛选语句)]
```



#### Tuple

**特性：**

一旦初始化就不能修改,不能修改的意思是tuple每个元素的指向不变

Tuple的陷阱：定义一个tuple时，tuple的元素必须被确定下来。

***一个元素的元组***

```python
t=(1,)
```

Python在显示只有1个元素的tuple时，也会加一个逗号`,`，以免你误解成数学计算意义上的括号。所以在点numpy array的shape的时候可以看到一维的array的形状是(n,)

#### dict

#### set



***

### 循环判断

#### if 标准格式

```python
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```



#### for x in list: 循环

```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```

要是想重复一个操作n次,可以使用range(n)

```python
for i in range(n):
    循环体
```

range(n)生成的就是特殊的range对象，如果想取出range里的数据可以用`list()`将range对象变为列表

#### while 循环

```python
while (条件):
    循环体
```

条件有无括号都行

可以使用`break`提前退出循环

也可以使用`continue`提前结束本轮循环，直接开始下一轮



***

### 函数

#### 函数的参数

> Python 函数参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数

需要注意命名关键字参数需要一个特殊分隔符`*`

可变参数：`*args`,是将参数作为list或者tuple传进来

关键字参数：`**kw`，将参数作为字典，传入keyword

#### 递归函数

用递归函数解决汉诺塔：

```python
def move(n,a,b,c):
    if n==1:
        print(a,'-->',c)
    else:
        move(n-1,a,c,b)
        print(a,'-->',c)
        move(n-1,b,a,c)
```

```python
move(3,'A','B','C')
```

输出：

```python
A --> C
A --> B
C --> B
A --> C
B --> A
B --> C
A --> C
```

#### MapReduce

##### 练习

利用`map`和`reduce`编写一个`str2float`函数，把字符串`'123.456'`转换成浮点数`123.456`：

```python
from functools import reduce

DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4':4, '5': 5, '6': 6, '7': 7,
          '8': 8, '9': 9,'.':'dot'}
def char2num(s):
    return DIGITS[s]
def str2num(x,y):
    if y=='dot':
        return x
    return x*10+y
def str2float(s):
    dot_position=0
    for i,j in  enumerate(s):
        if j=='.':
            dot_position=len(s)-1-i
    num=reduce(str2num,map(char2num,s))
    return num*10**(-dot_position)
print('str2float(\'123.456\') =', str2float('123.456'))
if abs(str2float('123.456') - 123.456) < 0.00001:
    print('测试成功!')
else:
    print('测试失败!')
```



