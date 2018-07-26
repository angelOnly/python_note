
## （四）面向对象

### 一切皆对象
关于类与对象的BIFs
type() 返回对象类型
id()，memoryview(),查看对象id和内存地址
dir()，查看对象下变量及函数
issubclass(),isinstance()子类,实例操作
hasattr(),getattr(),setattr(),delattr()对象属性操作
globals(),locals()，全局与局部的名称空间
import(),reload()，模块的导入与重载

- 面向过程：根据业务逻辑从上到下写垒代码
- 函数式：将某功能代码封装到函数中，日后便无需重复编写，仅调用函数即可
- 面向对象：对函数进行分类和封装，让开发“更快更好更强…”
<li>
- 面向过程编程容易理解，其往往用一长段代码来实现指定功能。
- 函数是对面向过程的一次封装
- 面向对象是更高一层的封装
  
#### 类与对象的关系
- 类：从近似的对象中抽象出类
- 对象：然后再从类出实例化出对象

#### 类class
类是对一类事物的抽象。比如汽车，门，猫。

Python中, 类(class)的变量是所有对象共享使用, 只有一个拷贝, 所有对象修改, 都可以被其他对象所见;
对象(object)的变量由类的每个对象所拥有,每个对象都包含自己的一份拷贝, 不会影响其他对象;

之前学习的都是Python自带的数据类型，class则是我们自己定义的类型。

#### 对象object
某类事物中的一个具体的实例，对应类。如果我家的那辆汽车，张伟办公室的大门，隔壁丽丽家的那只小花猫。
#### 类与对象的关系
类就像是对象的模板，可以批量生产出许多的对象。
好比a这个变量其实是整形数字int类的一个实例
那int这个类还可以’复刻’出许许多多的整形对象。
这些对象共有的特征就是：整数性。

### 1. 类的创建与对象的初始化

**完成一个学生类的设计**
要求能查看总学生人数，全部学生姓名，毕业分数标准1000，已经毕业学员数量。
实现考试方法，成绩分数如果大于60分代表其通过考试，分数计入该学员总分。
如果该学员累计分数达到1000分，该学员即毕业
实现查分方法，向该学员返回是否已经毕业，或者还差多少分数才能毕业
实现查询所有已毕业学生数量的功能
实现查询所有学生数量的功能
实现查询所有学生姓名的功能


```python
class Student:
    student_total=0 #总学生数
    pass_score=1000 #毕业总分
    student_graduated=0 #毕业人数
    student_list=[]
    
    def __init__(self,name,age,gender):
        self.__name=name
        self.__age=age
        self.__gender=gender
        self.__score=0
        
        Student.student_total+=1
        Student.student_list.append(self.__name)
        
    def exam(self,score):
        if score<60:
            print(self.__name+',sorry, you are faild this time, better luck next time')
        else:
            self.__score+=score
            str1=self.__name+',Good!Your score is '+str(self.__score)+' now'
            
            if self.__score>=Student.pass_score:
                Student.student_graduated+=1
            return str1
        
    def check(self):
        if self.__score<Student.pass_score:
            return self.__name+',You have '+str(Student.pass_score-self.__score)+' scores to archive!'
        else:
            return self.__name+',You have graduated from julyedu.com'
             
    @classmethod
    def get_student_graduated(cls):
        return Student.student_graduated
    
    @staticmethod
    def static1():
        return 'this is a static method from Student,it can be called by both the instance and class'
    
 
david=Student('david',22,'female')
david.exam(60)    
david.exam(100)
david.exam(900)
print(david.get_student_graduated())
print(david.check())

xiaoming=Student('xiaoming',22,'female')
xiaoming.exam(60)    
xiaoming.exam(100)
print(david.get_student_graduated())
print(xiaoming.check())   
```

    1
    david,You have graduated from julyedu.com
    1
    xiaoming,You have 840 scores to archive!


### 2. 类的内部结构
##### 数据成员
- 类变量：在类中且在函数体外，实例之间共享
- 实例变量：定义在方法中，作用于当前实例的类
##### 方法成员
- 类方法：定义时需要使用@classmethod装饰器，第一个参数为cls
- 实例方法：绑定到实例的方法，第一个参数为self
- 静态方法[普通方法]：
    定义的时候使用@staticmethod装饰器
    静态方法没有参数限制，不需要实例参数self和类参数cls
    静态方法可以通过类名访问，也可以通过实例方法访问
**cls**
cls是指向类的指针，在类方法中第一个形参要命名为cls.

