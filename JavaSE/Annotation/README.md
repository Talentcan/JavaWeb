# 注解
概念：说明程序，给计算机看

定义：Java 注解（Annotation）又称 Java 标注，是 JDK5.0 引入的一种注释机制。Java 语言中的类、方法、变量、参数和包等都可以被标注。和 Javadoc 不同，Java 标注可以通过反射获取标注内容。在编译器生成类文件时，标注可以被嵌入到字节码中。Java 虚拟机可以保留标注内容，在运行时可以获取到标注内容 。

定义描述：</br>
JDK1.5之后的新特性；是用来说明程序的；使用注解：@注解名称

作用分类：</br>
编写文档：通过代码里标识的元数据生成文档[生成doc文档]</br>
代码分析：通过代码里标识的元数据对代码进行分析[使用反射]</br>
编译检查：通过代码里标识的元数据让编译器能够实现基本的编译检查，如：安全检查[override]</br>

## JDK中预定义的一些注解
@Override:检测被该注解标注的方法是否是继承自父类（接口）的
```
//看方法声明是否跟父类的方法一致，不一样会失败报错，如果不加这个注解，表示是这个类特有的方法，不构成重写
@Override
public String toString(){
}
```
@Deprecated：检测该注解标注的内容，表示时候已过时
```
//虽然过时，也不推荐使用，但是还是能用
@Deprecated
public void show1(){
  //有缺陷，已过时
}
public void show2(){
  //替代show1方法
}
```

@SuppressWarnings用来压制警告,一般传递参数all
```
//用来压制编辑器产生的警告
@SuppressWarnings("all")  //压制所有警告，all
public Class a(){
}
```

## 自定义注解
格式</br>
元注解</br>
public @interface 注解名称{</br>
    属性列表;</br>
}

本质：注解本质上是一个接口，该接口默认继承Annotation接口

public interface MyAnno extends java.lang.annotation.Annotation {}

属性：接口中的抽象方法</br>
要求：</br>
1.属性的返回值类型，只能是以下几种，别的类型都不行</br>
基本数据类型</br>
String</br>
枚举</br>
注解</br>
以上类型的数组</br>

2.定义了属性，在使用时需要给属性赋值</br>
(1).如果定义属性时，使用default关键字给属性默认初始化值，则使用注解时，可以不进行属性的赋值
(2).如果只有一个属性需要赋值，并且属性的名称是value，则value可以省略，直接定义值即可，如：JDK中@SuppressWarnings("all")只有一个属性，且名称为value的字符串数组
(3). 数组赋值时，值使用{}包裹，如果数组中只有一个值，则可以省略{}。
```
public @interface MyAnno {
    int age ();
    String name() default "zhangsan";
}
@MyAnno (age = 12) //name可以不用赋值，有默认的值
public class Worker{
}

public @interface MyAnno {
    int value;
}
@MyAnno (12) //可以不写属性名称
public class Worker{
}
```

元注解：用于描述注解的注解，或者说元注解是一种基本注解，它能应用到其他的注解上面，java已经帮我们定义好了，我们可以用来注解我们自定义的注解

@Taret：描述注解能够作用的位置
```
在@Target注解中传递ElementType枚举数组
ElementType的取值：
TYPE：可以作用于类上
METHOD：可以作用于方法上
FIRLD：可以作用于成员变量上

import java.lang.annotation.ElementType;
import java.lang.annotation.Target;

@Target(value = {ElementType.TYPE,ElementType.METHOD,ElementType.FIELD}) //表示该MyAnno注解只能作用于类上
public @interface MyAnno {
}

@MyAnno   //类上
public class Worker {
    @MyAnno //成员变量上
    public String a = "";
    @MyAnno  //方法上
    public void show(){
    }
}
```
@Retention：描述注解被保留的阶段，说明这个注解的存活时间
```
它的取值如下：
RetentionPolicy.SOURCE 注解只在源码阶段保留，在编译器进行编译时它将被丢弃忽视
RetentionPolicy.CLASS 注解只被保留到编译进行的时候，它并不会被加载到 JVM 中
RetentionPolicy.RUNTIME 注解可以保留到程序运行的时候，它会被加载进入到 JVM 中，所以在程序运行时可以获取到它们

//我们定义的注解一般使用第三个值，因为一般不会去操作编译器
@Retention(RetentionPolicy.RUNTIME)  //当前被描述的注解，会保留到class字节码文件中，并被JVM读取到
@Retention(RetentionPolicy.CLASS)当前被描述的注解，会保留到class字节码文件中，但不会被JVM读取到
@Retention(RetentionPolicy.SOURCE)  //当前被描述的注解，不会保留到class字节码文件中

import java.lang.annotation.*;

@Target(value = {ElementType.TYPE,ElementType.METHOD,ElementType.FIELD}) //表示该MyAnno注解只能作用于类上
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnno {
}
```
@Documented：描述注解是否被抽取到API文档中,能够将注解中的元素包含到Javadoc中
@Inherited：描述注解是否被子类继承，不是说注解本身可以继承，而是如果一个超类被@Inherited注解过的话，那么它的子类如果没有被任何注解应用的话，那么这个子类就继承这个超类的注解
@Repeatable ：可重复的意思，是java1.8加进来的一个新特性，通常是注解的值可以同时取多个











