---
description: test
---

# python

## py基础

### 与C语言不同

* 缩进有语法含义
* 注释以`#`开头
* 当语句以冒号`:`结尾时，缩进的语句视为代码块
* 大小写敏感
* 补充
  * 逻辑运算符
  * 

### 数据表示

* 对于很大的数，例如`10000000000`，很难数清楚0的个数。Python允许在数字中间以`_`分隔，因此，写成`10_000_000_000`和`10000000000`是完全一样的。十六进制数也可以写成`0xa1b2_c3d4`
* 字符串用单引号`'`或双引号`"`括起来，如果`'`本身也是一个字符，那就要用`""`括起来
* 转义字符与C语言相同，额外的是**：**如果字符串里面有很多字符都需要转义，就需要加很多`\`，为了简化，Python还允许用`r''`表示`''`内部的字符串默认不转义，如下例：
* 在Python中，可以直接用`True`、`False`表示布尔值（请注意大小写）

### 变量

* python的变量类型不固定，称作动态语言，与之对应的是_静态语言_。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错
* 两种除法：

  `/`除法计算结果是浮点数，即使是两个整数恰好整除，结果也是浮点数

  ```python
  >>> 9 / 3
  3.0
  ```

  还有一种除法是`//`，称为地板除，两个整数的除法仍然是整数

  ```python
  >>> 10 // 3
  3
  ```

### 字符串

