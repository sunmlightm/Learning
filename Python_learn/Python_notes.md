# Python基础
- #单行注释
- '''多行

     注释'''

- """
  使用双3个双引号，也可以多行注释
  使用双3个双引号，也可以多行注释
  """
- 如果直接在程序中用到了中文，比如
print('你好')如果直接运行输出，程序会出错
解决的办法为：在程序的开头写入如下代码，这就是中文注释
``` 
   #coding=utf-8
在python的语法规范中推荐使用的方式： # -*- coding:utf-8 -*-
```

#### 变量以及数据类型
- num1 = 100 #num1就是一个变量
- 可以使用type(变量的名字)，来查看变量的类型

#### 标识符和关键字
- 标识符由字母、下划线和数字组成，且数字不能开头
    - fromNo12、my_Boolean
- 标识符是区分大小写的
    - Cat 和cat是两个不同的变量



#### 字符串
- **sys.getsizeof(boject)** 以字节（byte）为单位返回对象大小。
- **len()**  方法返回对象（字符、列表、元组、字典等）长度或项目个数。
- print('{0},{1}'.**format**('刘备',20)) >>刘备，20
  print('{1},{0},{1}'.format('刘备',20)) >>20，刘备，20
  print('{name},{age}'.format(age=28,name='曹操'))>>曹操，28
  通过映射list：a_list=['曹操'，20] format（a_list）
- 切片的语法：**[起始:结束:步长]**  选取的区间属于 **左闭右开型**,不写步长默认是1
  
  name[0:3:1]

  逆序：**name[-1:0:-1]**----**name[::-1]**
 ```
  小结
[:] 提取从开头（默认位置0）到结尾（默认位置-1）的整个字符串
[start:] 从start 提取到结尾
[:end] 从开头提取到end - 1
[start:end] 从start 提取到end - 1
[start:end:step] 从start 提取到end - 1，每step 个字符提取一个
[::-1]逆序
```
#### 字符串常见函数
- **count()** 方法用于统计字符串里某个字符出现的次数。可选参数为在字符串搜索的开始与结束位置。str.count(sub, start= 0,end=len(string))
- **find**:检测 str 是否包含在 mystr中，如果是返回开始的索引值，否则返回-1
- **rfind**
类似于 find()函数，不过是从右边开始查找
- **index()** 参数是要查找的元素。跟find()方法一样，只不过如果str不在 mystr中会报一个异常.
- ridex
- **replace** 把 mystr 中的 str1 替换成 str2,如果 count 指定，则替换不超过 count 次，最多等于count     
    str.replace(str1, str2, mystr.count(str1))
- **split** 以 str 为分隔符切片 mystr，如果 maxsplit有指定值，则仅分隔 maxsplit 个子字符串
- **partition** 把str以str1分成三部分，str1前，str1自身，str1后
- **rpartition** 从右边开始
- **splitlines** 按照行分隔，返回一个包含各行作为元素的列表,按照换行符分割
- **startswith** 检查字符串是否是以 obj 开头, 是则返回 True，否则返回 False  str.startswith(obj)
- **endswith** 检查字符串是否以obj结束，如果是返回True,否则返回 False. 
- **lower** 转换 str 中所有大写字符为小写  str.lower() 
- **upper** 转换 str 中的小写字母为大写
- **lstrip**  删除 str 左边的空白字符  str.lstrip()
- **rstrip**   删除 str 右边的空白字符  str.rstrip()
- **center**  居中，两边加相同位数的空格  str.center(10)
- **strip**  删除两段空白字符
- **isspace** 如果 str 中只包含空格，则返回 True，否则返回 False.如果有多个空格同样返回True
- **join**  ','.join('abc')  将字符串abc中的每个成员以字符','分隔开再拼接成一个字符串。join里放列表、元组、字典也是可以的
- **capitalize** 把字符串的第一个字符大写 str.capitalize()
- **title** 把字符串的每个单词首字母大写
- **ljust**  str.ljust(width)  返回一个原字符串左对齐,并使用空格填充至长度 width 的新字符串
- **rjust** 返回一个原字符串右对齐,并使用空格填充至长度 width 的新字符串
- **isalpha** str.isalpha() str 所有字符都连续的是字母 则返回 True,否则返回 False
- **isdigit** str.isdigit() str 只包含数字则返回 True否则返回False.应用场景：输入数字的时候，判断是纯数字的时候，就可以转成ini
- **isalnum** str 所有字符都是字母或数字则返回 True,否则返回 False

