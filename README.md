# -
面试相关
第四部分 前端、框架和其他（155题）
1.	谈谈你对http协议的认识。
# 通过/r/n分割
# 请求头请求体之间：/r/n/r/n
# 无状态
# 短连接
2.	谈谈你对websocket协议的认识。
# a.什么是websocket？
    是给浏览器新建的一套协议
    协议规定:创建连接后不断开
    通过'\r\n'分割,让客户端和服务端创建连接后不断开、验证+数据加密
# b.本质:
# 就是一个创建连接后不断开的socket
# 当连接成功后:
    - 客户端(浏览器)会自动向服务端发送消息
    - 服务端接收后,会对该数据加密:base64(sha1(swk+magic_string))
    - 构造响应头
    - 发送给客户端
# 建立双工通道,进行收发数据
# c.框架中是如何使用websocket的？
    django：channel
    flask：gevent-websocket
    tornado：内置
# d.websocket的优缺点
    优点：代码简单，不再重复创建连接
    缺点：兼容性没有长轮询好，如IE会有不兼容
3.	什么是magic string ？
# 客户端向服务端发送消息时，会有一个'sec-websocket-key'和'magic string'的随机字符串(魔法字符串)
# 服务端接收到消息后会把他们连接成一个新的key串，进行编码、加密，确保信息的安全性







4.	如何创建响应式布局？
# a.可以通过引用Bootstrap实现
# b.通过看Bootstrap源码文件，可知其本质就是通过CSS实现的
 <style>
        /*浏览器窗口宽度大于768,背景色变为 green*/
        @media (min-width: 768px) {
            .pg-header{
                background-color: green;
            }
        }

        /*浏览器窗口宽度大于992,背景色变为 pink*/
        @media (min-width: 992px) {
            .pg-header{
                background-color: pink;
            }
        }
    </style>
</head>
<body>
<div class="pg-header"></div>
</body>
5.	你曾经使用过哪些前端框架？
# Jquery、Vue、Bootstrap、
6.	什么是ajax请求？并使用jQuery和XMLHttpRequest对象实现一个ajax请求。
http://www.cnblogs.com/wupeiqi/articles/5703697.html
7.	如何在前端实现轮训？
# 轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP request，
# 然后由服务器返回最新的数据给客户端的浏览器。
var xhr = new XMLHttpRequest();
    setInterval(function(){
        xhr.open('GET','/user');
        xhr.onreadystatechange = function(){

        };
        xhr.send();
    },1000)




8.	如何在前端实现长轮训？
# ajax实现:在发送ajax后,服务器端会阻塞请求直到有数据传递或超时才返回。 
# 客户端JavaScript响应处理函数会在处理完服务器返回的信息后，再次发出请求，重新建立连接。
    function ajax(){
        var xhr = new XMLHttpRequest();
        xhr.open('GET','/user');
        xhr.onreadystatechange = function(){
              ajax();
        };
        xhr.send();
    }
9.	vuex的作用？
1.不同组件之间共享状态，可以进行状态的修改和读取。
2.可以理解为是一个全局对象，所有页面都可以访问
3.还有比较重要的单一状态树管理，让数据的修改脉络更加清晰，便于定位问题。
# 比如用户做了一些加减的操作、三个页面都要用、可以用传参、但是很麻烦、这种时候用vuex就简单一些
10.	vue中的路由的拦截器的作用？
# 统一处理所有http请求和响应时，可以用axios的拦截器。
# 通过配置http response inteceptor，当后端接口返回401 Unauthorized（未授权），让用户重新登录。
# so可以用来做登录拦截验证
11.	axios的作用？
# axios是vue-resource后出现的Vue请求数据的插件
# 可以做的事情：
    从浏览器中创建 XMLHttpRequest
    从 node.js 发出 http 请求
    支持 Promise API
    拦截请求和响应
    转换请求和响应数据
    取消请求
    自动转换JSON数据
    客户端支持防止 CSRF/XSRF




12.	列举vue的常见指令。
#   1、v-if指令:判断指令，根据表达式值得真假来插入或删除相应的值。
#   2、v-show指令:
#     条件渲染指令，无论返回的布尔值是true还是false，元素都会存在html中，
#     false的元素会隐藏在html中，并不会删除.
#   3、v-else指令:配合v-if或v-else使用。
#   4、v-for指令:循环指令，相当于遍历。
#   5、v-bind:给DOM绑定元素属性。
#   6、v-on指令:监听DOM事件。
13.	简述jsonp及实现原理？
# 原理：
1、先在客户端注册一个callback, 然后把callback的名字传给服务器。 
2、此时，服务器先生成 json 数据。 
3、然后以 javascript 语法的方式，生成一个function , function 名字就是传递上来的参数 jsonp. 
4、最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。

客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时数据作为参数，
传入到了客户端预先定义好的 callback 函数里.（动态执行回调函数） 
# 注意
    # JSON 是一种数据格式
    # JSONP 是一种数据调用的方式













14.	是什么cors ？
跨域资源共享（Cross-Origin Resource Sharing）
其本质是设置响应头，使得浏览器允许跨域请求。

# 简单请求(一次请求)
1、请求方式：HEAD、GET、POST
2、请求头信息：
    Accept
    Accept-Language
    Content-Language
    Last-Event-ID
    Content-Type 对应的值是以下三个中的任意一个
                            application/x-www-form-urlencoded
                            multipart/form-data
                            text/plain
# 非简单请求(两次请求)
在发送真正的请求之前，会默认发送一个'options'请求，做'预检'，预检成功后才发送真正的请求
    # 预检：
    如果复杂请求是PUT等请求，则服务端需要设置允许某请求，否则“预检”不通过
        Access-Control-Request-Method
    如果复杂请求设置了请求头，则服务端需要设置允许某请求头，否则“预检”不通过
        Access-Control-Request-Headers
15.	列举Http请求中常见的请求方式？
# http请求方法有8种:
        'GET'
        'POST'
        'HEAD'
        'OPTIONS'
        'PUT'
        'DELETE'
        'TRACE'
        'CONNECT'






16.	列举Http请求中的状态码？
# 2开头（成功）
    200：请求成功
    202：已接受请求，尚未处理
    204：请求成功，且不需返回内容
# 3开头（重定向）
    301：永久重定向
    302：临时重定向
# 4开头（客户端错误）
    400（Bad Request）：请求的语义或是参数有错
    403（Forbidden）：服务器拒绝了请求(csrf)
    404（Not Found）：找不到页面(资源)
# 5开头（服务器错误）
    500：服务器遇到错误，无法完成请求
    502：网关错误，一般是服务器压力过大导致连接超时       
    503：服务器宕机
17.	列举Http请求中常见的请求头？
# 常见请求头：
User-Agent、Referer、Host、Cookie、Connection、Accept
18.	看图写结果：
 
李杰
19.	看图写结果：
 
武沛奇
20.	看图写结果：
 
老男孩
21.	看图写结果：
  
undefined
22.	看图写结果：
 
武沛奇
23.	看图写结果：
 
Alex
24.	django、flask、tornado框架的比较？
Django：
# 对于django来说，是一个大而全的框架，内部组件特别多，
# 例如：ORM、admin、Form、ModelForm、中间件、信号、缓存、csrf等；
Flask：
# flask是一个微型框架，但可扩展性很强；如果开发简单程序，使用flask比较快捷；
# 如果实现复杂功能，则需要引入一些组件；
# 例如：flask-session\flask-SQLAlchemy\wtforms\flask-migrate\flask-script\blinker

