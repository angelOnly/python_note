
## (五)文件操作，并发编程及常用系统模块

#### 文本文件读写

```python
#  r = read, w = write, a = append, b = binary, +表示文件不存在就创建
f=open('/Users/admin/test/text.txt','r') 
text=f.read()
print(text)
f.close()
```

    text

```python
f=open('')
try:
    do something
except:
    pass
finally:
    if f:
        f.close()
```


```python
#如果with里面的代码出现异常，就会自动捕捉异常并把文件关闭
with open('/Users/admin/test/text.txt','r') as f:
    line=f.readline()
    while line:
        print(line.strip())
        line=f.readline()
```

    text

```python
with open('/Users/admin/test/text.txt','r') as f:
    for line in f.readlines():
        print(line.strip())   #strip()：去掉最后一个换行符
```

    text
    Dnjxk
    Sdnjl
    Dshl
    Ndskj
    Ndskndkjs
    ncccccccccccccds
    测试
    学习


##### 实现一个readlines生成器
Python中除了''、""、0、()、[]、{}、None为False之外，其他的都是True。


```python
def readlines(f):
    line=f.readline()
    while line:
        yield line
        line=f.readline()
        
with open('/Users/admin/test/text.txt','r') as f:
    for line in readlines(f):
        print(line.strip())   #strip()：去掉最后一个换行符
```

    text
    Dnjxk
    Sdnjl
    Dshl
    Ndskj
    Ndskndkjs
    ncccccccccccccds
    测试
    学习

```python
texts=['New line #1 hello world', 'Line #2 life is not easy']
with open('/Users/admin/test/text.txt','w+') as f:
    for text in texts:
        f.write(text+'\n')
        
# a+ 追加内容，文件不存在就创建
with open('/Users/admin/test/new_text.txt','a+') as f:
    f.write('something new\n')
```

#### json
- load：（文件操作，传递文件句柄）把字符串或文件变成json对象
- dump：（文件操作，传递文件句柄）把json对象变成字符串或文件
- loads：（字符串操作，传递字符串）把json字符串变成字典对象
- dumps：（字符串操作，传递字符串）把字典对象变成json字符串


```python
import json
config = {'ip': '192.168.1.1', 'port': ['9100', '9101', '9102']}
with open('/Users/admin/test/new_json.txt','w+') as f:
    json.dump(config,f) #dump把字典写入json文件
    
with open('/Users/admin/test/new_json.txt','r') as f:
    new_config=json.load(f)
    
print(type(new_config))
print(new_config)

#json.loads 解析的是字符串 ""
#把字符串的json解析成字典对象
config_str='{"ip": "192.168.1.1", "port": ["9100", "9101", "9102"]}'
config=json.loads(config_str)
print(type(config))
print('config',config)
#json.dumps 把json对象变回json字符串
new_config=json.dumps(config)
print(type(new_config))
print(new_config)
```

    <class 'dict'>
    {'ip': '192.168.1.1', 'port': ['9100', '9101', '9102']}
    <class 'dict'>
    config {'ip': '192.168.1.1', 'port': ['9100', '9101', '9102']}
    <class 'str'>
    {"ip": "192.168.1.1", "port": ["9100", "9101", "9102"]}


#### 模拟dumps的实现


```python
def json_dumps(d1):
    s='{\n'
    lines=[]
    for k,v in d1.items():
        _s='"'+k+'":'
        if type(v)!=list:
            _s+='"'+str(v)+'"'
        else:
            items=['"'+i+'"' for i in v]
            _s+='['+','.join(items)+']'
        lines.append(_s)
    s+=',\n'.join(lines)
    s+='\n}'
    return s
    
config_str={'ip': '192.168.1.1', 'port': ['9100', '9101', '9102']}
print(json_dumps(config_str))
```

    {
    "ip":"192.168.1.1",
    "port":["9100","9101","9102"]
    }


#### 实现cvs文件读取


