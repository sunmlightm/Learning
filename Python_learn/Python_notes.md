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
- 切片的语法：**[起始:结束:步长] ** 选取的区间属于**左闭右开型**,不写步长默认是1
  
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
- **index()** 跟find()方法一样，只不过如果str不在 mystr中会报一个异常.
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
    - reverse方法是将list逆置。
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
```
    - 遍历字典和遍历值：
    ```
    infos = {'name':'宋江', 'id':100, 'sex':'男生', 'address':'中国梁山'}
    for index,value in enumerate(infos):
       print("%d %s " % (index,value))
    遍历值
    infos = {'name':'宋江', 'id':100, 'sex':'男生', 'address':'中国梁山'}
    for index,value in enumerate(infos.values()):
       print("%d %s " % (index,value))
```
