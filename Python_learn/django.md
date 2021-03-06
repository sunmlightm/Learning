


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
- STATIC_URL:
  - 添加一行: STATICFILES_DIRS=[os.path.join(BASE_DIR,'static')]
  - 创建static文件夹
  - html中需要加载: {%load staticfiles%}

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

    class StudentInfo(models.Model):
        name=models.CharField(max_length=20,verbose_name='学生姓名')   #CharField=varchar,verbose_name:别名
        age=models.IntegerField(default=18,verbose_name='学生年龄')
        gender=models.CharField(choices=(('girl','女'),('boy ','男')),max_length=6,default='girl',verbose_name='学生性别')
        height=models.DecimalField(max_digits=5,decimal_places=2,verbose_name='学生身高')  #max_digits总位数,decimal_places小数位数
        image = models.ImageField(upload_to='user/%y/%m/%d',max_length=100,verbose_name='学生头像')  #upload_to上传到
        add_time=models.DateTimeField(default=datetime.now,verbose_name='添加时间') #datetime需要引入:from datetime import datetime
        is_delete=models.BooleanField(default=False,*****)
        def __str__(self):  #python2中是__Unicode__
            return self.name
        class Meta:
            # db_table=''  #设置在数据库中显示的名字,默认是app名+ _ +模型类名小写形式
            # ordering=[ '-age' ] #设置以某个字段进行排序, -表示倒序
            verbose_name='学生信息'
            verbose_name_plural=verbose_name #后台默认显示复数形式,加上这一行不会自动加s

- 使用内置表,为内置表添加内容:
  - from django.contrib.auth.models import AbstractUser
  - class UserProfile(AbstractUser):加需要增加的内容
  - def --str--(self):  &    class Meta:
  - 在seeting中指定默认用户表为自己创建的这个表:AUTH_USER_MODEL = 'users.UserProfile'

在pycharm--底部--Terminal中执行以下操作
- 生成迁移文件:python manage.py makemigrations
- 同步文件(将数据迁移到数据库中):python manage.py migrate

**单个数据库操作**

在pycharm--底部--PythonConsole中执行以下操作
**from students.models import StudentInfo

- **数据插入**
    - 方法一:
    - a=StudentInfo()
    - a.name='',a.age=''....
    - a.save()
    - 方法二:
    - stu=StudentInfo.objects.create(name='name',age='12'......)

- **查询**
  - all_students=StudentInfo.objects.all() 查询全部数据(class里需要有 _ _str__ () )
  - StudentInfo.objects.filter(+查询条件)
  - StudentInfo.objects.get(条件) ---只能获取一个,获取不到则报异常
  - filter(add_time__year)可以按addtime的年份查找

- **更改数据**
  - StudentInfo.objects.filter(过滤条件).update(age='')

- **删除数据**
  - StudentInfo.objects.filter(过滤条件).delete()


**创建管理员账号:**
- python manage.py createsuperuser

**admin.py**
- from .models import 数据表名
>
      class StudentInfoAdmin(admin.ModelAdmin):
        #配置列表页的字段显示
        list_display = ['name','age','gender','add_time']
        #配置添加搜索框
        search_fields = ['name','age','gender','add_time']
        #配置分页显示数据条数
        list_per_page = 1
        #配置过滤器
        list_filter = ['age','gender']
        #配置详情页的字段显示以及顺序
        fields = ['add_time','name']
      admin.site.register(StudentInfo,StudentInfoAdmin)

**重定向**: 引入包:from django.core.urlresolvers  import reverse
`例:return redirect(reverse('student:student_delete')) # redirect需要引入`


cookie:
- 获取: request.COOKIES.get('name',None)
- 设置: return HttpResponseRender(...)


#### HTML重用:
- base.html 父模板
  - {% block name%}
  - {% endblock %}
- 子html:
  - {% extend 'base.html' %}
  - {% block name%}
  - 重写的内容
  - {% endblock %}
