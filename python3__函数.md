## （三）函数

函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。

函数能提高应用的模块性，和代码的重复利用率。

你已经知道Python提供了许多内建函数，比如print()。

但你也可以自己创建函数，这被叫做用户自定义函数。

#### 自定义函数

函数名以 def 关键词开头，后接函数标识符名称和圆括号()。

任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。

函数体以冒号起始，并且缩进。

return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的 return 相当于返回 None。

#### 函数中的参数

##### 语法

func(positional_args,keyword_args,*tuple_nonkw_args,**dict_kw_args)

#### 按参数传递方式

位置参数（定位参数，非关键字参数）：位置顺序十分重要

#### 关键字参数

-  位置参数包裹及使用*

-  关键字参数包裹及使用**

-  包裹解包顺序

-  传递参数时使用包裹


#### 按参数的类型

-  必选(位置参数)
-  关键字/默认

-  *args可变长位置参数，**kwargs可变长关键字参数

### 1. Python 中的函数


```python
n=5
# for i in range(n):
#     print(i)
    
#一函数名对以上代码块进行封装
def foo(num):
    for i in range(num):
        print(i)

#函数调用
foo(5)

#函数的定义 
def foo1(num): #函数名和参数
    #函数体
    sum=0 #函数内部的变量
    for i in range(num):
        sum+=i
    #返回值
    return sum

print('foo1',foo1(5))
    
#函数的返回值，无返回值 
def foo2(num): #函数名和参数
    #函数体
    sum=0 #函数内部的变量
    for i in range(num):
        sum+=i
    #无返回值或return后为空
#     return sum

print('foo2',foo2(5))

#函数的返回值，有返回值 
def foo3(num): #函数名和参数
    #函数体
    sum=0 #函数内部的变量
    for i in range(num):
        sum+=i
    return sum,sum*2

print('foo3',foo3(5))

#return与yield关键字

#return 
def foo1():#不返回任何的函数
    print('i\'m foo1,but i return nothing')

def foo2():#使用return返回值
    return 'i\'m foo2, this is what i return'

def foo3():#函数被调用时，遇到结尾或return时就准备结束了。
    return 'i\'m foo3, this is the first return'
    return 'i\'m foo3, this is the secod return'

#yield
def foo4():
    for i in range(5):
        return i#执行第一次时foo4函数就结束了

    
#yield
def foo5():
    for i in range(5):
        yield i
        yield 'f' #再加入一个yield看看会不会被执行
        i+=1

if __name__=="__main__":
    foo1()
    print(foo2())
    print(foo3())
    g1=foo5()
    print(g1)
    print(type(g1)) # <generator object foo5 at 0x10f3341a8>
    print(next(g1)) # <class 'generator'>
    print(next(g1)) # 0
    print(next(g1)) # f
    print(next(g1)) # 1
    #看一下调用foo4()返回的是什么type(g1)
    #看一下g1是个什么样子的对象next(g1)
    #继续上一次的位置，进入下一层循环
    #执行完最后一次循环，结束 yield语句并抛出StopIteration 异常
```

    0
    1
    2
    3
    4
    foo1 10
    foo2 None
    foo3 (10, 20)
    i'm foo1,but i return nothing
    i'm foo2, this is what i return
    i'm foo3, this is the first return
    <generator object foo5 at 0x10f314f10>
    <class 'generator'>
    0
    f
    1
    f


### 2. 函数中的参数

###### func(positional_args,keyword_args,*tuple_nonkw_args, **dict_kw_args)

```python
func(a, b, c=0, *args, **kw)
	print ('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

>>> func(1,2,3,'4','5','6', d='7',e='8')
'''
a = 1 b = 2 c = 3 args = ('4', '5', '6') kw = {'d': '7', 'e': '8'}
'''
```