**self**
self是指向每个独立对象的指针.在实例方法中第一个形参被命名为self,以区别其它函数。

### 3. 类的继承和多态


```python
class person():
    def speak(self,):
        return 'people can speak language!'
    def work(self,):
        print('people should have work to do!')

class fireMan(person):
    def work(self,):
        print('A great work that can save people!')
    def speak2(self,):
        print(super().speak(),'FireMan needs to speak loudly!')

class employee(person):
    def work(self,):
        print('To gain profits for the company is our job!')
        
fireman1=fireMan()
fireman1.work()#多态
fireman1.speak2()#super方法调用父类

employee1=employee()
employee1.work()
```

    A great work that can save people!
    people can speak language! FireMan needs to speak loudly!
    To gain profits for the company is our job!

```python
# 多态的概念是应用于Java和C#这一类强类型语言中，
# Python是弱类型语言，Python崇尚“鸭子类型”
# 在Python世界中,一切都是对象

class A:
    def bar(self):
        print ('A.bar')
class B(A):#继承自A
    def car(self):
        print ('B.car')

#和A,B类型不相关的类C
class C():
    def sar(self):
        print ('C.sar')
    def car(self):
        print('C.car')

def fun1(obj):#接收一个参数obj
    obj.car()#调用该参数下的car()方法。而不关心obj到底是什么类型~

b1=B()
c1=C()

fun1(b1)#一切皆对象，不care是什么class
fun1(c1) #一切皆对象，不care是什么class
```

### 4. OOP三大特性总结
##### 封装
封装就是将抽象的数据（变量）和行为（函数）打包，形成一个逻辑上的整体（即类）；
封装可以增强安全性（数据）并简化编程（函数），用户只能通过类对外接口的访问权限来使用类的成员。

##### 继承
一个类可以以 class newclsname():来开始全新构造（实际上会默认继承自object）；
也可以从某个已经存在的类继承。继承的类叫做subclass。
比如要构造蜘蛛这个类，可以从昆虫这个类继承。构建学生,雇员,战士都可以从人这个类继承。

##### 多态
因为类具有继承关系，子类可以向上转型被看做是父类的类型，比如无论是战士还是快递员，都是人类。
也因为有了继承关系，子类可以继承父类的所有方法和属性，
当然也可以重载父类的成员函数及属性。例如，当子类（直升机）和父类（飞机）都存在相同的fly()方法时，
子类的fly()覆盖了父类的fly()，在运行时就总是会调用子类的fly()。这就是继承带来的多态。

### 5.访问控制
Python没有像其它语言有访问控制关键字，例如private，protected等，python通过命名约定来实现访问控制。
- 对模块级的控制，通过在标识符前加单下划线_实现
- 对类内部的属性和方法，通过在标识符钱加双下划线__来实现
    类中的两个双下划线包裹的属性或方法为特殊方法
    
### 6.魔术方法
##### 构造和初始化魔术
每个人都知道一个最基本的魔术方法， __init__ 。
通过此方法我们可以定义一个对象的初始操作。
然而，当我调用 x = SomeClass() 的时候， __init__ 并不是第一个被调用的方法。
实际上，还有一个叫做 __new__ 的方法，来构造这个实例。
然后给在开始创建时候的初始化函数来传递参数。
在对象生命周期的结束时，也有一个 __del__ 方法。


```python
class myclass():
    def __init__(self):
        print('被__init__')

    def __del__(self):
        print('我被__del__了，再见')        

c1=myclass()
del c1
```

    被__init__
    我被__del__了，再见


#### 比较魔法
python对实现对象的比较，使用魔法进行大的逆转，使他们非常直观而不是笨拙的方法调用。而且还提供了一种方法可以重写python对对象比较的默认行为（通过引用），一下是这些方法和他们的作用。
**__ cmp __ (self),other**
__ cmp __ 是最基本的用于比较的魔法方法。
它实际上实现了所有的比较符号(<,==,!=,etc)
但是它的表现并不会总是如你所愿（比如，当一个实例相等是通过一个规则来判断，而一个实例大于另一个实例是通过另外一个规则来判断）。
- self<other return 负数
- self==other return 0
- self>other return正数
通常最好的一种方式是去分别定义每一个比较符号而不是一次性将他们定义。
但是 __ cmp __ 方法是你想要实现所有的比较符号而一个保持清楚明白的一个好方法。
- __ eq __ (self, other) == 
- __ ne __ (self, other) != 
- __ lt __ (self, other) < 
- __ gt __ (self, other) >= 


