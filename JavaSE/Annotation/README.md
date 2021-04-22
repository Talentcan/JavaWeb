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
public @interface 注解名称{}

本质：注解本质上是一个接口，该接口默认继承Annotation接口

public interface MyAnno extends java.lang.annotation.Annotation {}

属性：接口中可以定义的成员方法