```python
def read_csv(f):
    line=f.readline()
    while line:
        line=line.strip()
        yield line.split(',')
        line=f.readline()
        
feature_list=[]
label_list=[]
headers=None
with open('/Users/admin/test/sales.csv','r') as f:
    for row in read_csv(f):
        if not headers: #如果不是headers，说明已经不是第一行
            headers=row
        else:
            label_list.append(row[-1])
            row_dict={}
            for i in range(1,len(row)-1):
                row_dict[headers[i]]=row[i]
            feature_list.append(row_dict)
            
print(feature_list)
print(label_list)
```

    [{'Age': 'youth', 'Income': 'high', 'Student': 'no', 'CreditRating': 'fair'}, {'Age': 'youth', 'Income': 'high', 'Student': 'no', 'CreditRating': 'excellent'}, {'Age': 'middle', 'Income': 'high', 'Student': 'no', 'CreditRating': 'fair'}, {'Age': 'senior', 'Income': 'medium', 'Student': 'no', 'CreditRating': 'fair'}, {'Age': 'senior', 'Income': 'low', 'Student': 'yes', 'CreditRating': 'fair'}, {'Age': 'senior', 'Income': 'low', 'Student': 'yes', 'CreditRating': 'excellent'}, {'Age': 'middle', 'Income': 'low', 'Student': 'yes', 'CreditRating': 'excellent'}, {'Age': 'youth', 'Income': 'medium', 'Student': 'no', 'CreditRating': 'fair'}, {'Age': 'youth', 'Income': 'low', 'Student': 'yes', 'CreditRating': 'fair'}, {'Age': 'senior', 'Income': 'medium', 'Student': 'yes', 'CreditRating': 'fair'}, {'Age': 'youth', 'Income': 'medium', 'Student': 'yes', 'CreditRating': 'excellent'}, {'Age': 'middle', 'Income': 'medium', 'Student': 'no', 'CreditRating': 'excellent'}, {'Age': 'middle', 'Income': 'high', 'Student': 'yes', 'CreditRating': 'fair'}, {'Age': 'senior', 'Income': 'medium', 'Student': 'no', 'CreditRating': 'excellent'}]
    ['no', 'no', 'yes', 'yes', 'yes', 'no', 'yes', 'no', 'yes', 'yes', 'yes', 'yes', 'yes', 'no']


#### 序列化和反序列化


```python
import pickle

class MyObject:
    def __init__(self, x, y):
        self.x = x
        self.y = y

obj = MyObject(100, 200)
s_obj = pickle.dumps(obj)
print(s_obj)
obj = pickle.loads(s_obj)
print(obj.x, obj.y)
```

    b'\x80\x03c__main__\nMyObject\nq\x00)\x81q\x01}q\x02(X\x01\x00\x00\x00xq\x03KdX\x01\x00\x00\x00yq\x04K\xc8ub.'
    100 200