# 他们两个都基于wsgi协议实现的，但默认使用的wsgi模块是不一样的；
# （Django：wsigref  Flask：werkzurg）
# 还有一个显著的特点，他们处理请求方式不同：
　　# Django：通过将请求封装成Request对象，再通过参数进行传递。
　　# Flask：通过上下文管理机制实现。
　　# 对了，感觉Flask的上下文管理还是挺有意思的

Tornado
# 是一个轻量级的Web框架，异步非阻塞+内置WebSocket功能。
'目标'：通过一个线程处理N个并发请求(处理IO)。
'内部组件'
    #内部自己实现socket
    #路由系统 
    #视图 
    #模板 
    #cookie 
    #csrf


25.	什么是wsgi？
# 是web服务网关接口，是一套协议
#目前接触的：
# wsigref（Django，性能较低）
# werkzurg（Flask，性能较低）
# uwsig（性能较高、线上发布）

# 以上模块的本质：
#实现wsgi协议的模块本质上是写了一个socket服务端，用来监听用户请求；
#如果有请求进来，则将请求进行一次封装，然后将封装后的请求交给web框架进行后续处理。
26.	django请求的生命周期？
# 1、请求进来
# 2、走到wsgi
# 3、走到中间件
# 4、路由匹配
# 5、执行相应的视图函数，ORM数据库操作
# 6、模板渲染成字符串
# 7、再经过中间件走回wsgi
 
27.	列举django的内置组件？
Django中内置组件
#例如：ORM、admin、Form、ModelForm、中间件、信号、缓存、csrf等，
#这些都是django内置的组件
哪个组件最好，最熟悉？
#我感觉不能单说哪个组件最好，因为他们各有所长，单独拿出来进行比较不合适；
#ORM用的最多，因为只要涉及到数据操作，基本都会用到ORM
28.	列举django中间件的5个方法？以及django中间件的应用场景？
# 作用
# 对所有的请求进行批量处理，在视图函数执行前后进行自定义操作。
1、process_request(self, request)
2、process_view(self, request, callback, callback_args, callback_kwargs)
3、process_template_response(self, request, response)
    （当视图函数返回值对象中有render方法时，该方法才会被调用。）
4、process_exception(self, request, exception)
5、process_response(self, request, response)
# 应用场景
　　- '登录验证'
　　- '权限处理'
　　- 'CORS跨域'
　　- 还有一些'内置'的：
　　　　　- csrf？
　　　　　- session？
　　　　　- 全站缓存(中间件2/4)（见下图）？
　　- 另外还有一个就是处理跨域（前后端分离时，本地测试开发时使用的）
 








29.	简述什么是FBV和CBV？
FBV
def index(request):
　　pass
CBV（源码中走的 as_view）
class IndexView(View):
路由：IndexView.as_view()
他们两个有啥区别？
首先，我认为没什么区别，他们的本质都是函数。
因为CBV中.as_view()返回的是view函数，view函数中调用类的dispatch方法；
在dispatch方法中通过反射执行get/post/delete/put等方法。

如果非要说区别的话，CBV比较简洁，它的GET/POST等业务功能分别放在不同get/post函数中。
而FBV则自己做判断进行区分。
遇到的难题：
CBV是添加csrf装饰器，要加到dispatch
多数据库配置 allow_relation方法，存在bug
30.	django的request对象是在什么时候创建的？
# 当请求一个页面时, Django会建立一个包含请求元数据的 HttpRequest 对象. 
# 当Django 加载对应的视图时, HttpRequest对象将作为视图函数的第一个参数. 
# 每个视图会返回一个HttpResponse对象.
31.	如何给CBV的程序添加装饰器？
'常规添加装饰器'
  from django.views import View
  from django.utils.decorators import method_decorator
  def auth(func):
      def inner(*args,**kwargs):
          return func(*args,**kwargs)
      return inner
  class UserView(View):                       
      @method_decorator(auth)
      def get(self,request,*args,**kwargs):
          return HttpResponse('...')
'csrf的装饰器要加到dispath'
      from django.views import View
      from django.utils.decorators import method_decorator
      from django.views.decorators.csrf import csrf_exempt,csrf_protect
      class UserView(View):
          @method_decorator(csrf_exempt)
          def dispatch(self, request, *args, **kwargs):
              return HttpResponse('...')  
  '或加在外面'
      @method_decorator(csrf_exempt,name='dispatch')
      class UserView(View):
          def dispatch(self, request, *args, **kwargs):
              return HttpResponse('...')
32.	列举django orm 中所有的方法（QuerySet对象的所有方法）
返回QuerySet对象的方法有：
      all()
      filter()
      exclude()
      order_by()
      reverse()
      distinct()
特殊的QuerySet：
      values()       返回一个可迭代的字典序列
      values_list() 返回一个可迭代的元组序列
返回具体对象的：
      get()
      first()
      last()
返回布尔值的方法有：
      exists()
返回数字的方法有：
      count()
33.	only和defer的区别？
def defer(self, *fields):
     #映射中排除某列数据
     models.UserInfo.objects.defer('username','id')
    或
     models.UserInfo.objects.filter(...).defer('username','id')
    
 def only(self, *fields):
    #仅取某个表中的数据
     models.UserInfo.objects.only('username','id')
     或
     models.UserInfo.objects.filter(...).only('username','id')




34.	select_related和prefetch_related的区别？
# 他俩都用于连表查询，减少SQL查询次数
\select_related
select_related主要针一对一和多对一关系进行优化，通过多表join关联查询，一次性获得所有数据，
存放在内存中，但如果关联的表太多，会严重影响数据库性能。
def index(request):
    obj = Book.objects.all().select_related("publisher")
    return render(request, "index.html", locals())
\prefetch_related
prefetch_related是通过分表，先获取各个表的数据，存放在内存中，然后通过Python处理他们之间的关联。
def index(request):
    obj = Book.objects.all().prefetch_related("publisher")
    return render(request, "index.html", locals())
35.	filter和exclude的区别？
def filter(self, *args, **kwargs)
    # 条件查询(符合条件)
    # 条件可以是：参数，字典，Q
def exclude(self, *args, **kwargs)
    # 条件查询(排除条件)
    # 条件可以是：参数，字典，Q
36.	列举django orm中三种能写sql语句的方法。
1.使用execute执行自定义SQL
# from django.db import connection, connections
# cursor = connection.cursor()  # cursor = connections['default'].cursor()
# cursor.execute(''SELECT * from auth_user where id = %s'', [1])
# row = cursor.fetchone()
2.使用extra方法 
# extra(self, select=None, where=None, params=None, tables=None, order_by=None, select_params=None)
# Entry.objects.extra(select={'new_id': "select id from tb where id > %s"}, select_params=(1,), order_by=['-nid'])
# Entry.objects.extra(where=['headline=%s'], params=['Lennon'])
3.使用raw方法
　　解释：执行原始sql并返回模型
　　说明：依赖model多用于查询
　　用法：
　　　　book = Book.objects.raw("select * from hello_book")
　　　　for item in book:
　　　　　　print(item.title)
37.	django orm 中如何设置读写分离？
# 配置数据库
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    },
    'db2': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db2.sqlite3'),
    },
}

# 创建models并执行数据库迁移
   ……
# 读写分离
在使用数据库时，通过.using(db_name)来手动指定要使用的数据库
def write(request):
    models.Products.objects.using('default').create(name='公仔', price=12.99)
    return HttpResponse('写入成功')
def read(request):
    obj = models.Products.objects.filter(id=1).using('db2').first()
    return HttpResponse(obj.prod_name)
