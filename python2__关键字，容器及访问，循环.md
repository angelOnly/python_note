
# （二）容器及使用

## 1. Python中的序列    

### 序列对象：str，list，tuple

##### Tuple 
    用小括号或无括号命名
    Tuple 是只读有序序列。它的许多操作和 List 很接近。
    当 Tuple 中的元素是不可变对象时，不可修改，比如基本数据类型，不可变对象 Number，String 等。
    当 Tuple 中元素是可变对象时，可进行修改。
##### List
    用中括号命名。


```python
#初始化
s1='julyedu.com '
l1=['julyedu','AI教育']
l2=['.com','平台']
l3=[5,12,6,3,8,9]
l4=['tensorflow','sklearn','']
l5=['','','','']
t1=('julyedu',['国内领先的人工智能平台','AI'])

#标准操作
#成员操作
print('julyedu' in t1)
print('com' not in s1)

#连接与重复(共类型之间)
s1*10
s1+s1
l1*5

#索引访问
print(s1[0])
print(l1[0])
print(t1[1])

#切片访问
print(s1[0:-1:3])
print(t1[0:-1])

#其它操作
print('len',len(t1))
print('reversed',list(reversed(t1)))
print('sorted',sorted(s1))
print('sorted',sorted(l1))
print('sorted',sorted(l3))
print('max',max(l3))
print('min',min(l3))
print('sum',sum(l3))

#枚举
for i,item in enumerate(l1):
    print(i,item)
    
#序列拼接
print(list(zip(l1,t1)))
print(list(zip(l1,l2)))

#any判断对象是否为空对象，如果都为空、0、false，则返回false，如果不都为空、0、false，则返回true
any(l4)#l4中有空元素，但也有不为空的元素
any(l5)#l5中的元素全部为空，0或者false,any返回的就是false

#all判断对象中的所有元素不为0、''、False或者x为空对象，则返回True，否则返回False
all(l4)#l4中有一个空元素，则返回False
all(l3)#l5中的元素全部为空，0或者false,any返回的就是false

#类型转换
print(type(list(t1)))
print(type(str(l1)))
print(type(tuple(s1)))
```

```python
True
False
j
julyedu
['国内领先的人工智能平台', 'AI']
jyuo
('julyedu',)
len 2
reversed [['国内领先的人工智能平台', 'AI'], 'julyedu']
sorted [' ', '.', 'c', 'd', 'e', 'j', 'l', 'm', 'o', 'u', 'u', 'y']
sorted ['AI教育', 'julyedu']
sorted [3, 5, 6, 8, 9, 12]
max 12
min 3
sum 43
0 julyedu
1 AI教育
[('julyedu', 'julyedu'), ('AI教育', ['国内领先的人工智能平台', 'AI'])]
[('julyedu', '.com'), ('AI教育', '平台')]
<class 'list'>
<class 'str'>
<class 'tuple'>
```


### 列表 List


```python
#初始化
l1=['julyedu.com','AI','tensorflow','','sklearn','AI']
l2=list(range(1,6))
l3=list(range(1,18,2))

#列表长度
print(len(l1))

#成员操作
print('AI' in l1)
print('tensor' not in l1)

#列表访问，索引与切片
print(l1[2])
print(l1[0:-1:2])

#列表内部操作
l1[3]='Caffe' #赋值
l1.append(l2) #追加到末尾，如果元素是列表，也是按列表追加进来
l1.extend(['Torch']) #扩展，如果扩展元素是列表，是只添加列表内的元素
l1.insert(0,'sklearn') #指定位置插入
l1.index('sklearn') #获取指定位置元素的索引位置，如果存在相同的元素，返回从右到左的第一个元素
l1.count('AI') #计数
l1.pop() #返回并弹出
l1.pop(3) #返回并弹出指定位置的元素

print(l1)
del l1[-1]
print('del',l1) #删除列表元素，按索引位置删除
l1.remove('AI')
print('remove',l1) #指定元素删除，如果存在相同元素，则删除从左到右第一个元素

#列表操作
print('reversed',list(reversed(l1)))
print('sorted',list(sorted(l1)))

```

