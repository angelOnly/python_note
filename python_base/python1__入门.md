
## （一）Python 入门

## Python 中的关键字
#### 常量
```python
True,False,None
```
#### 函数，类，对象和模块
```python
def,class,import,from,del,global,return,lambda
```
#### 判断与循环
```python
if,elif,else,is,in,assert,and,or,not
```
#### 循环
```python
for,while,continue,break,pass
```
#### 异常
```python
with,raise,try,except,finally,as
```

## BIF: Python 的自带电池
#### 查看
```python
dir(__builtins__)
```
#### IO
```python
print(),open(),input()
```
#### 列表与帮助
```python
dir(),help()
```
#### 类型与身份
```python
type(),id(),memoryview(),isinstance(),insubclass()
```
#### 数学运算类
```python
sum,pow,round,min,max,hash
```
#### 类型转换
```python
int,bin,hex,oct,str,float,list,bytes
```
#### 序列
```python
 len(),range(),zip(),map(),reduce(),filter(),
 reversed(),sorted(),enumerate()
```

## 1. Python 中标准操作符


```python
#算术操作符
a=50;b=100

print('a+b=',a+b)
print('a-b=',a-b)
print('a*b=',a*b)
print('a/b=',a/b)
print('a%b=',a%b)
print('a//b=',a//b) #取整
print('a**2=',a**2) #求幂
print('a**0.5=',a*0.5)
```

```python
a+b= 150
a-b= -50
a*b= 5000
a/b= 0.5
a%b= 50
a//b= 0
a**2= 2500
a**0.5= 25.0
```


#### 比较运算符


```python
#比较运算符
a=50;b=100
print('a==b',a==b)
print('a!=b',a!=b)
print('a>b',a>b)
print('a<b',a<b)
```

```python
a==b False
a!=b True
a>b False
a<b True
```


#### 逻辑运算符


```python
#逻辑运算符
a=50;b=100
if a>=50 and b > 60:
    print('a and b both greater than 50')
if a>=50 or b>200:
    print('a or b greater than 50')
```

```python
a and b both greater than 50
a or b greater than 50
```

#### 成员运算符


```python
#成员运算符
website='http://www.julyedu.com'
print('com' in website)
print('com' not in website)
```

```python
True
False
```


#### 身份运算符


```python
#身份运算符
websiteUrl='julyedu'
websiteUrl2='julyedu'
print('websiteUrl is websiteUrl2', websiteUrl is websiteUrl2)
```

```python
websiteUrl is websiteUrl2 True
```


#### 高级赋值


```python
#简单赋值
a=100
print(a)

#多重赋值
a=b=c=100
print(a,b,c)

#多元赋值
a,b,c=99,100,101
print(a,b,c)

#变量交换赋值
a,b,c=b,c,a
print(a,b,c)
```

```python
100
100 100 100
99 100 101
100 101 99
```


## 2. 循环与判断


```python
#for 迭代循环
#左闭右开[3,7)
for i in range(5):
    print('For loop, ',i,' items run')

#while 条件循环
i=0
while i<5:
    print('While loop ',i,' items run')
    i+=1
    
#continue 跳过循环
for i in range(5):
    if i==2:continue
    print('For loop with continue, ',i,' items run')

#break终止循环
i=0
while True:
    print('While loop with break, ',i,' items run')
    i+=1
    if i==5:break

#pass填行
for i in range(5):
    if i==2:
        pass
    else:
        print('For loop with pass, ',i,' items run')
```

```python
For loop,  0  items run
For loop,  1  items run
For loop,  2  items run
For loop,  3  items run
For loop,  4  items run
While loop  0  items run
While loop  1  items run
While loop  2  items run
While loop  3  items run
While loop  4  items run
For loop with continue,  0  items run
For loop with continue,  1  items run
For loop with continue,  3  items run
For loop with continue,  4  items run
While loop with break,  0  items run
While loop with break,  1  items run
While loop with break,  2  items run
While loop with break,  3  items run
While loop with break,  4  items run
For loop with pass,  0  items run
For loop with pass,  1  items run
For loop with pass,  3  items run
For loop with pass,  4  items run
```


#### 判断


```python
age=32
#单if
if age>18:
    print('you are a adult!')

#if else
if age>18:
    print('you are a adult!')
else:
    print('you are a teenager!')
    
#if elif
l1=list('china')
print(l1)

for item in l1:
    if item=='a':
        print('-aaa-')
    elif item=='i':
        print('iiii')
    elif item=='h':
        print('>>>h')
    else:
        print(item)
        
#三元表达符
websiteUrl='julyedu.com'
print('.com域名') if '.com' in websiteUrl else print('其它类型域名')
```