#### 列表(list)
- 循环遍历 for name in names_list
- **插入元素**
    - **append** 向列表添加元素 names.append(temp) 
    - **extend** 将另一个集合中的元素逐一添加到列表中names.extend(a_name)
    - **insert** 在指定位置index前插入元素 insert(index, object) 在指定位置index前插入元素object
        - **append的注意事项，直接修改的是原列表**
- **删除元素**
    - del根据下标进行删除 del names[1]
    - pop删除最后一个元素  names.pop()
    - remove根据元素的值进行删除 names.remove(name)
- **通过下标修改元素("改")**
    - 修改元素的时候，要通过下标来确定要修改的是哪个元素，然后才能进行修改
    - names[1] = input("请输入要修改后的内容:")
- **查找元素**
    - in和not in （in（存在）,如果存在那么结果为True，否则为False
  not in（不存在），如果不存在那么结果为True，否则False   if find_name in names:
）
    - index和count index和count与字符串中的用法相同
- **排序**
    - sort方法是将list按特定顺序重新排列，默认为由小到大，参数reverse=True可改为倒序，由大到小。
    - sort(key=none,reverse=falus) key:按照key排序（字典）reverse方法是将list逆置。


#### 元组tuple
- 定义方式：
    - 2,3,4
    - 使用（）：（2,3,4）
    - 注意：a=（10）>>int类型 a=（10，）>>元组类型
- 元组中数据无法修改、删除、添加
- 元组可以使用的函数：index，count
- tuple（）可以将列表、字符串转换为元组。参数不能为int类型

#### 字典
- 以键值对作为整体保存数据。一个字典中的key不能重复，如果有相同的则后面的值覆盖前边的。
    字典中元素是无序的
- 字典中根据key获取值：字典名[key]。也可以通过get（）。字典名.get(key,default)>>如果找不到key显示默认值
- 删除
    - del 字典['key']没有返回值
    - del+字典名（删除整个字典,删除后字典不存在）
    - clear 清空字典
    - pop  字典.pop（‘key’）返回被删除的值
    - popitem 随机删除 字典.popitem（）返回被删除的键值对
- 修改 字典[key]=新值
- .keys():字典.keys()返回字典中所有的key
- .values():值
- .items(): 键值对
- has_key
- 遍历字典的key-value（键值对）:for key,value in infos.items():
   print("key={},value={}".format(key,value))
- 使用枚举遍历enumerate():既要遍历索引又要遍历元素时
``` 
names = ["宋江","卢俊义","吴用"]
for index,value in enumerate(names):
   print("%d %s " % (index,value))
   
enumerate还可以接收第二个参数，用于指定索引起始值，如：
names = ["宋江","卢俊义","吴用"]
for index,value in enumerate(names,2):
   print("%d %s " % (index,value))
>>>2宋江
   3卢俊义
   4吴用

    - 遍历字典和遍历值：
   
    infos = {'name':'宋江', 'id':100, 'sex':'男生', 'address':'中国梁山'}
    for index,value in enumerate(infos):
       print("%d %s " % (index,value))
    遍历值
    infos = {'name':'宋江', 'id':100, 'sex':'男生', 'address':'中国梁山'}
    for index,value in enumerate(infos.values()):
       print("%d %s " % (index,value))
```



#### set集合
- set:{1,2,3} 无序，元素不允许重复

#### Python内置函数
- cmp(item1, item2) python2中比较两个值。相等返回0，小于返回-1大于返回1
- len(item) 计算容器中元素个数
- max(item)返回容器中元素最大值
- min(item)
- del(item) && del item删除