```python
6
True
True
tensorflow
['julyedu.com', 'tensorflow', 'sklearn']
['sklearn', 'julyedu.com', 'AI', 'Caffe', 'sklearn', 'AI', [1, 2, 3, 4, 5]]
del ['sklearn', 'julyedu.com', 'AI', 'Caffe', 'sklearn', 'AI']
remove ['sklearn', 'julyedu.com', 'Caffe', 'sklearn', 'AI']
reversed ['AI', 'sklearn', 'Caffe', 'julyedu.com', 'sklearn']
sorted ['AI', 'Caffe', 'julyedu.com', 'sklearn', 'sklearn']
```


### 列表推导式
定义:
列表推导式也叫列表解析式(list comprehension)， 是利用现有列表创建新列表。
□ 这种可以非常简洁的方式来快速生成满足特定需求的列表，代码可读性强。
□ Python 的内部实现对列表推导式做了大量优化，可以保证很快的运行速度。

语法:
□ [表达式for变量in列表]
□ [表达式for变量in列表if条件]


```python
l1=list(range(300))

print([x for x in l1 if x>=288])

#从一个列表中
print([i for i in range(9) if i%2==0])

#从两个列表中进行推导
print([(i,j) for i in range(5) for j in range(5)])
```

```python
[288, 289, 290, 291, 292, 293, 294, 295, 296, 297, 298, 299]
[0, 2, 4, 6, 8]
[(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 0), (1, 1), (1, 2), (1, 3), (1, 4), (2, 0), (2, 1), (2, 2), (2, 3), (2, 4), (3, 0), (3, 1), (3, 2), (3, 3), (3, 4), (4, 0), (4, 1), (4, 2), (4, 3), (4, 4)]
```


### 元组 Tuple


```python
#可认为是一个只读列表

#tuple成员操作
t1=(5,6,7)
#print(t1+4) #报错  TypeError: can only concatenate tuple (not "int") to tuple
#通常我们在命令行输入4,5,6返回的是一个tuple
#而只输入4时，返回的是一个数值型
t1+(4,) #(4,)属于一个元组，元组之间可以进行添加

#解包unpack
# a,b,c,d=t1
t1=(1,2,3,[4,5,6])
# print(t1) #ValueError: not enough values to unpack (expected 4, got 3)

# t1[0]=0 #TypeError: 'tuple' object does not support item assignment

#列表可修改
print('t1 id:',id(t1))
print('t1[-1] id：',id(t1[-1]))

t1[-1].append(7)
print(t1) #(1, 2, 3, [4, 5, 6, 7])
print('t1[-1] id：',id(t1[-1])) # t1[-1] id： 4481289608
```

```python
t1 id: 4481313592
t1[-1] id： 4481289608
(1, 2, 3, [4, 5, 6, 7])
t1[-1] id： 4481289608
```


### 集合Set
一组 key 的无序排列集合，因此无法用索引及切片访问。
主要作用:
□ 用于去重及集合间操作


```python
l1=['julyedu','julyedu.com','julyedu','AI']
l2=['Caffe','julyedu','apple','AI']

#初始化
a=set(l1)
b=set(l2)

# a[0] #TypeError: 'set' object does not support indexing

#成员操作
print('AI' in a)
print('Caffe' not in b)

#内部操作
a.add('f') #添加key
print(a)
a.remove('AI')
print(a)

# & 交集
print(a&b)

# | 并集
print(a|b)

# - 差集
print(a-b)

#集合合并
print(a.update(b))
```

```python
True
False
{'AI', 'f', 'julyedu.com', 'julyedu'}
{'f', 'julyedu.com', 'julyedu'}
{'julyedu'}
{'AI', 'Caffe', 'f', 'apple', 'julyedu.com', 'julyedu'}
{'f', 'julyedu.com'}
None
```


### 字典 Dictionary