```python
#按参数传递方式

#位置参数
def foo3(companyName,websiteUrl): #位置参数的定义
    print('公司名：',companyName,'公司网址：',websiteUrl)
    
foo3('七月在线','http://www.julyedu.com')
foo3('http://www.julyedu.com',websiteUrl='七月在线') 

#位置参数，对位置敏感，传递时不用指定参数名
#关键字参数
def foo4(companyName,websiteUrl,intro='专注AI教育'):
    print('公司名：',companyName,'公司网址：',websiteUrl,'介绍：',intro)
    
foo4('七月在线','http://www.julyedu.com') #不传关键字参数，函数依旧可以被调用，采用默认值
foo4('七月在线','http://www.julyedu.com',intro='国内领先的AI教育平台')#传关键字参数，覆盖默认值

#传入不定长个位置参数
#位置参数包裹及使用*
def mysum1(a,b,c):
    return a+b+c

print(mysum1(5,7,15))
#mysum1(5,7)  #报错，因为传入的参数少于函数定义时的个数
#mysum1(5,7,15,22)  #报错，因为传入的参数多于函数定义时的个数

#这时需要使用包裹进行接收
def mysum2(*args): # args
    print(type(args))
    return sum(args)

print('mysum2',mysum2(5,7,15))
print('mysum2',mysum2(5,7,15,22,33)) #正常调用
print('mysum2',mysum2(5,7)) #正常调用

#传入不定长关键字参数，也可以使用一个包裹进行接收
#关键字参数包裹及使用**
def filmInfo(**kwargs):  # keyword-args
    print(type(kwargs))
    for key,values in kwargs.items():
        print(key,':',values)

filmInfo(film='羞羞的铁拳',box=3.5)
filmInfo(film='羞羞的铁拳',box=3.5,rate=7.9)
# d1={'羞羞的铁拳':3.5,'box':3.5}

print('\n\n')
#包裹解包顺序
#首先拆位置参数包裹，按顺序给必选，默认，可变。
#再抓给关键字参数包裹
def scoreReport(name,age,*args,course='python',**kwargs):
    print('个人信息:',name,age)
    for item in args:
        print(item)
    print('课程信息:',course)
    print('每节课成绩:')
    for key,value in kwargs.items():
        print (key,value)
        
scoreReport('xiaoming',22,'高中部','三年二班',Lesson1=80,Lesson2=85)
scoreReport('xiaoming',22,'三年二班',course='machine learning',Lesson1=80,Lesson2=85)


def mysum2(*args): # args
    print(type(args))
    return sum(args)
#传递参数时使用包裹-位置参数
l1=[1,5,6,7,2,5,3.5,9,6,3,4]
print(mysum2(*l1))

#zip案例
l1=[(1,3),(2,4)]
print(list(zip(*l1)))


def filmInfo(**kwargs):  # keyword-args
    print(type(kwargs))
    for key,values in kwargs.items():
        print(key,':',values)
##传递参数时使用包裹-关键字型参数
d1={'羞羞的铁拳':3.5,'雷神3':3.1,'战狼2':60}
print(filmInfo(**d1))
```

    公司名： 七月在线 公司网址： http://www.julyedu.com
    公司名： http://www.julyedu.com 公司网址： 七月在线
    公司名： 七月在线 公司网址： http://www.julyedu.com 介绍： 专注AI教育
    公司名： 七月在线 公司网址： http://www.julyedu.com 介绍： 国内领先的AI教育平台
    27
    <class 'tuple'>
    mysum2 27
    <class 'tuple'>
    mysum2 82
    <class 'tuple'>
    mysum2 12
    <class 'dict'>
    film : 羞羞的铁拳
    box : 3.5
    <class 'dict'>
    film : 羞羞的铁拳
    box : 3.5
    rate : 7.9
    
    个人信息: xiaoming 22
    高中部
    三年二班
    课程信息: python
    每节课成绩:
    Lesson1 80
    Lesson2 85
    个人信息: xiaoming 22
    三年二班
    课程信息: machine learning
    每节课成绩:
    Lesson1 80
    Lesson2 85
    <class 'tuple'>
    51.5
    [(1, 2), (3, 4)]
    <class 'dict'>
    羞羞的铁拳 : 3.5
    雷神3 : 3.1
    战狼2 : 60
    None


