##### input()用于输入，其有返回值（即用户输入的值），默认返回字符串。括号里可放提示语句

##### 一行代码若想分为多行来写，需要在每一行的末尾加上“\”

##### 单个“/”表示数学中的除法，不会取整。“//”才会向下取整。

##### 字符串类型可以乘以整数类型，相当于这个字符串被复制了整数倍，若做输出，即会重复输出。

##### 用`pass`来占位，相当于`//TODO`

##### 条件语句

if [条件] : 

    [执行语句]

    [执行语句]

elif [条件二]:

    [执行语句] 

else : 

    [执行语句]

（要有缩进，[条件]外面不用中括号也不用小括号）

##### 逻辑关键词

(not 非) > (and 与) > (or 或)

##### 方法与函数

方法：对象.方法名()

函数：函数名()

##### 列表（list）

1. **与普通数据类型（字符串，整型，浮点型，布尔型）的区别**：列表在调用函数或方法对其代表的值进行改变时，其本身值确实会被改变；而普通数据类型调用函数或方法进行改变时，其本身的值不会被改变，相当于是其值被复制了一遍，改变的是复制后的值，然后进行输出或其他操作。

2. **常用方法**：`.remove(【元素】)`*（移除）*，`.append(【元素】)`*（添加）* `.min(【列表】)`（返回列表中的最小值）`.max(【列表】)``.sort(【列表】)`（给列表排序）`len(【列表】)`（返回列表长度）

3. **命名方式**：`a = [【元素】,【元素】]`    （可以为空，里面可以有任何元素（但必须是同一类型），用逗号分隔）

4. **赋值**：`a[1] = 【另一个元素】`

##### 字典（dictionary）

1. **命名方式**：`a = { 【key】 : 【value】,  【key】 : 【value】 }` *（key必须是不可变的数据结构）*

2. **旧键赋新值**或**新增键值对**：`a[【key1】] = 【value2】`

3. **判断某个键是否已经存在**：`【key】 in a`，若存在，则该表达式的值为True，否则为False

4. **删除键值对**：`del a[【key1】]`

5. **常用方法**：`.keys()`（返回里面的所有键）`.values()`（返回里面的所有值）`.items()`（返回里面的所有键值对）

##### 元组（tuple）

1. **命名方式**：`a = (【元素】, 【元素】)` 

2. **不可变**，可作为字典的key

3. **访问元组中的元素**：a[1]、a[0]

##### 循环（for）

1. 写法：`for 【变量名】 in 【可迭代的对象】:`（变量名处可以是多个变量，相应的可迭代对象得有同样多数量的值）

2. **range(a, b)**：a≤ x<b        **range(a, b, c)** ：c为步长

##### 格式化字符串

用format()方法或直接在字符串前加 ‘ f ’，举例

```python
y = 90
a = 90.2
c = "jijin"
str1 = "嘻嘻哈哈{0}红红火火{2}恍恍惚惚{1}是啊{0}".format(y, a, c)
#或者如下
str2 = "嘻嘻哈哈{y2}红红火火{c2}恍恍惚惚{a2}是啊{y2}".format(y2 = y, a2 = a, c2 = c)
#或者如下
str3 = "嘻嘻哈哈{y2}红红火火{c2}恍恍惚惚{a2}是啊{y2}".format(y2 = 90, a2 = 90.2, c2 = "jijin")
#或者如下
str4 = "嘻嘻哈哈{y}红红火火{c}恍恍惚惚{a}是啊{y}".format(y = y, a = a, c = c)
#或者如下
str5 = f"嘻嘻哈哈{y}红红火火{c}恍恍惚惚{a}是啊{y}"   # 个人比较喜欢这种
#或者如下
str6 = f"嘻嘻哈哈{90}红红火火{'jijin'}恍恍惚惚{90.2}是啊{90}"

#打印结果皆如下
嘻嘻哈哈90红红火火jijin恍恍惚惚90.2是啊90
```