```python
class comp():
    def __init__(self,num):
        self.__num=num
        print('被__init__')
        
    def __del__(self):
        print('被__del__')   
        
    def __eq__(self,other):
        if type(other)==int:
            return True if self.__num>other else False
        else:
            print('can\'t compare with other datatype except int',)
            
            
c=comp(3)
print(c.__eq__(1))
print(c=='china')
```

    被__init__
    被__del__
    True
    can't compare with other datatype except int
    None


#### 数值处理魔法


```python
__pos__(self) 实现正号的特性(比如 +some_object)
__neg__(self) 实现负号的特性(比如 -some_object)
__abs__(self) 实现内置 abs() 函数的特性。
__invert__(self) 实现 ~ 符号的特性。
__add__(self, other) 实现加法。
__sub__(self, other) 实现减法。 
__mul__(self, other) 实现乘法。
__floordiv__(self, other) 实现 // 符号实现的整数除法。
__div__(self, other) 实现 / 符号实现的除法。
__truediv__(self, other) 实现真除法。
__iadd__(self, other) 实现赋值加法+=

__str__(self) 定义当 str() 调用的时候的返回值
__repr__(self) 定义 repr() 被调用的时候的返回值。
__hash__(self) 定义当 hash() 调用的时候的返回值，它返回一个整型
```


```python
class comp():
    def __init__(self,num):
        self__num=num
        print('被__init__')
        
    def __pos__(self):
        self.__num=0
        print(self.__num)
        
c=comp(-3)
c.__pos__()
```

    被__init__
    0


#### 类表现魔法
一个模块的__name__的值取决于你如何应用模块。如果import一个模块，那么模块__name__的值通常为模块文件名，不带路径或者文件的扩展名。
但你也可以像一个标准的程序一样运行模块
在这种情况下，__name__的值将是一个特别缺省 __ main __ 。上述类中加上 
__ name __ == '__ main __' 的判断语句，可以直接在终端环境下执行 python dirfile.py /tmp 进行测试，不必非得在交互式环境下导入模块进行测试。


```python
class myClss():
    #表示类的描述信息，重写代表自定义描述
    __doc__='this is myClass document'
    #模块是对象，并且所有的模块都有一个内置属性 __name__
    __name__='moduel name is V'
    
    def __init__(self):
        pass
    
    def __str__():
        return 'str'
    
    def __repr__():
        return 'repr'
    
    def __hash__():
        return 7
```

#### 容器魔法
_xx:protected
__ xx:private
__ xx __ :类自己调用，子类也不行


```python
class functionalList():
    
    def __init__(self,values=None):
        if values is None:
            self.__values=[]
        else:
            self.__values=values
    
    def __getitem__(self,key):
        if type(key)==slice:#如果传入的key是一个slice类，则这是一个切片方法
            start=key.start
            stop=key.stop+1
            if key.stop==None:
                stop=-1
            if key.start==None:
                start=0
            return self.__values[start:stop]
        else:
            return str(self.__values[key]) #故意多输出2次
        
    def __setitem__(self,key,value):
        self.__values[key]=str(value)+'haha' 
        
    def delitem__(self,key):
        pass
        #del self.__values[key] #故意不删
        
    def iter__(self):
        return iter(self.__values)
    
    def __reversed__(self):
        return reversed(self.__values)
            
    def __append__(self,value):
        self.__values.append(value)
        
    def __len__(self):
        print('__len__')
        return len(self.__values)
    
l1=list(range(10))
o1=functionalList(l1)
len(o1)

o1.__setitem__(1,1)
o1.__setitem__(2,2)
o1.__setitem__(3,3)
o1.__setitem__(4,4)
o1.__setitem__(5,5)
o1.__setitem__(6,6)
o1.__setitem__(7,7)
o1.__setitem__(8,8)
o1.__setitem__(9,9)
print(o1.__getitem__(1))

o1[0:9]
```

    __len__
    1haha
    [0,
     '1haha',
     '2haha',
     '3haha',
     '4haha',
     '5haha',
     '6haha',
     '7haha',
     '8haha',
     '9haha']

### 7. 反射
你可以通过魔术方法控制控制使用 isinstance() 和 issubclass() 内置方法的反射行为。
这些魔术方法是:
- __ instancecheck __ (self, instance)：检查一个实例是不是你定义的类的实例
- __ subclasscheck __ (self, subclass)：检查一个类是不是你定义的类的子类