#### 引用
- id（item）获取item的内存地址以数字形式表现
- 可变类型：列表，字典。  不可变：字符串 数值 元组
- 字符串 a，b交换位置： a，b=b，a

#### 函数
- 具有独立功能的代码组织为一个小模块
- 函数定义：
            
        def 函数名（参数1，参数2）：
        代码
        注意：标识符由字母下划线和数字组成切不能以数字开头。（推荐：函数名小写可以加入下划线增加可读性）
> - 不定长参数：def test(a,b,*args,**kwargs)
> tsst(1,2,3,4)3,4赋值给args，args是一个元组，**kwargs是字典。
- 在函数中，加入global会将局部变量转为全局变量 （global a）
> - 递归:

    def sum(num):
        if num==1:
            return num
        else:
            return num+sum(num-1)
    print(sum(10))
- 匿名函数 sum=**lambda** x,y:x+y print(sum(1,2))
- eval 将字符串去除“ ”变为程序代码
- 保存多个返回值
> 
    return a，b
    a，b=函数名（）
- 查看內建函数
> 
    func_names = dir(__builtins__)
    print(func_names)

    在交互模式下
    dir(__builtin__)或者dir(__builtins__)
    或者
    import builtins
    print(dir(builtins))
### 文件
> 
    f=open("text.txt","w")
    f.write("hello world")
    f.close()

- **open**(file,mode='r')打开文件
    - **r** :以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。如果文件不存在会崩溃。
    - **w** :打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
    - **r+** 打开一个文件用于读写。文件指针将会放在文件的开头。如果文件不存在会崩溃.会**从文件开头开始覆盖文件**
    - **w+** 打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。
    - **a+** 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是**追加模式**。如果该文件不存在，创建新文件用于读写。
    - **操作二进制文件：普通操作指令加b 如：rb,wb,rb+,ab+**
- **close()** 关闭
- **write** ("写入的内容")
- **read(num)** 使用read(num)可以从文件中读取数据，num表示要从文件中读取的数据的长度（单位是字节(如果是汉字，则单位是字符)），如果没有传入num，那么就表示读取文件中所有的数据。
- **readlines** 就像read没有参数时一样，readlines可以按照行的方式把整个文件中的内容进行一次性读取，并且返回的是一个列表，其中每一行的数据为一个元素.
- **readline** 读取一行
- 文件复制：源文件 目标文件循环读写
- **tell()** 获取当前指针位置
- **seek(offset,from)** offset偏移量 from方向：0开头1:表示当前位置 2:表示文件末尾
    - **python3中：**
        - 定位到文件开头：seek(0,0)，seek(3,0);不支持seek(负数,0);
        - 定义文件当前位置：支持seek(0,1)；不支持seek(正,1)和seek(负数,1)
        - 定位到文件末尾：支持seek(0,2)；不支持seek(正,2)和seek(负数,2)
    - python2中支持seek（负数，1,）（负数，2）

#### OS模块
**导入os模块：import OS** 系统内置，如果使用需要导入
- **renam** (原文件名，目标文件名)文件或文件夹重命名 OS.rename(text1,text2)
- **remove**(文件名) 删除文件
- os.**mkdir**("name")创建单个文件夹
- os.**makedirs**("names/name/na")多层文件夹创建，最外层文件夹若存在返回提示错误
- os.**getcwd**()获取当前路径
- os.**chdir**("./../")改变目录,进入当前目录的上级目录 切换到当前目录的子文件夹：os.chdir(./文件夹名)
- os.**listdir**("./")获取当前目录下所有的文件和文件夹，返回值是一个列表
- os.**rmdir** 删除文件夹（必须是空文件夹）
- import shutil

    **shutil.rmtree**("张三")
#### 换行问题：
- Linux，新mac下，**\n** 换行
- windows  **\r\n**换行

#### 面向对象(Object Oriented Programming，OOP)
- 定义类：
> 
    class Name(object): 命名：大驼峰
        def name1(self):
            ...
        def name2(self):
            ...
- 对象：
    对象名=Name（）