```python
#K：V对应

#初始化
d1={'name':'jack','age':24}
d2=dict({'salary':9999,'level':5})

#成员判断（针对key）
print('name' in d1)
print('address' in d1)

#新增成员
d1['address']='beijing'
print(d1)

#访问：按key访问value
print(d1['name'])
print(d1.get('name',-1))
#访问所有key
print(d1.keys())
#访问所有value
print(d1.values())
#访问所有元素
print(d1.items())

#删除成员
d1.pop('address') #返回指定key的值并弹出
print(d1)
d1.popitem() #返回整个元素并弹出
print(d1)

#清空
d1.clear()
print(d1)

#key值的选取，能被hash的值都可以作为key，即不可变类型可以作为key值
print(hash('a'))
```

```python
True
False
{'name': 'jack', 'age': 24, 'address': 'beijing'}
jack
jack
dict_keys(['name', 'age', 'address'])
dict_values(['jack', 24, 'beijing'])
dict_items([('name', 'jack'), ('age', 24), ('address', 'beijing')])
{'name': 'jack', 'age': 24}
{'name': 'jack'}
{}
-3208227752651135475
```


## 2. Python内存管理


```python
#引用概念
a='julyedu' #python在内存中创建了一个字符串，然后创建了a这个变量去指向这个字符串
b=a #创建了一个变量b，并把它引向变量a指向的字符串julyedu

a='AI' #这时在内存中创建了一个字符串AI，并把变量a的指向重新指向AI这个字符串
print(a)
print(b) #b的指向并没有变，还是 julyedu
print('a id == b id',id(a)==id(b))

c=a #再创建一个变量c，指向a所指向的字符串AI
del a #删除的是b这个引用，而非AI这个字符串,所以c这个变量指向的还是AI这个字符串
print(c)

del c #这时AI字符串的最后一个引用c也被删除了,我们就无法再去访问AI这个字符串了
# print(c) #NameError: name 'c' is not defined

#在Python中，每个对象都有存有指向该对象的引用总数，即引用计数 (reference count)。
#我们可以使用 sys 包中的 getrefcount()，来查看某个对象的引用计数。
#需要注意的是，当使用某个引用作为参数，传递给 getrefcount() 时，参数实际上创建了一个临时的引用。
#因此，getrefcount() 所得到的结果，会比期望的多 1。

from sys import getrefcount
a=[1,2,3]
print(getrefcount(a))

b=a
print(getrefcount(a))
```

```python
AI
julyedu
a id == b id False
AI
2
3
```


### 可变与不可变对象


```python
#知识点：引用与对象分离

a=b=c=5 #创建了三个变量，均指向一个int类型的对象5，一个对象可以被多个引用指向
del c #删除c这个变量对5的引用
print(a,b)
# print(a,b,c) #NameError: name 'c' is not defined
a=[1,2,3] #把a这个变量的指向，重新指向了一个列表对象，引用可以随时指向一个新的对象
print(a,b) #b依旧指向5，5没有被改变

#什么是可变对象？
a=b=c=[1,2,3]
print(a,b,c)
a.append(4) #通过a能真正改变列表[1,2,3],
print(a,b,c) #通过引用其元素，改变对象自身

#什么是不可变对象？
a=b=c='beijing'
a='shanghai'
#打印a,b,c,d指向对象的id，看看是否是一个家伙
print('id(a):',id(a),'id(b):',id(b),'id(c):',id(c))
#看似是把a变量指向的字符串从beijing，改为shanghai,但其它并没有改变beijing，只是a的指向被改变了
print(a,b,c)
#不能改变对象本身，只能改变引用的指向
```

```python
5 5
[1, 2, 3] 5
[1, 2, 3] [1, 2, 3] [1, 2, 3]
[1, 2, 3, 4] [1, 2, 3, 4] [1, 2, 3, 4]
id(a): 4481480048 id(b): 4481261384 id(c): 4481261384
shanghai beijing beijing
```


## 3. 练习