若要控制浮点数的小数位数，比如三位小数，则在具体值或者变量的后面加上“`:.3f`”

##### 函数

1. 写法：

```python
def fun1():
    #函数体
    #。。。

def fun2(a, b):            #无需说明参数类型，也无需说明函数类型
    c = a+b
    print(c)
    return a          #若没写 return 语句会有默认的 return None

```



##### python内置函数

![](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042212762.png)


##### 引入模块

1. import 【模块】

2. from 【模块】 import 【函数】

3. from 【模块】 import *        （引入该模块的所有函数）

4. 引入第三方库，需要先在互联网上下载，用命令pip install来安装，pypi.org这个网站可以对第三方库进行搜素。
   
   

##### 类

```python
#定义一个类
class Cat:
    def __init__(self, name, age):  #构造函数，必写，名字固定为 __init__() （注意，左右各两个横线）  第一个参数必须是self，代表自己
        self.name = name              #左侧即为对象拥有的属性，在构造函数里定义，不能在外面定义。
        self.age = age
        self.color = "white"

    def meow(self):                  #自定义方法，第一个参数也必须是self
        print(f"{self.name} is meowing.")

    def show_info(self):
        print(f"{self.name} is {self.age} years old and {self.color} in color.")

#创建一个对象
cat1 = Cat("Fluffy", 3)     #创建对象的时候可以不用传入self的值
cat1.meow()                 #调用方法的时候也可以不用传入self的值
cat1.show_info()

#输出结果
Fluffy is meowing.
Fluffy is 3 years old and white in color.


#再定义一个类
class Cat:
    #不写构造器的话会有一个默认的无参构造器，则属性就需要另外声明
    name = None
    age = None
    color = None

    def meow(self):
        print(f"{self.name} is meowing")

    def show_info(self):
        print(f"{self.name} is {self.color} and is {self.age} years old.")

cat = Cat()
cat.name = "kitty"
cat.age = 3
cat.color = "white"
cat.meow()
cat.show_info()


```

##### 继承

```python
class Mammal:
    # 定义哺乳动物类，初始化时接受一个名字参数
    def __init__(self, name):
        self.name = name
        self.has_tail = True

    def speak(self):
        print(f"{self.name} speaks.")

class Dog(Mammal):
    # 定义狗类，继承自哺乳动物类，初始化时接受一个名字参数
    def __init__(self, name):
        super().__init__(name)   

    # 重写说话方法，打印狗叫的信息
    def speak(self):
        print(f"{self.name} barks.")

    # 定义取物方法，打印狗取物的信息
    def fetch(self):
        print(f"{self.name} is fetching.")

class Human(Mammal):
    # 定义人类，继承自哺乳动物类，初始化时接受一个名字参数
    def __init__(self, name):
        super().__init__(name)   
        self.has_tail = Flase     #修改父类继承过来的属性

    # 重写说话方法，打印人说话的信息
    def speak(self):
        print(f"{self.name} talks.")

    # 打印人是否有尾巴的信息
    def show_has_tail(self):
        print("Do humen have tails? " + str(self.has_tail))

# 创建一个Dog对象，名字为Rufus
dog = Dog("Rufus")  
dog.speak()  # 调用Dog对象的speak方法
dog.fetch()  # 调用Dog对象的fetch方法

# 创建一个Cat对象，名字为Whiskers
human = Human("Jack")  
human.speak()  # 调用Human对象的speak方法
human.show_has_tail() # 调用human对象的show_has_tail方法

# 输出结果
Rufus barks.
Rufus is fetching.
Jack talks.
Do humen have tails? False
```

无论是父类的公有属性（公有方法）还是私有属性（私有方法），都会被子类继承下来，但是，子类无法直接访问父类的私有成员值

在多重继承（如：`class A(B, C)`中，如果出现重名的情况，则由继承的顺序来决定谁的优先级高 （B高）。