38.	F和Q的作用?
F查询主要用来获取原数据进行计算，对象和常数之间的加减乘除和取模的操作
# 例如：
Goods.objects.update(price=F("price")+10)
# 对于goods表中每件商品的价格都在原价格的基础上增加10元

Q查询主要用来进行复杂查询，
Q(条件1) | Q(条件2)或
Q(条件1) & Q(条件2)且
Q(条件1) & ~Q(条件2)非
Book.objects.filter(Q(id=3)|Q(title="Go"))[0] 
# 查询id=3或者标题是“Go”的书
39.	values和values_list的区别？
values() #返回一个可迭代的字典序列
values_list() #返回一个可迭代的元组序列


40.	如何使用django orm批量创建数据？
# 使用bulk_create批量插入
def bulk_create(self, objs, batch_size=None):
   # batch_size表示一次插入的个数
   objs = [
      models.DDD(name='r11'),
      models.DDD(name='r22')
   ]
   models.DDD.objects.bulk_create(objs, 10)
41.	django的Form和ModeForm的作用？
# 作用：
- 对用户请求数据格式进行校验
- 自动生成HTML标签

# 区别：
Form，字段需要自己手写。
class Form(Form):
   xx = fields.CharField(.)
   xx = fields.CharField(.)
   xx = fields.CharField(.)
   xx = fields.CharField(.)

ModelForm，可以通过Meta进行定义
class MForm(ModelForm):
   class Meta:
      fields = "__all__"
      model = UserInfo
# 应用：只要是客户端向服务端发送表单数据时，都可以进行使用，如：用户登录注册
# 问题：choice的数据如果从数据库获取可能会造成数据无法实时更新
# 答案：重写构造方法，在构造方法中重新去数据库获取值。








42.	django的Form组件中如果字段中包含choices参数请使用两种方式实现数据源实时更新
# 方式一: 重写构造方法，在构造方法中重新去数据库获取值
class UserForm(Form):
   name = fields.CharField(label='用户名', max_length=32)
   email = fields.EmailField(label='邮箱')
   ut_id = fields.ChoiceField(
      # choices=[(1,'二B用户'),(2,'山炮用户')]
      choices=[])
   def __init__(self, *args, **kwargs):
      super(UserForm, self).__init__(*args, **kwargs)
      self.fields['ut_id'].choices = models.UserType.objects.all().values_list('id', 'title')

# 方式二: ModelChoiceField字段
from django.forms import Form
from django.forms import fields
from django.forms.models import ModelChoiceField
class UserForm(Form):
   name = fields.CharField(label='用户名', max_length=32)
   email = fields.EmailField(label='邮箱')
   ut_id = ModelChoiceField(queryset=models.UserType.objects.all())

# 依赖：
class UserType(models.Model):
   title = models.CharField(max_length=32)
   def __str__(self):
      return self.title
43.	django的Model中的ForeignKey字段中的on_delete参数有什么作用？
on_delete有[CASCADE、PROTECT、SET_NULL、SET_DEFAULT、SET()]
五个可选择的值
CASCADE：#此值设置，是级联删除。
PROTECT：#此值设置，是会报完整性错误。
SET_NULL：#此值设置，会把外键设置为null，前提是允许为null。
SET_DEFAULT：#此值设置，会把设置为外键的默认值。
SET()：#此值设置，会调用外面的值，可以是一个函数。





44.	django中csrf的实现机制？
1、在用户访问时，django反馈给用户的表单中有一个隐含字段csrftoken，
这个值是在服务器端随机生成的，每一次提交表单都会生成不同的值
2、服务器校验这个表单的csrftoken是否和自己保存的一致，来判断用户的合法性
3、当用户被csrf攻击,从其他站点发送精心编制的攻击请求时，
   由于其他站点不可能知道隐藏的csrftoken字段的信息,
   这样在服务器端就会校验失败，攻击被成功防御