### 8. 调用
可以调用的对象
Python中，方法也是一种的对象。这意味着他们也可以被传递到方法中就像其他对象一样。
__ call __ 可以让类的实例的行为表现的像函数一样被调用
将一个函数当做一个参数传到另外一个函数中等等。这是一个非常强大的特性让Python编程更加舒适甜美。 

魔法函数 __ call __ (self, [args...])
__ call __ 允许一个类的实例像函数一样被调用。
实质上说，这意味着 x() 与 x.__ call __ () 是相同的。
注意 __ call __ 参数可变。这意味着你可以定义 __ call __ 为其他你想要的函数，无论有多少个参数。



```python
class callableInstance():
    def __init__(self,x,y):
        self.x,self.y=x,y
        
    def __call__(self):
        self.x,self.y=self.y,self.x
        
c=callableInstance(1,5)
print(c.x,c.y)
c()
print(c.x,c.y)
```

    1 5
    5 1


### 9. 模块与包
##### 模块定义
一个.py文件
包含了对象定义与语句
##### 模块作用
用来从逻辑上组织代码
##### 模块使用
- 搜索路径（标准模块，自定义与第三方模块）路径
    搜索路径设置（修改sys.path.append()），设置环境变量
- 导入方法
    import test #作为模块空间导入
    from ** import * #指定模块下具体的类，对象导入，并入当前空间
    from ** * import * ** #将模块下所有对象导入，并入当前空间
    
#### 包 package
##### 包定义
- 含有 __ init __ .py文件间被称为包， __ init __ .py文件用于标识当前文件夹是一个包
- 包用于组织模块，通常把相近的模块进行再次封装成为包
#### 包的目录结构
- 模块
- 子包
    子包下的子包
##### 包的安装，导入与访问
- 包的安装(pip,conda)
- 不同的导入方式(假设包名为test)
    import test #导入 __ init __ .py这个moduel
    
    from test import * #导入 __ init __ .py这个魔都了下所有对象导入到当前空间
    
    from test.test_level1.test_level2 import test_level2 #导入的层次目录下的模块

### 10.练习

##### 创建一个名为phone的类
- 1）类实例成员变量有screeen_size、price、brand
- 2）给成员变量创建访问及设置方法
- 3）定义play方法，功能为打印：play game
- 4）定义sendMessage方法，功能为打印：text message
- 5）定义powerOff方法，功能为打印：power off
- 6）创建get_info方法，打印对象的相关信息
- 7）实例化类phone()，对象名为phone1, 屏幕尺寸为5.5,价格为6288,品牌为apple
- 8）调用3，4，5，6方法，查看结果
- 9）实例化类phone()，对象名为phone2, 屏幕尺寸为5,价格为1999,品牌为mi.
- 10）调用3，4，5，6方法，查看结果


```python
class Phone:

    def __init__(self,scree_size,price,brand):
        self.__scree_size=scree_size
        self.__price=price
        self.__brand=brand
        
    def setPrice(self,price):
        self.__price=price
        
    def getPrice(self):
        return self.__price
        
    def getScreeSize(self):
        return self.__scree_size
    
    def getBrand(self):
        return self.__brand
    
    def play(self):
        print('play name')
        
    def sendMessage(self,text):
        print('新消息来啦!',text)
        
    def powerOff(self):
        print('power off')
        
    def get_info(self):
        print('手机品牌：',self.__brand,'屏幕尺寸',self.__scree_size,'价格',self.__price)
        
phone1=Phone(5.5,6288,'apple')
phone1.play()
phone1.sendMessage('买新手机啦')
phone1.powerOff()
phone1.get_info()

phone2=Phone(5,1999,'mi')
phone2.play()
phone2.sendMessage('买新手机啦')
phone2.powerOff()
phone2.get_info()
```

    play name
    新消息来啦! 买新手机啦
    power off
    手机品牌： apple 屏幕尺寸 5.5 价格 6288
    play name
    新消息来啦! 买新手机啦
    power off
    手机品牌： mi 屏幕尺寸 5 价格 1999


##### 设计一个公司类，完成以下要求，并实例化不同对象进行验证
**类变量**
- 类下公司总个数，类下实例的名称列表
  
**类方法**
- 返回公司类共有多少个公司实例
- 返回公司类的公司实例的名称列表
  
**实例变量**
- 公司名，简介，利润，销售额，总成本，雇员姓名，雇员列表
  
