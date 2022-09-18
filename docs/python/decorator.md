# Decorator

## 简单装饰器

装饰器其实有点类似游戏中的`Buff`，红蓝`Buff`，红`Buff`可以减速、攻击附带，蓝`Buff`可以法术加成。

也可以类比于各种特效加成，比如仙剑四中武器的各种注灵加成，不同注灵方式可以加成不同的效果，比如冰冻、中毒、灼烧等等。 在`python`中，装饰器就是为了给原有函数加上额外的特效。

下面举例说明：

``` python
def test():
    print('just for test')
```

现在有个新的需求，要在执行函数后打印log，显示当前执行的函数是哪个，那可以这样：

``` python
def test():
    print('just for test')
    logging.info('test is running')
```

一个函数好办，要是有多个函数都要呢，每个函数都加的话就太冗余了。那么另外写个函数：

``` python
def logged(func):
    logging.info('{} is running'.format(func.__name__))
    func()

def test():
    print('just for test')

logged(test)
```

这样虽然可以，但是每次调用函数都要外加个壳子logged,显然是不合情理的，破坏了原有的代码逻辑。那怎么解决呢，这就是装饰器的出场时间了：

``` python
def logged(func):
    def wrapper(*args, **kwargs):
        logging.info('{} is running'.format(func.__name__))
        return func(*args, **kwargs)
    return wrapper


def test():
    print('just for test')

test = logged(test)
test()
```

在这里，`logged`就是个装饰器，业务逻辑在test中实现，装饰器对test进行了装饰，也就是加了特效，专业术语叫`AOP`，即[面向切面编程](https://baike.baidu.com/item/AOP/1332219?fromtitle=面向切面编程&fromid=6016335)。

使用语法糖`@`, 在业务方法外层添加`@logged`即可

``` python
def logged(func):
    def wrapper(*args, **kwargs):
        logging.info('{} is running'.format(func.__name__))
        return func(*args, **kwargs)
    return wrapper

@logged
def test():
    print('just for test')

test()
```

## 带参装饰器

由于装饰器本身也是一个函数，那么带参也是被允许的，那么如何实现呢？

``` python
def logged(level):
    def decorator(func):
        def wrapper(*args, **kwargs):
            if level == 'info':
                logging.info('{} is running'.format(func.__name__))
            return func(*args, **kwargs)
        return wrapper
    return decorator

@logged(level='info')
def test():
    print('just for test')

test()
```

可以看出来，在上面简单装饰器的基础上又加了一层封装，同时返回了一个装饰器`decorator`,`Python`解释器在解析到`@logged(level='info')`的时候，能够发现这层封装，并将参数`level`传入装饰器中。

## 保留原函数元信息

使用装饰器有个缺陷，就是会丢失原函数的元信息，比如函数的`__name__`、docstring、注解和参数签名等。

解决方法是使用另一个装饰器`functools.wraps`

``` python
from functools import wraps

def logged(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        logging.info('{} is running'.format(func.__name__))
        return func(*args, **kwargs)
    return wrapper

@logged
def test():
    print('just for test')

test()
```

## 类装饰器

## 内置装饰器

### @staticmethod

静态函数`staticmethod`原本是可以在类外定义的，如：

``` python
def foo():
    print('foo is running')

Class A():
    def __init__(self):
        pass

    def run(self):
        foo()
        print('start running')
```

但是呢，如果`foo`这个函数仅仅被类`A`内部函数调用，或者仅仅与类`A`相关的操作需要用到函数`foo`,那么放在外面就显得不太合适了，容易污染命名空间。此时既想把`foo`与类`A`关联起来，同时又想通过类名直接快捷访问，就可以通过`@staticmethod`来实现：

``` python
Class A():
    def __init__(self):
        pass

    @staticmethod
    def foo():
        print('foo is running')

    def run(self):
        self.foo()
        print('start running')

A.foo()
a = A()
a.run()
```

可以看出，`staticmethod`就是普普通通的函数，只不过刚好某个类需要用到它，就把它扔进去了，这个函数本身最好不去调用类的属性或成员函数。

### @classmethod

`@classmethod`有个必要的首参，用于指向当前所在类，所以通常有类似这样的定义：

``` python
Class A():
    def __init__(self, user):
        self.user = user
        print(user + ' is login')

    @classmethod
    def f1(cls):
        return cls('Emily')
```

在上面的例子中，函数`f1`通过类对象`cls`定义并返回了一个A类的实例对象。

在爬虫框架`Scrapy`源码中，有个很常用的`@classmethod`, 就是`crawl.py`中的`from_crawler`函数：

``` python
@classmethod
def from_crawler(cls, crawler, *args, **kwargs):
    spider = super(CrawlSpider, cls).from_crawler(crawler, *args, **kwargs)
    spider._follow_links = crawler.settings.getbool(
            'CRAWLSPIDER_FOLLOW_LINKS', True)
    return spider
```

该函数继承于`Spider`类中的`from_crawler`函数，最终返回的是一个`spider`实例对象。

`@classmethod`主要用于返回实例对象，同时可以直接访问类中属性及函数。

### @staticmethod & @classmethod

`@staticmethod`与`@classmethod`的对比随处可见。

先说共同点，两种装饰器对应的函数都可以通过以下两种方式调用：

- `ClassName.function()`
- `Instance.function()`

再看看不同点，从定义和调用方面区分：

- `@staticmethod`对应函数通常只是与类有所关联，但与其对象属性关联不大或没有关联，要想访问类的方法和属性，需要通过类名或者`self`访问。
- `@classmethod`第一个参数必须是自身类参数`cls`，名称随意，可以是self；而且因为持有类参数，所以可以通过`cls`直接访问类的方法和属性。

大部分情况下，添加这两个装饰器的目的就是为了方便通过类名直接访问，而无需实例化对象。

在**应用场景**方面，

- `@staticmethod`适用于普通函数，就是那种放不放类中都可以用，只不过恰好在这个类中而已。
- `@classmethod`适用于创建实例对象，即通过这个函数返回一个类的实例对象

### @property

至于属性装饰器`@property`就比较简单了，通常用于实现类内部某个属性的`set`,`get`操作，**将被装饰的函数模拟成一个类的属性**，然后可以对其进行直接读取和赋值。

``` python
class A():
    def __init__(self):
        self._user = 'Emily'

    @property
    def user(self):
        return self._user

    @user.setter
    def user(self, value):
        self._user = value

a = A()
print(a.user) # Emily
a.user = 'Litreily'
print(a.user) # Litreily
```

## 参考资料

- [如何解释Python装饰器](https://www.zhihu.com/question/26930016/answer/99243411)
- [What is the difference between @staticmethod and @classmethod?](https://stackoverflow.com/questions/136097/what-is-the-difference-between-staticmethod-and-classmethod)
- [Python3-cookbook 创建装饰器时保留函数元信息](https://python3-cookbook.readthedocs.io/zh_CN/latest/c09/p02_preserve_function_metadata_when_write_decorators.html)