在多层继承（如：`class A(B)  class B(C)`）中，A中访问父类成员会从父类或兄弟类逐层往上查找，直到找到为止。不能链式写法：`super().super().fun()`

###### 子类调用父类成员

1.基本语法：

    1.`父类名.成员变量`，`父类名.成员方法(self)`（从该父类开始往上找，若该父类没有所要访问的成员，则再往上找）

    2.`super().成员变量`，`super().成员方法()`（从子类的直接父类开始往上查找）



###### 文件路径常识（对于Windows系统来说）（相对路径）

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042215370.png)


![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042215892.png)


在同一目录下的文件，如果想要相互找到彼此的话，可以直接使用文件名，不用前面再加一个“./”



##### 读取文件

1. 使用函数`open()`，`open("【文件路径】", "【模式】", "【encoding=】")`

2. 【文件路径】：可以写绝对路径，也可以写相对路径。

3. 【模式】：传入一个字符串，常用的有"r"（只读），和"w"（只写）两种模式。若不写，则默认为只读模式。读取模式下，如果程序找不到对应的文件名的话，就会报一个`"FileNotFoundError"`的错误。

4. 【encoding】：也是可选的参数，可不写

5. `open()`函数会返回一个文件对象，可以后续对它进行读取和写入的操作。

6. **读取（“r”）**：
   
   1. 例如，把文件对象赋值给一个变量`f`，`f.read()`就可以一次性读取文件里的所有内容，并以字符串返回，`print(f.read())`即可将其打印出来。
   
   2. 一个文件对象的read()方法不可以连续调用，因为每次调用都会读取全部的内容出来，并且它会记录上次读取到哪。所以，第一次调用完之后，第二次调用时只能读取到空的字符串了。
   
   3. 若不想全部读取，那就传入一个数字作为参数，表示一次读取多少字节。

```python
f.read(10)  # 第一次，读1-10字节的文件内容
f.read(10)  # 第二次，读11-20字节的文件内容
f.readline() # 每次读一行的文件内容，根据换行付来判断什么时候本行结束
f.readlines() # 会读取全部内容，并把每行作为列表元素返回，常与for循环结合
f.close()  # 关闭文件，释放资源


# 若容易忘记调用close()方法，可用如下写法：
with open("./data.txt") as f :     # 用with写法
    print(f.read())  # 对文件进行操作   要记得缩进
# 这样，当缩进部分的代码执行完后，资源会自动释放
```

7. **写入（“w”）**：
   
   1. 写入模式下，如果找不到文件名，会自动在路径下创建一个新的文件。
   
   2. 若文件是存在的，那么会将文件原有内容清空，然后写入新的内容。若不想原有内容被清空，则应该用“a”模式（附加模式）
   
   3. 用write()方法来进行写入。如`write("aaaa")`。

8. 其他模式：
   
   1. “**r+**”：可读也可写入
   
   2. **“a+**”：可读也可追加
   
   3. 写入和追加是有区别的。追加是在文件末尾进行写入。而写入是看当前指针在哪个位置，最开始指针位置为1，如果之有过read操作，那么指针会后移，这时再调用write()的话，就是从上次read的结束位置开始写入。
      
      

##### 异常处理

捕获异常，使得后续的程序不会被此异常终止而可以正常运行。

```python
try:
    user_weight = float(input("Enter your weight in kilograms: "))
    user_height = float(input("Enter your height in meters: "))
    bmi = user_weight / (user_height ** 2)
except ValueError as e:                     # If user enters non-numeric input
    print(f"{e}. Invalid input. Please enter a number.")
except ZeroDivisionError:               # If user enters height as zero
    print("Invalid input. Height cannot be zero.")
except:                                 # If any other error occurs
    print("An error occurred. Please try again.")
else:                                   # If no error occurs
    print("Your BMI is:", bmi)
finally:                               # This block is always executed
    print("Thank you for using our BMI calculator.")
    //通常写一些关闭资源的语句
```