### 3. 参数传递的处理


```python
#值传递，参数本身不会被修改
a=7
b='julyedu'
print('before reference:',a,b)

def foo1(a,b):
    a+=1
    b+='.com'
    print('In foo1 a,b has changed to',a,b)
    
foo1(a,b)

print('after reference:',a,b)
#结论：值传递时，变量传递给函数后，函数复制一份，不会影响原有变量

print('>'*40)

#指针传递参数，会修改参数本身
l1=[1,2,3.4]
d1={'name':'jack'}
def foo2(a,b):
    a.pop()
    b['age']=22
    
print('before reference:',l1,d1)

foo2(l1,d1)

print('after reference:',l1,d1)
#结论：指针（或引用）传递时，变量传递给函数的是及引用，该引用可以改变原变量
```

    before reference: 7 julyedu
    In foo1 a,b has changed to 8 julyedu.com
    after reference: 7 julyedu
    >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
    before reference: [1, 2, 3.4] {'name': 'jack'}
    after reference: [1, 2] {'name': 'jack', 'age': 22}


### 4. 变量作用域


```python
#全局变量
website='julyedu.com'
companyName='七月在线'
list1=[7,2.5,'julyedu.com']

def getWebsite():
    #既想引用又想修改全局变量？ global
    global website
    website='www.julyedu.com' #并非真正意义修改
    #只是改变了website这个引用，指向到了'www.julyedu.com'
    list1.append('AI教育') #主要这里的全局变量是list型，因此修改是全局性的
    
    print('list1',list1)
    
    #如果想在函数内部引用全局变量呢?直接使用即可
    print('函数内部引用全局变量',website)
    
    #新建局部变量
    #貌似是给全局变量赋值，其实是新建了一个局部变量
    website='julyedu.org'#函数内部与全局同名，即覆盖
    #这个website变量名的生命周期只在该函数被调用时，调用结束，也就结束了。
    print('新建局部变量',website)
    
    #变量搜索顺序，如果要使用的变量名在局部中有，则使用，如果没有则向上一层寻找
    companyName='JulyEdu'
    print(companyName)
    
getWebsite() # 调用函数，开始函数内局部变量的生命周期，函数结束后，它们也就结束了。

#全局变量
print('全局变量',website)
```

    list1 [7, 2.5, 'julyedu.com', 'AI教育']
    函数内部引用全局变量 www.julyedu.com
    新建局部变量 julyedu.org
    JulyEdu
    全局变量 julyedu.org

### 5.偏函数 PFA

偏函数 PFA（Partial function application）

使用场景：如果一个函数的参数很多，而在每次调用的时候有些又经常不需要指定时，就可以使用偏函数。

**语法：** partical(func,*args,**keywords) 

**使用：** from functools import partial

**原理：** 创建一个新函数，**固定住**原函数的部分参数（可以为位置参数，也可以是关键字参数）


```python
#Partial function application(PFA)
# 只设置了一部分的参数的函数
# 固定一部分参数，使得被调用时，某些参数被固定住了。

#例如我们要定义一个函数将传进来的16进制的字符串，转换为10进制的
def hex2int(num):
    return int(str(num),base=16)#base为关键字参数，这个在调用int这个函数时，固定给16。因为这个函数就是用来转换16进制到10进制

print('F -> int',hex2int('F')) #这时调用，相当于实际上会把10作为*args的一部分自动加到左边，也就是：int('F',base=16),这样就少写了一个函数

#这时也可以使用偏函数，固定int函数的关键字参数base，可以这样定义：
import functools
hex2int2=functools.partial(int,base=16)
print('A -> int',hex2int2('A'))

#偏函数能固定位置参数
max100=functools.partial(max,100) #定义一个叫max100的偏函数，将这个偏函数的第一个值固定为100
max100(99) #这时调用它，传入的值，都会与100进行比较反并返回。

print('type',type(max100)) #偏函数的类型与普通函数不一样
```

    F -> int 15
    A -> int 10
    type <class 'functools.partial'>


### 6.递归

**递归的方法求一个列表中数值的累加**