#### 1.使用列表推导式找出单词长度大于n的单词


```python
l1=['julyedu.com','AI','tensorflow','','sklearn','AI','com']
print([x for x in l1 if len(x)>3])
```

```python
['julyedu.com', 'tensorflow', 'sklearn']
```


#### 2. 使用列表推导式寻找两个列表中的相同元素


```python
l1=['tensorflow','sklearn','AI']
l2=['python','sklearn','AI']
print([(x,y) for x in l1 for y in l2 if x==y])
```

```python
[('sklearn', 'sklearn'), ('AI', 'AI')]
```


#### 3.去除一个列表中相邻且重复的元素。


```python
l1=['tensorflow','sklearn','AI','AI','sklearn']
print(list(set(l1)))
```

```python
['tensorflow', 'AI', 'sklearn']
```


#### 4.用户名密码对应
给定两个列表，一个存放用户名，一个存放密码。请将用户名和密码按顺序进行对应为一个元素。


```python
d1={'u1','u2','u3'}
d2={'p1','p2','p3'}
print(list(zip(d1,d2)))
```

```python
[('u3', 'p3'), ('u1', 'p2'), ('u2', 'p1')]
```


#### 5. 使用列表推导式计算笛卡尔积（组合）
词频统计
利用dict统计词频
对每个参数进行判断，若在则对应的value+1
否则根据该字符创建一个key并且value设置为1
最后输出该词典


```python
l1=['sklearn','AI','julyedu.com','Caffe','AI','sklearn']
base={}.fromkeys(l1,0)
for item in l1:
    base[item]+=1
print(base)
```

```python
{'sklearn': 2, 'AI': 2, 'julyedu.com': 1, 'Caffe': 1}
```

#### 6. 实现行列互转

**解法一**


```python
import numpy as np
arr= [[1, 2, 3], [4, 5, 6], [7,8, 9], [10, 11, 12]]
np.array(arr).T.tolist()
```


    [[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12]]

**解法二**


```python
arr= [[1, 2, 3], [4, 5, 6], [7,8, 9], [10, 11, 12]]
print(list(zip(arr[0],arr[1],arr[2],arr[3])))
```

```python
[(1, 4, 7, 10), (2, 5, 8, 11), (3, 6, 9, 12)]
```


#### 7.实现求指定长度的Fibonacci数列
Fib数组初始为[0,1]
分别要求使用循环和数组实现
F0 = 0     (n=0)
F1 = 1    (n=1)
Fn = F[n-1]+ F[n-2] (n=>2)

**解法一**


```python
def fibonacci(n):
    fib=[0,1]
    a=fib[0]
    b=fib[1]
    i=2
    while i<n:
        temp=a
        a=b
        b=a+temp
        fib.append(b)
        i+=1
    return fib

fibonacci(10)
```


    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

**解法二**


```python
import numpy as np
def fibonacci2(n):
    fib=[0,1]
    a=np.zeros(n)
    a[0]=fib[0]
    a[1]=fib[1]
    for i in range(2,n):
        a[i]=a[i-1]+a[i-2]
        fib.append(int(a[i]))
    return fib

fibonacci2(10)
```


    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

#### 8. [ ]对应检查
输入含有[]的字符串，输出对中括号出现规则的检测结果
[] OK ][ NOT OK

[][] OK ][][ NOT OK

[[][]] OK []][[] NOT OK

[[][[]]] OK ][]][[][ NOT OK


```python
s=input()
dictbase={'[':0,']':0}
if s.count('[')!=s.count(']'):
    print("'[' and ']'have different number")
else:
    for i in s:
        if i=='[':
            dictbase['[']+=1
        elif (i==']') and (dictbase[']']<dictbase['[']):
            dictbase[']']+=1
        else:
            pass
        
if (dictbase['[']==dictbase[']']) and (dictbase['[']!=0):
    print('OK')
elif dictbase['[']!=0:
    print('NOT OK')
else:
    pass
```

    []][[]
    NOT OK