**实例方法**
- 招聘人才（每招一个人会有成本产生，影响该实例雇员列表，人数，总成本）
- 解雇人员（每解雇一个人会有成本产生，影响该实例雇员列表，人数，总成本）
- 公司广告推广（影响该实例总成本）
- 交社保（按公司雇员总人数计算，影响该实例总成本）
- 交税（按公司雇员总人数计算，影响该实例总成本）
- 销售（按 销售件数*价格 计算销售额，利润按 销售额*利润率 计算利润）
- 获取公司雇员列表
- 获取公司净利润


```python
class Company:
    total=0  #公司总数
    compay_list=[]  #名称列表
    
    def __init__(self,name,desc):
        self.__name=name
        self.__desc=desc
        self.__profit=0  #利润
        self.__sales_total=0 #销售额
        self.__all_cost=0 #总成本
        self.__employee_name='' #雇员名字
        self.__employee_list=[]
        Company.compay_list.append(name)
        
    def recruit(self,employee_name,recruit_cost):
        self.__employee_list.append(employee_name)
        self.__all_cost+=recruit_cost
        Company.total+=1
            
    def fire(self,employee_name,recruit_cost):
        self.____employee_list.remove(employee_name)
        self.__all_cost-=recruit_cost
        Company.total-=1
            
    def advertise(self,adv_cost):
        self.__all_cost+=adv_cost
            
    def paySocialSecurity(self,security_cost): #交保险
        result=security_cost*Company.total
        self.__all_cost+=result
          
    def payTaxRevenue(self,revenue_cost): #交税
        result=revenue_cost*Company.total
        self.__all_cost+=result
            
    def sale(self,sale_count,sale_price,sale_profit):
        self.__sales_total=sale_count*sale_price
        self.__profit=self.__sales_total*sale_profit
            
    def getCompanyEmployeeList(self):
        return self.__employee_list
        
    def getPureProfit(self):
        return self.__profit
    
    def getAllCost(self):
        return self.__all_cost
    
    @classmethod
    def getTotal(cls):
        return Company.total
    
    @classmethod
    def getCompayList(cls):
        return Company.compay_list
    
c=Company('july','人工智能AI')
c.recruit('zs',7000)
print('总人数',Company.getTotal())
c.paySocialSecurity(20000)
print('总成本',c.getAllCost())
```

    总人数 1
    总成本 27000


**设计一个叫Cinema电影院的类，包含：**
- 类变量
    - 类下所有实例电影院的数量，销售额总和
- 类方法
    - 初始化方法，并初始化相应的类变量，实例变量
    - getSales（获取全部电影院实际销售的方法）的电影院实例方法
- 实例变量
    - 电影院名称，位置，销售额
- 实例方法
    - saleTickets方法，要求更新实例的销售总额及类的销售总额类变量
    
创建一个MiniCinema迷你电影院的类，继承自Cinima类
- 重写卖票方法，大于100元的票价加入打9折扣的功能
- 对MiniCinema实例进行调用体现多态性


```python
class Cinema:
    cinema_total=0
    sales_total=0
    
    def __init__(self,name,location,sales):
        self.name=name
        self.location=location
        self.sales=sales
        Cinema.cinema_total+=1
    
    @classmethod
    def getSales(cls):
        return Cinema.sales_total
    
    def saleTickets(self,tickt_price,ticket_num):
        self.sales+=tickt_price*ticket_num
        Cinema.sales_total+=self.sales

class MiniCinema(Cinema):
    def saleTickets(self,tickt_price,ticket_num):
        super().__init__(self,tickt_price,ticket_num)
        Cinema.cinema_total-=1
        if tickt_price>100:
            tickt_price*=0.9
            print('票价大于100元，自动打九折！')
        self.sales=Cinema.getSales()
        Cinema.sales_total += self.sales

A = Cinema('A', '天河', 0)
A.saleTickets(30, 10000)
print('电影院 A 的票房是： ', A.sales)
print('所有电影院销售总额---->', Cinema.getSales())

B = Cinema('B', '番禺', 0)
B.saleTickets(120, 20000)
print('电影院 B 的票房是： ', B.sales)
print('所有电影院销售总额---->', Cinema.getSales())

C = MiniCinema('C', '白云', 0)
C.saleTickets(120, 26000)
print('电影院 C 的票房是： ', C.sales)
print('共有电影院 %d 家！' % Cinema.cinema_total)
print('所有电影院销售总额---->', Cinema.sales_total)
```

    电影院 A 的票房是：  300000
    所有电影院销售总额----> 300000
    电影院 B 的票房是：  2400000
    所有电影院销售总额----> 2700000
    票价大于100元，自动打九折！
    电影院 C 的票房是：  2700000
    共有电影院 3 家！
    所有电影院销售总额----> 5400000