```python
def foo1(num):
    if len(num)==1:
        return num[0]
    else:
        print(num[0],'>'*6)
        print(num[1:],'   >'*6)
        return num[0]+foo1(num[1:])
    
print(foo1([1,2,31,5,6,55]))
```

    1 >>>>>>
    [2, 31, 5, 6, 55]    >   >   >   >   >   >
    2 >>>>>>
    [31, 5, 6, 55]    >   >   >   >   >   >
    31 >>>>>>
    [5, 6, 55]    >   >   >   >   >   >
    5 >>>>>>
    [6, 55]    >   >   >   >   >   >
    6 >>>>>>
    [55]    >   >   >   >   >   >
    100

**使用递归分解质因数**


```python
l1=[]
def fenji(num):
    num=int(num)
    for i in range(2,num):
        if num%i==0:
            l1.append(i)
            nextv=int(num/i)
            fenji(nextv)
            break
    return l1

fenji(60)
```


    [2, 2, 3]

**阶乘**


```python
def factorial(n):
    if n==1:
        return 1
    else:
        return n*factorial(n-1)
factorial(5)
```


    120

### 7.匿名函数 lambda


```python
#匿名函数
print(type(lambda a,b:a*b))
#定义函数体，不写return

#使用1：作为正常函数使用，不推荐
foo=lambda x,y:x+y #不写return
print(foo(1,2))

#使用2：lambda关键字定义在高阶函数的参数位上
d1={'China':15,'India':9,'USA':2,'Japan':1.5}
#按d1.items()第0个元素升序，国家名
print(list(sorted(d1.items(),key=lambda x:(x[0],x[1]))))
#按d1.items()第1个元素升序,人口数
print(list(sorted(d1.items(),key=lambda x:(x[1]))))
```

    <class 'function'>
    3
    [('China', 15), ('India', 9), ('Japan', 1.5), ('USA', 2)]
    [('Japan', 1.5), ('USA', 2), ('India', 9), ('China', 15)]

### 8.高阶函数

**函数的引用于调用**

- 引用：访问，变量别名（多个别名引用）
- 调用：()

函数对象可以被引用，也可以作为参数被传入或作为结果被返回

**高阶函数：**一个函数接收另一个函数作为参数

**回调函数：**函数作为调用函数的结果返回


```python
#函数对象的引用于调用
num=5
a=b=c=abs
#引用
print(abs,a)

#调用
print(a(num))
print(b(-8.8))
print(c(7))

#函数名本质即变量，同一个函数对象可以被多个变量引用
def foo(): #新建一个函数对象，并用foo这个变量名对其进行引用 
    pass

del foo#对函数对象的引用可以删除
# foo() #NameError: name 'foo' is not defined

#高阶函数
def mycalucate(num,func): #将func这个函数作为参数
    return func(num)

l1=[5,8,3,6,9,15,22]

print(mycalucate(l1,max))
print(mycalucate(l1,min))
print(mycalucate(l1,sum))
print(list(mycalucate(l1,reversed)))

#回调函数
def callbackfunc(*num):
    return max(*num)
callbackfunc(53,5,33)
```

    <built-in function abs> <built-in function abs>
    5
    8.8
    7
    22
    3
    68
    [22, 15, 9, 6, 3, 8, 5]
    
    53

### 9.BIFS0高阶函数

**filter:** 对每个元素做过滤

**map:** 对每个函数做映射

**reduce:** 两两转换传给func

Python 3.x 中，reduce() 函数已经从全局名字空间移除，它和 partical() 一样放在 functools 模块中，使用前需要调用。

**匿名函数 lambda:**

- 使用场景：返回简单，不需要专门定义函数
- 特点：简洁，同一行定义体+声明。不用写return
- 定义：定义后，赋值给一个变量，做正常函数使用。lambda 关键字定义在高阶函数参数位上
- 语法：lambda(args1,args2,argsN):expression