- 调用：对象名.name1()
- 添加属性： 对象名.属性名=value（添加的属性只应用到了此对象中，类不受影响）
- self:某个对象调用其方法时，Python解释器会把这个对象作为第一个参数传递给self.（可以使用其他名字替代self，推荐使用self）

> 
    class Cat(object):
            def eat(self):
                print("%s:eat",%(self.name))
    bluecat=Cat()
    bluecat.name="蓝猫"
    bluecat.eat  >>>打印：蓝猫：eat

- __ init __定义一个初始化函数，通常可以用来实现默认值赋值.init函数在类中可以多个同时存在，下边的默认覆盖上面的属性
> 
    class Cat(object):
        def __ init__(self):
            self.name="tom"
        def eat(self):
            print("%s:eat",%(self.name))
    bluecat=Cat()
    bluecat.eat  >>>打印：tom：eat

- id(对象名)打印内存地址
- __ str __：打印对象名时默认调用str方法：必须有return  
- __del __:删除对象 Python解释器执行完整个代码后会默认最后调用__del __
- import sye   sys.getrefcount(对象)查看此对象的引用空间有几个引用关系（sys.getrefcount自身也算一个）
- 面向对象四大特征：抽象、封装、继承、多态
- 继承：子类可以继承父类的属性和方法，但不能继承私有
- 重写:所谓重写，就是子类中，有一个和父类相同名字的方法，在子类中的方法会覆盖掉父类中同名的方法
- super（）1、通过super().work()调用父类的方法 2、通过类名.父类方法名.(self)
- .__mro __可以查看类的对象搜索方法时的先后顺序
- **类方法：@classmethod** 类方法中不能使用对象的属性
- **静态方法：@staticmethod** 可以调用类属性，要想使用对象属性必须要传参，通过参数对象调用。
- **__ new__** 执行的第一个动作
> def __ new__(cls) **注意参数不是self** 方法定义为静态方法，并且至少需要传递一个参数cls

- __call __ 对象当做方法使用的时候:对象()
- __base__属性，可以查看类上一层的父类是什么


- **简单工厂模式**:
- **工厂方法模式**: 
- 



- __name __:class的名字.如果在当前类使用的话,默认值是 __main __.如果是当前类导入到其他类中,则打印的是类名
if __ name __ == __main __判断是否为当前类


- 调用父类的 __ init __():
    - super().__init __()
    - Father.__init __(self)
    - super().__init __(name)
    - super(Son,self).__init __(name)



#### 异常
- 捕获异常:
>
    try:
        可能发生异常的代码
    except +异常类型:一个try可以有多个except
    没有异常则except部分不执行
    except(异常1,异常2)
    except:
        发生异常时进入的代码
    不加异常状态的except必须放在最下面

- 获取异常的信息描述:
> 
    except (要捕获的异常1,异常2) as result:
        print("异常:%s"%result)
    except Exception as result :(捕获所有异常)
    print("出错了:%s" % result)

- else
> 
    try:
    num = 100
    print(num)
    except Exception as result :
        print("出错了:%s" % result)
    
    else:(程序没有错执行else)
        print("程序没有错，正常执行到else这里了...") 
- finally:无论有没有异常都会执行的代码
- try嵌套
> 
    try
        ..
        try
            ..
    except
    异常有传递性
- raise抛出系统的异常
- 
-

#### 模块
- 模块.__file __获取模块的位置  
- 导入:
    - import 模块名
    - from 模块名 import 方法名
    - from 模块名 import * 导入该模块所有的内容
    - __ all __ :__all __ = ["num","test1","Person"]对import *有用（定义可以导入的内容）（ __all __加在模块中）

- sys.argv接收程序传递的参数
- 列表推导式：list=[x for x in range(1,5)]>>>1,2,3,4
- 列表生成式：list=[5 for x in range(1,5)]>>>[5,5,5,5]
- list=[x for x in range(1,5) if x%2==0]>>>2,4
- list=[(x,y) for x in range(2) for y in range(2)]>>>[(0,0),(0,1),(1,0),(1,1)]
