# python guidebook（learning record）

###### 本文适合有一定编程基础的人阅读。



## 0. 知识引用声明

CSDN博主「骆昊」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/jackfrued/article/details/79521404

https://github.com/jackfrued/Python-100-Days/blob/master/Day01-15/08.%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80.md

https://github.com/jackfrued/Python-100-Days

https://blog.csdn.net/taotiezhengfeng/article/details/72236323

###### 持续更新中......

**仅作为个人学习使用，不作为商业用途。**



## 1. 库



### turtle.

```python
turtle.forward()
turtle.backward()
turtle.color("")
```

[detail](https://docs.python.org/3/library/turtle.html)



## 2. python编译过程和执行原理



###  编译过程

​	对于Python而言，python源码**不需要编译成二进制代码**，它可以**直接从源代码运行程序**

​	当我们运行python文件程序的时候，python解释器将源代码转换为**字节码**，然后再由**python解释器**来执行这些字节码

​	这样，**python就不用担心程序的编译,库的链接加载等问题了**



### 特性

* 每次运行都要进行转换成字节码，然后再有虚拟机把字节码转换成机器语言，最后才能在硬件上运行。
* 与编译性语言相比，每次多出了编译和链接的过程，性能肯定会受到影响
* 而python并不是每次都需要转换字节码，解释器在转换之前会**判断代码文件的修改时间是否与上一次转换后的字节码pyc文件的修改时间一致，若不一致才会重新转换**
* 不用关心**程序的编译和库的链接**等问题
* python代码与机器底层更远了，**python程序更加易于移植，基本上无需改动就能在多平台上运行**。



### 程序设计语言的一般运行过程

* 编译实现的语言，不解释。

* **解释型语言，解释器不产生目标机器代码，而是产生中间代码**
  * 中间代码与机器代码不同，**中间代码的解释是由软件支持的**，不能直接使用在硬件上
  * 用解释型语言编写的程序是由另一个可以理解中间代码的解释程序执行的。
  *  解释程序的任务是逐一将源代码的语句解释成可执行的机器指令，不需要将源程序翻译成目标代码再执行
  * 对于解释型语言，需要一个专门的解释器来执行该程序，每条语句只有在执行是才能被翻译，这种解释型语言每执行一次就翻译一次，因而**效率低下**
* Java解释器，java很特殊，java是需要编译的，但是**没有直接编译成机器语言，而是编译成字节码**，然后在Java虚拟机上**用解释的方式**执行字节码。
* python是一门解释语言，但是出于效率的考虑，提供了一种编译的方法。编译之后就得到pyc文件，存储了字节码。
* 除了效率之外，字节码的形式也增加了反向工程的难度，可以保护源代码。这个只是一定程度上的保护，反编译还是可以的。



### python内部执行过程

* 当我们执行Python代码的时候，在Python解释器用四个过程“拆解”我们的代码，最终被CPU执行返回给用户。
* 首先当用户键入代码交给Python处理的时候会先进行词法分析，例如用户键入关键字或者当输入关键字有误时，都会被词法分析所触发，不正确的代码将不会被执行。
* 下一步Python会进行语法分析
* 在执行Python前，Python会生成.pyc文件，这个文件就是字节码，如果我们不小心修改了字节码，**Python下次重新编译该程序时会和其上次生成的字节码文件进行比较，如果不匹配则会将被修改过的字节码文件进行覆盖，以确保每次编译后字节码的准确性。**
* 那么什么是字节码？**字节码在Python虚拟机程序里对应的是PyCodeObject对象。.pyc文件是字节码在磁盘上的表现形式。**
  * Python中有一个内置函数compile()，可以将源文件编译成codeobject
* python字节码其实是模仿的x86的汇编，将代码编译成一条一条的指令交给一个虚拟的cpu去执行
* 什么是pyc？
  * pyc是一种二进制文件，是由py文件经过编译后，生成的文件，是一种byte code。
  * py文件变成pyc文件后，加载的速度有所提高，而且pyc是一种跨平台的字节码，是由[Python](http://lib.csdn.net/base/python)的虚拟机来执行的，这个是类似于[Java](http://lib.csdn.net/base/javase)或者.NET的虚拟机的概念。
  * pyc的内容，是跟python的版本相关的，**不同版本编译后的pyc文件是不同的**，2.5编译的pyc文件，2.4版本的python是无法执行的。

[detail](https://blog.csdn.net/helloxiaozhe/article/details/78104975)



## 3. 常用函数



* `input()`: 读入一个**string**  

  ###### 它也只能以string的形式读入

* `print()`: 打印值

* 类型转化：

  * `int()`: 将一个数值或字符串转换成整数，可以指定进制。
  * `float()`：将一个字符串转换成浮点数。
  * `str()`：将指定的对象转换成字符串形式，可以指定编码。
  * `chr()`：将整数转换成该编码对应的字符串（一个字符）。
  * `ord()`：将字符串（一个字符）转换成对应的编码（整数）。

| 运算符                                          | 描述                           |
| ----------------------------------------------- | ------------------------------ |
| `[]` `[:]`                                      | 下标，切片                     |
| `**`                                            | 指数                           |
| `~` `+` `-`                                     | 按位取反, 正负号               |
| `*` `/` `%` `//`                                | 乘，除，模，整除               |
| `+` `-`                                         | 加，减                         |
| `>>` `<<`                                       | 右移，左移                     |
| `&`                                             | 按位与                         |
| `^` `|`                                         | 按位异或，按位或               |
| `<=` `<` `>` `>=`                               | 小于等于，小于，大于，大于等于 |
| `==` `!=`                                       | 等于，不等于                   |
| `is` `is not`                                   | 身份运算符                     |
| `in` `not in`                                   | 成员运算符                     |
| `not` `or` `and`                                | 逻辑运算符                     |
| `=` `+=` `-=` `*=` `/=` `%=` `//=` `**=` `&=` ` | =` `^=` `>>=` `<<=`            |

* 占位符语法
  * 其中`%d`是整数的占位符
  * `%f`是小数的占位符
  * `%%`表示百分号（因为百分号代表了占位符，所以带占位符的字符串中要表示百分号必须写成`%%`）
  * 字符串之后的`%`后面跟的变量值会替换掉占位符然后输出到终端中
  * （example）`print('%d ** %d = %d' % (a, b, a ** b))`
* 



## 4. 逻辑结构与数据结构



* python中没有用花括号来构造代码块而是**使用了缩进的方式来表示代码的层次结构**，如果`if`条件成立的情况下需要执行多条语句，只要保持多条语句具有相同的缩进就可以了。换句话说**连续的代码如果又保持了相同的缩进那么它们属于同一个代码块**，相当于是一个执行的整体。**缩进**可以使用任意数量的空格，但**通常使用4个空格**，建议大家**不要使用制表键**或者**设置你的代码编辑工具自动将制表键变成4个空格**。
* Python查找一个变量时会按照“**局部作用域”、“嵌套作用域”、“全局作用域”和“内置作用域**”的顺序进行搜索

### 分支结构（if）

* 同理`elif`和`else`中也可以再构造新的分支，我们称之为嵌套的分支结构，**也就是说上面的代码也可以写成下面的样子。**
* example

```python
if x > 1:
    y = 3 * x - 5
elif x >= -1:
    y = x + 2
else:
    y = 5 * x + 3
```





### 循环结构



#### for

- `range(101)`：可以用来产生0到100范围的整数，需要注意的是取不到101。
- `range(1, 101)`：可以用来产生1到100范围的整数，相当于前面是闭区间后面是开区间。
- `range(1, 101, 2)`：可以用来产生1到100的奇数，其中2是步长，即每次数值递增的值。
- `range(100, 0, -2)`：可以用来产生100到1的偶数，其中-2是步长，即每次数字递减的值。

```python
for x in range(101):
    sum += x
print(sum)                                                                     (example)
```



#### while

```python
while True'''(这里放表达式)''':
    counter += 1
    number = int(input('请输入: '))
    if number < answer:
        print('大一点')
    elif number > answer:
        print('小一点')
    else:
        print('恭喜你猜对了!')
        break                                                                  (example)
```





### 字符串

* 所谓**字符串**，就是由零个或多个字符组成的有限序列，一般记为[![$${\displaystyle s=a_{1}a_{2}\dots a_{n}(0\leq n \leq \infty)}$$](https://github.com/jackfrued/Python-100-Days/raw/master/Day01-15/res/formula_5.png)](https://github.com/jackfrued/Python-100-Days/blob/master/Day01-15/res/formula_5.png)。在Python程序中，如果我们把单个或多个字符用单引号或者双引号包围起来，就可以表示一个字符串。
* 可以在字符串中使用`\`（反斜杠）来表示转义，也就是说`\`后面的字符不再是它原来的意义，例如：`\n`不是代表反斜杠和字符n，而是表示换行；而`\t`也不是代表反斜杠和字符t，而是表示制表符。所以如果想在字符串中表示`'`要写成`\'`，同理想表示`\`要写成`\\`。
* 在`\`后面还可以跟一个八进制或者十六进制数来表示字符，例如`\141`和`\x61`都代表小写字母`a`，前者是八进制的表示法，后者是十六进制的表示法。也可以在`\`后面跟Unicode字符编码来表示字符

* 可以使用`+`运算符来实现**字符串的拼接**
* 可以使用`*`运算符来重复一个**字符串的内容**
* 可以使用`in`和`not in`来判断**一个字符串是否包含另外一个字符串****（成员运算）**
* 我们也可以用`[]`和`[:]`运算符**从字符串取出某个字符或某些字符****（切片运算）**
* Python 3.6以后，格式化字符串还有更为简洁的书写方式，就是在字符串前加上字母`f`，我们可以使用下面的**语法糖**来简化上面的代码。
* 除了**字符串**，**Python还内置了多种类型的数据结构**，如果要在程序中保存和操作数据，绝大多数时候可以利用现有的数据结构来实现，最常用的包括**列表、元组、集合和字典**。
* **数值类型是标量类型，也就是说这种类型的对象没有可以访问的内部结构；而字符串类型是一种==结构化的、非标量类型==，所以才会有一系列的属性和方法。**



### 列表



下面的代码演示了如何定义列表、如何遍历列表以及列表的下标运算。

```
list1 = [1, 3, 5, 7, 100]
print(list1) # [1, 3, 5, 7, 100]
# 乘号表示列表元素的重复
list2 = ['hello'] * 3
print(list2) # ['hello', 'hello', 'hello']
# 计算列表长度(元素个数)
print(len(list1)) # 5
# 下标(索引)运算
print(list1[0]) # 1
print(list1[4]) # 100
# print(list1[5])  # IndexError: list index out of range
print(list1[-1]) # 100
print(list1[-3]) # 5
list1[2] = 300
print(list1) # [1, 3, 300, 7, 100]
# 通过循环用下标遍历列表元素
for index in range(len(list1)):
    print(list1[index])
# 通过for循环遍历列表元素
for elem in list1:
    print(elem)
# 通过enumerate函数处理列表之后再遍历可以同时获得元素索引和值
for index, elem in enumerate(list1):
    print(index, elem)
```

下面的代码演示了如何向列表中添加元素以及如何从列表中移除元素。

```
list1 = [1, 3, 5, 7, 100]
# 添加元素
list1.append(200)
list1.insert(1, 400)
# 合并两个列表
# list1.extend([1000, 2000])
list1 += [1000, 2000]
print(list1) # [1, 400, 3, 5, 7, 100, 200, 1000, 2000]
print(len(list1)) # 9
# 先通过成员运算判断元素是否在列表中，如果存在就删除该元素
if 3 in list1:
	list1.remove(3)
if 1234 in list1:
    list1.remove(1234)
print(list1) # [1, 400, 5, 7, 100, 200, 1000, 2000]
# 从指定的位置删除元素
list1.pop(0)
list1.pop(len(list1) - 1)
print(list1) # [400, 5, 7, 100, 200, 1000]
# 清空列表元素
list1.clear()
print(list1) # []
```

和字符串一样，列表也可以做切片操作，通过切片操作我们可以实现对列表的复制或者将列表中的一部分取出来创建出新的列表，代码如下所示。

```
fruits = ['grape', 'apple', 'strawberry', 'waxberry']
fruits += ['pitaya', 'pear', 'mango']
# 列表切片
fruits2 = fruits[1:4]
print(fruits2) # apple strawberry waxberry
# 可以通过完整切片操作来复制列表
fruits3 = fruits[:]
print(fruits3) # ['grape', 'apple', 'strawberry', 'waxberry', 'pitaya', 'pear', 'mango']
fruits4 = fruits[-3:-1]
print(fruits4) # ['pitaya', 'pear']
# 可以通过反向切片操作来获得倒转后的列表的拷贝
fruits5 = fruits[::-1]
print(fruits5) # ['mango', 'pear', 'pitaya', 'waxberry', 'strawberry', 'apple', 'grape']
```

下面的代码实现了对列表的排序操作。

```
list1 = ['orange', 'apple', 'zoo', 'internationalization', 'blueberry']
list2 = sorted(list1)
# sorted函数返回列表排序后的拷贝不会修改传入的列表
# 函数的设计就应该像sorted函数一样尽可能不产生副作用
list3 = sorted(list1, reverse=True)
# 通过key关键字参数指定根据字符串长度进行排序而不是默认的字母表顺序
list4 = sorted(list1, key=len)
print(list1)
print(list2)
print(list3)
print(list4)
# 给列表对象发出排序消息直接在列表对象上进行排序
list1.sort(reverse=True)
print(list1)
```

### 生成式和生成器

我们还可以使用列表的生成式语法来创建列表，代码如下所示。

```python
f = [x for x in range(1, 10)]
print(f)
f = [x + y for x in 'ABCDE' for y in '1234567']
print(f)
# 用列表的生成表达式语法创建列表容器
# 用这种语法创建列表之后元素已经准备就绪所以需要耗费较多的内存空间
f = [x ** 2 for x in range(1, 1000)]
print(sys.getsizeof(f))  # 查看对象占用内存的字节数
print(f)
# 请注意下面的代码创建的不是一个列表而是一个生成器对象
# 通过生成器可以获取到数据但它不占用额外的空间存储数据
# 每次需要数据的时候就通过内部的运算得到数据(需要花费额外的时间)
f = (x ** 2 for x in range(1, 1000))
print(sys.getsizeof(f))  # 相比生成式生成器不占用存储数据的空间
print(f)
for val in f:
    print(val)
```



### 元组



Python中的元组与列表类似也是一种容器数据类型，可以用一个变量（对象）来存储多个数据，不同之处在于元组的元素不能修改，在前面的代码中我们已经不止一次使用过元组了。顾名思义，我们把多个元素组合到一起就形成了一个元组，所以它和列表一样可以保存多条数据。下面的代码演示了如何定义和使用元组。

```python
# 定义元组
t = ('骆昊', 38, True, '四川成都')
print(t)
# 获取元组中的元素
print(t[0])
print(t[3])
# 遍历元组中的值
for member in t:
    print(member)
# 重新给元组赋值
# t[0] = '王大锤'  # TypeError
# 变量t重新引用了新的元组原来的元组将被垃圾回收
t = ('王大锤', 20, True, '云南昆明')
print(t)
# 将元组转换成列表
person = list(t)
print(person)
# 列表是可以修改它的元素的
person[0] = '李小龙'
person[1] = 25
print(person)
# 将列表转换成元组
fruits_list = ['apple', 'banana', 'orange']
fruits_tuple = tuple(fruits_list)
print(fruits_tuple)
```

这里有一个非常值得探讨的问题，我们已经有了列表这种数据结构，为什么还需要元组这样的类型呢？

1. 元组中的元素是无法修改的，事实上我们在项目中尤其是[多线程](https://zh.wikipedia.org/zh-hans/多线程)环境（后面会讲到）中可能更喜欢使用的是那些不变对象（一方面因为对象状态不能修改，所以可以避免由此引起的不必要的程序错误，简单的说就是一个不变的对象要比可变的对象更加容易维护；另一方面因为没有任何一个线程能够修改不变对象的内部状态，一个不变对象自动就是线程安全的，这样就可以省掉处理同步化的开销。一个不变对象可以方便的被共享访问）。所以结论就是：如果不需要对元素进行添加、删除、修改的时候，可以考虑使用元组，当然如果一个方法要返回多个值，使用元组也是不错的选择。
2. 元组在创建时间和占用的空间上面都优于列表。我们可以使用sys模块的getsizeof函数来检查存储同样的元素的元组和列表各自占用了多少内存空间，这个很容易做到。我们也可以在ipython中使用魔法指令%timeit来分析创建同样内容的元组和列表所花费的时间.



### 集合



Python中的集合跟数学上的集合是一致的，不允许有重复元素，而且可以进行交集、并集、差集等运算。

[![img](https://github.com/jackfrued/Python-100-Days/raw/master/Day01-15/res/python-set.png)](https://github.com/jackfrued/Python-100-Days/blob/master/Day01-15/res/python-set.png)

可以按照下面代码所示的方式来创建和使用集合。

```
# 创建集合的字面量语法
set1 = {1, 2, 3, 3, 3, 2}
print(set1)
print('Length =', len(set1))
# 创建集合的构造器语法(面向对象部分会进行详细讲解)
set2 = set(range(1, 10))
set3 = set((1, 2, 3, 3, 2, 1))
print(set2, set3)
# 创建集合的推导式语法(推导式也可以用于推导集合)
set4 = {num for num in range(1, 100) if num % 3 == 0 or num % 5 == 0}
print(set4)
```

向集合添加元素和从集合删除元素。

```
set1.add(4)
set1.add(5)
set2.update([11, 12])
set2.discard(5)
if 4 in set2:
    set2.remove(4)
print(set1, set2)
print(set3.pop())
print(set3)
```

集合的成员、交集、并集、差集等运算。

```
# 集合的交集、并集、差集、对称差运算
print(set1 & set2)
# print(set1.intersection(set2))
print(set1 | set2)
# print(set1.union(set2))
print(set1 - set2)
# print(set1.difference(set2))
print(set1 ^ set2)
# print(set1.symmetric_difference(set2))
# 判断子集和超集
print(set2 <= set1)
# print(set2.issubset(set1))
print(set3 <= set1)
# print(set3.issubset(set1))
print(set1 >= set2)
# print(set1.issuperset(set2))
print(set1 >= set3)
# print(set1.issuperset(set3))
```

> **说明：** Python中允许通过一些特殊的方法来为某种类型或数据结构自定义运算符（后面的章节中会讲到），上面的代码中我们对集合进行运算的时候可以调用集合对象的方法，也可以直接使用对应的运算符，例如`&`运算符跟intersection方法的作用就是一样的，但是使用运算符让代码更加直观。



### 字典



字典是另一种可变容器模型，Python中的字典跟我们生活中使用的字典是一样一样的，它可以存储任意类型对象，与列表、集合不同的是，字典的每个元素都是由一个键和一个值组成的“键值对”，键和值通过冒号分开。下面的代码演示了如何定义和使用字典。

```python
# 创建字典的字面量语法
scores = {'骆昊': 95, '白元芳': 78, '狄仁杰': 82}
print(scores)
# 创建字典的构造器语法
items1 = dict(one=1, two=2, three=3, four=4)
# 通过zip函数将两个序列压成字典
items2 = dict(zip(['a', 'b', 'c'], '123'))
# 创建字典的推导式语法
items3 = {num: num ** 2 for num in range(1, 10)}
print(items1, items2, items3)
# 通过键可以获取字典中对应的值
print(scores['骆昊'])
print(scores['狄仁杰'])
# 对字典中所有键值对进行遍历
for key in scores:
    print(f'{key}: {scores[key]}')
# 更新字典中的元素
scores['白元芳'] = 65
scores['诸葛王朗'] = 71
scores.update(冷面=67, 方启鹤=85)
print(scores)
if '武则天' in scores:
    print(scores['武则天'])
print(scores.get('武则天'))
# get方法也是通过键获取对应的值但是可以设置默认值
print(scores.get('武则天', 60))
# 删除字典中的元素
print(scores.popitem())
print(scores.popitem())
print(scores.pop('骆昊', 100))
# 清空字典
scores.clear()
print(scores)
```



## 5. 封装结构



### 函数

利用`def`来定义函数

​	在函数名后面的圆括号中可以放置传递给函数的参数，这一点和数学上的函数非常相似，程序中函数的参数就相当于是数学上说的函数的自变量，而函数执行完成后我们可以通过`return`关键字来返回一个值，这相当于数学上说的函数的因变量。

```python
def fac(num):
    """求阶乘"""
    result = 1
    for n in range(1, num + 1):
        result *= n
    return result                                                             （example）
```

* 需要说明的是，**如果我们导入的模块除了定义函数之外还中有可以执行代码，那么Python解释器在导入这个模块时就会执行这些代码**，事实上我们可能并不希望如此，因此如果我们在模块中编写了执行代码，最好是将这些执行代码放入如下所示的条件中，这样的话除非直接运行该模块，if条件下的这些代码是不会执行的，因为只有直接执行的模块的名字才是"__main__"。

```python
# __name__是Python中一个隐含的变量它代表了模块的名字
# 只有被Python解释器直接执行的模块的名字才是__main__
if __name__ == '__main__':
    print('call foo()')
    foo()
    print('call bar()')
    bar()                                                                      (example)
```



### 面向对象的语言编程



* 把一组数据结构和处理它们的方法组成对象（object）
* 把相同行为的对象归纳为类（class）
* 通过类的封装（encapsulation）隐藏内部细节
* 通过继承（inheritance）实现类的特化（specialization）和泛化（generalization）
* 通过多态（polymorphism）实现基于对象类型的动态分派。

#### 类的定义

​	在Python中可以使用`class`关键字定义类

```python
class Student(object):

    # __init__是一个特殊方法用于在创建对象时进行初始化操作
    # 通过这个方法我们可以为学生对象绑定name和age两个属性
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self, course_name):
        print('%s正在学习%s.' % (self.name, course_name))

    # PEP 8要求标识符的名字用全小写多个单词用下划线连接
    # 但是部分程序员和公司更倾向于使用驼峰命名法(驼峰标识)
    def watch_movie(self):
        if self.age < 18:
            print('%s只能观看《熊出没》.' % self.name)
        else:
            print('%s正在观看岛国爱情大电影.' % self.name)
```

​	通过下面的方式来创建对象并给对象发消息。

```python
def main():
    # 创建学生对象并指定姓名和年龄
    stu1 = Student('骆昊', 38)
    # 给对象发study消息
    stu1.study('Python程序设计')
    # 给对象发watch_av消息
    stu1.watch_movie()
    stu2 = Student('王大锤', 15)
    stu2.study('思想品德')
    stu2.watch_movie()
```

访问权限

​	在Python中，属性和方法的访问权限只有两种，也就是公开的和私有的，如果希望属性是私有的，在给属性命名时可以用两个下划线作为开头。

```
class Test:

    def __init__(self, foo):
        self.__foo = foo

    def __bar(self):
        print(self.__foo)
        print('__bar')


def main():
    test = Test('hello')
    # AttributeError: 'Test' object has no attribute '__bar'
    test.__bar()
    # AttributeError: 'Test' object has no attribute '__foo'
    print(test.__foo)


if __name__ == "__main__":
    main()
```

​	**Python并没有从语法上严格保证私有属性或方法的私密性**，它只是给私有的属性和方法换了一个名字来妨碍对它们的访问，事实上如果你知道更换名字的规则仍然可以访问到它们

​	因为绝大多数程序员都认为开放比封闭要好，而且**程序员要自己为自己的行为负责。**

​	在实际开发中，我们并不建议将属性设置为私有的，因为这会导致子类无法访问（后面会讲到）。所以大多数Python程序员会遵循一种命名惯例就是让属性名以单下划线开头来表示属性是受保护的，本类之外的代码在访问这样的属性时应该要保持慎重。这种做法并不是语法上的规则，**单下划线开头的属性和方法外界仍然是可以访问的，所以更多的时候它是一种暗示或隐喻**

​	面向对象有三大支柱：封装、继承和多态

简单的说，类和类之间的关系有三种：is-a、has-a和use-a关系。

- is-a关系也叫继承或泛化，比如学生和人的关系、手机和电子产品的关系都属于继承关系。
- has-a关系通常称之为关联，比如部门和员工的关系，汽车和引擎的关系都属于关联关系；关联关系如果是整体和部分的关联，那么我们称之为聚合关系；如果整体进一步负责了部分的生命周期（整体和部分是不可分割的，同时同在也同时消亡），那么这种就是最强的关联关系，我们称之为合成关系。
- use-a关系通常称之为依赖，比如司机有一个驾驶的行为（方法），其中（的参数）使用到了汽车，那么司机和汽车的关系就是依赖关系。

里氏替换原则的内容可以描述为： “派生类（子类）对象可以在程序中代替其基类（超类）对象。”



[继承与多态][https://github.com/jackfrued/Python-100-Days/blob/master/Day01-15/09.%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%BF%9B%E9%98%B6.md]





## 6. 简洁语法

```python
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b---------------------（简洁的赋值式）
        （DO NOT DO THAT IN C/C++/JAVA）
        yield a


def main():
    for val in fib(20):
        print(val)


if __name__ == '__main__':
    main()
```



## 7. 常见陷阱



* 在 Python 中一切都是对象，整数也是对象，在比较两个整数时有两个运算符==和is，它们的区别是：

  is比较的是两个整数对象的id值是否相等，也就是比较两个引用是否代表了内存中同一个地址。
  “==”比较的是两个整数对象的内容是否相等，使用时其实是调用了对象的__ eq __()方法。

  

  * Python出于对性能的考虑所做的一项优化。对于整数对象，**Python把一些频繁使用的整数对象缓存起来，保存到一个叫small_ints的链表中**，**在Python的整个生命周期内，任何需要引用这些整数对象的地方，都不再重新创建新的对象，而是直接引用缓存中的对象。**Python把频繁使用的整数对象的值定在[-5, 256]这个区间，如果需要这个范围的整数，就直接从small_ints中获取引用而不是临时创建新的对象。因为大于256或小于-5的整数不在该范围之内，所以就算两个整数的值是一样，但它们是不同的对象。
    https://blog.csdn.net/jackfrued/article/details/79521404



* Python内部为了进一步提高性能，凡是在一个代码块中创建的整数对象，如果值不在small_ints缓存范围之内，但在同一个代码块中已经存在一个值与其相同的整数对象了，那么就直接引用该对象，否则创建一个新的对象出来，这条规则对不在small_ints范围的负数并不适用，对负数值浮点数也不适用，但对非负浮点数和字符串都是适用的
  https://blog.csdn.net/jackfrued/article/details/79521404



* Python中有一种内置的数据类型叫列表，它是一种容器，可以用来承载其他的对象（准确的说是其他对象的引用），列表中的对象可以称为列表的元素，很明显我们可以把列表作为列表中的元素，这就是所谓的嵌套列表。

  * **程序中可以使用的内存从逻辑上可以为五个部分，按照地址从高到低依次是：栈（stack）、堆（heap）、数据段（data segment）、只读数据段（static area）和代码段（code segment）**
    * 栈用来存储局部、临时变量，以及函数调用时保存现场和恢复现场需要用到的数据，这部分内存在代码块开始执行时自动分配，代码块执行结束时自动释放，通常由编译器自动管理
    * 堆的大小不固定，可以动态的分配和回收
  * 像Python、Java等编程语言都使用了垃圾回收机制来实现自动化的内存管理（自动回收不再使用的堆空间）
  * 所以下面的代码中，变量`a`并不是真正的对象，它是对象的引用，相当于记录了对象在堆空间的地址，通过这个地址我们可以访问到对应的对象；同理，变量`b`是列表容器的引用，它引用了堆空间上的列表容器，而列表容器中并没有保存真正的对象，它保存的也仅仅是对象的引用。

  ```
  a = object()
  b = ['apple', 'pitaya', 'grape']
  ```

* Python类中的那些魔法方法，如__ str __ 、__ repr __等，这些方法并不是私有成员哦，虽然它们以双下划线开头，但是他们也是以双下划线结尾的，这种命名并不是私有成员的命名，这一点对初学者来说真的很坑

* 在Python中我们实在没有必要将类中的属性或方法用双下划线开头的命名处理成私有的成员，因为这并没有任何实际的意义。

  * 建议用单下划线开头的受保护成员，虽然它也不能真正保护这些属性或方法，但是它相当于给调用者一个暗示，让调用者知道这是不应该直接访问的属性或方法，而且这样做并不影响子类去继承这些东西。
  * https://blog.csdn.net/jackfrued/article/details/79521404