```python
l1=[2,3,5,7,3,4,5,9,'julyedu.com',[2,3,3],5,2]

filter
#语法：filter(function,list)
#函数f的作用是对每个元素进行判断，返回true或false，true表示留下，false表示过滤
# filter()根据判断结果自动过滤掉不符合条件的元素，返回由符合条件元素组成的新list。

def myfilter(x):
    if x>60:
        return True
    else:
        return False

print(myfilter(61))

l1=[1,61,62]

print(list(filter(myfilter,l1)))

l2=[1,61,62,'abc']
print(list(filter(lambda x:True if type(x)==str else False,l2)))

#map
# 语法：map(function, list)
#让list的每一个元素依次调用function函数，并获取返回值存入一个新的list中。

print(list(map(lambda x:(x,l1.count(x)),l1)))
```

    True
    [61, 62]
    ['abc']
    [(1, 1), (61, 1), (62, 1)]

### 10.闭包(Closure)

**闭包的概念：**

- 涉及嵌套函数时才有闭包问题
- 内层函数引用了外层函数的变量（参数），然后返回内层函数的情况，称为闭包。
- 这些外层空间中被引用的变量叫做这个函数的环境变量。
- 环境变量和这个非全局函数一起构成了闭包。

**闭包的特点：** 函数会记住外层函数的变量

````python
def foo1(args):
    def foo2():
        pass
    return foo2
````

**闭包的特点：** 函数会记住外层函数的变量


```python
nums_in_global=[15,2,3,9,3.2]#声明一个全局

def foo1(nums_in_function):
    print('nums_in_function此时在是foo1中，可以被访问：',nums_in_function)
    def foo2():
        #虽然没有给foo2传入任何参数，但foo2却能访问到foo1中的变量nums_in_function
        return max(nums_in_function)
        #虽然没有给foo2传入任何参数，但foo2却能访问到全局变量nums_in_global
#         return max(nums_in_global)
    return foo2

print(foo1(nums_in_global)())
# print(nums_in_function)# name 'nums_in_function' is not defined

#调用
print(foo1([5,3,8])())
```

    nums_in_function此时在是foo1中，可以被访问： [15, 2, 3, 9, 3.2]
    15
    nums_in_function此时在是foo1中，可以被访问： [5, 3, 8]
    8

### 11.装饰器

**定义：** 以函数作参数并返回一个替换函数的可执行函数

**简单理解：**

- 装饰器的作用就是为已存在的对象添加额外功能
- 为一个函数增加一个装饰（用另一个函数装饰）
- 本质上就一个返回函数的高阶函数

**应用：** 给函数动态增加功能（函数）


```python
#现有如下 三个函数
def foo1():
    print ('this is foo1 function')

def foo2():
    print ('this is foo2 function')

def foo3():
    print ('this is foo3 function')
    
#现在想为每一个函数都添加一个打印当前时间的功能
#一种解决办法是一个一个修改，在底部添加代码
import datetime
def foo1():
    print ('this is foo1 function')
    print(datetime.datetime.now())

def foo2():
    print ('this is foo2 function')
    print(datetime.datetime.now())
    
def foo3():
    print ('this is foo3 function')
    print(datetime.datetime.now())  
    
#另一种办法是，写一个函数，负责打印时间,然后修改那三个函数
import datetime
def printtime():
    print(datetime.datetime.now())  
    
def foo1():
    print ('this is foo1 function')
    printtime()

def foo2():
    print ('this is foo2 function')
    printtime()
    
def foo3():
    print ('this is foo3 function')
    printtime()
    
foo1()
foo2()
foo3()
#虽然不那么麻烦了，但还是每个函数都要修改，依旧很麻烦。
```

    this is foo1 function
    2018-07-25 15:21:41.910571
    this is foo2 function
    2018-07-25 15:21:41.910703
    this is foo3 function
    2018-07-25 15:21:41.910798

```python
#我们可以这样解决
def foo1():
    print ('this is foo1 function')

def foo2():
    print ('this is foo2 function')

def foo3():
    print ('this is foo3 function')

def extrafoo(func):
    print(datetime.datetime.now())
    return func

decorated=extrafoo(foo2)
decorated()

#这样每次调用还是有点麻烦，要先写一个函数接收，再调用。OK，再弄简单一些
```

    2018-07-25 15:22:39.218693
    this is foo2 function