##### 测试

调用python自带的库：unittest

```python
# 被测试函数 add2() 所在文件为 add_calculator
def add2(a, b):
    return a + b


# 测试文件 test_add_calculator 
import unittest
from add_calculator import add2

class TestAdd2(unittest.TestCase):      # 写一个子类继承于unittest.TestCase
    # 每一个方法就是一个测试用例，命名方式必须以test_开头，只有这样才能被unittest当作测试用例
    def test_positive_with_negative(self):                
        self.assertEqual(add2(100, -100), 0)

    def test_positive_with_positive(self):
        self.assertEqual(add2(100, 100), 200)

    def test_negative_with_negative(self):
        self.assertEqual(add2(-100, -100), -200)

    def test_negative_with_positive(self):
        self.assertEqual(add2(-100, 100), 0)

if __name__ == '__main__':
    unittest.main()

# 输出结果
....               # 通过为 . 不通过为 F
----------------------------------------------------------------------
Ran 4 tests in 0.000s

OK


```

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042216818.png)


本质上，assertTrue可以代替这些所有的方法。

但推荐使用更有针对性的方法，因为更有针对性的方法会给出更详细具体的原因。

##### 高阶函数

高阶函数可以把函数作为参数。作为参数的函数是直接把函数名作为参数传入，后面不要带括号和参数，因为如果带括号和参数，传入的就是函数的返回值了，而不是函数本身了。

##### 匿名函数

无需名字，即用即扔。关键字：lambda

```python
def calculate_and_print(num1, num2,  calc_func):  
    print(calc_func(num1,  num2))

calculate_and_print(7, 5, lambda num1, num2: num1 * num2)  # 输出35
# num1、num2为传给匿名函数的参数，匿名函数不需要专门写 return，直接放上要放回的结果即可（即上面冒号后面的 “num1 * num2”，只能写一行）

# lambda表达式的语法：lambda 参数1, 参数2, ... : 表达式
# lambda表达式也可以直接作为一个函数来计算，如下：
(lambda num1, num2: num1 * num2)(7, 5)  # 输出35
# 但是一般不推荐这么做，因为lambda表达式的可读性不高。

# 匿名函数也有局限，即它的冒号后面不能有复杂的语句，只能是一行表达式。
```

##### 封装

私有属性或方法：以双下划线开头：`__`

```python
class Cat:
    # 公有属性
    name = None

    # 私有属性
    __age = None       # 实际上完整的名称为 _Cat__age
    __color = None     # 实际上完整的名称为 _Cat__color

    # 公有方法
    def meow(self):
        print(f"{self.name} is meowing.")

    # 私有方法
    def __show_info(self):
        print(f"{self.name} is {self.__age} and {self.__color}")

    def set_age(self, age):
        self.__age = age

    def get_age(self):
        return self.__age

cat1 = Cat()
cat1.name = "kitty"
cat1.__age = 4   # 可以成功赋值，不会报错，但它和Cat里的私有属性age不是同一个变量，而是新创建的一个变量
cat1.set_age(3)
_Cat__age = 9    # 不会报错，但是为无用代码，不会被执行
print(f"{cat1.__age}  {cat1.get_age()}")  # 4  3
```



##### 类型注解

如：`def fun(a: str):`，给形参a进行类型注解，标注a的类型为str。有了类型注解后，当遇到传参的类型错误时，pycharm会给出警告，但是不会报错。

* 变量类型注解
  容器详细类型注解：
  
  ```python
  my_list: list[int] = [100,200,300]
  my_tuple: tuple[str, str, str, float] = ("run", "sing", "fly", 1.0)
  my_set2: set[str] = {"ack", "tim", "hsp"}
  my_dict: dict[str, int] = {"no1": 100, "no2": 200}
  ```
  
  在注释中使用注解：
  
  ```python
  a = 1 # type: int
  b = 8.9    # type: float
  c = 'a' #type: str
  print(a, b, c)
  ```

