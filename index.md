# 飞桨领航团零基础Python速成营--面向对象学习心得
# 课程链接：https://aistudio.baidu.com/aistudio/course/introduce/7073
# 一、如何定义类？
class Athlete:

第一部分：class定义类的关键字，Athlete符合python标识符命名规则，：表示类内容的开始
def init(self,a_name,a_dob=None,a_times=[]):

第二部分：def定义函数的关键字，init 方法是一个特殊方法会在实例化对象时自动调用，我们会在这个方法中对数据进行赋值。self作为类中函数的第一个参数，方便该方法调用该类的其他属性和方法。

第三部分：自定义的属性和方法
<font color=#999AAA >代码如下（示例）：
```python
class Athlete:
    def __init__(self,a_name,a_dob=None,a_times=[]):
        self.name = a_name
        self.dob = a_dob
        self.times = a_times

    def top3(self):
        return sorted(set([self.sanitize(t) for t in self.times]))[0:3]
        
    def sanitize(self,time_string):
        if '-' in time_string:
            splitter = '-'
        elif ':' in time_string:
            splitter = ':'
        else:
            return (time_string)
        (mins,secs) = time_string.split(splitter)
        return (mins+'.'+secs)
```


# 二、如何使用类
1.创建对象

对象名 = 类名(参数)

2.使用.调用类的方法和属性

对象.属性名

对象.方法名()


<font color=#999AAA >代码如下（示例）：



```python
ath = Athlete(a_name,a_dob=None,a_times=[])

ath.top3()
```
# 三、子类
## 定义子类

class 子类名(父类名)：

情况1，如果子类有新增的属性，那么需要在子类__init方法中，调用父类的__init__

情况2，如果子类没有新增的属性,子类不需要写__init__方法

使用：
对象名 = 子类名(参数)

继承的好处：代码重用，升级功能（重写），新增功能（新的方法）

## 方法重写
子类方法与父类方法完全相同，子类若重写了父类的方法，则子类对象调用方法时就是调用的自己类中重新的方法。


<font color=#999AAA >代码如下（示例）：
```python

class OtherAthlete(Athlete):
    def __init__(self,a_name,a_bod,a_squat,a_times):

        Athlete.__init__(self,a_name,a_bod,a_times)

        self.squat = a_squat
    def top3(self):
        return sorted([self.sanitize(t) for t in self.times])[0:3]
```

# 四、多态
多态性：一个事物多种形态
多态的好处是：减少重复代码，分离经常改变的代码与不经常改变的代码，使得代码可维护性提高。
<font color=#999AAA >代码如下（示例）：
```python
class Rugby(Athlete):
    def __init__(self,a_name,a_bod,a_squat,a_times):

        Athlete.__init__(self,a_name,a_bod,a_times)

        self.squat = a_squat
    def top3(self):
        return sorted([self.sanitize(t) for t in self.times])[-3:]


class OtherAthlete(Athlete):
    def __init__(self,a_name,a_bod,a_squat,a_times):

        Athlete.__init__(self,a_name,a_bod,a_times)

        self.squat = a_squat
    def top3(self):
        return sorted([self.sanitize(t) for t in self.times])[0:3]
        
loren = get_coach_data('mywork/loren.txt')
mark = get_coach_data('mywork/mark.txt')

loren = Rugby(loren.pop(0),loren.pop(0),loren.pop(0),loren)
mark = OtherAthlete(mark.pop(0),mark.pop(0),mark.pop(0),mark)
#Rugby 和 OtherAthlete是Athlete的子类
def print_rugby(athlete):

    print(athlete.name)
    print(athlete.dob)
    print(athlete.squat)
    print(athlete.top3())

print_rugby(loren)
print_rugby(mark)
```
运行结果
loren
2011-11-3
270
['3.11', '3.23', '3.59']
mark
2010-2-4
300
['3.11', '3.11', '3.23']
上面例子中print_rugby的参数athlete，athlete.name，athlete.top3()的行为由athlete的子类决定。