```python
#我们可以这样解决
import datetime
def extrafoo(func):
    def inner():
        print('from inner to execute:',func.__name__)
        print('the',func.__name__,'result:',func())
        print('extra:',datetime.datetime.now())
    return inner

#@是python装饰器的简便写法，也叫语法糖
#装饰器语法糖在要被包裹的函数前声明。@后面的函数名，是包裹下边函数的函数名extrafoo
#该语法糖省略了
decorated=extrafoo(foo1)
decorated()

print('-----------')

@extrafoo #装饰器特性，被装饰的函数定义之后立即运行。
def foo1():
    return 'this is foo1 function--'

# 装饰器在Python使用如此方便都要归因于
# Python的函数能像普通的对象一样能作为参数传递给其他函数
# 可以被赋值给其他变量，可以作为返回值，可以被定义在另外一个函数内。
foo1()
```

    from inner to execute: inner
    from inner to execute: foo1
    the foo1 result: this is foo1 function--
    extra: 2018-07-25 15:29:42.162464
    the inner result: None
    extra: 2018-07-25 15:29:42.162735
    -----------
    from inner to execute: foo1
    the foo1 result: this is foo1 function--
    extra: 2018-07-25 15:29:42.163103

### 12.练习

定义一个函数，接收任意3个数字的输入，并按顺序从小到大输出


```python
def func(*args):
    print(type(args))
    print(sorted(args))

func(5,2,3)
```

    <class 'tuple'>
    [2, 3, 5]


要求创建一个函数，它可以接收，位置参数，不定长位置参数，不定长关键词参数，并按要求输出 。

 输入班级名，班级特色(如’勤奋’,’颜值高’)等等不同特色，班级不同同学的姓名与年龄。

 要求输出，班级名，班级特色，班级成员，班级成员的平均年龄。


```python
def scoreReport(name,age,*args,course='python',**kwargs):
    print('个人信息:',name,age)
    for item in args:
        print(item)
    print('课程信息:',course)
    print('每节课成绩:')
    for key,value in kwargs.items():
        print (key,value)
        
scoreReport('xiaoming',22,'高中部','三年二班',Lesson1=80,Lesson2=85)

#func(positional_args,keyword_args,*tuple_nonkw_args,**dict_kw_args)：
def func(class_name,*args,**kwargs):
    print('班级名:',class_name)
    print('班级特色')
    for item in args:
        print(item)
    print('学生信息:')
    curSum=0
    for key,value in kwargs.items():
        print(key,value)
        if(type(value)==int):
            curSum+=value
    print(curSum/(len(kwargs.items())/2))
    
func('三年二班','勤奋','颜值高',name='zhangsan',age=20,name1='lisi',age1=22)



```

    个人信息: xiaoming 22
    高中部
    三年二班
    课程信息: python
    每节课成绩:
    Lesson1 80
    Lesson2 85
    班级名: 三年二班
    班级特色
    勤奋
    颜值高
    学生信息:
    name zhangsan
    age 20
    name1 lisi
    age1 22
    21.0


使用reduce函数实现找出一组数字列表中的最大值


```python
from functools import reduce
reduce(lambda x,y:max(x,y),[1,2,3,4,5,6])
```


    6

求1000以内能同时被3和7整除的数有哪些
要求使用map和filter函数

语法：filter(function,list)
函数f的作用是对每个元素进行判断，返回true或false，true表示留下，false表示过滤
filter()根据判断结果自动过滤掉不符合条件的元素，返回由符合条件元素组成的新list。
filter(lambda x:True if type(x)==str else False,l2)