本节内容并未深究，详见[网址](https://www.liaoxuefeng.com/wiki/1016959663602400/1017075323632896)编码部分

* 在最新的Python 3版本中，字符串是以Unicode编码的，也就是说，Python的字符串支持多语言
* 由于Python的字符串类型是`str`，**在内存中以Unicode表示，一个字符对应若干个字节**。如果要在网络上传输，或者保存到磁盘上，就需要把`str`变为以字节为单位的`bytes`。

  Python对`bytes`类型的数据用带`b`前缀的单引号或双引号表示：

  ```text
  x = b'ABC'
  ```

  要注意区分`'ABC'`和`b'ABC'`，前者是`str`，后者虽然内容显示得和前者一样，但`bytes`的每个字符都只占用一个字节

* 要计算`str`包含多少个**字符**，可以用`len()`函数：

  ```python
  >>> len('ABC')
  3
  >>> len('中文')
  2
  ```

* `len()`函数计算的是`str`的字符数，如果换成`bytes`，`len()`函数就计算字节数：

  ```python
  >>> len(b'ABC')
  3
  >>> len(b'\xe4\xb8\xad\xe6\x96\x87')
  6
  >>> len('中文'.encode('utf-8'))
  6
  ```

* **格式化字符串**

  在Python中，采用的格式化方式和C语言是一致的，用`%`实现，举例如下：

  ```python
  >>> 'Hello, %s' % 'world'
  'Hello, world'
  >>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
  'Hi, Michael, you have $1000000.'
  ```

  格式见例子，占位符和C语言一样

* 普通%字符用`%%`来转义表示
* f-string

  最后一种格式化字符串的方法是使用以`f`开头的字符串，称之为`f-string`，它和普通字符串不同之处在于，字符串如果包含`{xxx}`，就会以对应的变量替换：

  ```text
  >>> r = 2.5
  >>> s = 3.14 * r ** 2
  >>> print(f'The area of a circle with radius {r} is {s:.2f}')
  The area of a circle with radius 2.5 is 19.62
  ```

  上述代码中，`{r}`被变量`r`的值替换，`{s:.2f}`被变量`s`的值替换，并且`:`后面的`.2f`指定了格式化参数（即保留两位小数），因此，`{s:.2f}`的替换结果是`19.62`

### list

Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。

```python
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']
```

变量`classmates`就是一个list。用`len()`函数可以获得list元素的个数：

```python
>>> len(classmates)
3
```

* 如果要**取最后一个元素**，除了计算索引位置外，还可以用`-1`做索引，直接获取最后一个元素

  以此类推，-2是倒数第二个元素，-3是倒数第三个元素

* list是一个**可变的有序表**，所以，可以往list中追加元素到末尾：

  ```text
  >>> classmates.append('Adam')
  >>> classmates
  ['Michael', 'Bob', 'Tracy', 'Adam']
  ```

  也可以把元素插入到指定的位置，比如索引号为`1`的位置：

  ```text
  >>> classmates.insert(1, 'Jack')
  >>> classmates
  ['Michael', 'Jack', 'Bob', 'Tracy', 'Adam']
  ```

* 要删除list末尾的元素，用`pop()`方法：

  ```text
  >>> classmates.pop()
  'Adam'
  >>> classmates
  ['Michael', 'Jack', 'Bob', 'Tracy']
  ```

  要删除指定位置的元素，用`pop(i)`方法，其中`i`是索引位置：

  ```text
  >>> classmates.pop(1)
  'Jack'
  >>> classmates
  ['Michael', 'Bob', 'Tracy']
  ```

  要把某个元素替换成别的元素，可以直接赋值给对应的索引位置：

  ```text
  >>> classmates[1] = 'Sarah'
  >>> classmates
  ['Michael', 'Sarah', 'Tracy']
  ```

* list元素也可以是另一个list，比如：

  ```text
  >>> s = ['python', 'java', ['asp', 'php'], 'scheme']
  >>> len(s)
  4
  ```

### tuple

另一种有序列表叫元组：tuple。tuple和list非常类似，但是**tuple一旦初始化就不能修改**，比如同样是列出同学的名字：**注意使用圆括号括起来的，而list是方括号**

```text
>>> classmates = ('Michael', 'Bob', 'Tracy')
```

现在，classmates这个tuple不能变了，它也没有append\(\)，insert\(\)这样的方法。其他获取元素的方法和list是一样的，你可以正常地使用`classmates[0]`，`classmates[-1]`，但不能赋值成另外的元素。

不可变的tuple有什么意义？因为**tuple不可变，所以代码更安全**。如果可能，能用tuple代替list就尽量用tuple。

* tuple在声明时必须初始化
* `a=(1)`时，括号内只有一个元素，与数学符号圆括号冲突，此时默认a=1

  所以，只有1个元素的tuple定义时必须加一个逗号`,`，来消除歧义：

  ```text
  >>> t = (1,)
  >>> t
  (1,)
  ```

  Python在显示只有1个元素的tuple时，也会加一个逗号`,`，以免你误解成数学计算意义上的括号。

### 其他

* `elif`是`else if`的缩写，完全可以有多个`elif`
* input\(\)函数

  ```text
  birth = input('birth: ')
  if birth < 2000:
      print('00前')
  else:
      print('00后')
  ```

  这里input使用错误，input返回的是str类型，而str无法和int型的2000比较

  py提供`int()`函数来实现类型转换：从字符串转换到对应的整数

  但此时若输入非数字的字符串，如'abc'，int\(\)函数就会报错

### 循环

* **for...in循环：**

  ```python
  names = ['Michael', 'Bob', 'Tracy']
  for name in names:
      print(name)
  ```

  再比如我们想计算1-10的整数之和，可以用一个`sum`变量做累加：

  ```python
  sum = 0
  for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
      sum = sum + x
  print(sum)
  ```

* 如果要计算1-100的整数之和，从1写到100有点困难，幸好Python提供一个`range()`函数，可以生成一个整数序列，再通过`list()`函数可以转换为list。比如`range(5)`生成的序列是从0开始小于5的整数：

  ```text
  >>> list(range(5))
  [0, 1, 2, 3, 4]
  ```

  `range(101)`就可以生成0-100的整数序列

* 计算0-100

  ```text
  sum = 0
  for x in range(101):
      sum = sum + x
  print(sum)
  ```

### 字典

* Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。
* 如果用dict实现，只需要一个“名字”-“成绩”的对照表，直接根据名字查找成绩，无论这个表有多大，查找速度都不会变慢。用Python写一个dict如下：

  ```text
  >>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
  >>> d['Michael']
  95
  ```

* 键-值（key-value），如果key不存在，dict就会报错
* 要避免key不存在的错误，有两种办法，一是通过`in`判断key是否存在：

  ```text
  >>> 'Thomas' in d
  False
  ```

  二是通过dict提供的`get()`方法，如果key不存在，可以返回`None`，或者自己指定的value：

  ```text
  >>> d.get('Thomas')
  >>> d.get('Thomas', -1)
  -1
  ```

  注意：返回`None`的时候Python的交互环境不显示结果。

* dict牺牲了空间来换取时间，而list相反，查找耗时较高，但空间占用少

  dict的算法是通过key计算位置，称为哈希算法（Hash）

  要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。**而list是可变的，就不能作为key**

### 再议不可变对象

上面我们讲了，str是不变对象，而list是可变对象。

对于可变对象，比如list，对list进行操作，list内部的内容是会变化的，比如：

```text
>>> a = ['c', 'b', 'a']
>>> a.sort()
>>> a
['a', 'b', 'c']
```

而对于不可变对象，比如str，对str进行操作呢：

```text
>>> a = 'abc'
>>> a.replace('a', 'A')
'Abc'
>>> a
'abc'
```

虽然字符串有个`replace()`方法，也确实变出了`'Abc'`，但变量`a`最后仍是`'abc'`，应该怎么理解呢？

我们先把代码改成下面这样：

```text
>>> a = 'abc'
>>> b = a.replace('a', 'A')
>>> b
'Abc'
>>> a
'abc'
```

要始终牢记的是，`a`是变量，而`'abc'`才是字符串对象！有些时候，我们经常说，对象`a`的内容是`'abc'`，但其实是指，`a`本身是一个变量，它指向的对象的内容才是`'abc'`：

```text
┌───┐                  ┌───────┐
│ a │─────────────────>│ 'abc' │
└───┘                  └───────┘
```

当我们调用`a.replace('a', 'A')`时，实际上调用方法`replace`是作用在字符串对象`'abc'`上的，而这个方法虽然名字叫`replace`，但却没有改变字符串`'abc'`的内容。相反，**`replace`方法创建了一个新字符串`'Abc'`并返回**，如果我们用变量`b`指向该新字符串，就容易理解了，变量`a`仍指向原有的字符串`'abc'`，但变量`b`却指向新字符串`'Abc'`了：

```text
┌───┐                  ┌───────┐
│ a │─────────────────>│ 'abc' │
└───┘                  └───────┘
┌───┐                  ┌───────┐
│ b │─────────────────>│ 'Abc' │
└───┘                  └───────┘
```

所以，**对于不变对象来说，调用对象自身的任意方法，也不会改变该对象自身的内容**。**相反，这些方法会创建新的对象并返回，这样，就保证了不可变对象本身永远是不可变的**。

## 函数

### 数据类型转换

Python内置的常用函数还包括数据类型转换函数，比如`int()`函数可以把其他数据类型转换为整数：

```python
>>> int('123')
123
>>> int(12.34)
12
>>> float('12.34')
12.34
>>> str(1.23)
'1.23'
>>> str(100)
'100'
>>> bool(1)
True
>>> bool('')
False
```

函数名其实就是指向一个函数对象的引用，完全可以把函数名赋给一个变量，相当于给这个函数起了一个“别名”：

```python
>>> a = abs # 变量a指向abs函数
>>> a(-1) # 所以也可以通过a调用abs函数
1
```

### 函数定义

在Python中，定义一个函数要使用`def`语句，依次写出函数名、括号、括号中的参数和冒号`:`，然后，在缩进块中编写函数体，函数的返回值用`return`语句返回。

```python
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```

### 空函数

如果想定义一个什么事也不做的空函数，可以用`pass`语句：

```text
def nop():
    pass
```

`pass`语句什么都不做，那有什么用？实际上`pass`可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个`pass`，让代码能运行起来。

`pass`还可以用在其他语句里，比如：

```text
if age >= 18:
    pass
```

缺少了`pass`，代码运行就会有语法错误。

### 返回多个值

函数可以返回多个值吗？答案是肯定的。

比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的坐标：

```python
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
```

`import math`语句表示导入`math`包，并允许后续代码引用`math`包里的`sin`、`cos`等函数。

然后，我们就可以同时获得返回值：

```text
>>> x, y = move(100, 100, 60, math.pi / 6)
>>> print(x, y)
151.96152422706632 70.0
```

但其实这只是一种假象，Python函数返回的仍然是单一值：

```text
>>> r = move(100, 100, 60, math.pi / 6)
>>> print(r)
(151.96152422706632, 70.0)
```

原来**返回值是一个tuple**！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

### 默认参数

[链接](https://www.liaoxuefeng.com/wiki/1016959663602400/1017261630425888)

```python
def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)
```

这样，大多数学生注册时不需要提供年龄和城市，只提供必须的两个参数：

```python
>>> enroll('Sarah', 'F')
name: Sarah
gender: F
age: 6
city: Beijing
```

只有与默认参数不符的学生才需要提供额外的信息：

```python
enroll('Bob', 'M', 7)
enroll('Adam', 'M', city='Tianjin')
```

### 可变参数

```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```

定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个`*`号。在函数内部，参数`numbers`接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数：

```text
>>> calc(1, 2)
5
>>> calc()
0
```

如果已经有一个list或者tuple，要调用一个可变参数怎么办？可以这样做：

```text
>>> nums = [1, 2, 3]
>>> calc(nums[0], nums[1], nums[2])
14
```

这种写法当然是可行的，问题是太繁琐，所以Python允许你在list或tuple前面加一个`*`号，把list或tuple的元素变成可变参数传进去：

```text
>>> nums = [1, 2, 3]
>>> calc(*nums)
14
```

`*nums`表示把`nums`这个list的所有元素作为可变参数传进去。这种写法相当有用，而且很常见。

### 关键字参数

可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict

```python
def person(name, age, **kw):
#kw是fict
    print('name:', name, 'age:', age, 'other:', kw)
```

函数`person`除了必选参数`name`和`age`外，还接受关键字参数`kw`。在调用该函数时，可以只传入必选参数：

```python
>>> person('Michael', 30)
name: Michael age: 30 other: {}
```

也可以传入任意个数的关键字参数：

```python
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```

**`*args`是可变参数，args接收的是一个tuple；**

**\`**kw\`是关键字参数，kw接收的是一个dict。\*\*

### 本章练习

写出函数可计算一个或多个数的乘积，能够处理无参数输入的情况

```python
def mul(firstNum, *numbers):
    # 通过加一个位置参数firstNum来处理异常情况
    if not isinstance(firstNum, (int, float)):
        return -1
    mulResult = firstNum
    for num in numbers:
        # 判断numbers中的元素类型
        if not isinstance(num, (int, float)):
            return -1
        mulResult *= num
    return mulResult
#测试部分
try:
    mul()
    print('测试失败!')
except TypeError:
    print('测试成功!')
```

### 递归

#### 汉诺塔

```python
def move(n, a, b, c):
    if n == 1:
        print(a, '-->', c)
    else: 
        move(n-1,a,c,b)
        move(1,a,b,c)
        move(n-1,b,a,c)
```

## 高级特性

### 切片

```python
 L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
```

取一个list或tuple的部分元素，可以使用py的切片操作符

`L[0:3]`表示，从索引`0`开始取，直到索引`3`为止，**但不包括索引`3`**。即索引`0`，`1`，`2`，正好是3个元素。

如果第一个索引是`0`，还可以省略：`L[:3]`

类似的，既然Python支持`L[-1]`取倒数第一个元素，那么它同样支持倒数切片，如下：

```python
>>> L[-2:]
['Bob', 'Jack']
>>> L[-2:-1]
['Bob']
```

* 其他应用：

  ```text
  L = list(range(100))
  ```

  在前10个数中，每两个取一个：

  ```text
  >>> L[:10:2]
  [0, 2, 4, 6, 8]
  ```

  所有数，每5个取一个：

  ```text
  >>> L[::5]
  [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]
  ```

  甚至什么都不写，只写`[:]`就可以原样复制一个list：

  ```text
  >>> L[:]
  [0, 1, 2, 3, ..., 99]
  ```

* tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple：

  ```text
  >>> (0, 1, 2, 3, 4, 5)[:3]
  (0, 1, 2)
  ```

* 字符串`'xxx'`也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串：

  ```text
  >>> 'ABCDEFG'[:3]
  'ABC'
  >>> 'ABCDEFG'[::2]
  'ACEG'
  ```

#### 练习：去除字符串开头和结尾的空格

```python
def trim(s):
    if s =='':
        return s
    else:
        while s[0] == ' ' and len(s)>1: #加and len(s)>1是避免下面的切片s[1:]中只有1个元素而访问出错
            s = s[1:]                           #这样写可以删除第一个元素，s[1:]默认包含最后一个元素
        if s ==' ':
            return ''
        if len(s)>0:                             #对类似'hello  '进行处理
            while s[-1] == ' ':
                s = s[0:-1]                        #s = s[0:-1]不包含s[-1]
    return s
```

### 迭代

如果给定一个`list`或`tuple`，我们可以通过`for`循环来遍历这个`list`或`tuple`，这种遍历我们称为迭代（Iteration）。

在Python中，迭代是通过`for ... in`来完成的，而很多语言比如C语言，迭代`list`是通过下标完成的

Python的`for`循环不仅可以用在`list`或`tuple`上，还可以作用在其他可迭代对象上。

`list`这种数据类型虽然有下标，但很多其他数据类型是没有下标的，但是，只要是可迭代对象，无论有无下标，都可以迭代，比如`dict`就可以迭代：

```python
d = {'a': 1, 'b': 2, 'c': 3}
for key in d:
    print(key)
>>> a
    b
    c
```

* **因为`dict`的存储不是按照`list`的方式顺序排列，所以，迭代出的结果顺序很可能不一样**

  默认情况下，`dict`迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。

* 由于字符串也是可迭代对象，因此，也可以作用于`for`循环
* 最后一个小问题，如果要对`list`实现类似Java那样的下标循环怎么办？Python内置的`enumerate`函数可以把一个`list`变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身：

  ```python
  for i, value in enumerate(['A', 'B', 'C']):
      print(i, value)
  ...
  0 A
  1 B
  2 C
  ```

  上面的`for`循环里，同时引用了两个变量，在Python里是很常见的，比如下面的代码：

  ```python
  for x, y in [(1, 1), (2, 4), (3, 9)]:
      print(x, y)
  ...
  1 1
  2 4
  3 9
  ```

#### 练习：返回list中的最大值和最小值为tuple类型

```python
def findMinAndMax(L):
    if L==[]:
        return (None,None)      #判空必做！
    max=min=L[0]                  #一开始max和min直接赋0 样例2过不去
    for x in L:
        if x > max:
            max = x
        if x < min:
            min = x
    return (min, max)

# 测试
if findMinAndMax([]) != (None, None):
    print('1测试失败!')
elif findMinAndMax([7]) != (7, 7):
    print('2测试失败!')
elif findMinAndMax([7, 1]) != (1, 7):
    print('3测试失败!')
elif findMinAndMax([7, 1, 3, 9, 5]) != (1, 9):
    print('4测试失败!')
else:
    print('测试成功!')
```