#### 多进程与多线程
**进程** 
- 进程（Process）是计算机中的程序关于某数据集合上的一次运行活动，
- 是系统进行资源分配和调度的基本单位，是操作系统结构的基础。
**线程：** 
- 线程，有时被称为轻量级进程(Lightweight Process，LWP），是程序执行流的最小单元。
一个标准的线程由线程ID，当前指令指针(PC），寄存器集合和堆栈组成。
另外，线程是进程中的一个实体，是被系统独立调度和分派的基本单位，线程自己不拥有系统资源，只拥有一点儿在运行中必不可少的资源，
但它可与同属一个进程的其它线程共享进程所拥有的全部资源。一个线程可以创建和撤消另一个线程，同一进程中的多个线程之间可以并发执行。

#### 多进程
```python
# 多进程
from multiprocessing import Process
import os

# 子进程要执行的代码
def run_proc(name):
    print('Run child process %s (%s)...' % (name, os.getpid())) # 复制到文件然后在cmd窗口下执行

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Process(target=run_proc, args=('test',))
    print('Child process will start.')
    p.start()
    p.join()
    print('Child process end.')
```

    Parent process 7232.
    Child process will start.
    Run child process test (8019)...
    Child process end.

#### 多线程
```python
# 多线程
import time, threading

# 新线程执行的代码:
def loop():
    print('thread %s is running...' % threading.current_thread().name)
    n = 0
    while n < 5:
        n = n + 1
        print('thread %s >>> %s' % (threading.current_thread().name, n))
        time.sleep(1)
    print('thread %s ended.' % threading.current_thread().name)

print('thread %s is running...' % threading.current_thread().name)
t = threading.Thread(target=loop, name='LoopThread')
t.start()
t.join()
print('thread %s ended.' % threading.current_thread().name)
```

    thread MainThread is running...
    thread LoopThread is running...
    thread LoopThread >>> 1
    thread LoopThread >>> 2
    thread LoopThread >>> 3
    thread LoopThread >>> 4
    thread LoopThread >>> 5
    thread LoopThread ended.
    thread MainThread ended.

#### 进程池
```python
# 进程池
from multiprocessing import Pool
import os, time, random

def long_time_task(name):
    print('Run task %s (%s)...' % (name, os.getpid()))
    start = time.time()
    time.sleep(random.random() * 3)
    end = time.time()
    print('Task %s runs %0.2f seconds.' % (name, (end - start)))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Pool(4)
    for i in range(5):
        p.apply_async(long_time_task, args=(i,))
    print('Waiting for all subprocesses done...')
    p.close()
    p.join()
    print('All subprocesses done.')
```

    Parent process 7232.
    Run task 3 (8037)...
    Run task 1 (8035)...
    Run task 2 (8036)...
    Run task 0 (8034)...
    Waiting for all subprocesses done...
    Task 2 runs 0.43 seconds.
    Run task 4 (8036)...
    Task 0 runs 1.30 seconds.
    Task 1 runs 1.58 seconds.
    Task 4 runs 1.93 seconds.
    Task 3 runs 2.83 seconds.
    All subprocesses done.

#### 线程池

```python
# 线程池
import threadpool
import time

def long_op(x):
    print('%d\\n' % n)
    time.sleep(2)

pool = threadpool.ThreadPool(os.cpu_count())
tasks = threadpool.makeRequests(long_op, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]) # 可以尝试函数使用多个参数，必须看源代码
print(len(tasks))
[pool.putRequest(task) for task in tasks]
pool.wait()
```
#### 多线程的应用

```python
### 多线程的应用
求每个列表中最大的三个数
```


```python
def top3(data):
    data.sort()
    temp_result[threading.current_thread().name]=data[-3:]

data_set = [[1, 7, 8, 9, 20, 11, 14, 15],
            [19, 21, 23, 24, 45, 12, 45, 56, 31],
            [18, 28, 64, 22, 17, 28]]
temp_result={}
threads=[]
for i in range(len(data_set)):
    t=threading.Thread(target=top3,name=str(i),args=(data_set[i],))
    threads.append(t)

for t in threads:
    t.start()
    
for t in threads:
    t.join()

result=[]
for k,v in temp_result.items():
    result.extend(v)

result.sort()
print(result[-3:])
```

    [45, 56, 64]


#### 多进程变量共享
```python
# 多进程变量共享
from multiprocessing import Process, Queue
import os, time, random

def write(q):
    print('Write: %s' % os.getpid())
    for value in ['AAA', 'BBB', 'Hello World']:
        print('Write %s' % value)
        q.put(value)
        time.sleep(random.random())
        
def read(q):
    print('Read: %s' % os.getpid())
    while True:
        value = q.get(True)
        print('Read %s' % value)
        
if __name__ == '__main__':
    q = Queue()
    pw = Process(target=write, args=(q,))
    pr = Process(target=read, args=(q,))
    pw.start()
    pr.start()
    pw.join()
    time.sleep(3)
    pr.terminate()
    print('Done')
```

    Write: 8131
    Write AAA
    Read: 8132
    Read AAA
    Write BBB
    Read BBB
    Write Hello World
    Read Hello World
    Done


#### 锁
```python
# 锁
import threading

lock = threading.Lock()

balance = 0
def change_balance(n):
    global balance
    balance += n 
    # balance = 100，但是两个进程，1个加10，一个加20，同时操作，最后balance可能变成110，也可能变成120，
    # 但不是我们要的130。
    
def run_thread(n):
    lock.acquire()
    try:
        change_balance(n)
    except:
        pass
    finally:
        lock.release()
    
threads = []
for i in range(11):
    t = threading.Thread(target=run_thread, args=(i, ))
    threads.append(t)
for t in threads:
    t.start()
for t in threads:
    t.join()
print(balance)
```

    55


#### sys应用
```python
# sys应用
import sys
print(sys.argv)
print(sys.path)
# sys.path.append(...)
```

    ['/Users/admin/anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py', '-f', '/Users/admin/Library/Jupyter/runtime/kernel-2d7863d3-e036-4b2f-9be8-966a8c17391f.json']


#### os应用
```python
# os应用
# 关键部分：os.listdir, os.path.abspath/isdir/join
import os  

def dir_s(path, tabs=0):
    path = os.path.abspath(path)
    files= os.listdir(path) #得到文件夹下的所有文件名称 
    my_dirs = []
    for f in files:
        #拼接绝对路径
        abs_path = os.path.join(path, f)
        if os.path.isdir(abs_path): 
            my_dirs.append(f)
        else: #不是目录，直接打印
            print('\t' * tabs + f)
    for my_dir in my_dirs:
        print('\t' * tabs + my_dir)
        #解决 \\ 可能不解析的问题
        dir_s(os.path.join(path, my_dir), tabs + 1)

dir_s('.') # 尝试walk函数更简单的实现
```


```python
### 练习
使用线程池实现对50个文本进行单词出现频率统计并汇总结果（可以自己写一个随机文件生成器）
```


```python
读取文本文件，将全部内容倒序后写入新文件
```