```python
#filter
def func(n):
    if n%21==0:
        return n
    else:
        pass 

print(list(filter(func,range(1001))))

a=list(map(func,range(1001)))
print([i for i in a if i])
```

    [21, 42, 63, 84, 105, 126, 147, 168, 189, 210, 231, 252, 273, 294, 315, 336, 357, 378, 399, 420, 441, 462, 483, 504, 525, 546, 567, 588, 609, 630, 651, 672, 693, 714, 735, 756, 777, 798, 819, 840, 861, 882, 903, 924, 945, 966, 987]
    [21, 42, 63, 84, 105, 126, 147, 168, 189, 210, 231, 252, 273, 294, 315, 336, 357, 378, 399, 420, 441, 462, 483, 504, 525, 546, 567, 588, 609, 630, 651, 672, 693, 714, 735, 756, 777, 798, 819, 840, 861, 882, 903, 924, 945, 966, 987]


体现闭包的思想，创建一个三层嵌套的函数，并调用。


```python
def first(first):
    a=first
    def second(a):
        b=a
        def third(b):
            print('third-->',b)
        print('second-->',a,third(a))
    print('first-->',a,second(a))
    
first('first')
```

    third--> first
    second--> first None
    first--> first None


请以round函数，定义一个偏函数roundN，调用为输入一个数字N，返回圆周率后N位的数字(提示:import math math.pi)
请以sorted函数，定义一个偏函数sortedDESC，结果为输入一个序列，返回为按降序排列后序列


```python
import functools
import math
def roundN(n):
    return round(math.pi,n)
print(roundN(15))

l1=[1,5,6,4,2]
def sortedDESC(l1):
    return sorted(l1,reverse=True)
print(sortedDESC(l1))
```

    3.141592653589793
    [6, 5, 4, 2, 1]

要求使用map与filter函数，输出一个输入字符串里每个字符出现的次数


```python
l1=input()
def myMap(l1):
    return dict(map(lambda x:(x,l1.count(x)),l1))
print(myMap(l1))
```

    dsjkhsdalmvadfs
    {'d': 3, 's': 3, 'j': 1, 'k': 1, 'h': 1, 'a': 2, 'l': 1, 'm': 1, 'v': 1, 'f': 1}


创建一个能够快速排序的递归函数


```python
l1=[3,5,2,6,0,3,1,3,5,7,8,9]
l2=[]
k=0
def my_sort(l1):
    if len(l1)==1:
        l2.append(l1[0])
    else:
        k=l1.index(min(l1))
        l2.append(l1[k])
        l1.pop(k)
        my_sort(l1)
    return l2
my_sort(l1)
```


    [0, 1, 2, 3, 3, 3, 5, 5, 6, 7, 8, 9]

创建一个能打印一个字典中包含所有字典对象的递归函数


```python
def my_dict(d):
    for key,value in d.items():
        print(key)
        if type(value)==dict:
           my_dict(value)
        else:
            print(value)                                                                    
                                                                                
dic={"北京":{"东城": ["天坛", "东单", "王府井"],"西城": ["西单", "军博", "复兴门"],},
     "上海":{"杨浦":['五角场','政通路','世界路']},
    "天津":['天津港']}
my_dict(dic)                                                                                                                                                      
                                                                                
```

    北京
    东城
    ['天坛', '东单', '王府井']
    西城
    ['西单', '军博', '复兴门']
    上海
    杨浦
    ['五角场', '政通路', '世界路']
    天津
    ['天津港']


编写一个生成器，实现fib数列的效果
f(0) = 1,
f(1) = 1,
f(n) = f(n-1) + f(n-2)


```python
def fib(num):
    n,a,b = 0,0,1
    while n<num:
        yield b
        a,b = b,a+b
        n +=1
 
for n in fib(5):
    print(n)
```

    1
    1
    2
    3
    5

创建一个能接收不定长位置参数（数字）函数，返回是所有参数的和。

现要求在这个函数每次调用时都有进行屏幕打印（该函数被调用）。

请在不改动这个函数内部及调用的前提下实现。


```python
def print_name(func):
    def inner(*args,**kwargs):
        return func(*args,**kwargs)
    return inner

@print_name
def summary(*args):
    n=0
    sum=0
    for n in args:
        sum+=n
    return sum

print(summary(1,3,5,6,8,2,4))
```

    29
