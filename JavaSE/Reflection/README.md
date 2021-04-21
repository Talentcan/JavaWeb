# 反射
反射是框架设计的灵魂。框架是半成品的软件，可以在框架的基础上进行软件开发，简化编码。

反射机制：是将类的各个组成部分封装为其他对象。

例如：java代码在计算机中经历的三个阶段就有用到反射
![](../Reflection/图片1.png)
在图中，Source源代码阶段，成员变量被封装成Field对象，构造方法被封装成Construction对象，成员方法被封装成Method对象

反射的好处：

1.可以在程序运行过程中，操作这些对象，比如创建一个字符串对象，可以在idea运行的过程中操作，得到它其中的一些方法

2.可以解耦（降低程序的一些耦合性，紧密的联系程度），提高程序的可扩展性

## 获取class类对象的方式

1.class.forName("全类名"); 在java代码的第一个阶段，将字节码文件加载进内存，返回class对象
  多用于配置文件，将类名定义在配置文件中。读取文件，加载类。
2.类名.class; 在java代码的第二个阶段，通过类名的属性Class获取
  多用于参数的传递
3.对象. getClass(); 在java代码的第三个阶段，getClass()方法在Object类中定义着
  多用于对象的获取字节码的方式
```
public static void main(String[] args) throws Exception {
        //1.class.forName("全类名");
        Class cls1 = Class.forName("cn.reflect.Person");
        System.out.println(cls1);
        //2.类名.class;
        Class<Person> cls2 = Person.class;
        System.out.println(cls2);
        //3.对象. getClass();
        Person p = new Person();
        Class cls3 = p.getClass();
        System.out.println(cls3);
        //结果为true
        System.out.println(cls1 == cls2 && cls1 == cls3);
    }
```
结论

同一个字节码文件(*.class)在一次程序运行过程中，只会被加载一次，不论通过哪一种方式获取的Class对象都是同一个