```python
you are a adult!
you are a adult!
['c', 'h', 'i', 'n', 'a']
c
>>>h
iiii
n
-aaa-
.com域名
```


## 3. Python数值类型


```python
#整数类型
a=100;b=200

#进制表示与转化
a=0b0101 #二进制，bin()
b=0o0101 #八进制，oct()
c=0x0101 #十六进制，hex()

#浮点型
a=5.117

#科学计数法
c=5e3
d=73-4

#数字正负无穷
float('inf') #正无穷
float('-inf') #负无穷

1+float('inf')
1+float('-inf')

#数字正负无穷不等式：
# 当涉及 > 和 < 运算时，
# 所有数都比-inf大
# 所有数都比+inf小
#数字正负无穷等式：
# +inf 和 +inf相等  -inf 和 -inf相等
# inf不是nan(not a number)，inf-inf或者-inf+inf是nan。
# inf是∞，一个比其他所有值都大的值。
# inf是-∞，一个比其他所有值都小的值。
print(float('inf')==float('inf'))
print(float('inf')+float('-inf'))

#复数
#complex() 函数用于创建一个值为 real + imag * j 的复数或者转化一个字符串或数为复数。
#如果第一个参数为字符串，则不需要指定第二个参数
#class complex([real[, imag]])
#real -- int, long, float或字符串；
#imag -- int, long, float；
a=5+22j
print(type(a))
print(a.real,a.imag)

#操作
#数值类型转化
a=-5.555
print(int(a))
print(float(a))
print(complex(a))

#绝对值与四舍五入
print(abs(a))
print(round(a,1))
```

```python
True
nan
<class 'complex'>
5.0 22.0
-5
-5.555
(-5.555+0j)
5.555
-5.6
```


## 4. Python字符串类型


```python
#初始化及转义
#单引与双引在表示字符串时没有区别。但字符串开头结尾必须使用同一种引号。否则报错
url='http://www.julyedu.com'
print(url)
url="http://www.julyedu.com"
print(url)

#如果是字符串包含单引号或者双引号，则需要对其转义
sentence='Today\'s news is not a good news'
print(sentence)

#字符串属性
print('len:',len(url))

#访问 属性
for item in url:
    print(item)
    
#访问 索引Indexing
print(url[0])

#访问切片
#[::] 三个参数分别为：开始索引位置，结束索引位置，步长
print(url[7:22:2])

#格式化访问
url='http://www.{}.com'
companyName='julyedu'
print(url.format(companyName)+'中国领先的AI教育平台')
print(url.format(companyName)*3)

#查找与替换
url=url.format(companyName)+'中国领先的AI教育平台'
print(url.find('http'))
print(url.find('平台'))
print(url)
print(url.replace('AI','人工智能'))

#统计
print('t',url.count('t'))
print('平台',url.count('平台'))

#获取索引
print(url.index('台'))

#大小写
print(url.title()) #首字母大写
print(url.upper()) #全部字母大写
print(url.lower()) #全部字母小写

#去空格
url_1='   test lstrip'
print(url_1.lstrip()) #截掉字符串左边的空格或指定字符。
url_2='   test rstrip   '
print(url_2.rstrip()) #截掉字符串右边的空格或指定字符。
url_2='   test rstrip   '
print(url_2.strip()) #截掉字符串左边和右边的空格或指定字符

s='abc'
print('abc isalpha',s.isalpha()) #是否由字母组成
print('abc isdigit',s.isdigit()) #是否由数字组成
print('abc isidentifier',s.isidentifier()) #是否是有效的 Python 标识符，可用来判断变量名是否合法。

#编码与解码
s1=s.encode()
print(type(s1))
print(s1)
s2=s1.decode()
print(type(s2))
print(s2)

```

```python
http://www.julyedu.com
http://www.julyedu.com
Today's news is not a good news
len: 22
h
t
t
p
:
/
/
w
w
w
.
j
u
l
y
e
d
u
.
c
o
m
h
wwjleucm
http://www.julyedu.com中国领先的AI教育平台
http://www.julyedu.comhttp://www.julyedu.comhttp://www.julyedu.com
0
31
http://www.julyedu.com中国领先的AI教育平台
http://www.julyedu.com中国领先的人工智能教育平台
t 2
平台 1
32
Http://Www.Julyedu.Com中国领先的Ai教育平台
HTTP://WWW.JULYEDU.COM中国领先的AI教育平台
http://www.julyedu.com中国领先的ai教育平台
test lstrip
   test rstrip
test rstrip
abc isalpha True
abc isdigit False
abc isidentifier True
<class 'bytes'>
b'abc'
<class 'str'>
abc
```