* 函数（方法）中的类型注解
  
  ```python
  def fun(e: int, f: str) -> float:  # float即为函数返回值类型
      pass
  ```

* Union类型
  
  * 使用的时候需要先导入Union ：`from typing import Union`
  
  * `Union[x, y]`等价于`x|y`，意味着满足 x 或者 y 之一。可以有多个，不仅限于两个。
  
  ```python
  my_list: list[Union[int, str]] = [100,200,300,"fadfa"]
  ```
  
  

##### 多态

不同对象调用相同的方法，表现出不同的状态，称为多态。多态通常作用在继承关系上。

一个父类，具有多个子类，不同子类对象调用相同的方法，执行时产生不同的状态，称为多态。

```python
class Animal:
    def cry(self):
        print("叫叫叫")

class Dog(Animal):
    def cry(self):
        print("汪汪汪")

class Cat(Animal):
    # def cry(self):
    #     print("喵喵喵")
    pass

class Pig(Animal):
    def cry(self):
        print("噜噜噜")

def func(animal: Animal):  # 在python中，子类对象可以传递给父类类型
    animal.cry()

# 测试
dog = Dog()
cat = Cat()
pig = Pig()
func(dog)           # 汪汪汪
func(cat)           # 叫叫叫
func(pig)           # 噜噜噜

```

###### 多态在非继承关系上的体现——来源于python语言的不严谨性

```python
class A:
    def say(self):
        print("aa")

class B:
    def say(self):
        print("bb")

def func2(obj):
    obj.say()

# 测试
a = A()
b = B()
func2(a)     # aa
func2(b)     # bb
```



##### 魔术方法

所有以双下划线"____"包起来的方法，统称为魔术方法。他很特殊，普通方法需要调用，而魔术方法不需要调用就可以自动执行。

魔术方法在类或对象的某些事件发生时会自动执行。若想根据自己的程序定制特殊功能的类，那么就需要对这些方法进行重写。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042216429.png)


###### 举例：`__str__`

打印对象默认返回：类型名+对象内存地址，如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042217252.png)


子类往往重写`__str__`，用于返回对象的属性信息

重写`__str__`方法，`print(对象)`或`str(对象)`时，都会自动调用该对象的`__str__`

```python
class A:
    def say(self):
        print("aa")

    def __str__(self):
        return "A的信息"

print(a, id(a), hex(id(a)))

# 输出
# A的信息 2322140834048 0x21caa612900
```

（像是 java 里的`toString()`）

*（题外话：*

```python
print(a, id(a), hex(id(a)))  

#输出
# <__main__.A object at 0x0000024291282C90> 2484926426256 0x24291282c90
```

###### 再举例：`__eq__`

`"=="`是一个比较运算符，对象之间进行比较时，比较的是内存地址是否相等，即判断是不是同一个对象。重写`__eq__`方法，可以用于判断对象内容/属性是否相等。

*（题外话：* `isinstance(a, A)`：判断 a 是不是 A 类型



##### 类对象和静态方法

###### 类对象

```python
class Monster:
    name = "蝎子精"
    age = 300

    def show_info(self):
        print(f"{self.name} is {self.age} years old")

print(Monster)  # 此时，Monster类已经有对象了，称为“类对象”
print(Monster.name, Monster.age)  # 属性值即为类中赋给它的值
Monster.show_info(Monster)  # 直接将Monster类最为对象传入show_info()方法

# 输出
# <class '__main__.Monster'>
# 蝎子精 300
# 蝎子精 is 300 years old
```

###### 静态方法

加上`@staticmethod`将方法转换为静态方法，静态方法不会接收隐式的第一个参数，要声明一个静态方法，语法为：

```python
class A:
    @staticmethod
    def f(arg1, arg2, argN):
        ...
```

