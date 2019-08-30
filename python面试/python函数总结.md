1. 如何面试，调整心态。

   1. 相信自己，可以的。
   2. 这两周非常重要，总结梳理。
   3. 面试技巧，知识点总结到本上。切忌！！！自我介绍用背的方式。

2. 函数：

   1. 函数的参数。

      + 给你出例子，看代码写结果。
      + 默认参数为可变的数据类型。

      ```
      def func(a,b,*args,c,sex='男',**kwargs):
          print(c)  # 仅限关键字参数
      
      func(1,2,4,5,6,c=666)
      ```

      ![1566896274823](assets/1566896274823.png)

      ```
      def foo(a,b,*args,c,sex=None,**kwargs):
          print(a,b)
          print(c)
          print(sex)
          print(args)
          print(kwargs)
      # foo(1,2,3,4,c=6)
      # foo(1,2,sex='男',name='alex',hobby='old_woman')
      # foo(1,2,3,4,name='alex',sex='男')
      # foo(1,2,c=18)
      # foo(2, 3, [1, 2, 3],c=13,hobby='喝茶')
      # foo(*[1, 2, 3, 4],**{'name':'太白','c':12,'sex':'女'})
      ```

   2. 作用域

      ```
      # 修改一个全局变量
      a = 'alex'
      def func():
          # global a
          a += 'aaa'
      func()
      # 声明一个全局变量
      def func():
          global r
          r = 666
      func()
      print(r)
      ```

   3. *处理剩余元素

      ```
      # *处理剩余元素
      # a,*b,c = [1, 2, 3, 4, 5]
      # a,*b, c = range(5)
      # print(a,b,c)
      ```

   4. 闭包：

      1. 内层函数对外层函数非全局变量的引用。
      2. 存在嵌套函数中。
      3. 内层函数的函数名必须作为返回值返回。

      闭包的作用？

      被引用的变量被称为自由变量，不会随着函数的结束而消失，保证数据安全。

      闭包的应用： 装饰器。

   5. 装饰器。

      1. 手写一个装饰器。

         ```
         def wrapper(func):  # f = func
         	def inner(*args, **kwargs):
         		"""执行之前的代码"""
         		print(111)  # 3
         		ret = func(*args,**kwargs)
         		"""执行之后的代码"""
         		print(222)  # 5
         		return ret
             return inner
             
         @wrapper  f = wrapper(f)   1  f = inner
         def f():
         	print('in f')  # 4
         f()  # inner()  # 2
         	
         ```

         

      2. 利用装饰器手写一个登陆认证。自己完成。

         ```
         pass
         ```

      3. 装饰器的执行流程。

      4. 多个装饰器装饰同一个函数的流程。

         ```
         def wrapper1(func):
             def inner1(*args, **kwargs):
                 print('in inner1')  # 2
                 ret = func(*args,**kwargs)
                 print(555)  # 4
                 return ret
             return inner1
         
         def wrapper2(func):
             def inner2(*args, **kwargs):
                 print('in inner2')  # 1
                 ret = func(*args,**kwargs)
                 print(777)  # 5
                 return ret
             return inner2
         
         @wrapper2
         @wrapper1
         def func():
             print(666)  # 3
         
         func()
         '''
         in inner2
         in inner1
         666
         555
         777
         '''
         ```

      5. 迭代器

         ![1566900475181](assets/1566900475181.png)

       6. 生成器：

          1. 生成器本质上就是迭代器，

             生成器与迭代器区别：迭代器是python直接给你提供的，或者通过iter()转化的，生成器是自己通过python代码构建。

             ​	构建生成器的几种方式：

               1. 通过生成器函数。（yield）
               2. 生成器推导式。
               3. 有一部分是python给你提供的。

            2. 生成器表达式列表推导式考点。

               [1,4,9,16,.....100]

               ['class1'， 'class 3',  'class5',]

               循环模式：

               [变量（加工后的变量） for 变量 in iterable]

               筛选模式： 

               [变量（加工后的变量） for 变量 in iterable if 条件]

          3. yield from 考点

             yield from 代替了生成器的内层循环，提高效率。

             ```
             yield from
             
             def func():
                 # yield 1
                 # yield from [1,2,3]
                 for i in range(1,4):
                     yield i
             obj = func()
             print(next(obj))
             print(next(obj))
             print(next(obj))
             ```

             

             ```
             def chain(*iterables):
             
             	for it in iterables:
             
             		for i in it:
             
             			yield i
             
             g = chain('abc',(0,1,2))
             
             print(list(g))  # 将迭代器转化成列表
             ```

             

      	7.  内置函数

           max, min,filter,map,zip,sorted,reduce,

           与lambda结合。

           l1 = [ {'sales_volumn': 0},

           	{'sales_volumn': 108},
           	
           	{'sales_volumn': 337},
           	
           	{'sales_volumn': 475},
           	
           	{'sales_volumn': 396},
           	
           	{'sales_volumn': 172},
           	
           	{'sales_volumn': 9},
           	
           	{'sales_volumn': 58}, 
           	
           	{'sales_volumn': 272}, 
           	
           	{'sales_volumn': 456}, 
           	
           	{'sales_volumn': 440},
           	
           	{'sales_volumn': 239}]
           ```
           def num():
           	return [lambda x:i*x for i in range(4)]
           print([m(2)for m in num()])
           ```

           ```
           def func():
               for num in range(10):
                   pass
               v4 = [lambda :num+10,lambda :num+100,lambda :num+100,]
               result1 = v4[1]()
               result2 = v4[2]()
               print(result1,result2)
           func()
           ```

           ```
           def demo():
               for i in range(4):
                   yield i
           g=demo()
           g1=(i for i in g)
           g2=(i for i in g1)
           print(list(g1))
           print(list(g2))
           ```

   3. 模块

      1. 列举你使用的内置模块,不少于10个.

         os sys random time datetime hashlib logging json pickle re

         uuid socket socketserver threading mutiprocess collections

         functiontools 

      2. 列举一下第三方模块

         requests beatifusoup Django flask pillow pandas gevent greenlet redis pymysql .....

      3. 一些模块中的一些小功能.

         re模块 search 与match的区别?

   4. 面向对象

      1. 面向对象的优势:
         1. 结构分析: 相似功能的集合.代码更加清晰化,标准化.

         2. 站在上帝的角度: 构建类, 一切以对象为核心,得到对象的天下.

            得到对象可以得到对象属性,从属于类的属性,方法,可以得到父类的属性方法.

      2. 实例化对象发生了三件事:

         

         ```
         class A:
         	pass
         obj = A()
         ```

         

         1. 先调用object类`__new__`方法在内存中开辟一个对象空间,并返回.
         2. 自动执行`__init__`方法,并将对象空间传给self.
         3. 在`__init__`方法里面给其封装属性.

      3. 函数vs方法:

         只要是隐形传参的就是方法,显性传参的就是函数.

      4. 面向对象的三大特性: 继承,封装,多态.

         多态: a = 'sfads' a = 123 a = [1,2,3]

         ```
         java:
         int a = 123
         ```

      5. 单继承: 

         对象如何既执行子类的方法,又执行父类的方法.

         重构父类的方法.

         ```
         class A:
             
             def func(self):
                 print('in A func')
         
         
         class B(A):
             
             def func(self):
                 # A.func(self)
                 super(B,self).func()
                 print('in B func')
         
         obj = B()
         obj.func()
         ```

      6. 多继承:

         python面向对象:

         新式类: 继承object类. C3算法. mro()

         C3算法: 建议你们过一遍.

         经典类:不继承object类.深度优先.

      7. 私有成员:只能在类的内部调用,不能在派生类,或者类的外部调用.

         私有类的属性,私有类的方法,私有对象属性.

      8. 属性property: 

         设置属性的两种方式: 装饰器的形式. 实例化对象的形式.

         ```
         class Foo:
             @property
             def AAA(self):
                 print('get的时候运行我啊')
         
             @AAA.setter
             def AAA(self,value):
                 print('set的时候运行我啊')
         
             @AAA.deleter
             def AAA(self):
                 print('delete的时候运行我啊')
         obj = Foo()
         obj.AAA
         obj.AAA = 'alex'
         del obj.AAA
         ```

         ```
         class Foo:
             def get_AAA(self):
                 print('get的时候运行我啊')
         
             def set_AAA(self,value):
                 print('set的时候运行我啊')
         
             def delete_AAA(self):
                 print('delete的时候运行我啊')
             AAA=property(get_AAA,set_AAA,delete_AAA) #内置property三个参数与get,set,delete一一对应
         
         f1=Foo()
         f1.AAA
         f1.AAA='aaa'
         del f1.AAA
         ```

      9. object 与 type类什么关系?

         python中一切皆对象,类是不是个对象? 大部分类都是type类的对象,包括object类也是type类的对象.

         type类 是object类的子类.

      10. 双下方法.
          1. 你用过的双下方法?
          2. 比如`__call__` 等方法如何调用?
          3. `__new__`方法, 单利模式.
          4. `__enter__`  `__exit__`

      11. 项目整体流程

          1. 项目的整体流程

          2. 项目的表结构设计.

          3. 项目的亮点是什么?

          4. 项目中不足?

          5. 项目中你负责哪一步?

          6. 你在项目中遇到的困难问题是什么? 怎么解决的?

          7. 你的项目有没有拓展性?

          8. 你的项目中用的新的技术点?

             