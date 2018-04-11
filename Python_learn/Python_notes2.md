#### 深浅拷贝，作用域

- is ：用作比较两值的引用地址，==比较的是值
- 浅拷贝 copy,copy(被拷贝对象)：产生一个新的对象（引用）但是里面引用的元素还是原来的元素（元素地址没变）作用与“=”相同（切片，工厂函数）
- 深拷贝deepcopy：可变类型都新产生了一份，不可变类型共用
- 特殊：
    - 不可变类型：没有拷贝这种说法
        - 数值：小整数对象池（-5,256）
         - 元组：对象 不可变 注意：如果是元组，元组中的类型是可变类型才可以执行深拷贝
    - 可变类型：
        - 字典 中copy（）
        - list（）id不一样

- 原码反码补码
    - 正数：原码=补码=反码
    - 负数：反码=符号位不变，其他位取反。 补码=反码+1
    - 补码转回原码：原码 = 补码的符号位不变 -->数据位取反--> 尾+1
- 0b开头是二进制；0o开头是八进制；0x开头是十六进制。
- binary二进制 bin（进制）二进制
- oct（）八进制
- hex（）十六进制
- int（“0xa3”，16）16进制a3转十进制
- locals（）查看局部变量情况（字典形式）
- globals（）全局

- **属性property**
> 
   	其实就是为私有属性  ——》set和get方法

   	变形1：
		步骤1： 	
		def set_age(self,age):
			….
		def get_age(self):
			…
		步骤2：
		age=property(get_age,set_age)
		步骤3：
		使用:
		person= Person()
		person.age = 20   ——>判断有没有“=”  就调用set_age
		myage=person.age   ——> 就调用的是get_age

	变形2：
		步骤1：通过@property声明get方法

  			class Person:
				
				
				@property
				def age(self):
					return ….
		步骤二：
				根据步骤1的函数名定义
				@age.setter
		
		步骤三：定义函数，函数名与步骤一的函数名一致，就是多了一个参数
   				def age(self,age):
					self.__age=age

		步骤四:
			使用:
		person= Person()
		person.age = 20   ——>判断有没有“=”  就调用set_age
		myage=person.age   ——> 就调用的是get_age

#### 生成器
边循环边计算的机制称为生成器:generator。节省内存
- 创建生成器：
    - 列表推导式的 [ ] 改成 ( )
    - 使用yield关键字：将函数内要返回的值使用yield返回。yield是一个关键词，类似return, 不同之处在于，yield返回的是一个生成器。
- 生成器获取元素的方式：
    - next（生成器对象） （指针到最后会报异常）
    - for x in 生成器对象  （不会报异常）
    - next(f)等价f.send(None)
    - 生成器对象.__ next __()

#### 迭代器
迭代是访问集合元素的一种方式。迭代器是一个可以记住遍历的位置的对象。迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。
- 可用作for循环的对象都是Iterable类型
- 判断是否可迭代：isinstance（被判断，Iterable）
（from collections import Iterable）
- 判断是否为迭代器：
from collections import Interator
isinstance(被判断的对象,Iterator)

- 生成器都是 Iterator(迭代器) 对象，但 list 、 dict 、 str 虽然是 Iterable(可迭代的) ，却不是 Iterator(迭代器) 。
- 使用iter()函数把Iterable变成迭代器

#### 闭包
- 定义 ：
    - 1.闭包函数必须有内嵌函数；
    - 2.内嵌函数需要引用该嵌套函数上一级namespace中的变量；
    - 3.闭包函数必须返回内嵌函数；




#### 装饰器
>   
    mport time
    def text_add(func):
        print("text_add")
        def add():
            print("add")
            func()
        return add
    @text_add
    def text():
       print("text")
    text()
    
    
- 对象动态添加带参数的函数：
> 
    import types
    p.func=types.MethodType(func,p)
    p.func(参数)

- 删除属性方法：
    - del 对象.属性名
    - delattr（对象，“属性名”）
- __slots __ ：限制添加实例属性和实例方法，但类属性和类方法和静态方法可以添加  __slots __ = ("name","age")

_slots__定义的属性仅对当前类实例起作用，对继承的子类是不起作用的
- type 动态创建类：text=type（“Phone”，（object，），{}）
- __metaclass __ 自定义元类

#### 垃圾回收
- 小整数对象池【-5,256】在一个 Python 的程序中，所有位于这个范围内的整数使用的都是同一个对象. 不会被回收
- 引用计数机制，三代列表（标记清除）



#### 类和对象的内建属性

- __getattribute __：属性拦截器  访问实例方法和属性时触发
> 
     def __getattribute__(self,obj): obj是被调用的属性
        if obj == 'subject1':
            print('log subject1')
            return 'redirect python'
        else:
            return object.__getattribute__(self,obj)




#### 进程

- **并发**：在多核系统里的,同时执行多个进程，一般会情况下会有些进程没有机会执行，这种情况是并发。
- **并行**：在多核系统里，同时执行多个进程，这些进程都有机会执行，这种情况是并行。

- **os.fork** 创建进程，windows不支持。多次fork线程数会变成2^n 个
    - os.getpid()获取子进程id
    - os.getppid()获取父进程id
- from multiprocessing import **Process**创建进程
    - p = Process(target=子进程函数名,args=("test",))
    - **start()** 启动进程实例
    - **join()** 方法可以等待子进程结束后再继续往下运行，通常用于进程间的同步。
    - **join([timeout])**：是否等待进程实例执行结束，或等待多少秒；
    - target：表示这个进程实例所调用对象；
    - args：表示调用对象的位置参数元组；
    - kwargs：表示调用对象的关键字参数字典；
    - name：为当前进程实例的别名；
- **自定义Process类**
>
    from multiprocessing import **Process**
    class MyProcess(Process)
        def run(self): #重写run方法
            pass 
    p=MyProcess 
    p.start() #启动，不用手动调用run

- **进程池Pool**
- 非阻塞式：全部添加到执行队列，立刻返回，并等执行完后有回调函数
- 阻塞式：执行完一个再执行，没有回调函数
>
    pool=Pool(2)#创建两个进程
    pool.apply_async(进程的函数名) #非阻塞式
    pool.close #如果没有close，则pool仍然等待任务进来，则不做上面分配的任务



#### 线程
- 自定义线程：
    - 自定义线程类必须继承Thread
    - __init __ 方法注意调用super().__init __()

- 互斥锁:
    - from threading import Lock
    - mutex = Lock()创建锁
    - mutex.acquire()锁定,可以设置超时
    - mutex.release()释放