具体配置如下：
template中添加{ % csrf_token %}标签
45.	django如何实现websocket？
django中可以通过channel实现websocket
46.	基于django使用ajax发送post请求时，都可以使用哪种方法携带csrf token？
Data、header、 ajaxSetup()
47.	django中如何实现orm表中添加数据时创建一条日志记录。
使用django的信号机制，可以在添加、删除数据前后设置日志记录
pre_init  # Django中的model对象执行其构造方法前,自动触发
post_init  # Django中的model对象执行其构造方法后,自动触发
pre_save  # Django中的model对象保存前,自动触发
post_save  # Django中的model对象保存后,自动触发
pre_delete  # Django中的model对象删除前,自动触发
post_delete  # Django中的model对象删除后,自动触发
48.	django缓存如何设置？
三种粒度缓存
# 1、中间件级别
'django.middleware.cache.UpdateCacheMiddleware',
'django.middleware.cache.FetchFromCacheMiddleware',
CACHE_MIDDLEWARE_SECONDS = 10
# 2、视图级别
from django.views.decorators.cache import cache_page
@cache_page(15)
def index(request):
import time
t = time.time()
return render(request, "index.html", locals())
# 3、局部缓存
{ % loadcache %}
...
{ % cache 15 "time_cache" %}
< h3 > 缓存时间: {{t}} < / h3 >
{ % endcache %}
49.	django的缓存能使用redis吗？如果可以的话，如何配置？
pip install django-redis
然后在settings.py里面添加：
CACHES = {
'default': {
   'BACKEND': 'redis_cache.cache.RedisCache',
   'LOCATION': '127.0.0.1:6379',
   "OPTIONS": {
      "CLIENT_CLASS": "redis_cache.client.DefaultClient",
   },
}
50.	django路由系统中name的作用？
路由系统中name的作用：反向解析
url(r'^home', views.home, name='home')
在模板中使用：{ % url 'home' %}
在视图中使用：reverse(“home”）
51.	django的模板中filter和simple_tag的区别？
1、模板继承：{ % extends 'layouts.html' %}
2、自定义方法
  	 'filter'：只能传递两个参数，可以在if、for语句中使用
  	 'simple_tag'：可以无线传参，不能在if for中使用
  	 'inclusion_tags'：可以使用模板和后端数据
3、防xss攻击： '|safe'、'mark_safe'
52.	django-debug-toolbar的作用？
一、查看访问的速度、数据库的行为、cache命中等信息。 
二、尤其在Mysql访问等的分析上大有用处(sql查询速度)
https://blog.csdn.net/weixin_39198406/article/details/78821677
53.	django中如何实现单元测试？
https://www.jianshu.com/p/34267dd79ad6
54.	解释orm中 db first 和 code first的含义？
db first: 先创建数据库，再更新表模型
code first：先写表模型，再更新数据库
55.	django中如何根据数据库表生成model中的类？
1、修改seting文件，在setting里面设置要连接的数据库类型和名称、地址
2、运行下面代码可以自动生成models模型文件
   	- python manage.py inspectdb
3、创建一个app执行下下面代码：
   	- python manage.py inspectdb > app/models.py 
56.	使用orm和原生sql的优缺点？
SQL：
# 优点：
执行速度快
# 缺点：
编写复杂，开发效率不高
---------------------------------------------------------------------------
ORM：
# 优点：
让用户不再写SQL语句，提高开发效率
可以很方便地引入数据缓存之类的附加功能
# 缺点：
在处理多表联查、where条件复杂查询时，ORM的语法会变得复杂。
没有原生SQL速度快
57.	简述MVC和MTV
MVC：model、view(模块)、controller(视图)
MTV：model、tempalte、view 
58.	django的contenttype组件的作用？
contenttype是django的一个组件(app)，它可以将django下所有app下的表记录下来
可以使用他再加上表中的两个字段,实现一张表和N张表动态创建FK关系。
   - 字段：表名称
   - 字段：数据行ID
应用：路飞表结构优惠券和专题课和学位课关联
59.	谈谈你对restfull 规范的认识？
restful其实就是一套编写接口的'协议'，规定如何编写以及如何设置返回值、状态码等信息。
# 最显著的特点：
# 用restful: 
    给用户一个url，根据method不同在后端做不同的处理
    比如：post创建数据、get获取数据、put和patch修改数据、delete删除数据。
# 不用restful: 
    给调用者很多url，每个url代表一个功能，比如：add_user/delte_user/edit_user/
# 当然，还有协议其他的，比如：
    '版本'来控制让程序有多个版本共存的情况，版本可以放在 url、请求头（accept/自定义）、GET参数
    '状态码'200/300/400/500
    'url中尽量使用名词'restful也可以称为“面向资源编程”
    'api标示'
        api.luffycity.com
        www.luffycity.com/api/
60.	接口的幂等性是什么意思？
'一个接口通过1次相同的访问，再对该接口进行N次相同的访问时，对资源不造影响就认为接口具有幂等性。'
    GET，  #第一次获取结果、第二次也是获取结果对资源都不会造成影响，幂等。
    POST， #第一次新增数据，第二次也会再次新增，非幂等。
    PUT，  #第一次更新数据，第二次不会再次更新，幂等。
    PATCH，#第一次更新数据，第二次不会再次更新，非幂等。
    DELTE，#第一次删除数据，第二次不在再删除，幂等。
61.	什么是RPC？
'远程过程调用协议'
是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。
进化的顺序: 现有的RPC,然后有的RESTful规范
62.	Http和Https的区别？
#Http: 80端口
#https: 443端口
# http信息是明文传输，https则是具有安全性的ssl加密传输协议。
#- 自定义证书 
    - 服务端：创建一对证书
    - 客户端：必须携带证书
#- 购买证书
    - 服务端： 创建一对证书，。。。。
    - 客户端： 去机构获取证书，数据加密后发给咱们的服务单
    - 证书机构:公钥给改机构
63.	为什么要使用django rest framework框架？
# 在编写接口时可以不使用django rest framework框架，
# 不使用：也可以做，可以用django的CBV来实现，开发者编写的代码会更多一些。
# 使用：内部帮助我们提供了很多方便的组件，我们通过配置就可以完成相应操作，如：
    '序列化'可以做用户请求数据校验+queryset对象的序列化称为json
    '解析器'获取用户请求数据request.data，会自动根据content-type请求头的不能对数据进行解析
    '分页'将从数据库获取到的数据在页面进行分页显示。
     # 还有其他组件：
         '认证'、'权限'、'访问频率控制





64.	django rest framework框架中都有那些组件？
#- 路由，自动帮助开发者快速为一个视图创建4个url
        www.oldboyedu.com/api/v1/student/$
        www.oldboyedu.com/api/v1/student(?P<format>\w+)$
        www.oldboyedu.com/api/v1/student/(?P<pk>\d+)/$
        www.oldboyedu.com/api/v1/student/(?P<pk>\d+)(?P<format>\w+)$
#- 版本处理
    - 问题：版本都可以放在那里？
            - url
            - GET 
            - 请求头 
#- 认证 
    - 问题：认证流程？
#- 权限 
    - 权限是否可以放在中间件中？以及为什么？
#- 访问频率的控制
    匿名用户可以真正的防止？无法做到真正的访问频率控制，只能把小白拒之门外。
    如果要封IP，使用防火墙来做。
    登录用户可以通过用户名作为唯一标示进行控制，如果有人注册很多账号，则无法防止。
#- 视图
#- 解析器 ，根据Content-Type请求头对请求体中的数据格式进行处理。request.data 
#- 分页
#- 序列化
    - 序列化
        - source
        - 定义方法
    - 请求数据格式校验
#- 渲染器
65.	django rest framework框架中的视图都可以继承哪些类？
#a. 继承 APIView
    # 这个类属于rest framework中顶层类，内部帮助我们实现了一些基本功能：
        # 认证、权限、频率控制，但凡是数据库、分页等操作都需要手动去完成，比较原始。
#b. 继承 GenericViewSet(ViewSetMixin, GenericAPIView)
    # 如果继承它之后，路由中的as_view需要填写对应关系 ---> .as_view({'get':'list','post':'create'})
    # 在内部也帮助我们提供了一些方便的方法：
        - get_queryset
        - get_object
        - get_serializer
    注意：要设置queryset字段，否则会抛出断言的异常。
#c. 继承ModelViewSet(根据继承可以对数据直接增\删\改\查)
    # 对数据库和分页等操作不用我们在编写，只需要继承相关类即可。
66.	简述 django rest framework框架的认证流程。
如何编写？'写类并实现authticate'
方法中可以定义三种返回值：
    - [user,auth]，认证成功
    - None , 匿名用户
    - 异常 ，认证失败
流程：
    - 先到dispatch 、再去request中进行认证处理
67.	django rest framework如何实现的用户访问频率控制？
# 对匿名用户，根据用户IP或代理IP作为标识进行记录，为每个用户在redis中建一个列表
    {
        throttle_1.1.1.1:[1526868876.497521,152686885.497521...]，
        throttle_1.1.1.2:[1526868876.497521,152686885.497521...]，
        throttle_1.1.1.3:[1526868876.497521,152686885.497521...]，
    } 
 每个用户再来访问时，需先去记录中剔除过期记录，再根据列表的长度判断是否可以继续访问。
 '如何封IP'：在防火墙中进行设置
--------------------------------------------------------------------------
# 对注册用户，根据用户名或邮箱进行判断。
    {
        throttle_xxxx1:[1526868876.497521,152686885.497521...]，
        throttle_xxxx2:[1526868876.497521,152686885.497521...]，
        throttle_xxxx3:[1526868876.497521,152686885.497521...]，
    }
每个用户再来访问时，需先去记录中剔除过期记录，再根据列表的长度判断是否可以继续访问。
\如1分钟：40次，列表长度限制在40，超过40则不可访问
68.	Flask框架的优势？
Flask自由、灵活，可扩展性强，透明可控，第三方库的选择面广，
开发时可以结合最流行最强大的Python库，
69.	Flask框架依赖组件？
# 依赖jinja2模板引擎
# 依赖werkzurg协议
70.	Flask蓝图的作用？
# blueprint把实现不同功能的module分开.也就是把一个大的App分割成各自实现不同功能的module.
# 在一个blueprint中可以调用另一个blueprint的视图函数, 但要加相应的blueprint名.
71.	列举使用过的Flask第三方组件？
# Flask组件
    flask-session  session放在redis
    flask-SQLAlchemy 如django里的ORM操作
    flask-migrate  数据库迁移
    flask-script  自定义命令
    blinker  信号-触发信号
# 第三方组件
    Wtforms 快速创建前端标签、文本校验
    dbutile	 创建数据库连接池
    gevnet-websocket 实现websocket
# 自定义Flask组件
    自定义auth认证 
    参考flask-login组件
72.	简述Flask上下文管理流程?
# a、简单来说，falsk上下文管理可以分为三个阶段：
　　1、'请求进来时'：将请求相关的数据放入上下问管理中
　　2、'在视图函数中'：要去上下文管理中取值
　　3、'请求响应'：要将上下文管理中的数据清除
# b、详细点来说：
　　1、'请求刚进来'：
        将request，session封装在RequestContext类中
        app，g封装在AppContext类中
        并通过LocalStack将requestcontext和appcontext放入Local类中
　　2、'视图函数中'：
        通过localproxy--->偏函数--->localstack--->local取值
　　3、'请求响应时'：
        先执行save.session()再各自执行pop(),将local中的数据清除
73.	Flask中的g的作用？
# g是贯穿于一次请求的全局变量，当请求进来将g和current_app封装为一个APPContext类，
# 再通过LocalStack将Appcontext放入Local中，取值时通过偏函数在LocalStack、local中取值；
# 响应时将local中的g数据删除：
74.	Flask中上下文管理主要涉及到了那些相关的类？并描述类主要作用？
RequestContext  #封装进来的请求（赋值给ctx）
AppContext      #封装app_ctx
LocalStack      #将local对象中的数据维护成一个栈（先进后出）
Local           #保存请求上下文对象和app上下文对象

75.	为什么要Flask把Local对象中的值stack 维护成一个列表？
# 因为通过维护成列表，可以实现一个栈的数据结构，进栈出栈时只取一个数据，巧妙的简化了问题。
# 还有，在多app应用时，可以实现数据隔离；列表里不会加数据，而是会生成一个新的列表
# local是一个字典，字典里key（stack）是唯一标识，value是一个列表
76.	Flask中多app应用是怎么完成？
请求进来时，可以根据URL的不同，交给不同的APP处理。蓝图也可以实现。
    #app1 = Flask('app01')
    #app2 = Flask('app02')
    #@app1.route('/index')
    #@app2.route('/index2')
源码中在DispatcherMiddleware类里调用app2.__call__，
  原理其实就是URL分割，然后将请求分发给指定的app。
之后app也按单app的流程走。就是从app.__call__走。
77.	在Flask中实现WebSocket需要什么组件？
# gevent-websocket
78.	wtforms组件的作用？
#快速创建前端标签、文本校验；如django的ModelForm
79.	Flask框架默认session处理机制？
# 前提:
    不熟的话:记不太清了,应该是……分两个阶段吧   
# 创建:
    当请求刚进来的时候,会将request和session封装成一个RequestContext()对象,
    接下来把这个对象通过LocalStack()放入内部的一个Local()对象中;
　　 因为刚开始 Local 的ctx中session是空的;
　　 所以,接着执行open_session,将cookie 里面的值拿过来,重新赋值到ctx中
    (Local实现对数据隔离,类似threading.local) 
# 销毁:
    最后返回时执行 save_session() 将ctx 中的session读出来进行序列化,写到cookie
    然后给用户,接着把 ctx pop掉





80.	解释Flask框架中的Local对象和threading.local对象的区别？
# a.threading.local
作用：为每个线程开辟一块空间进行数据存储(数据隔离)。

问题：自己通过字典创建一个类似于threading.local的东西。
storage = {
   4740: {val: 0},
   4732: {val: 1},
   4731: {val: 3},
   }

# b.自定义Local对象
作用：为每个线程(协程)开辟一块空间进行数据存储(数据隔离)。
class Local(object):
   def __init__(self):
      object.__setattr__(self, 'storage', {})
   def __setattr__(self, k, v):
      ident = get_ident()
      if ident in self.storage:
         self.storage[ident][k] = v
      else:
         self.storage[ident] = {k: v}
   def __getattr__(self, k):
      ident = get_ident()
      return self.storage[ident][k]
obj = Local()
def task(arg):
   obj.val = arg
   obj.xxx = arg
   print(obj.val)
for i in range(10):
   t = Thread(target=task, args=(i,))
   t.start()







81.	Flask中blinker 是什么？
# flask中的信号blinker
信号主要是让开发者可是在flask请求过程中定制一些行为。
或者说flask在列表里面预留了几个空列表，在里面存东西。
简言之，信号允许某个'发送者'通知'接收者'有事情发生了
@ before_request有返回值，blinker没有返回值
# 10个信号
request_started = _signals.signal('request-started') #请求到来前执行
request_finished = _signals.signal('request-finished') #请求结束后执行
before_render_template = _signals.signal('before-render-template')#模板渲染前执行
template_rendered = _signals.signal('template-rendered')#模板渲染后执行
got_request_exception = _signals.signal('got-request-exception') #请求执行出现异常时执行
request_tearing_down = _signals.signal('request-tearing-down')#请求执行完毕后自动执行（无论成功与否）
appcontext_tearing_down = _signals.signal('appcontext-tearing-down')# 请求上下文执行完毕后自动执行（无论成功与否）
appcontext_pushed = _signals.signal('appcontext-pushed') #请求app上下文push时执行
appcontext_popped = _signals.signal('appcontext-popped') #请求上下文pop时执行
message_flashed = _signals.signal('message-flashed')#调用flask在其中添加数据时，自动触发
82.	SQLAlchemy中的 session和scoped_session 的区别？
# Session：
由于无法提供线程共享功能，开发时要给每个线程都创建自己的session
打印sesion可知他是sqlalchemy.orm.session.Session的对象
# scoped_session：
为每个线程都创建一个session，实现支持线程安全
在整个程序运行的过程当中，只存在唯一的一个session对象。
创建方式:
   通过本地线程Threading.Local()
   # session=scoped_session(Session)
   创建唯一标识的方法(参考flask请求源码)
83.	 SQLAlchemy如何执行原生SQL？
# 使用execute方法直接操作SQL语句(导入create_engin、sessionmaker)
engine=create_engine('mysql://root:*****@127.0.0.1/database?charset=utf8')
DB_Session = sessionmaker(bind=engine)
session = DB_Session()
session.execute('alter table mytablename drop column mycolumn ;')
84.	ORM的实现原理？
# ORM的实现基于一下三点
映射类：描述数据库表结构，
映射文件：指定数据库表和映射类之间的关系
数据库配置文件：指定与数据库连接时需要的连接信息(数据库、登录用户名、密码or连接字符串)
85.	DBUtils模块的作用？
# 数据库连接池
使用模式：
1、为每个线程创建一个连接，连接不可控，需要控制线程数
2、创建指定数量的连接在连接池，当线程访问的时候去取，不够了线程排队，直到有人释放(推荐)
---------------------------------------------------------------------------
两种写法：
1、用静态方法装饰器，通过直接执行类的方法来连接使用数据库
2、通过实例化对象，通过对象来调用方法执行语句
https://www.cnblogs.com/ArmoredTitan/p/Flask.html
86.	以下SQLAlchemy的字段是否正确？如果不正确请更正：
from datetime import datetime
from sqlalchemy.ext.declarative
import declarative_base
from sqlalchemy import Column, Integer, String, DateTime

Base = declarative_base()
class UserInfo(Base):
    __tablename__ = 'userinfo'   
    id = Column(Integer, primary_key=True, autoincrement=True)
    name = Column(String(64), unique=True)
ctime = Column(DateTime, default=datetime.now())
-----------------------------------------------------------------------
不正确：
	Ctime字段中参数应为’default=datetime.now’
	now 后面不应该加括号，加了的话，字段不会实时更新。
87.	SQLAchemy中如何为表设置引擎和字符编码？
sqlalchemy设置编码字符集，一定要在数据库访问的URL上增加'charset=utf8'
否则数据库的连接就不是'utf8'的编码格式

eng=create_engine('mysql://root:root@localhost:3306/test2?charset=utf8',echo=True)
88.	SQLAchemy中如何设置联合唯一索引？
通过'UniqueConstraint'字段来设置联合唯一索引
__table_args=(UniqueConstraint('h_id','username',name='_h_username_uc'))
#h_id和username组成联合唯一约束
89.	简述Tornado框架的特点。
异步非阻塞+websocket
90.	简述Tornado框架中Future对象的作用？
# 实现异步非阻塞
视图函数yield一个futrue对象，futrue对象默认：
    self._done = False   ，请求未完成
    self._result = None  ，请求完成后返回值，用于传递给回调函数使用。

tornado就会一直去检测futrue对象的_done是否已经变成True。

如果IO请求执行完毕，自动会调用future的set_result方法：
            self._result = result
            self._done = True
参考：http://www.cnblogs.com/wupeiqi/p/6536518.html（自定义异步非阻塞web框架）
91.	Tornado框架中如何编写WebSocket程序？？？？？？？？？？？？
Tornado在websocket模块中提供了一个WebSocketHandler类。
这个类提供了和已连接的客户端通信的WebSocket事件和方法的钩子。
当一个新的WebSocket连接打开时，open方法被调用，
而on_message和on_close方法，分别在连接、接收到新的消息和客户端关闭时被调用。

此外，WebSocketHandler类还提供了write_message方法用于向客户端发送消息，close方法用于关闭连接。
92.	Tornado中静态文件是如何处理的？如： 
<link href="{{static_url("commons.css")}}" rel="stylesheet" />
# settings.py
settings = {
    "static_path": os.path.join(os.path.dirname(__file__), "static"),
   # 指定了静态文件的位置在当前目录中的"static"目录下
    "cookie_secret": "61oETzKXQAGaYdkL5gEmGeJJFuYh7EQnp2XdTP1o/Vo=",
    "login_url": "/login",
    "xsrf_cookies": True,
}

经上面配置后
static_url()自动去配置的路径下找'commons.css'文件
93.	Tornado操作MySQL使用的模块？
torndb
torndb是基于mysqldb的再封装，所以使用时要先安装myqldb

94.	Tornado操作redis使用的模块？
tornado-redis
95.	简述Tornado框架的适用场景？
web聊天室，在线投票
96.	git常见命令作用：
# git init
    初始化，当前所在的文件夹可以被管理且以后版本相关的数据都会存储到.git文件中
# git status
    查看当前文件夹以及子目录中文件是否发生变化：
    内容修改/新增文件/删除，已经变化的文件会变成红色，已经add的文件会变成绿色
# git add .
    给发生变化的文件（贴上一个标签）或 将发生变化的文件放到某个地方，
    只写一个句点符就代表把git status中红色的文件全部打上标签
# git commit -m
    新增用户登录认证功能以及xxx功能将“绿色”文件添加到版本中
# git log
    查看所有版本提交记录，可以获取版本号
# git reset --hard 版本号   
    将最新的版本回退到更早的版本
# git reflog   
    回退到之前版本后悔了，再更新到最新或者最新之前的版本
# git reset --hard 版本 回退
97.	简述以下git中stash命令作用以及相关其他命令。
'git stash'：将当前工作区所有修改过的内容存储到“某个地方”，将工作区还原到当前版本未修改过的状态
'git stash list'：查看“某个地方”存储的所有记录
'git stash clear'：清空“某个地方”
'git stash pop'：将第一个记录从“某个地方”重新拿到工作区（可能有冲突）
'git stash apply'：编号, 将指定编号记录从“某个地方”重新拿到工作区（可能有冲突） 
'git stash drop'：编号，删除指定编号的记录
98.	git 中 merge 和 rebase命令的区别。
merge：
会将不同分支的提交合并成一个新的节点，之前的提交分开显示，
注重历史信息、可以看出每个分支信息，基于时间点,遇到冲突,手动解决,再次提交
rebase：
将两个分支的提交结果融合成线性，不会产生新的节点;
注重开发过程，遇到冲突，手动解决，继续操作


99.	公司如何基于git做的协同开发？
1、你们公司的代码review分支怎么做？谁来做？
答：组长创建review分支，我们小功能开发完之后，合并到review分支交给老大（小组长）来看，
1.1、你组长不开发代码吗？
        他开发代码，但是它只开发核心的东西，任务比较少。
        或者抽出时间，我们一起做这个事情
2、你们公司协同开发是怎么协同开发的？
每个人都有自己的分支，阶段性代码完成之后，合并到review，然后交给老大看
--------------------------------------------------------------------------
# 大致工作流程
公司：
    下载代码
        git clone https://gitee.com/wupeiqi/xianglong.git
        或创建目录 
        cd 目录 
        git init 
        git remote add origin https://gitee.com/wupeiqi/xianglong.git
        git pull origin maste 
    创建dev分支
        git checkout dev 
        git pull origin dev 
        继续写代码
        git add . 
        git commit -m '提交记录'
        git push origin dev 
回家： 
    拉代码：
        git pull origin dev 
    继续写：
        继续写代码
        git add . 
        git commit -m '提交记录'
        git push origin dev 
100.	如何基于git实现代码review？
https://blog.csdn.net/june_y/article/details/50817993
101.	git如何实现v1.0 、v2.0 等版本的管理？
在命令行中，使用“git tag –a tagname –m “comment”可以快速创建一个标签。
需要注意，命令行创建的标签只存在本地Git库中，还需要使用Git push –tags指令发布到服务器的Git库中

102.	什么是gitlab？
gitlab是公司自己搭建的项目代码托管平台
103.	github和gitlab的区别？
1、gitHub是一个面向开源及私有软件项目的托管平台
(创建私有的话，需要购买，最低级的付费为每月7刀，支持5个私有项目)
2、gitlab是公司自己搭建的项目托管平台
104.	如何为github上牛逼的开源项目贡献代码？
1、fork需要协作项目
2、克隆/关联fork的项目到本地
3、新建分支（branch）并检出（checkout）新分支
4、在新分支上完成代码开发
5、开发完成后将你的代码合并到master分支
6、添加原作者的仓库地址作为一个新的仓库地址
7、合并原作者的master分支到你自己的master分支,用于和作者仓库代码同步
8、push你的本地仓库到GitHub
9、在Github上提交 pull requests
10、等待管理员（你需要贡献的开源项目管理员）处理
105.	git中 .gitignore文件的作用?
一般来说每个Git项目中都需要一个“.gitignore”文件，
这个文件的作用就是告诉Git哪些文件不需要添加到版本管理中。

实际项目中，很多文件都是不需要版本管理的，比如Python的.pyc文件和一些包含密码的配置文件等等。
106.	什么是敏捷开发？
'敏捷开发'：是一种以人为核心、迭代、循序渐进的开发方式。

它并不是一门技术，而是一种开发方式，也就是一种软件开发的流程。
它会指导我们用规定的环节去一步一步完成项目的开发。
因为它采用的是迭代式开发，所以这种开发方式的主要驱动核心是人
107.	简述 jenkins 工具的作用?
'Jenkins'是一个可扩展的持续集成引擎。

主要用于：
   持续、自动地构建/测试软件项目。
   监控一些定时执行的任务。
108.	公司如何实现代码发布？
nginx+uwsgi+django(点击查看详情)

109.	简述 RabbitMQ、Kafka、ZeroMQ的区别？
点击查看
110.	RabbitMQ如何在消费者获取任务后未处理完前就挂掉时，保证数据不丢失？
为了预防消息丢失，rabbitmq提供了ack
即工作进程在收到消息并处理后，发送ack给rabbitmq，告知rabbitmq这时候可以把该消息从队列中删除了。
如果工作进程挂掉 了，rabbitmq没有收到ack，那么会把该消息 重新分发给其他工作进程。
不需要设置timeout，即使该任务需要很长时间也可以处理。

ack默认是开启的，工作进程显示指定了no_ack=True
参考
111.	RabbitMQ如何对消息做持久化？
1、创建队列和发送消息时将设置durable=Ture，如果在接收到消息还没有存储时，消息也有可能丢失，就必须配置publisher confirm
    channel.queue_declare(queue='task_queue', durable=True)

2、返回一个ack，进程收到消息并处理完任务后，发给rabbitmq一个ack表示任务已经完成，可以删除该任务

3、镜像队列：将queue镜像到cluster中其他的节点之上。
在该实现下，如果集群中的一个节点失效了，queue能自动地切换到镜像中的另一个节点以保证服务的可用性
112.	RabbitMQ如何控制消息被消费的顺序？
默认消息队列里的数据是按照顺序被消费者拿走，
例如：消费者1 去队列中获取奇数序列的任务，消费者2去队列中获取偶数序列的任务。

channel.basic_qos(prefetch_count=1) 
表示谁来谁取，不再按照奇偶数排列（同时也保证了公平的消费分发）








113.	以下RabbitMQ的exchange type分别代表什么意思？如：fanout、direct、topic。
amqp协议中的核心思想就是生产者和消费者隔离，生产者从不直接将消息发送给队列。
生产者通常不知道是否一个消息会被发送到队列中，只是将消息发送到一个交换机。
先由Exchange来接收，然后Exchange按照特定的策略转发到Queue进行存储。
同理，消费者也是如此。Exchange 就类似于一个交换机，转发各个消息分发到相应的队列中。
--------------------------------------------------
type=fanout 类似发布者订阅者模式，会为每一个订阅者创建一个队列，而发布者发布消息时，会将消息放置在所有相关队列中
type=direct 队列绑定关键字，发送者将数据根据关键字发送到消息exchange，exchange根据 关键字 判定应该将数据发送至指定队列。
type=topic  队列绑定几个模糊的关键字，之后发送者将数据发送到exchange，exchange将传入”路由值“和 ”关键字“进行匹配，匹配成功，则将数据发送到指定队列。
---------------------------------------------------
发送者路由值              队列中
old.boy.python          old.*  -- 不匹配    *表示匹配一个
old.boy.python          old.#  -- 匹配      #表示匹配0个或多个
114.	简述 celery 是什么以及应用场景？
# Celery是由Python开发的一个简单、灵活、可靠的处理大量任务的分发系统，
# 它不仅支持实时处理也支持任务调度。
# http://www.cnblogs.com/wupeiqi/articles/8796552.html
115.	简述celery运行机制。
 





116.	celery如何实现定时任务？
# celery实现定时任务
启用Celery的定时任务需要设置CELERYBEAT_SCHEDULE 。 
CELERYBEAT_SCHEDULE='djcelery.schedulers.DatabaseScheduler'#定时任务
'创建定时任务'
# 通过配置CELERYBEAT_SCHEDULE：
#每30秒调用task.add
from datetime import timedelta
CELERYBEAT_SCHEDULE = {
    'add-every-30-seconds': {
        'task': 'tasks.add',
        'schedule': timedelta(seconds=30),
        'args': (16, 16)
    },
}
117.	简述 celery多任务结构目录？
pro_cel
    ├── celery_tasks     # celery相关文件夹
    │   ├── celery.py    # celery连接和配置相关文件
    │   └── tasks.py     #  所有任务函数
    ├── check_result.py  # 检查结果
    └── send_task.py     # 触发任务
118.	celery中装饰器 @app.task 和 @shared_task的区别？
# 一般情况使用的是从celeryapp中引入的app作为的装饰器：@app.task
# django那种在app中定义的task则需要使用@shared_task
119.	简述 requests模块的作用及基本使用？
# 作用：
使用requests可以模拟浏览器的请求
# 常用参数：
   url、headers、cookies、data
   json、params、proxy
# 常用返回值：
   content
   iter_content
   text 
   encoding="utf-8"
   cookie.get_dict()
参考：点击


120.	简述 beautifulsoup模块的作用及基本使用？
# BeautifulSoup
用于从HTML或XML文件中提取、过滤想要的数据形式
#常用方法
解析：html.parser 或者 lxml（需要下载安装） 
   find、find_all、text、attrs、get 
121.	简述 seleninu模块的作用及基本使用?
Selenium是一个用于Web应用程序测试的工具，
他的测试直接运行在浏览器上，模拟真实用户，按照代码做出点击、输入、打开等操作

爬虫中使用他是为了解决requests无法解决javascript动态问题
参考:点击查看
122.	scrapy框架中各组件的工作流程？
#1、生成初始的Requests来爬取第一个URLS，并且标识一个回调函数
第一个请求定义在start_requests()方法内默认从start_urls列表中获得url地址来生成Request请求，
默认的回调函数是parse方法。回调函数在下载完成返回response时自动触发
#2、在回调函数中，解析response并且返回值
返回值可以4种：
    a、包含解析数据的字典
    b、Item对象
    c、新的Request对象（新的Requests也需要指定一个回调函数）
    d、或者是可迭代对象（包含Items或Request）
#3、在回调函数中解析页面内容
通常使用Scrapy自带的Selectors，但很明显你也可以使用Beutifulsoup，lxml或其他你爱用啥用啥。
#4、最后，针对返回的Items对象将会被持久化到数据库
    通过Item Pipeline组件存到数据库
    或者导出到不同的文件（通过Feed exports）
参考：点击查看+按住Ctrl
123.	在scrapy框架中如何设置代理（两种方法）？
scrapy自带的代理组件：
from scrapy.downloadermiddlewares.httpproxy import HttpProxyMiddleware
from urllib.request import getproxies





124.	scrapy框架中如何实现大文件的下载？
from twisted.web.client import Agent, getPage, ResponseDone, PotentialDataLoss
from twisted.internet import defer, reactor, protocol
from twisted.web._newclient import Response
from io import BytesIO

class _ResponseReader(protocol.Protocol):
    def __init__(self, finished, txresponse, file_name):
        self._finished = finished
        self._txresponse = txresponse
        self._bytes_received = 0
        self.f = open(file_name, mode='wb')
    def dataReceived(self, bodyBytes):
        self._bytes_received += len(bodyBytes)
        # 一点一点的下载
        self.f.write(bodyBytes)
        self.f.flush()
    def connectionLost(self, reason):
        if self._finished.called:
            return
        if reason.check(ResponseDone):
            # 下载完成
            self._finished.callback((self._txresponse, 'success'))
        elif reason.check(PotentialDataLoss):
            # 下载部分
            self._finished.callback((self._txresponse, 'partial'))
        else:
            # 下载异常
            self._finished.errback(reason)
        self.f.close()
125.	scrapy中如何实现限速？
参考：点击查看(+Ctrl)






126.	scrapy中如何实现暂定爬虫？
# 有些情况下，例如爬取大的站点，我们希望能暂停爬取，之后再恢复运行。
# Scrapy通过如下工具支持这个功能:
一个把调度请求保存在磁盘的调度器
一个把访问请求保存在磁盘的副本过滤器[duplicates filter]
一个能持续保持爬虫状态(键/值对)的扩展
Job 路径
要启用持久化支持，你只需要通过 JOBDIR 设置 job directory 选项。
这个路径将会存储所有的请求数据来保持一个单独任务的状态(例如：一次spider爬取(a spider run))。
必须要注意的是，这个目录不允许被不同的spider 共享，甚至是同一个spider的不同jobs/runs也不行。
也就是说，这个目录就是存储一个 单独 job的状态信息。
参考：点击查看
127.	scrapy中如何进行自定制命令？
在spiders同级创建任意目录，如：commands
在其中创建'crawlall.py'文件（此处文件名就是自定义的命令）
from scrapy.commands import ScrapyCommand
    from scrapy.utils.project import get_project_settings
    class Command(ScrapyCommand):
        requires_project = True
        def syntax(self):
            return '[options]'
        def short_desc(self):
            return 'Runs all of the spiders'
        def run(self, args, opts):
            spider_list = self.crawler_process.spiders.list()
            for name in spider_list:
                self.crawler_process.crawl(name, **opts.__dict__)
            self.crawler_process.start()
在'settings.py'中添加配置'COMMANDS_MODULE = '项目名称.目录名称''
在项目目录执行命令：'scrapy crawlall' 
参考：点击查看
128.	scrapy中如何实现的记录爬虫的深度？
'DepthMiddleware'是一个用于追踪每个Request在被爬取的网站的深度的中间件。 
其可以用来限制爬取深度的最大深度或类似的事情。
'DepthMiddleware'可以通过下列设置进行配置(更多内容请参考设置文档):

'DEPTH_LIMIT':爬取所允许的最大深度，如果为0，则没有限制。
'DEPTH_STATS':是否收集爬取状态。
'DEPTH_PRIORITY':是否根据其深度对requet安排优先
129.	scrapy中的pipelines工作原理？
Scrapy 提供了 pipeline 模块来执行保存数据的操作。
在创建的 Scrapy 项目中自动创建了一个 pipeline.py 文件，同时创建了一个默认的 Pipeline 类。
我们可以根据需要自定义 Pipeline 类，然后在 settings.py 文件中进行配置即可
参考：点击查看
130.	scrapy的pipelines如何丢弃一个item对象？
通过raise DropItem()方法
131.	简述scrapy中爬虫中间件和下载中间件的作用？
参考：点击查看
132.	scrapy-redis组件的作用？
实现了分布式爬虫，url去重、调度器、数据持久化
'scheduler'调度器
'dupefilter'URL去重规则（被调度器使用）
'pipeline'数据持久化
133.	scrapy-redis组件中如何实现的任务的去重？
a. 内部进行配置，连接Redis
b.去重规则通过redis的集合完成，集合的Key为：
   key = defaults.DUPEFILTER_KEY % {'timestamp': int(time.time())}
   默认配置：
      DUPEFILTER_KEY = 'dupefilter:%(timestamp)s'
c.去重规则中将url转换成唯一标示，然后在redis中检查是否已经在集合中存在
   from scrapy.utils import request
   from scrapy.http import Request
   req = Request(url='http://www.cnblogs.com/wupeiqi.html')
   result = request.request_fingerprint(req)
   print(result)  # 8ea4fd67887449313ccc12e5b6b92510cc53675c
134.	scrapy-redis的调度器如何实现任务的深度优先和广度优先？
'广度优先'：先进先出（默认）有序集合
'深度优先'：先进后出
参考：点击查看
135.	简述 vitualenv 及应用场景?
'vitualenv'是一个独立的python虚拟环境
如：
   当前项目依赖的是一个版本，但是另一个项目依赖的是另一个版本，这样就会造成依赖冲突，
   而virtualenv就是解决这种情况的，virtualenv通过创建一个虚拟化的python运行环境，
   将我们所需的依赖安装进去的，不同项目之间相互不干扰
参考：点击查看
136.	简述 pipreqs 及应用场景？
可以通过对项目目录扫描，自动发现使用了那些类库，并且自动生成依赖清单。

pipreqs ./ 生成requirements.txt
137.	在Python中使用过什么代码检查工具？
1）PyFlakes：静态检查Python代码逻辑错误的工具。
2）Pep8： 静态检查PEP8编码风格的工具。
3）NedBatchelder’s McCabe script：静态分析Python代码复杂度的工具。
Python代码分析工具：PyChecker、Pylint
138.	简述 saltstack、ansible、fabric、puppet工具的作用？

139.	B Tree和B+ Tree的区别？
1.B树中同一键值不会出现多次，并且有可能出现在叶结点，也有可能出现在非叶结点中。
  而B+树的键一定会出现在叶结点中，并有可能在非叶结点中重复出现，以维持B+树的平衡。
2.因为B树键位置不定，且在整个树结构中只出现一次，
140.	请列举常见排序并通过代码实现任意三种。
冒泡/选择/插入/快排
参考1：点击查看
参考2：点击查看
141.	请列举常见查找并通过代码实现任意三种。
无序查找、二分查找、插值查找
参考：点击查看
142.	请列举你熟悉的设计模式？
工厂模式/单例模式等
参考：点击查看
143.	有没有刷过leetcode？
leetcode是个题库，里面有多很编程题目，可以在线编译运行。
网址：点击查看
144.	列举熟悉的的Linux命令。
参考：点击查看
145.	公司线上服务器是什么系统？
Linux/Centos


146.	解释 PV、UV 的含义？
PV访问量（Page View），即页面访问量，每打开一次页面PV计数+1，刷新页面也是。
UV访问数（Unique Visitor）指独立访客访问数，一台电脑终端为一个访客。
(例：我博客页面访量记录，用的是UV模式点击查看)
147.	解释 QPS的含义？
'QPS(Query Per Second)'
每秒查询率，是对一个特定的查询服务器在规定时间内所处理流量多少的衡量标准。？？？？
148.	uwsgi和wsgi的区别？
wsgi是一种通用的接口标准或者接口协议，实现了python web程序与服务器之间交互的通用性。

uwsgi:同WSGI一样是一种通信协议
uwsgi协议是一个'uWSGI服务器'自有的协议，它用于定义传输信息的类型，
'uWSGI'是实现了uwsgi和WSGI两种协议的Web服务器，负责响应python的web请求。
149.	supervisor的作用？
# Supervisor：
是一款基于Python的进程管理工具，可以很方便的管理服务器上部署的应用程序。
是C/S模型的程序，其服务端是supervisord服务,客户端是supervisorctl命令

# 主要功能:
1 启动、重启、关闭包括但不限于python进程。
2 查看进程的运行状态。
3 批量维护多个进程。
150.	什么是反向代理？
正向代理代理客户端(客户端找哟个代理去访问服务器，服务器不知道你的真实IP)
反向代理代理服务器(服务器找一个代理给你响应，你不知道服务器的真实IP)
151.	简述SSH的整个过程。
SSH 为 'Secure Shell' 的缩写，是建立在应用层基础上的安全协议。
SSH 是目前较可靠，为远程登录会话和其他网络服务提供的安全性协议。
利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。
参考：点击查看
152.	有问题都去那些找解决方案？
起初是百度，发现搜到的答案不精准，净广告
转战谷歌，但墙了；捣鼓怎么翻墙

还会去知乎、stackoverfloow、必应、思否(segmentfault)


153.	是否有关注什么技术类的公众号？
python之禅(主要专注Python相关知识，作者：刘志军)
码农翻身(主要是Java的，但不光是java，涵盖面很广，作者：刘欣)
实验楼(在线练项目)
and so on
154.	最近在研究什么新技术？
Numpy
pandas(金融量化分析、聚宽)
百度AI
图灵API
智能玩具
155.	是否了解过领域驱动模型？
Domain-Driven Design
参考：点击查看