## 5. 练习题

##### 1. 求从1到100的数字中所有能被3整除的数字的有哪些


```python
for i in range(1,101):
    if i % 15 == 0:
        print(i)
```

```python
15
30
45
60
75
90
```


#### 2. 输入一个字符串返回满足以下条件的字符串
如果字符串长度大等于3，添加 'ing' 到字符串的末尾
如果字符串是以 'ing' 结尾的，就在末尾添加 'ly'
如果字符串长度小于3，返回原字符串


```python
s = input()

if len(s)>3:
    if s.endswith("ing"):
        s += "ly"
    else:
        s += "ing"
else:
    pass

print(s)
```

```python
sding
sdingly
```


#### 3.判断是否为回文
提示：回文：62426是回文数字


```python
s = input()
if s == s[::-1]:
    print("True")
else:
    print("False")
```

```python
abcba
True
```


#### 4. 输入一个字符串，返回满足以下条件字符串
找到字符串中的子串 'not' 和 'bad’
如果 'bad' 出现在 'not' 后面，就把 'not' ... 'bad' 之间包含的所有字符串替换成 'good'


```python
a = 'Study is not only to learn, actually i think this is a bad way. '
if a.find("bad") > a.find("not"):
    b = a[0:a.find("not")+3] + " good " + a[a.find("bad"):]
print(b)
```

```python
Study is not good bad way. 
```


#### 5. 输入一个字符串，把字符串拆分成两个等分
如果字符串长度是偶数，前一半和后一半的长度是相同的
如果字符串长度是奇数，则多出的一个字符加到前一半，如：'abcde'，前一半是'abc'，后一半是'de'


```python
s = input()
idx = len(s)//2
print(int(a))
if len(s)/2 == 0:
    c = s[0:idx]
    d = s[idx:]
else:
    c = s[0:idx+1]
    d = s[idx+1:]
print(c)
print(d)
```

```python
abcde
2
abc
de
```


#### 6.输入一个字符串返回满足以下条件的字符串
找出与字符串的第一个字母相同的字母，把它们替换成 '*'，除了第一个字母本身以外
例如: 输入'babble'， 返回 'ba**le'


```python

s = input()
first = s[0]
a = first + s[1:].replace(first,"*")
print(a)
```

```python
iliviwhdkoi
il*v*whdko*
```


#### 7. 输入一个字符串 返回满足以下条件的字符串
由字符串的最前面两个字母和最后两个字母组成的字符串。
例如： 'spring' 返回 'spng'， 'is' 返回 'is’
当输入的字符串长度小于2时，返回空字符串


```python
s = input()
if len(s) > 2:
    a = s[0:2] + s[-2:]
elif len(s) == 2:
    a = s
else:
    a = ""
print(a)
```

```python
jik
jiik
```


#### 8. 输入字符串 a 和 b,返回添加以下条件的字符串
交换两个字符串的最前面的两个字母
使用空格把两个字符串分隔后合并成一个字符串
字符串 a 和 b 的长度都大等于 2


```python
a = input()
b = input()
if len(a)>2 and len(b)>2:
    c = b[0:2] + a[2:]
    d = a[0:2] + b[2:]
    e = a + " " + b
else:
    pass
print(c)
print(d)
print(e)
```

```python
qqwwgajkd
fbjsfndd
fbwwgajkd
qqjsfndd
qqwwgajkd fbjsfndd
```


#### 9. 落球计算
一球从100米高度自由落下，假设每次落地后反跳回原高度的一半；再落下，再弹起。请问第6次落地后会弹起多少米？
使用for与while循环完成


```python
s = 100
i = 1
while True:
    s /= 2
    i += 1
    if i > 6:
        break
print(s)

for i in range(1,7):
    s /= 2
    if i <= 6:
        continue
print(s)
```

```python
1.5625
```


#### 10. 求两个数字之间的素数
素数：只能被1及自己整除的数，如3，7，13，23等


```python
a = input()
b = input()
for i in range(int(a), int(b)):
    for j in range(2, i+1):
        if i % j == 0 and j < i:
            print(i,"非素数")
            break
        elif i == j:
            print(i, "素数")
```

```python
1
34
2 素数
3 素数
5 素数
7 素数
11 素数
13 素数
17 素数
19 素数
23 素数
29 素数
31 素数
```

