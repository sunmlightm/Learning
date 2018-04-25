


1.进入虚拟环境 workon python3

2.django-admin startproject dir_name创建项目文件夹(项目配置及设置文件)

3.cd进入项目文件夹

4.python manage.py startapp dir_name (应用文件夹)

5.使用pycharme打开项目文件夹

6.设置虚拟环境

7.**settings.py**:
- INSTALLED_APPS:添加应用文件
- TEMPLATES: 'DIRS': [os.path.join(BASE_DIR),'templates'],并在项目文件夹下新建templates文件夹
- DATABASES:
    - ENGINE:'django.db.backends.**mysql**'
    - 之后设置mysql的user,password,host,prot,name等
    
8.**urls.py**:
- 首先引入应用文件夹下views文件内自己写入的文件
- urlpatterns:创建引入的url项:(正则,函数名,自定义小名)
- 例:
> 
    from haha.views import index,page_html
    url(r'page/',page_html, name='page_html'),

9.**views.py**
- 导包:from django.shortcuts import render,HttpResponse(render用于请求网页,HttpResponse用于字符串)
- 自定义函数,用于返回字符串和html页面(存放在templates文件夹里的html)
- 例:
> 
    def index(request):
        return HttpResponse('123456')
    def page_html(request):
        a="123"
        b=[1,2,3]
    	return render(request,'test1.html',{'a':a,'b':b})
 
10.**models.py** 数据库

**创建表**
>
    class StudentInfo(models.Model):
        name=models.CharField(max_length=20,verbose_name='学生姓名')   #CharField=varchar,verbose_name:别名
        age=models.IntegerField(default=18,verbose_name='学生年龄')
        gender=models.CharField(choices=(('girl','女'),('boy ','男')),max_length=6,default='girl',verbose_name='学生性别')
        height=models.DecimalField(max_digits=5,decimal_places=2,verbose_name='学生身高')  #max_digits总位数,decimal_places小数位数
        image = models.ImageField(upload_to='user/%y/%m/%d',max_length=100,verbose_name='学生头像')  #upload_to上传到
        add_time=models.DateTimeField(default=datetime.now,verbose_name='添加时间') #datetime需要引入:from datetime import datetime
        is_delete=models.BooleanField(default=False,*****)
        class Meta:
            # db_table=''  #更改表名
            # ordering=[ '-age' ]
            verbose_name='学生信息'
            verbose_name_plural=verbose_name #后台默认显示复数形式,加上这一行不会自动加s
- 生成迁移文件:python manage.py makemigrations
- 同步文件:python manage.py migrate

**单个数据库操作**
- 数据插入
    - 方法一: from students.models import StudentInfo
    - a=StudentInfo()
    - a.name=,...
    - a.save()
    - 方法二: StudentInfo.object.create(name='name',age='12'......)