**导入包完成遍历目录**
- 导入os包
- 创建递归循环完成一个目录的遍历
    - 如果还有一个目录，依次进行遍历


```python
import os

def openPackage(path):
    for root,dirs,files in os.walk(path):
        #os.walk能直接遍历的目录
        if len(dirs)==0:
            print('Root =  ', root)
            print('文件有： ', files)
            print('本文件夹中已没有其他目录！')
        else:
            print('路径等于  ', root)
            print('文件夹有： ', dirs)
            print('文件有：  ', files)
            print('---------->')
            
openPackage('/Users/admin/test')

import os
def openPack(path):
    listDir=os.listdir(path)
    for item in listDir:
        pathName=os.path.join(path,item)
        if os.path.isfile(pathName):
            print('文件名为：',item)
            print('文件路径为：',pathName)
        else:
            openPack(pathName)
            
openPack('/Users/admin/test')
```

    路径等于   /Users/admin/test
    文件夹有：  ['a', 'b']
    文件有：   ['.DS_Store']
    ---------->
    路径等于   /Users/admin/test/a
    文件夹有：  ['a_c']
    文件有：   ['.DS_Store', 'a.py']
    ---------->
    Root =   /Users/admin/test/a/a_c
    文件有：  ['a_c.py']
    本文件夹中已没有其他目录！
    路径等于   /Users/admin/test/b
    文件夹有：  ['b_c']
    文件有：   ['.DS_Store', 'b.py']
    ---------->
    Root =   /Users/admin/test/b/b_c
    文件有：  []
    本文件夹中已没有其他目录！
    文件名为： .DS_Store
    文件路径为： /Users/admin/test/.DS_Store
    文件名为： .DS_Store
    文件路径为： /Users/admin/test/a/.DS_Store
    文件名为： a.py
    文件路径为： /Users/admin/test/a/a.py
    文件名为： a_c.py
    文件路径为： /Users/admin/test/a/a_c/a_c.py
    文件名为： .DS_Store
    文件路径为： /Users/admin/test/b/.DS_Store
    文件名为： b.py
    文件路径为： /Users/admin/test/b/b.py


**练习使用PIL包**
- 导入PIL包
    - 如果没有该包，请自行安装后导入
- 将一张图片进行尺寸缩放,颜色调整后保存。
    - (dir,help函数查看库）


```python
from PIL import Image
img=Image.open('/Users/admin/test/img.jpg')
# img.show()  #显示彩色图片

form=img.format
print('size',img.size)
out=img.resize((120,140))
print('size1',out.size)
out.show() 
out.save('/Users/admin/test/new_img.jpg')
dir(Image)
help(Image.open)
```

    size (256, 361)
    size1 (120, 140)
    Help on function open in module PIL.Image:
    
    open(fp, mode='r')
        Opens and identifies the given image file.
        
        This is a lazy operation; this function identifies the file, but
        the file remains open and the actual image data is not read from
        the file until you try to process the data (or call the
        :py:meth:`~PIL.Image.Image.load` method).  See
        :py:func:`~PIL.Image.new`.
        
        :param fp: A filename (string), pathlib.Path object or a file object.
           The file object must implement :py:meth:`~file.read`,
           :py:meth:`~file.seek`, and :py:meth:`~file.tell` methods,
           and be opened in binary mode.
        :param mode: The mode.  If given, this argument must be "r".
        :returns: An :py:class:`~PIL.Image.Image` object.
        :exception IOError: If the file cannot be found, or the image cannot be
           opened and identified.

**新建类并修改其实例的切片访问**
Python中对序列的切片访问，是左闭右开
- 创建一个可被迭代的类
- 改变默认的切片访问方式为左闭右闭
举例：
    c1=youClass([0,1,2,3,4,5,6,7,8,9])
    c1[2,7] 返回 2,3,4,5,6,7


```python
class CutClass:
    def __init__(self,oList=None):
        if oList==None:
            self.__oList=[]
        else:
            self.__oList=oList
            
    def getList(self,x,y):
        newList=[]
        print(x,y)
        if x<y and y<=len(self.__oList):
            newList=self.__oList[x:y]
            newList.append(self.__oList[y])
            return newList
        
c=CutClass([0,1,2,3,4,5,6,7,8,9])
print(c.getList(2,7))
```

    2 7
    [2, 3, 4, 5, 6, 7]