静态方法既可以由类调用（如`C.f()`），也可以由实例调用（如`C().f()`或`c.f()`）



##### 抽象类

* 需要导入模块`abc`才能使用抽象类

* 当我们需要抽象基类时，让类继承`ABC`（`abc`模块中的`ABC`类），使用`@abstractmethod`声明抽象方法（`@abstractmethod`用于声明抽象方法的装饰器，在`abc`模块中），那么这个类就是抽象类。

* 抽象类的价值更多的作用在于设计，是设计者设计好后，让子类继承并实现抽象类的抽象方法。

* 抽象类不能实例化，只能用来继承

* **注意：继承自抽象类的子类必须实现抽象类的所有抽象方法，否则该子类也为抽象类，不可实例化。而抽象类中也可以有普通方法。**

```python
from abc import ABC, abstractmethod


class Animal(ABC):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @abstractmethod
    def cry(self):
        pass

    # @abstractmethod
    # def run(self):
    #     pass

class Tiger(Animal):
    def cry(self):
        print("嗷~")

tiger = Tiger("皮皮", 4)
tiger.cry()

# 输出
# 嗷~
```



##### 其他

```python
print("排序后".center(32, "-"))  # 输出：--------------排序后--------------- （即 字符串居中，旁边填充‘-’，共占32位）
```

###### sort

`[列表].sort(key = None, reverse = False)`

`key`指以什么为依据进行排序，`reverse`指是否要按照从小到大排序。



##### 基于模块开发（房屋出租系统）

分析需求，理清关系，明确功能 --> 思路分析：主程序文件，行为函数文件，工具函数文件，数据储存设计 --> 代码实现

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042220343.png)


##### OOP分层模式（房屋出租系统）

* 主程序

* 界面层

* 业务层

* 数据层 

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410042220785.png)




##### 正则表达式

###### 限定符

1. 限定单个字符
   
   * `?`表示其前面的字符可有可无。如`used?`可以匹配到`used`以及`use`
   
   * `*`表示其前面的字符可出现0次或多次。如`ab*c`可以匹配到`abbbbbbc`、`abc`、`ac`等，但是不可以`adc`
   
   * `+`表示其前面的字符可出现1次或多次。如`ab*c`可以匹配到`abbbbbbc`、`abc`等，但是不可以`adc`、`ac`
   
   * `{a,b}`表示其前面的字符可出现 a 次到 b 次。`{a, }`表示a次以上。`{a}`表示a次。

2. 限定多个字符
   
   用`()`将想要匹配的多个字符包围起来。如`(ab)+`等。

###### “或”运算符

`a|b`则会匹配 a 或者 b。如`a (cat|dog)`会匹配到`a cat`或`a dog`。

###### 字符类

`[abc]`、`[a-z]`、`[A-Z]`、`[a-zA-Z]`、`[A-Za-z0-9]`限定了方括号位置的字符只能为括号里要求的字符。`[^a-zA-Z0-9]`前面有个尖号（脱字符），表示该位置的字符为除了括号里要求字符的其他字符。

###### 元字符

* `\d`代表数字字符，等同于`[0-9]`

* `\w`代表单词字符（英文、数字、下划线）

* `\s`代表空白字符（包括空格、Tab和换行符）

* `\D`代表非数字字符

* `\W`代表非单词字符

* `\S`代表非空白字符

* `.`代表除了换行符外的任意字符

* `^`会匹配行首，`$`会匹配行尾。如`^a`只会匹配行首的 a，而`a$`只会匹配行尾的 a。

* `\b`表示单词字符的边界

###### 贪婪与懒惰匹配

`string = "<span><b>This is a simple text</b></span>"`

1. 贪婪匹配：匹配结果尽可能多——`<span><b>This is a simple text</b></span>`

2. 懒惰匹配：匹配结果尽可能少——`<span>``<b>``</b>``</span>`


