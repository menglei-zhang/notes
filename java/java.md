SpringCloud五大组件详解    https://blog.csdn.net/weixin_40910372/article/details/89466955
Spring Cloud系列--Feign整合(一)      https://www.jianshu.com/p/75178737ce91
https://www.runoob.com/java/java-loop.html

## Java

```
一种计算机编程语言
一种面向对象语言；
一个 Java 程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。

对象：对象是类的一个实例; 有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
类：类是一个模板，它描述一类对象的行为和状态。
方法：方法就是行为，一个类可以有很多方法。逻辑运算、数据修改以及所有动作都是在方法中完成的。
实例变量：每个对象都有独特的实例变量，对象的状态由这些实例变量的值决定。

Java 跨平台性 （不区分操作系统化）  核心是 JVM(虚拟机)
JVM Java虚拟机 Java代码都在JVM上运行
JRE Java程序的运行环境，包含JVM 和 运行时所需的核心类库     只能运行不能开发Java
JDK Java程序的开发工具包，包含JRE 和 开发人员使用的工具     既能运行又能开发Java
```

###  Java 注意事项：
    大小写敏感；
    类名：大驼峰（首字母大写）例如 MyFirstJavaClass；
    方法名：小驼峰（首字母小写）；
    源文件名：源文件名必须和类名相同。文件名的后缀为 " .java ";
    主方法入口：所有的 Java 程序由 public static void main(String[] args) 方法开始执行。

### 源文件声明规则
    当在一个源文件中定义多个类，并且还有import语句和package语句时，要特别注意这些规则。
        一个源文件中只能有一个 public 类；
        一个源文件可以有多个非 public 类；
        源文件的名称应该和 public 类的类名保持一致；
    
    如果一个类定义在某个包中，那么 package 语句应该在源文件的首行。
    如果源文件包含 import 语句，那么应该放在 package 语句和类定义之间。如果没有 package 语句，那么 import 语句应该在源文件中最前面。
    import 语句和 package 语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。
    类有若干种访问级别，并且类也分不同的类型：抽象类和 final 类等。这些将在访问控制章节介绍。
    
    除了上面提到的几种类型，Java 还有一些特殊的类，如：内部类、匿名类。

### Java 包
    包主要用来对类和接口进行分类。当开发 Java 程序时，可能编写成百上千的类，因此很有必要对类和接口进行分类。

### 计算机的基础知识：

#### 二进制

```
一个0或者1 叫做一个bit（比特，位）字节： Byte
1 Byte = 8 bit
1 KB = 1024 Byte
1 MB = 1024 KB
1 GB = 1024 MB
1 TB = 1024 GB
1 PB = 1024 TB
1 EB = 1024 EB
1 ZB = 1024 ZB
```

### Java程序开发的三个步骤 ：

编写、编辑、运行

```java
javac.exe : 编译器
java.exe  : 解释器

HelloWorld.java

public class HelloWorld {
    public static void main(String[] args) {    // 程序执行的起点
        System.out.println("Hello World!!!");   // 打印输出
    }
}

javac HelloWorld.java   生成 HelloWorld.class 文件

java HelloWorld
```

### 修饰符

    Java语言提供了很多修饰符，主要分为两类：访问修饰符、非访问修饰符
    修饰符用来定义类、方法或者变量，通常放在语句的最前端。

#### 访问控制修饰符

    Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。
    default (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
    private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
    public : 对所有类可见。使用对象：类、接口、变量、方法
    protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。
    
    |-----------------------|------------------------------------------------------|
    |                       |    public  >   protected  >  (default)  >  private   |
    |      同一个类(自己)     |     YES           YES           YES           YES    |
    |      同一个包(邻居)     |     YES           YES           YES            NO    |
    |     不同包子类(儿子)    |     YES           YES            NO            NO    |
    |   不同包非子类(陌生人)   |     YES            NO            NO            NO    |
    |-----------------------|------------------------------------------------------|

#### 非访问修饰符

    static、 final、 abstract、 synchronized、 volatile
    static  用来修饰类方法和类变量 静态变量，静态方法，静态代码  静态内容总是先入非静态
        静态变量：static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。
            静态变量也被称为类变量。局部变量不能被声明为 static 变量。
        静态方法：static 关键字用来声明独立于对象的静态方法。
            静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。
        对类变量和方法的访问可以直接使用 classname.variablename 和 classname.methodname 的方式访问。
        如果没有static关键字，那么必须首先创建对象，然后通过对象才能使用；
        如果有了static关键字，那么不需要创建对象，直接就能通过类名称来使用它；
        静态变量，静态方法 推荐使用类名称进行调用。
        静态变量:类名称.静态变量
        静态方法:类名称.静态方法()
    
        注意事项：
        静态不能直接访问费静态；因为在内存中，先有静态内容，后有非静态内容；
        静态方法当中不能用this：this代表当前对象，通过谁调用的方法，谁就是当前对象；
    
        静态代码块的格式是：
        public class 类名称{
            static{
                // 静态代码块的内容
            }
        }
        当第一次用到本类时，静态代码块执行唯一的一次
        静态内容总是优先于非静态，所以静态代码块比构造方法先执行。
        静态代码块的典型用途：用来一次性的对静态成员变量进行赋值；
    
    final 修饰符，用来修饰类、方法和变量
        final关键字代表最终、不可改变，常见四种用法：
            1、修饰一个类：不能够被继承； public final class Test {}
            2、修饰一个方法：父类中的 final 方法可以被子类继承，但是不能被子类重写；public final void changeName(){}
            3、修饰一个局部变量：变量一旦赋值后，不能被重新赋值；
                final 修饰符通常和 static 修饰符一起使用来创建类常量。
                public static final int BOXWIDTH = 6;
            4、修饰成员变量： 成员变量具有默认值，必须手动赋值 或者 通过构造方法赋值，二者选其一；
                如果保证类当中的所有重载的构造方法都最终会对final的成员变量进行赋值；
    
    abstract 修饰符，用来创建抽象类和抽象方法。
        抽象类：不能实例化，可以被继承；声明抽象类的唯一目的是为了将来对该类进行扩充。
        一个类不能同时被 abstract 和 final 修饰。
        如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。
        抽象类可以包含抽象方法和非抽象方法。
    
        抽象方法：是一种没有任何实现的方法，该方法的的具体实现由子类提供。
        抽象方法不能被声明成 final 和 static。
        任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。
        如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。
        抽象类可以不包含抽象方法。
        抽象方法的声明以分号结尾，例如：public abstract sample();。
    
    synchronized 和 volatile 修饰符，主要用于线程的编程。
        synchronized：关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。
            public synchronized void showDetails(){
                .......
            }
        transient：序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。
            该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。
            public transient int limit = 55;   // 不会持久化
            public int b; // 持久化
        volatile 修饰符
            volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。
            而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。
            一个 volatile 对象引用可能是 null。

### 关键字
    1、完全的小写字母  2、编译器中变色

### 标识符 (不能是关键字)
    Java 所有的组成部分都需要名字。类名、变量名 以及 方法名 都被称为 标识符；
    关于 Java 标识符，有以下几点需要注意：
        所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
        首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
        关键字不能用作标识符
        标识符是大小写敏感的
    命名规范（建议）：
        类名称：大驼峰（首字母大写）
        方法名称、变量名：小驼峰（首字母小写）

### 常量 和 变量
    常量：字符串常量、整数常量、浮点数常量、字符常量、布尔常量、空常量 （字符串常量用双引号，字符用单引号）
        通常使用大写字母表示常量；
        使用 final 关键字来修饰常量，声明方式和变量类似：final double PI = 3.1415927;
    变量：
        变量类型有：
            类变量（静态变量）：独立于方法之外的变量，用 static 修饰。
                类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。
                无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
                静态变量除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。
                静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量。
                静态变量在第一次被访问时创建，在程序结束时销毁。
                与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。
                默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
                静态变量可以通过：ClassName.VariableName的方式访问。
                类变量被声明为public static final类型时，类变量名称一般建议使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。
            实例变量：独立于方法之外的变量，不过没有 static 修饰。
                实例变量声明在一个类中，但在方法、构造方法和语句块之外；
                当一个对象被实例化之后，每个实例变量的值就跟着确定；
                实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
                实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
                实例变量可以声明在使用前或者使用后；
                访问修饰符可以修饰实例变量；
                实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
                实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
                实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName。
    
            局部变量：
                局部变量声明在方法、构造方法或者语句块中；
                局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
                访问修饰符不能用于局部变量；
                局部变量只在声明它的方法、构造方法或者语句块中可见；
                局部变量是在栈上分配的。
                局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。
        数据类型 变量名称;
        变量名称 = 数据值;

### 常见的数据结构
    1、栈： 进栈 出栈 入口和出口在同一侧，因此是先进后出；像弹夹；
    2、队列： 入口和出口各占一侧，因此先进先出；
    3、数组： 查寻快(索引)，增删慢(数组长度固定)；
    4、链表： 查寻慢(地址不是连续的，每次查询都要从头查询)，增删快(地址不是连续的)； 单向链表，双向链表；
    5、红黑树： 趋近与平衡树，元素是有大小顺序的，左子树小，右子树大，查询的速度非常快，
        1、节点可以是红色的或者黑色的；
        2、根节点是黑色的；
        3、叶子节点(空节点)是黑色的；
        4、每个共色的节点的子节点都是黑色的；
        5、任何一个节点到其每一个子节点的所有路径上的黑节点数是相同的；

### 数据类型

只有 基本数据类型 和 引用数据类型 两种）

#### 基本数据类型

    数据类型 变量名称 = 数据值;
    基本类型：八种基本类型  六种数据类型（四个整数型、两个浮点型）、一种字符类型、一种布尔类型
        byte：数据类型是8位、有符号的，以二进制补码表示的整数；  -128 ~ 127
            byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
        short 数据类型是 16 位、有符号的以二进制补码表示的整数   
            Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
        int 数据类型是32位、有符号的以二进制补码表示的整数；
            一般地整型变量默认为 int 类型；
        long 数据类型是 64 位、有符号的以二进制补码表示的整数；
        float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
            float 在储存大型浮点数组的时候可节省内存空间；默认值是 0.0f；
            浮点数不能用来表示精确的值，如货币；
        double 数据类型是双精度、64 位、符合IEEE 754标准的浮点数；
            浮点数的默认类型为double类型；默认值是 0.0d；
            double类型同样不能表示精确的值，如货币；
        boolean数据类型表示一位的信息；
            只有两个取值：true 和 false；
            这种类型只作为一种标志来记录 true/false 情况；
            默认值是 false；
        char类型是一个单一的 16 位 Unicode 字符；
            最小值是 \u0000（即为0）；
            最大值是 \uffff（即为65,535）；
            char 数据类型可以储存任何字符；
        |-----------------------|--------------|-------------------|   
        |      数据类型	         |    默认值     |   字节数(1字节=8位) | 
        |        byte	        |     0        |         1         |
        |       short	        |     0        |         2         |
        |        int	        |     0        |         4         |
        |       long	        |     0L       |         8         |
        |       float	        |    0.0f      |         4         |
        |       double	        |    0.0d      |         8         |
        |        char	        |   'u0000'    |         2         |
        |      boolean	        |    false     |         1         |
        |-----------------------|--------------|-------------------| 
        1个字节（-128 ~~ 127）
            0  1  1  1  1 1 1 1
            1  1  1  1  1 1 1 1
            64 32 16  8 4 2 1
    数据类型注意事项：
        字符串不是基本类型， 而是引用类型；
        浮点型可能只是一个近似值，并非精确的值；
        数据范围与字节数不一定相关，例如float数据范围比long更加广泛，但是float是4个字节，long是8个字节；
        浮点数当中默认类型是double。如果一定要使用float类型，需要加上一个F，后缀名推荐是大写;
        整数中默认为int类型，如果一定要使用long类型，需要加上一个后缀L，后缀名推荐是大写；

#### 引用数据类型

```
字符串 、 数组 、 类 、 接口 、 Lambda
对象、数组都是引用数据类型。
所有引用类型的默认值都是null。
```

#### 数据类型转换：

    自动类型转换(隐士)
        1、特点：代码不需要进行特殊处理，自动完成；
        2、规则：数据范围从小到大；不一定是按照字节；可以从int转换成long，long不能转换陈int
    强制类型转换(显士)   不推荐

### 特殊的转义字符序列。
    符号	  字符含义
    \n	    换行 (0x0a)
    \r	    回车 (0x0d)
    \f	    换页符(0x0c)
    \b  	退格 (0x08)
    \0  	空字符 (0x0)
    \s	    空格 (0x20)
    \t	    制表符
    \"	    双引号
    \'	    单引号
    \\	    反斜杠
    \ddd	八进制字符 (ddd)
    \uxxxx	16进制Unicode字符 (xxxx)

### ACCII  48--'0'   65--'A'  97--'a'

### 运算符: 算术运算符、关系运算符、位运算符、逻辑运算符、赋值运算符、其他运算符
    算术运算符:     +、-、*、/、%、++、--
    关系运算符:     >、>=、<、<=、==、!=
    位运算符:       &、|、^、~、<<、>>、>>>
    逻辑运算符:     &&、||、!
    赋值运算符:     +、+=、-=、*=、/=、%=、<<=、>>=、&=、^=、|=
    三元运算符:     (?:)   variable x = (expression) ? value if true : value if false
    instanceof:   (Object reference variable) instanceof (class/interface type)
    Java运算符优先级  

#### 方法入门

public class StudentDemo {
    public static void main(String[] args) {
        age();  // 调用方法
        System.out.println('zhangsan');
    }
    public static void age() {
        // 方法体
        System.out.println(20);
    }
}

### 脚本 jshell
    jshell
    System.out.println("Hello");
    /exit

### 流程控制
    顺序结构
    判断结构
    循环结构
    
    循环结构：for、while、do...while
        for(int x = 10; x < 20; x = x+1){}
        增强 for 循环语法格式如下:
            for(声明语句 : 表达式){
                //代码句子
            }
        声明语句：声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。
        表达式：表达式是要访问的数组名，或者是返回值为数组的方法。
    
    break 关键字
        break 主要用在循环语句或者 switch 语句中，用来跳出整个语句块。
        break 跳出最里层的循环，并且继续执行该循环下面的语句。
    
    continue 关键字
        continue 适用于任何循环控制结构中。作用是让程序立刻跳转到下一次循环的迭代。
        在 for 循环中，continue 语句使程序立即跳转到更新语句。
        在 while 或者 do…while 循环中，程序立即跳转到布尔表达式的判断语句。
    
    判断结构
        if
        if...else
        if...else if...else if...else
    
    switch-case 语句
        switch(expression){
            case value :
            //语句
            break; //可选
            case value :
            //语句
            break; //可选
            //你可以有任意数量的case语句
            default : //可选
            //语句
        }
        switch 语句中的变量类型可以是： byte、short、int 或者 char。从 Java SE 7 开始，switch 支持字符串 String 类型了，同时 case 标签必须为字符串常量或字面量。

### 方法重载



### 数组:用来存储固定大小的同类型元素。
    声明数组变量
        首先必须声明数组变量，才能在程序中使用数组。下面是声明数组变量的语法：
        dataType[] arrayRefVar;   // 首选的方法
        dataType arrayRefVar[];   // 效果相同，但不是首选方法
        double[] myList;          // 首选的方法
        double myList[];          // 效果相同，但不是首选方法
    创建数组
        1、dataType[] arrayRefVar = new dataType[arraySize];
        2、dataType[] arrayRefVar = {value0, value1, ..., valuek};    从 0 到 arrayRefVar.length-1。


### 类

    一个类可以包含以下类型变量：
        局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。
        成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。
        类变量：类变量也声明在类中，方法体之外，但必须声明为 static 类型。
    
    一个标准的类通常要拥有下面四个组成部分：
        1、所有的成员变量都是用private关键字修饰；
        2、为每一个成员变量编写一对 Getter 和 Setter 方法；
        3、编写一个无参数的构造方法；
        4、编写一个全参数的构造方法；
    
    构造方法
        每个类都有构造方法。如果没有显式地为类定义构造方法，Java 编译器将会为该类提供一个默认构造方法。
        在创建一个对象的时候，至少要调用一个构造方法。构造方法的名称必须与类同名，一个类可以有多个构造方法。
        构造方法是专门用来创建对象的方法，当我们通过关键字new来创建对象时，其实就是在调用构造方法。
        当一个对象被创建时候，构造方法用来初始化该对象。构造方法和它所在类的名字相同，但构造方法没有返回值。
        通常会使用构造方法给一个类的实例变量赋初值，或者执行其它必要的步骤来创建一个完整的对象。
        不管你是否自定义构造方法，所有的类都有构造方法；
        因为Java自动提供了一个默认构造方法，默认构造方法的访问修改符和类的访问修改符相同；
        一旦你定义了自己的构造方法，默认构造方法就会失效。
    
        注意事项：
            构造方法名必须和所在的类名称完全一样；
            构造方法不要写返回值，void 因为不写；
            如果没有编写构造方法，那么编译器将会默认赠送一个构造方法，没有参数、方法体 什么都不做；
            一旦编写至少一个构造方法，那么编译器将不再赠送；
            构造方法也是可以进行重载， 重载：方法名称相同，参数列表不同；
    
    finalize() 方法
        Java 允许定义这样的方法，它在对象被垃圾收集器析构(回收)之前调用，这个方法叫做 finalize( )，它用来清除回收对象。
        例如，你可以使用 finalize() 来确保一个对象打开的文件被关闭了。
        在 finalize() 方法里，你必须指定在对象销毁时候要执行的操作。
        finalize() 一般格式是：
            protected void finalize(){
            // 在这里终结代码
            }
        关键字 protected 是一个限定符，它确保 finalize() 方法不会被该类以外的代码调用。
        Java 的内存回收可以由 JVM 来自动完成。如果你手动使用，则可以使用上面的方法。
    
    成员变量：类中，方法外；
    成员方法：不加static ， public void eat() {}
    
    抽象方法 和 抽象类
        抽象方法：加上abstract关键字，然后去掉大括号，直接分号结束：
            public abstract void eat();
        抽象类：抽象方法所在的类，必须是抽象类；抽象类中可以含有成员方法：
    
            // 抽象类
            public abstract class Animal {
                // 抽象方法
                public abstract void eat();
                // 普通成员方法
                public void method() {
    
                }
            }
    
        抽象类和抽象方法的使用：
            1、不能直接创建new抽象类对象；
            2、必须用一个子类来继承抽象父类；
            3、子类必须覆盖重写抽象类中的所有的抽象方法；
            4、创建子类对象进行使用；
    
        抽象类的注意事项：
            1、抽象类不能创建对象，只能创建其非抽象子类的对象；
            2、抽象类可以有构造方法，是供子类创建对象时，初始化父类成员变量使用；
            3、抽象类中不一定包含抽象方法，但是有抽象方法的类一定是抽象类；
            4、抽象类的子类必须重写抽象父类中的所有抽象方法；
        
    super关键字用来访问父类内容，而this关键字用来访问本类内容；
        super：
            1、在子类的成员方法中， 访问父类的成员变量；
            2、在子类的成员方法中， 访问父类的成员方法；
            3、在子类的成员方法中， 访问父类的构造方法；
        this：
            1、在本类的成员方法中， 访问本类的成员变量；
            2、在本类的成员方法中， 访问本类的另一个成员方法；
            3、在本类的构造方法中， 访问本类的另一个构造方法
        this(...)调用也必须是构造方法的第一个语句，唯一一个；
        super和this两种构造调用，不能同时使用。

## static关键字：
    只属于类，不属于对象；只在类中保存唯一一份；
    使用类名调用；
    静态不能访问非静态，现有静态后又非静态；
    静态方法不能使用this关键字；
    静态代码块： static {  }
        当第一次用到本类时，静态代码块执行唯一的一次，静态内容总是优先于非静态，所以惊天代码块比构造方法先执行；
        
        静态代码块的用途：用来一次性地对静态成员变量进行赋值；


### 对象
    类是抽象的，有属性和行为；
    对象是具体的；
    创建对象格式：类名称 对象名 = new 类名称()；Student stu = new Student();
    使用 分为两种情况
        使用成员变量； 对象名.成员变量名；
        使用成员方法； 对象名.成员方法名(参数)

#### 面向对象
    三大特征：封装、继承、多态；extends集合或者implements实现，是多态性的前提；
    面向过程：
    面向对象：

### 继承性 (extends、implements）  extends集合或者implements实现，是多态性的前提；
    继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
    继承是多态的前提，如果没有继承，就没有多态；
    
    继承的特性：
        子类拥有父类非 private 的属性、方法;
        子类可以拥有自己的属性和方法，即子类可以对父类进行扩展;
        子类可以用自己的方式实现父类的方法;
        Java 的继承是单继承，但是可以多重继承;
        提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码独立性越差）。 
    继承关键字
        继承可以使用 extends 和 implements 这两个关键字来实现继承，
        而且所有的类都是继承于 java.lang.Object;
        当一个类没有继承的两个关键字，则默认继承object（这个类在 java.lang 包中，所以不需要 import）祖先类。
        java.lang 包中的类都不用引用，可以直接使用；
        extends关键字：在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。
        implements关键字：使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

### 覆盖重写  @override
    1、必须保证父子之间方法的名称相同，参数列表也相同；
    2、子类方法的返回值必须小于等于父类方法的返回范围；
    3、子类方法的权限必须大于等于父类方法的权限修饰符： public > protected > (default) > private;
        (default) 不是关键字default，而是什么都不写；

### 内部类
    成员内部类：
        内部类可以直接访问外部类；外部类访问内部类需要内部类对象；
        使用内部类：
            1、间接方式： 在外部类的方法中使用内部类，然后在main方法中调用外部类；
            2、直接方式： 创建内部类对象
                外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称();
        内部类的同名变量访问：
            System.out.println(num);  // 内部类的方法内变量；
            System.out.println(this.num);   // 内部类的成员变量；
            System.out.println(Outer.this.num);  // 外部类变量；
    
    局部内部类：定义在方法内部；
        定义一个类的时候，权限修饰符规则：
            1、外部类：public/ (default);
            2、成员内部类：public/ protected/ (default)/ private;
            3、局部内部类：什么都不写
    
        public class Outer {
            public void method() {
                class Inner {
                    public void methodInner() {
                        int num = 10;
                        System.out.println("这是内部类的方法" + num);
                    }
                }
                Inner inner = new Inner();
                inner.methodInner();
            }
        }
    
        如果希望访问所在方法的局部变量，那么这个变量就必须是有效的final的；从Java8+开始，只要局部变量事实不变，final关键字可以省略；
        原因：
            1、new出来的对象在堆内存当中；
            2、局部变量是跟着方法走的，在栈内存当中；
            3、方法运行结束之后，立刻出栈，局部变量就会立即消失；
            4、但是new出来的对象会在堆当中持续存在，知道垃圾回收消失；
    
    匿名内部类：
        如果类只使用一次，可以省略掉该类的定义，改为使用匿名内部类；
        匿名内部类是省略了实现类、子类名称，匿名对象是省略了对象名称；
        
        接口名称 对象名 = new 接口名称() {
            // 覆盖重写所有抽象方法
        }





### 接口
    接口就是多个类的公共规范。
    接口是一种引用数据类型，最重要的内容就是其中的：抽象方法；
    
    public interface 接口名称 {
        // 接口内容
    }
    备注： 换成了关键字interface之后，编译生成的字节码文件依然是： .java --> .class
    
    如果是Java7， 那么接口中可以包含的内容有：
        1、常量；
            接口中也可以定义成员变量，但是必须使用public static final三个关键字进行修饰；
            从效果上看，这其实就是接口的常量；
            public static final 数据类型 常量名称 = 数据值；
            主要事项：
                1、一旦使用final关键字进行修饰，说明不可以改变；
                2、接口中的常量，可以省略 public static final；也可以省略；
                3、接口中的常量，必须进行赋值；
                3、接口中的常量名称，使用完全大写字母，用下划线进行分割；（推荐）；
        2、抽象方法；
            public abstract void methodAbs();
            // 修饰符 public 和 abstract 是两个固定的关键字，可以选择性的省略
    如果是Java8，还可以额外包含有：
        1、默认方法；默认方法含有方法体，也可以被实现类重写；为了接口升级；
            public default 返回值类型 方法名称(参数列表) {
                // 方法体
            }
        2、静态方法；含有方法体；通过接口名称调用接口中的静态方法： 接口名称.静态方法(参数)；、
            public static void methodStatic() {
                // 方法体
            }
            
    如果是Java9，还可以额外包含有：
        1、私有方法；
            1、普通私有方法：解决多个 默认方法 之间重复代码问题；
                private 返回值类型 方法名称(参数) {
                    // 方法体
                }
            2、静态私有方法：解决多个 静态方法 之间重复代码问题；
                private static 返回值类型 方法名称(参数) {
                    // 方法体
                }
    
    接口的使用步骤：
        1、接口不能直接使用，必须有一个实现类来实现该接口； implements；
        2、接口的实现类必须重写（实现）接口中多有的抽象方法；
        3、创建实现类的对象，进行使用；
    
    注意事项：
        如果实现类并没有覆盖重写接口中所有的先后向方法，那么这个实现类自己就必须是抽象方法；
    
    接口注意事项：
        1、接口是没有静态代码块或者构造方法的；
        2、一个类的直接父类是惟一的，但是一个类可以同时实现多个接口；
        3、如果实现类多有的多个接口中，存在重复的抽象方法，那么实现类只需要覆盖重写一次即可；
        4、如果实现类没有覆盖重写所有接口中的多有抽象方法，那么实现类就必须是一个抽象类；
        5、如果实现类所实现的多个接口中，存在重复的默认方法，那么实现类一定要对冲突的默认方法进行覆盖重写；
        6、一个类如果直接父类当中的方法和接口当中的默认方法发生冲突，优先用父类当中的方法；
    
    接口之间的继承关系：
        1、类与类之间是单继承的，直接父类只有一个；
        2、类与接口之间是多实现的，一个类可以实现多个接口；
        3、接口与接口之间是多继承的；
    
        注意事项：
            1、多个父接口当中的抽象方法如果重复，没关系；
            2、过个父接口当中的默认方法如果重复，那么子接口必须进行默认方法的覆盖重写，而且带着default关键字；

### 多态性：一个对象具有多种形态；
    extends集合或者implements实现，是多态性的前提；
    
    代码当中体现多态，其实就一句话：父类引用指向子类对象；
    父类名称 对象名 = new 子类名称();   Fu obj = new Zi();
        Collection<String> coll = new ArrayList<>();
        Collection<String> coll = new HashSet<>();
    接口名称 对象名 = new 实现类名称();   // 接口指向一个实现类
    
    多态中访问成员变量的两种方法：
        1、直接通过对象名称访问成员变量：看等号左边是谁，优先用谁，没有则向上找；
            Fu obj = new Zi();
            System.out.println(obj.num);   // 优先在父类中找；
        2、间接通过成员方法访问成员变量：看该方法属于谁，优先用谁，没有则向上找；
            Fu obj = new Zi();
            obj.showNum();  // 优先找子类；
    
    多态中访问成员方法： 看new的是谁，就优先用谁，没有则向上找；编译看左，运行看右；
            Fu obj = new Zi();
            obj.methodZi();  // 错误写法，因为obj是父类，父类中没有methodZi()方法；
            obj.method()   // 正确写法，obj是父类，父类中有method()方法，但是运行的时候首先看子类中有没有method重写；
    
    向上转型：其实就是多态： 父类名称 对象名 = new 子类名称();
        创建子类对象，把其当做父类来看待和使用；
        但是向上转型无法使用子类特有的方法，解决方案：向下转型；
    向下转型：其实就是还原： 子类名称 对象名 = (子类名称) 父类对象;
        将父类对象，还原 成原来的子类对象。
        如何才能知道父类引用的对象本来的子类？使用instanceof
            对象 instanceof 类名称；返回一个布尔值；判断前面的对象能不能当做后面类型的实例；

#### 常用API  (Application Programming Interface)
    Scanner / Random / ArrayList / String / Arrays / Math / Object / Date /

### Scanner 获取键盘中输入的内容
    1、导包 import java.util.Scanner;
    2、创建对象   Scanner sc = new Scanner(System.in);  // new Scanner(System.in) 是固定格式
    3、使用：
        整数： int num = sc.nextInt();
        字符串： String str = sc.next();

### Random
    1、导包 import java.util.Random;
    2、创建对象： Random ran = new Random();
    3、使用： 
        int num = ran.nextInt();
        int num = ran.nextInt(9);  [0-9)
        int num = ran.nextInt(9) + 1;  [1-9]

### ArrayList 集合
    集合长度可以改变，数组一旦被定义，长度就不可以被改变；
    ArraayList<String> list = new ArrayList<String>();
    JDK1.7以后，等号右边肩括号中的泛型可以不写： ArrayList<String> list = new ArrayList<>();
    泛型：只可以是引用类型，不可以是基本类型，基本类型没有地址，但是可以使用包装类；
    
    基本数据类型 （四类八种）范围跟内存占用不一定有关
        1、整数型 : byte(1) 、 short(2) 、 int(4) 、 long(8)
        2、浮点型 : float(单精度 4个字节) 、 double(默认 双精度 8个字节)
        3、字符型 : char(2)
        4、布尔型 : boolean(1)
    
        |-------------------------|
        |  基本类型  |   包装类     | 
        |-----------|-------------|
        |  byte     |   Byte      |
        |  short    |   Short     |
        |  long     |   Long      |
        |   int     |  Integer    |
        |  float    |   Float     |
        |  double   |   Double    |
        |   char    |  Character  |
        |  boolean  |   Boolean   |
        |-------------------------|
    
    引用数据类型（后面具体介绍）
        字符串 、 数组 、 类 、 接口 、 Lambda
    
    ArrayList 中常用的方法：
        1、public boolean add(E e);     ->  list.add("zhang");
        2、public E get(int index);     ->  String name = list.get(2);
        3、public E remove(int index);  ->  String name = list.remove(2);
        4、public int size()            ->  int size = list.size();

### String
    程序中的所有的双引号字符串，都是 String 类的对象（就算没有new也照样是）
    字符串的特点：
        1、字符串的内容用不可变，所以字符串是可以共享使用；
        2、字符串效果上相当于是char[]字符数组，但是底层原理是byte[]字节数组；
    对于引用类型来说， == 进行的是地址值得比较；
    双引号直接写的字符串在常量池当中，new的不在池当中;
    
    创建方法（3+1）三种构造方法 + 一种直接创建
        1、创建空字符：public String()
            String str = new String();
        2、public String(char[] array)
            char[] arr = {'a','b','c'};
            String str = new String(arr);
        3、public String(byte[] array)
            byte[] arr2 = {97,98,99};
            String str2 = new String(arr2);
            System.out.println(str2);   // abc
        4、String str = "zhang";
    
    字符串中的常用方法：
    
        1、比较：equals  具有对称性 区分大小写：
            "abc".equals(str)  推荐变量写在后面，如果变量写在前面时，若为空字符串，则会报错；
            str1.equalsIgnoreCase(Str2)  忽略大小写；
    
        2、
            public int length()  ->  str.length();
            public String concat(String str) -> str3 = str1.concat(str2)
            public char charAt(int index)    ->  char ch = str.charAt(2)  // str第二个字符（从0开始）
            public int indexOf(String str)   ->  int n = str.indexOf(str1)  // str中第一次出现str1字符串的位置，如果没有返回-1；
    
        3、字符串截取：
            public String substring(int index)  ->  str.substring(3)
            public String substring(int begin, int end) ->  str.substring(3,5)
    
        4、字符串转换：
            public char[] toCharArray();
                char[] arrs = str1.toCharArray();
                for (char arr : arrs) {
                    System.out.println(arr);
                }
            public byte[] getBytes();
                byte[] a = str1.getBytes();
                for (byte b : a) {
                    System.out.println(b);
                }
            public String replace(charSequence oldString, CharSequence newString);
                String str2 = println(str1.replace("b","c");  // str1中的b替换成c
    
        5、分割：参数其实是一个正则表达式  . => \\.
            public String[] split(String regix);
                String strstr = "a,b,c,d,1";
                String[] ss = strstr.split(",");
                for (String sss : ss){
                    System.out.println(sss);
                } 

### Arrays
    public static String toString(arr)  -> String str = Arrays.toSring(arr);
    public static void sort(arr)    ->  升序排序  Arrays.sort(arr)

### Math
    public static double abs(double num);   Math.abs();   // 绝对值
    public static double ceil(double num)   Math.ceil();  // 向上取整
    public static double floor(double num)  Math.floor(); // 向下取整
    public static long round(double num)    Math.round(); // 四舍五入
    
    Math.PI         圆周率


### Object类
    java.lang.Object类是Java语言中的根类，即所有类的父类。它中描述的所有方法子类都可以使用。在对象实例化的时候，最终找的父类就是Object。
    如果一个类没有特别指定父类，那么默认则继承自Object类。
    
    toString方法：public String toString()：返回该对象的字符串表示。
        public String toString()：返回该对象的字符串表示。
        toString方法返回该对象的字符串表示，其实该字符串内容就是对象的类型+@+内存地址值。
        由于toString方法返回的结果是内存地址，而在开发中，经常需要按照对象的属性得到相应的字符串表现形式，因此也需要重写它。
        覆盖重写：如果不希望使用toString方法的默认行为，则可以对它进行覆盖重写。
        在我们直接使用输出语句输出对象名的时候,其实通过该对象调用了其toString()方法。
    
    equals：public boolean equals(Object obj)：指示其他某个对象是否与此对象“相等”。
        默认比较两个方法的地址值
        public boolean equals(Object obj) {}

### Date
    java.util.Date:表示如期和时间的类；
    毫秒：千分之一秒
    
    Date类常用的方法：两个构造方法，一个成员方法：
    1、Date date = new Date();
    2、Date date1 = new Date(1602077494533L);
    3、date.getTime()

### DateFormat类
    java.text.DateFormat 日期/时间格式化子类的抽象类；











#### 泛型

### 使用泛型：
    1、避免了类型转换的麻烦，存储的是什么类型，取出的就是什么类型；
    2、把运行期的异常(代码运行之后会抛出的异常)，提升到了编译期(写代码的时候会报错)；
    
    // 使用泛型：
    pivate static void interator01() {
        ArrayList<String> list = new ArrayList<>();
        list.add("abc");
        // list.add(1) // 编译期会报错，定义泛型为String类型；
        // 使用迭代遍历list集合；获取迭代器
        Iterator<String> it = list.iterator();
        while(it.hasNext()) {
            String s = it.next();
            System.out.println(s+"->"+s.length());
        }
    }
    
    // 不使用泛型
    private static void interator02() {
        ArrayList list = new ArrayList();
        list.add("abc");
        list.add(1);  // 运行的时候会报错，不能把Integer类型转换为String类型
        // 使用迭代遍历list集合；获取迭代器
        Iterator it = list.interator();
        while(it.hasNext()) {
            // 取出的元素也是object类型
            Object obj = it.next();
            // 想要使用String类型特有的方法length，获取字符串的长度；
            // 不能使用
            // 多态 object obj = "abc";
            // 需要向下转型
            // 运行的时候会报错，不能把Integer类型转换为String类型
            String s = (String)obj;
            System.out.println(s.length());
        }
    }

### 泛型的定义与使用
    在集合中会大量使用到泛型；
    泛型，用来灵活地将数据类型应用到不同的类、方法、接口当中。将数据类型作为参数进行传递。
    
    定义和使用含有泛型的类： 修饰符 class 类名<代表泛型的变量> {  }
    
    定义一个含有泛型的类，模拟ArrayList集合
        泛型是一个位置的数据类型，当我们不确定什么数据类型的时候，可以使用泛型
        泛型可以接受任意的数据类型，可以使用Integer，String，Student...
        创建对象的时候确定泛型的数据类型
    
        public class GenericClass<E> {
            private E name;
        }
    
    定义含有泛型的方法 泛型定义在方法的修饰符和返回值类型之间 可以是任意字母
        修饰符 <泛型> 返回值类型 方法名(参数列表-使用泛型) {  }
    
        // 普通方法
        public <M> void method01(M m) {
            System.out.println(m);
        }
    
        // 静态方法调用建议使用类名直接调用，不需要创建对象使用
        public static <S> void method02(S s) {
            System.out.println(m);
        }
    
    含有泛型的接口
        有两种使用方式：
        1、重写方法是定义泛型；
        2、创建对象的时候定义；
        修饰符 interface 接口名 <泛型> {  }
    
        public interface MyGenericInterface<E>{
            public abstract viod add(E e);
            public abstract E getE();
        }

### 泛型通配符
    当使用泛型类或者接口时，传递的语句中，泛型类型不确定，可以通过通配符<?>表示。
    但是一旦使用泛型的通配符后，只能使用Object类中的共性方法，集合中圆度自身方法无法使用。
    
    通配符
        泛型的通配符：不知道使用说明类型来接收的时候，此时可以使用？，？表示位置通配符；
        此时只能接收数据，不能往该集合中存储数据。
    
    泛型的 上限 和 下限 使用
        类之间的继承关系：
        Integer extends Number extends Object
        String extends Object
        泛型的上限限定： ？ extends E     代表使用的泛型只能是E类型的子类/本身；
        泛型的上限限定： ？ super E     代表使用的泛型只能是E类型的父类/本身；

#### 集合框架 Collection Map
    集合按照其存储结构可以分为两大类:
    1、单列集合 java.util.Collection
        Collection<E>
    2、双列集合 java.util.Map
        Map(K, V)
        两个泛型
        Map集合是一个双列集合，一个元素可以包含两个值（一个key，一个value）
        Map集合中的元素，key和value的数据类型可以相同，也可以不同
        Map集合中的元素，key是不允许重复的，value是可以重复的
        Map集合中的元素，key和value是意义对应
    
    Collection 单列集合累的跟接口，有两个重要的子接口：
    1、java.util.List ：元素有序、元素可重复；
    2、java.util.Set ：无序的、元素不可以重复；
    
    List 接口的主要实现类有：
    1、java.util.ArrayList
    2、java.util.LinkedList
    
    Set 接口的主要实现类有：
    1、java.util.HashSet
    2、java.util.TreeSet

#### 集合： 集合是java中提供的一种容器，可以用来存储多个数据；
    集合和数组都是容器；
    数组的长度是固定的，集合的长度是可变的；
    数组中存储的是同一类的元素，可以存储基本数据类型值；
    集合存储的都是对象，对象类型可以不一致；



### Collection集合：是 所有 单列集合 的 父接口(根接口);
    Collection 常用的功能
        1、public boolean add(E e) :把给定的对象添加到集合中；
        2、public void clear() : 清空集合中所有的元素；
        3、public boolean remove(E e) :把给定的对象在集合中删除；
        4、public boolean contains(E e) :判断当前集合是否含有给定的对象；
        5、public boolean isEmpty(E e) :判断当前对象是否为空；
        6、public int size() :返回集合中元素的个数；
        7、public Object[] toArray :把集合中的元素存储到数组中。

### List接口 extends Collection接口
    1、有序的集合，存储元素和取出元素的顺序是一直的；
    2、有索引，包含了一些带索引的方法；
    3、允许存储重复的元素；
    
    List接口带有索引的方法（特有）
    1、public void add(int index, E element) : 将指定元素添加到指定的位置上；
    2、public E get(int index) : 返回集合中指定位置的元素；
    3、public E remove(int index) : 移除指定位置的元素，返回的是被移除的元素；
    4、public E set(int index, E element) : 用指定元素替换集合中指定位置的元素，返回的是被替换的元素；
    
    ArrayList 底层是数组结构，查询快，增删慢；
        ArrayList<String> list = new ArrayList<>();
    LinkedList 底层是链表结构，查询慢，增删快，里面包含了大量操作首尾元素的方法：
        注意：使用LinkedList特有的方法时，不能使用多态，多态的弊端是看不到子类特有的方法；
        创建LinkedList 集合对象： LinkedList<String> linked = new LinkedList<>();
        1、public void addFirst(E e)  // 将指定元素插入此列表的开头；
        2、public void addLast(E e)  // 将指定元素插入此列表的结尾； 等效于add；
        3、public E getFirst(E e)  // 返回此列表的第一个元素；
        4、public E getLast(E e)  // 返回此列表的最后一个元素；
        5、public E removeFirst(E e)  // 移除并返回列表的第一个元素；
        6、public E removeLast(E e)  // 移除并返回列表的最后一个元素；
        7、public E pop(E e)  // 等效于removeFirst
        8、public void push(E e) // 等效addLast；
        9、public boolean isEmpty() 
    Vector 底层是数组结构,由于是单线程，已经被ArrayList取代（了解即可）

### set 接口 extends Collection 接口
    1、不允许存储重复的元素；
    2、没有索引，没有带索引的方法，也不能使用普通的for循环遍历，使用迭代器或者增强for循环遍历；
    
    java.uril.HashSet 集合 implements Set 接口
        1、不允许存储重复的元素；
        2、没有索引，没有带索引的方法，也不能使用普通的for循环遍历，使用迭代器或者增强for循环遍历；
        3、是一个无序的集合，储存元素和取出元素的顺序有可能不一致；
        4、底层是一个哈希表结构（查询的速度非常快）；

### 哈希值 ： 是一个十进制的整数，由系统随机给出（就是对象的地址值，是一个逻辑地址，是模拟出来得到的地址，不是实际存储的物理地址）
    在Object类有一个方法，可以获取对象的哈希值：
    int hashCode() 返回该对象的哈希码值
    hashCode方法的源码：
        public native int hashCode();
        native: 代表该方法调用的是本地操作系统的方法
    
    HashSet 集合存储数据的结构（哈希表：查询速度快）
    jdk1.8版本之前：哈希表 = 数组 + 链表
    jdk1.8版本之后：
        哈希表 = 数组 + 链表；
        哈希表 = 数组 + 红黑树 （提高查询的速度）
        数组结构：把元素进行了分组（相同哈希值的元素是一组）；
        链表、红黑树结构：把相同哈希值的元素连接到一起；
    
    LInkedHashSet：底层是一个哈希表（数组+链表/红黑树）+链表；多了一条链表（记录元素的储存顺序），保证元素有序
    java.util.LInkedHashSet集合 extends HashSet集合

### 可变参数 JDK1.5之后出现的新特征   修饰符 返回值类型 方法名(数据类型...变量名){   }
    使用前提：方法的参数列表数据类型确定，个数不确定；
    注意事项：
        一个方法的参数列表，这能有一个可变参数；
        如果方法的参数有多个，那么可变参数必须写在参数列表的末尾；
    可变参数原理：底层及时一个数组，根据传递参数个数不同，会创建不同长度的数组；
    可变参数的特殊（终极）写法： public static void method(Object...obj) {   }

#### Iterator迭代器 (主要用于迭代访问(即遍历)Collection中的元素)
    java.util.Iterator
    public Iterator iterator() : 用于获取集合对应的迭代器，用来遍历集合中的元素；

### 迭代： Collection集合元素的通用获取方式。
    在取元素之前要先判断集合中有没有元素，如果有，就把这个元素取出来，继续判断。一直把集合中的所有元素全部取出；
    
    Iterator 接口的常用方法如下：
    1、public E next() : 返回迭代的下一个元素；
    2、public boolean hasNext() : 如果仍有元素可以迭代，则返回true；
    
    Iterator迭代器 是一个接口，我们无法直接使用，需要使用Iterator接口的实现类对象；获取实现类的方式比较特殊；
    Collection接口中有一个方法，叫Iterator(), 这个方法返回的就是迭代器的实现类对象；
    Iterator<E> iterator() 返回在此Collection的元素上进行迭代的迭代器；
    
    迭代器的是不步骤：
    1、使用集合中的方法Iterator()获取迭代器的实现类对象，使用Iterator接口接收(多态);
        Collection<String> coll = new ArrayList<>();
        Iterator<String> it = coll.iterator();  // 迭代器的泛型跟集合保持一致
    2、使用Iterator接口中的方法hasNext()判断还有没有下一个元素；
    3、使用Iterator接口中的方法next取出集合中的下一个元素；
        while(it.hasNext()) {
            String e = it.next();
            System.out.println(e);
        }

### 增强for循环 (可以替代遍历器)
    增强for循环(也称for each 循环)是JDK1.5以后出来的一个高级for循环，专门用来遍历数组和集合的；
    增强for循环的内部原理其实就是Iterator迭代器，所以在遍历的过程中，不能对集合中的元素进行增删操作；
    
    for(元素的数据类型 变量 : Collection集合or数组) {
        // 操作代码
    }

### demo

    public class Puke {
        public static void main(String[] args) {
            ArrayList<String> contain = new ArrayList<>();
            String[] colors = {"♥","♦","♠","♣"};
            String[] numbers = {"2","A","K","Q","J","10","9","8","7","6","5","4","3"};
            contain.add("大王");
            contain.add("小王");
            for (String number : numbers){
                for (String color : colors){
                    contain.add(color + number);
                }
            }
            Collections.shuffle(contain);
            ArrayList<String> wanjia01 = new ArrayList<>();
            ArrayList<String> wanjia02 = new ArrayList<>();
            ArrayList<String> wanjia03 = new ArrayList<>();
            ArrayList<String> dipai = new ArrayList<>();
            for (int i=0; i<contain.size(); i++){
                String p = contain.get(i);
                if(i>=51){
                    dipai.add(p);
                }else if(i%3==0){
                    wanjia01.add(p);
                }else if(i%3==1){
                    wanjia02.add(p);
                }else if(i%3==2){
                    wanjia03.add(p);
                }
            }
            System.out.println("玩家1: " + wanjia01);
            System.out.println("玩家2: " + wanjia02);
            System.out.println("玩家3: " + wanjia03);
            System.out.println("底 牌: " + dipai);
        }
    }

#### Collections addAll / shuffle / sort
    java.util.Collections 是几个工具类，用来对集合进行操作：
    public static <T> boolean addAll(Collections<T> c, T...element) : 往集合中添加一些元素；
    public static void shuffle(List<?> list) : 打乱集合顺序；  必须是list集合
    public static <T> void sort(List<?> list) : 将集合中元素按照默认规则（升序）排序；  必须是list集合   Collections.sort(list01);
        被排序的集合里边存储元素。必须实现Comparable。重写接口中的方法compareTo定义排序规则
        Comparable接口的排序规则： 自己（this) - 参数 ：升序
        package com.baidu.test.demo05;
    
            public class Person implements Comparable<Person> {
                @Override
                public int compareTo(Person o) {
                    // return 0;  // 元素都是相同的
                    return this.age - o.age;
                }
            }
    
            ArrayList<Person> list03 = new ArrayList<>();
            list03.add(new Person("zhangsan",18));
            list03.add(new Person("wangwu",20));
            list03.add(new Person("chenliu",19));
            list03.add(new Person("lisi",21));
            System.out.println(list03);
            Collections.sort(list03);
            System.out.println(list03);
    
    public static <T> boid sort(List<T> list, Comparator<? super T>) : 将集合中元素按照指定规则排序；  必须是list集合
        Comparator 和 Comparable 的区别：
            Comparable： 自己（this)和别人参数比较，自己需要实现Comparator接口，重写比较的参数compareTo方法
            Comparator：相当于找一个第三方的裁判，比较两个；
    
                ArrayList<Person> list03 = new ArrayList<>();
                list03.add(new Person("zhangsan",18));
                list03.add(new Person("wangwu",20));
                list03.add(new Person("chenliu",19));
                list03.add(new Person("lisi",21));
                System.out.println(list03);
    
                Collections.sort(list03, new Comparator<Person>() {
                    @Override
                    public int compare(Person o1, Person o2) {
                        // return 0;
                        return o2.getAge() - o1.getAge();
                    }
                });
                System.out.println("list03" + list03);

#### Map集合  Map(K, V)
    两个泛型
    Map集合是一个双列集合，一个元素可以包含两个值（一个key，一个value）
    Map集合中的元素，key和value的数据类型可以相同，也可以不同
    Map集合中的元素，key是不允许重复的，value是可以重复的
    Map集合中的元素，key和value是意义对应
    java.util.HashMap<k, v>集合 implements Map<k, v> 接口
    HashMap集合的特点：
        1、HashMap集合底层是哈希表：查询的速度特备得快
            JDK1.8 之前：数组+单向链表
            JDK1.8 之后：数组+单向链表/红黑树（链表长度超过8）：提高查询速度
        2、HashMap集合是一个无序的集合，存储元素和取出元素的顺序有可能不一致；
    java.util.LinkedHashMap<k, v>集合 implements HashMap<k, v> 集合
    LinkedHashMap 集合的特点：
        1、LinkedHashMap集合底层是哈希表： 保证迭代的顺序
        2、LinkedHashMap集合是一个有序的集合，存储元素和取出元素的顺序是一致的；

### Map接口中的常用方法： put / remove / get / containsKey 
    public V put(K key, V value) : 把指定的键与指定的值添加到Map集合中；  没有key的时候，返回null，如果key存在，返回key对应的value；
        map.put("李晨", "范冰冰2");
    public V remove(Object key) : 把指定的键 所对应的值与元素在Map集合中删除，返回别山车元素的值；
        key存在返回对应的value，key不存在，返回null；
    public V get(Object key) : 根据指定的键，在Map集合中获取对应的值；
    boolean containsKey(Obkect key) : 判断集合中是否包含指定的键；
    
    public Set(k) keySet() : 获取Map集合中所有的键，存储到Set集合中；
    public Set<Map.Entry<K, V>> entrySet() : 获取到Map集合中所有的键值对对象的集合（Set集合）；
    
    Map 集合遍历：
        1、通过键找值的方式；public Set(k) keySet() : 获取Map集合中所有的键，存储到Set集合中；
            a、使用Map集合中的方法keySet()，把Map集合所有的key取出来，存储到一个Set集合中；
            b、遍历Set集合，获取Map集合中的每一个key；（迭代器或者增强for循环）
            c、通过Map集合中的方法get(key)，通过key找到vlaue；
        2、使用Entry对象遍历： public Set<Map.Entry<K, V>> entrySet() : 获取到Map集合中所有的键值对对象的集合（Set集合）；
            a、使用Map集合中的方法entrySet()，把Map集合中多个Entry对象取出来，存储到一个Set集合中；
            b、遍历Set集合，获取每一个Entry对象；
            c、使用Entry对象中的方法getKey() 和 getValue() 获取键与值；
    
        // 通过键找值的方式；
        public static void main(String[] args) {
            Map<String, Integer> map = new HashMap<>();
            map.put("迪丽热巴", 165);
            map.put("古力娜扎", 160);
            map.put("梅梅", 170);
            map.put("李志玲", 168);
            map.put("李冰冰", 164);
            System.out.println(map);
            System.out.println("=========");
            Set<String> set = map.keySet();
            System.out.println(set);
            System.out.println("=========");
            Iterator<String> it = set.iterator();
            // 使用迭代器
            while (it.hasNext()) {
                String e = it.next();
                // System.out.println(e);
                Integer value = map.get(e);
                System.out.println(e + "=" + value);
            }
            System.out.println("=========");
            // 使用增强for循环
            for (String name : set) {
                // System.out.println(name);
                Integer value = map.get(name);
                System.out.println(name + "=" + value);
            }
        }
    
        // 使用Entry对象遍历
        public static void main(String[] args) {
            Map<String, Integer> map = new HashMap<>();
            map.put("迪丽热巴", 165);
            map.put("古力娜扎", 160);
            map.put("梅梅", 170);
            map.put("李志玲", 168);
            map.put("李冰冰", 164);
            System.out.println(map);
            System.out.println("===============");
            Set<Map.Entry<String, Integer>> set = map.entrySet();
            System.out.println(set);
            System.out.println("===============");
            // 使用迭代器
            Iterator<Map.Entry<String, Integer>> it = set.iterator();
            while (it.hasNext()) {
                Map.Entry<String, Integer> entry = it.next();
                String key = entry.getKey();
                Integer value = entry.getValue();
                System.out.println(key +"--"+ value);
            }
            System.out.println("--------------");
            // 使用增强for循环
            for (Map.Entry<String, Integer> entry : set) {
                String key = entry.getKey();
                Integer value = entry.getValue();
                System.out.println(key +"--"+ value);
            }
        }

### HashMap存储自定义类型键值
    key:Person类型
        Person类就必须重写hashCode方法和equal方法，以确保key唯一；
    value：String类型：可以重复；
    
    public static void main(String[] args) {
        demo01();
        demo02();
    }
    private static void demo02() {
        HashMap<Person, String> map = new HashMap<>();
        map.put(new Person("张三", 23), "北京");
        map.put(new Person("李四", 24), "上海");
        map.put(new Person("王五", 25), "广州");
        map.put(new Person("陈六", 26), "深圳");
        map.put(new Person("张三", 23), "河南");
        Set<Map.Entry<Person, String>> set = map.entrySet();
        for (Map.Entry<Person, String> entry : set) {
            Person key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + "===" + value);
        }
    }
    private static void demo01() {
        HashMap<String, Person> map = new HashMap<>();
        map.put("北京", new Person("张三", 23));
        map.put("上海", new Person("李四", 24));
        map.put("广州", new Person("王五", 25));
        map.put("深圳", new Person("陈六", 26));
        map.put("河南", new Person("周七", 27));
        Set<String> set = map.keySet();
        for (String key : set) {
            Person value = map.get(key);
            System.out.println(key + "===" + value);
        }
    }

### LinkedHashMap
    java.util.LinkedHashMap<K, V> extends HashMap<K, V>
    Map接口的哈希表和链接列表实现，具有可预知的迭代顺序。key也不允许重复；
    底层：哈希表+链表（记录元素的顺序）

### Hashtable
    java.util.Hashtable<K, V> 集合 implements Map<k, V>接口
    
    Hashtable：底层也是一个哈希表，是一个线程安全的集合，是单线程，速度慢；
    HashMap： 底层是一个哈希表，是一个线程不安全的集合，是多线程的集合，速度快；
    
    HashMap集合（之前学的所有的集合）：可以存储null值，null键；
    Hashtable集合，不能存储null值和null键；
    
    Hashtable 和 Vector 集合一样，在JDK1.2之后被更先进的集合（HashMap，ArrayList）取代了；
    Hashtable的子类Properties依然活跃；
    Properties集合是一个唯一和IO流结合的集合；

### demo
    // 统计一个字符串中每个字符出现的次数：
    public static void main(String[] args) {
        System.out.println("请输入字符串...");
        Scanner sc = new Scanner(System.in);
        String str = sc.next();
        System.out.println("输入的字符串为：" + str);
        tongji(str);
    }
    
    private static void tongji(String str) {
        HashMap<Character, Integer> map = new HashMap<>();
        char[] chs = str.toCharArray();
        for (int i = 0; i < chs.length; i++) {
            if(map.get(chs[i]) == null) {
                map.put(chs[i], 1);
            }else {
                Integer num = map.get(chs[i]) + 1;
                map.put(chs[i], num);
            }
        }
        Set<Map.Entry<Character, Integer>> set = map.entrySet();
        for (Map.Entry<Character, Integer> entry : set) {
            Character key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(key +"出现的次数为："+ value);
        }
    }
    
    public static void main(String[] args) {
        List<String> colors = List.of("♥", "♦", "♠", "♣");
        List<String> numbers = List.of("2", "A", "K", "Q", "J", "10", "9", "8", "7", "6", "5", "4", "3");
        HashMap<Integer, String> map = new HashMap<>();
        ArrayList<Integer> list = new ArrayList<>();
        map.put(0, "大王");
        map.put(1, "小王");
        Integer i = 2;
        for (String number : numbers) {
            for (String color : colors )  {
                map.put(i, color + number);
                i++;
            }
        }
        Set<Map.Entry<Integer, String>> set = map.entrySet();
        for (Map.Entry<Integer, String> entry : set) {
            list.add(entry.getKey());
        }
        Collections.shuffle(list);
        ArrayList<Integer> wanjia01 = new ArrayList<>();
        ArrayList<Integer> wanjia02 = new ArrayList<>();
        ArrayList<Integer> wanjia03 = new ArrayList<>();
        ArrayList<Integer> dipai = new ArrayList<>();
        for (int j = 0; j < list.size(); j++) {
            Integer p = list.get(j);
            if (j>50) {
                dipai.add(p);
            }else if (j%3 == 0) {
                wanjia01.add(p);
            }else if (j%3 == 1) {
                wanjia02.add(p);
            }else if (j%3 == 2) {
                wanjia03.add(p);
            }
        }
        Collections.sort(wanjia01);
        Collections.sort(wanjia02);
        Collections.sort(wanjia03);
        Collections.sort(dipai);
        lookPoker("wanjia01", map, wanjia01);
        lookPoker("wanjia02", map, wanjia02);
        lookPoker("wanjia03", map, wanjia03);
        lookPoker("dipai", map, dipai);
    }
    private static void lookPoker(String name, HashMap<Integer, String> map, ArrayList<Integer> list) {
        System.out.print(name + " : ");
        for (Integer key : list) {
            String value = map.get(key);
            System.out.print(value + " ");
        }
        System.out.println();
    }

###

#### 异常：程序在执行过程中，出现的非正常的情况，最终导致JVM的非正常停止；

### 异常
    在java等面向对象的编程语言中，异常本身是一个类，产生异常就是创建一项对象并抛出一个异常对象，java处理意向的方式是终端处理；
    
    异常体系
        异常机制其实是帮助我们找到程序中的问题，意向的根类是java.lang.Throwable,其下面有两个子类：
        java.lang.Error 与 java.lang.Exception ，平常所说的意向指java.lang.Exception;
        Throwable中常用的方法：
            publicvoid printStackTrace() : 打印异常的详细信息；
                包含了异常的类型，异常的原因，还有异常出现的位置，在开发和调试阶段，都要使用printStackTrace；
            public String getMessage() : 获取异常的原因；
                提示给用户的时候，就提示异常的原因；
            public String toString() : 获取异常的类型和异常描述信息（不用）
    异常分类
        Exception：编译器异常，进行编译（写代码）java程序出现的异常；
        RuntimeException：运行期异常，java程序运行过程中出现的问题
        Error：错误
    异常产生的过程

### 异常的处理
    java异常处理的五个关键字： try / catch / finally / throw / throws
    
    抛出异常 throw
        可以使用throw关键字在指定的方法中抛出指定的异常
        throw new xxxException("异常产生的原因");
        注意：
            1、throw关键字必须在方法的内部；
            2、throw关键字后边new的对象必须是Exception或者Exception的子类对象；
            3、throw关键字抛出指定的异常对象，我们必须处理这个异常对象；
                a、throw关键字后边创建的是RuntimeException或者是RuntimeException的子类对象，我们可以不处理，默认交给JVM处理（打印异常对象，中断程序）
                b、throw关键字后边创建爱你的是编译异常（写代码的时候报错），我们就必须处理这个异常，要么throws，要么try...catch
        工作中我们首先必须对方法传递火来的参数进行合法性校验：
        如果参数不合法，那么我们就必须使用抛出异常的方式，告知方法的调用者，传递参数有问题：
        注意：
            NullPointerException 是一个运行期异常，我们不用处理，默认交给JVM处理
                if(arr == null){
                    throw new NullPointerException("传递的数组的值为null");
                }
                
            ArrayIndexOutOfBoundsException 是一个运行期异常，我们不用处理，默认交给JVM处理
                if(index < 0 || index > arr.length - 1){
                    throw new ArrayIndexOutOfBoundsException("传递的索引超出了数组的使用范围");
                }

### Objects中的静态方法 非空判断
public static <T> T requireNonNull(T obj) : 查看指定引用对象不是null
    Object.requireNonNull(obj);
    Object.requireNonNull(obj, 传递的对象的值为null);

    throws 关键字：异常处理的第一种方式，交给别人处理
        当方法内部抛出异常对象的时候，那么我们就必须处理这个异常：
        可以使用throws关键字处理异常对象，会把异常对象声明抛出给方法的调用者处理（自己不处理，给别人处理），最终交给JVM处理 --> 中断处理
        修饰符 返回值类型 方法名(参数列表) throws AAAException, BBBException... {
            throw new AAAException("产生的原因");
            throw new BBBException("产生的原因");
        }
        注意：
            1、throws关键字必须写在方法声明处；
            2、throws关键字后边声明的异常处理是Exception 或者Exception的子类；
            3、方法内部如果抛出多个异常对象，那么throws后边必须也声明多个异常；
                如果抛出的多个异常对象有父子类关系，那么直接声明父类异常即可；
            4、调用了一个声明排除异常的方法，我们就必须处理声明的异常
                那么继续使用throws声明抛出，交给方法的调用者处理，最终交个JVM；
                要么try...catch自己处理异常
    
            public class Yichang02 {
                public static void main(String[] args) throws FileNotFoundException,IOException {
                    readFile("c:\\a.txt");
                }
                // FileNotFoundException 是 IOException 的子类
                // public static void readFile(String fileName) throws FileNotFoundException,IOException {
                public static void readFile(String fileName) throws IOException {
                    if (!fileName.equals("c:\\a.txt")){
                        throw new FileNotFoundException("传递的文件路径不是 c:\\a.txt");
                    }
                    if (!fileName.endsWith(".txt")){
                        throw new IOException("后缀名不是 .txt");
                    }
                    System.out.println("后续代码");
                }
            }
    
    try...catch
        try{
            // 可能产生异常的代码
        }catch(定义一个异常的变量，用来接收try中抛出的异常对象){
            异常的处理逻辑，异常对象之后，怎么处理异常对象
            一般在工作中，把异常的信息记录到一个日志中
        }
        ...catch(异常类名 变量名){
    
        }
    注意：
        1、try中可能抛出多个异常对象，那么就可以使用多个catch来处理这些异常对象；
        2、如果try中产生了异常，那么就会执行catch中的异常处理逻辑，执行完毕catch中的处理逻辑，继续执行try..catch之后的代码
            如果try中没有产生异常，那么就不会执行catch中异常的异常逻辑，执行完try中的代码，继续执行try...catch之后的代码
    
            public static void main(String[] args) {
                try {
                    test("d:\\a.txt");
                } catch (IOException e) {
                    e.printStackTrace();
                }
                System.out.println("后续代码！！！");
            }
    
            private static void test(String fileName) throws IOException {
                if(!fileName.endsWith(".txt")){
                    throw new IOException("文件后缀名不对");
                }
                System.out.println("文件后缀名没有问题");
            }
    
    Throwable 类中定义了三个异常处理方法：
        1、String getMessage() 返回此 throwable 的简短描述；
        2、String toString() 返回此 throwable 的详细消息字符串；
        3、void printStackTrace() JVM打印异常对象，默认此方法，打印的异常信息最全面；
            e.printStackTrace();
                // java.io.IOException: 文件后缀名不对
                    // at com.baidu.test.demo07.Yichang03.test(Yichang03.java:19)
                    // at com.baidu.test.demo07.Yichang03.main(Yichang03.java:8)
            System.out.println(e.getMessage());   // 文件后缀名不对
            System.out.println(e.toString());   // java.io.IOException: 文件后缀名不对
        
    finally
        try{
            // 可能产生异常的代码
        }catch(定义一个异常的变量，用来接收try中抛出的异常对象){
            异常的处理逻辑，异常对象之后，怎么处理异常对象
            一般在工作中，把异常的信息记录到一个日志中
        }
        ...catch(异常类名 变量名){
    
        }finally{
            // 无论是否出现异常都会执行
        }
        注意：
            1、finally不能单独使用，必须和try...catch一起使用
            2、finally一般用于资源释放（资源回收），无论程序是否出现异常，最后都要资源释放（IO）
    异常注意事项
        多个异常使用补货又该如何处理？
            1、多个异常分别处理；
            2、多个异常一次捕获，多次处理  推荐
                这种异常处理方式要求多个catch中的异常不能相同，并且若catch中的多个异常之间有子父类异常关系，那么子类异常在上面的catch中处理；
            3、多个异常一次捕获，一次处理
            
            一次捕获多次处理
            try{
    
            }catch(异常类型A e){
    
            }catch(异常类型B e){
                
            }
        运行时异常被抛出可以不处理，既不捕获，也不声明抛出；
        在try/catch后可以追加finally代码块，七种的代码一定会被执行，通常用于资源回收；
        如果finally有return语句，永远返回finally中的结果，尽量避免finally中有return；
        父类抛出了多个异常，子类覆盖父类方法时，只能抛出相同的异常或者是他的子集或者不抛出异常；
        父类方法没有抛出异常，子类覆盖父类该方法时，也不可抛出异常，此时子类产生该异常，只能捕获处理，不能声明抛出；
        子类异常和父类异常尽量保持一致；

### 自定义异常 java提供的异常类，不够使用，需要自定义一些异常
    自定义异常类一般都是以Exception结尾，说明该类是一个异常常量
    自定义异常类必须继承 Exception 或者 RuntimeException
        继承 Exception ： 那么自定义的异常类就是一个编译器异常，如果方法内部抛出了编译期异常，就不许处理这个异常，要么throws，要么try...catch
        继承 RuntimeException : 那么自定义的异常类就是一个运行期异常，无需处理，交给虚拟机（JVM）处理（中断处理）
    
    public class XXXException extends Exception (或者 RuntimeException) {
        // 添加一个空参数的构造方法
        // 添加一个带异常信息的构造方法
    }

###

#### 多线程

### 并发 和 并行
    并发：值两个或多个事件在同一个时间段发生        交替执行
    并行：值两个或多个事件在同一时刻发生(同时发生)   同时执行

### 线程 和 进程
    进程：是指一个内存中进行的应用程序，每个进程都有一个独立的内存空间；
         进程也是程序的一次执行过程，是系统运行程序的基本单位；
         系统运行一个程序：一个进程从创建、运行 到 消亡 的过程；
    
    线程：是进程的执行单位，一个进程中至少有一个线程；
         一个进程中是可以有多个线程的，这个应用程序也可以称之为多线程程序；
    
         线程的调度：
            分时调度：
            抢占式调度：
    
    一个程序运行后至少有一个进程，一个进程中可以包含多个线程；
    
    硬盘：永久存储ROM
    内存：临时存储RAM

### Thread类
常用方法：
    1、获取线程的名称
        1、使用Thread类中的getName()方法    public String getName();
        2、可以先获取到当前执行的线程，使用线程中的getName()方法获取线程名称   public static Thread crrentThread() 返回对当前正在执行的线程对象的引用；
            Thread.currentThread.getName();
    2、public void start() 导致该线程开始执行； Java虚拟机调用此线程的run方法；
    3、public void run() 此线程要执行的任务在此处定义代码；
    4、public static boid sleep(long millis) 使正在之功能性的线程以指定的毫秒数暂停（暂停时停止执行），暂停结束后执行；
        Thread.sleep(1000);

### 创建多线程程序的第一种方法： 创建Thread子类
    java.lang.Thread 类：是面熟线程的类，先要实现多线程程序，就必须继承 Thread 类
    1、创建一个 Thread 类的子类； extends
    2、在 Thread 类的子类中重写 Thread 类中的 run() 方法。设置线程任务（开启线程要做什么？）；
    3、创建 Thread 类的子类对象；
    4、调用 Thread 类中的方法 start 方法，开启新的线程，执行run方法：
        void start() 使该线程开始执行；Java虚拟机调用该线程的run方法；
        结果是两个线程并发运行，当前线程（main线程） 和 两一个线程（创建的新线程，执行其run方法）；
        多次启动一个线程是非法的，特别是当线程已经结束执行后，不能在重新启动；
    java程序属于抢占式调度，哪个线程的优先级高，哪个线程有限执行，同一优先级，随机选择一个执行；

### 创建多线程程序的第二种方法： 实现 Runnable 接口
    java.lang.Runnable
        Runnable 接口应该由那些打算通过某一线程执行其实例的类来实现。类必须定义一个run的午餐方法；
    java.lang.Thread 类的构造方法：
        Thread(Runnable targer) 分配新的 Thread 对象。
        Thread(Runnable target, String name) 分配新的Thread对象
    实现步骤：
        1、创建一个 Runnable 接口的实现类； implements
        2、在实现类中重写 Runnable 接口中的 run 方法，设置线程任务；
        3、创建一个 Runnable 接口的实现类对象；
        4、创建 Thread 类对象，构造方法中传递 Runnable 接口的实现对象；
        5、调用 Thread 类中的 start 方法，开启新的线程执行 run 方法；

### 实现Runnable接口 比 创建Thread子类的好处
    1、避免了单继承的局限性
        一个类只能继承一个类，类继承了Thread类就不能继承其他的类
        实现了Runnable接口，还可以继承其他的类，实现其他接口
    2、增强了程序的扩展性，降低了程序的耦合性（解耦）
        实现Runnable接口的方式，把设置线程任务和开启线程进行了分离（解耦）；
        实现类中，重写了run方法：用来设置线程任务；
        创建Thread类对象，调用start方法：用来开启新线程；

### 匿名内部类类实现多线程
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName()+"--"+i);
        };
    
        // 线程的父类 Thread
        new Thread(){
            @Override
            public void run() {
                for (int i = 0; i <5 ; i++) {
                    System.out.println(Thread.currentThread().getName()+"--"+i);
                }
            }
        }.start();
    
        // 线程的接口 Runnable
        Runnable r = new Runnable(){
            @Override
            public void run() {
                for (int i = 0; i <5 ; i++) {
                    System.out.println(Thread.currentThread().getName()+"--"+i);
                }
            }
        };
        new Thread(r).start();
    
        // 线程的接口 Runnable 简化
        new Thread(
                new Runnable(){
                    @Override
                    public void run() {
                        for (int i = 0; i <5 ; i++) {
                            System.out.println(Thread.currentThread().getName()+"-->"+i);
                        }
                    }
                }
        ).start();
    }

#### 线程安全问题

### demo
    ### 方案一：同步代码块
    synchronized(锁对象){
        // 可能会出现线程安全问题的代码(访问了共享数据)
    }
    注意：
        1、通过代码块中的锁对象，可以使用任意的对象；
        2、但是必须保证多个线程使用的锁对象是同一个；
        3、锁对象作用：把同步代码块锁住，只让一个线程在同步代码块中执行；
        public class RunnableImpl implements Runnable {
            private int tickets = 200;
            Object obj = new Object();
            @Override
            public void run() {
                while (true){
                    synchronized (obj) {
                        if(tickets>0){
                            try {
                                Thread.sleep(10);
                            } catch (InterruptedException e) {
                                e.printStackTrace();
                            }
                            System.out.println(Thread.currentThread().getName()+"正在卖"+tickets+"张票");
                            tickets--;
                        }
                    }
                }
            }
        }
    
    ### 方案二：同步方法
    1、把访问了共享数据的代码抽取出来，放到一个方法中；
    2、在方法上添加synchronized修饰符；
    修饰符 synchronized 返回值类型 方法名(参数列表) {
        // 可能会出现线程安全问题的代码(访问了共享数据)
    }
    public class RunnableImpl implements Runnable {
        private int tickets = 200;
        @Override
        public void run() {
            while (true){
                payTicket();
            }
        }
        public synchronized void payTicket() {
            if(tickets>0){
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName()+"正在卖"+tickets+"张票");
                tickets--;
            }
        }
    }
    
    静态的同步方法
    
    ### 方案三：lock锁
    java.util.concurrent.locks Lock接口
    Lock接口提供了比使用synchronized 方法和语句可获得的更广泛的锁定操作；
    Lock接口中的方法：
        void lock() 获取锁
        void unlock() 释放锁
    
    java.util.concurrent.locks.ReentrantLock implements Lock 接口
    
    使用步骤：
        1、在成员位置创建一个ReentrantLock对象；
        2、在可能会出现安全问题的代码前调用Lock接口中的方法lock获取锁；
        3、在可能会出现安全问题的代码后调用Lock接口中的方法unlock释放锁；
    
    import java.util.concurrent.locks.Lock;
    import java.util.concurrent.locks.ReentrantLock;
    
    public class RunnableImpl implements Runnable {
        private int tickets = 200;
        Lock l = new ReentrantLock();
        @Override
        public void run() {
            while (true){
                l.lock();
                if(tickets>0){
                    try {
                        Thread.sleep(10);
                        System.out.println(Thread.currentThread().getName()+"正在卖"+tickets+"张票");
                        tickets--;
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }finally {
                        l.unlock();
                    }
                }
            }
        }
    }


### 线程状态：
    1、 new(新建)   线程刚被创建，但是并未启动，还没有调用start方法；
    2、 Runnable(可运行)
    3、 Blocked(被锁)
    4、 Waiting(无限期等待)   wait(等待) <==> notify(唤醒)
    5、 Timed Waiting(计时等待)
    6、 Teminated(被终止)
    等待（wait）与唤醒（notify）之间的通讯
        Object 类中的方法：
            1、void wait() 在其他线程调用此对象的notify() 方法 或者 notifyAll() 方法前，导致当前线程等待；
            2、void notify() 唤醒在此对象监视器等待的单线程，会继续执行wait方法之后的代码；
        创建一个顾客线程（消费者）：告知老板要的包子的种类和数量，然后调用wait方法，让其CPU的执行，进入waiting状态（无限等待）；
        创建一个老板线程（生产者）：花了5秒做包子，做好包子之后，调用notify方法，唤醒顾客吃包子；
        注意：
            顾客和老板线程必须使用同步代码块包裹起来，保证等待和唤醒只能有一个执行；
            同步使用的锁对象必须保证唯一；
            只有锁对象才能调用wait和notify方法；
    
        public class WaitNotifyDemo {
            public static void main(String[] args) {
                Object obj = new Object();
    
                // 顾客线程
                new Thread(){
                    @Override
                    public void run() {
                        synchronized (obj) {
                            System.out.println("告知老板要的包子的种类和数量");
                            try {
                                obj.wait();
                            } catch (InterruptedException e) {
                                e.printStackTrace();
                            }
                            System.out.println("终于好了，开吃");
                        }
                    }
                }.start();
    
                // 老板线程
                new Thread(){
                    @Override
                    public void run() {
                        try {
                            Thread.sleep(3000);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                        synchronized (obj) {
                            System.out.println("包子最好了");
                            obj.notify();
                        }
                    }
                }.start();
            }
        }
    
    进入到TimeWaiting（计时等待）有两种：
        1、使用sleep(long m)方法，在毫秒值结束之后，线程睡醒进入到Runnable/Blocked状态；
        2、使用wart(long m)方法，wait方法如果在毫秒值结束之后，还没有被notify韩星，就会自动醒来，线程进入到Runnable/Blocked状态；
    
    唤醒的方法：
        1、void notify() 唤醒在此对象监听等待的多个线程，如果有多个，则随机唤醒一个；
        2、void notifyAll() 唤醒再次对象监视器上等待的所有线程；

###

#### 等待与唤醒机制

### 线程间通讯：多个线程在处理同一资源，但处理的动作（线程任务）却不相同；

### 等待与唤醒机制：就是用于解决线程间通讯的问题：
    1、wait： 想成不在活动，不再参与调度，进入wait set中，因此不会浪费CPU资源，也不会去竞争锁，这时的线程状态是WAITING；
    2、notify：
    3、notifyAll：
    调用wait和notify方法需要注意的细节：
        1、wait方法与notify方法必须要由同一个锁对象调用，因此，对应的锁对象可以通过notify唤醒使用同一个锁对象调用的wait方法后的线程；
        2、wait方法与notify方法是属于Object类的方法的。因此，锁对象可以是任意对象，而任意对象的所属类都是集成了Object类的；
        3、wait方法与notify方法必须要在同步代码块或者同步函数中使用，因此，必须要通过所对次昂调用这两个方法；

#### 线程池：就是一个容纳多个线程的容器，其中的线程可以反复使用，省了频繁创建线程对象的操作，无需反复创建想成而消耗过多的资源
    如果并发的线程数量很多，并且每个线程都是执行一个时间很短的任务就结束了，这样频繁创建线程就会大大降低系统的效率，因此频繁创建线程和销毁线程需要时间；
    在Java中可以通过线程池解决这一问题。
    合理利用线程池带来的好处：
        1、降低资源消耗。减少了创建和销毁线程的次数，每个工作线程都可以被重复利用，可以执行多个任务；
        2、提高响应速速。当任务达到时，任务可以不需要等到线程创建就立即执行；
        3、提高线程的可管理性。可以根据系统的承受能力，调整线程池中工作线程的数目，防止因为消耗过多的内存而把服务器累趴下（每个线程需要大约1M的内存）；
    集合: ArrayList、HashSet、LinkedList、HashMap
        LinkedList<Thread>
    当线程第一次启动的时候，创建多个线程，保存到一个集合中，当我们想要使用线程的时候，既可以从集合中取出来线程使用
        Thread t = list.remove(0)  返回的是被删除的元素（线程只能被一个任务使用，所以用remove）
        Thread t = linked.removeFirst();
    当我们使用完毕线程，需要把线程归还给线程池：
        list.add(t);
        linked.addLast(t);
    
    JDK 1.5 之后，JDK内置了线程池，我们可以直接使用
    
    线程池：JDK1.5之后提供的：
    java.util.concurrent.Executors: 线程池的工厂类。用来生成线程池；
    Executors类中的静态方法：
        static ExecutorService newFixedThreadPool(int nThreads) 创建一个可重用固定数量的线程池；
            参数 ： int nThread：创建线程池中包含的线程数量；
            返回值：ExecutorService接口，返回的是ExecutorService接口的实现类对象，我们可以使用ExecutorService接口接收（面向接口编程）；
    java.util.conturrent.ExecutorService:线程池接口
        用来从线程池中获取线程，调用start方法，执行线程任务：submit(Runnable task) 提交一个Run那边了任务用于执行
        关闭/销毁线程池的方法： void shutdown()
    
    线程池的使用步骤：
        1、使用线程池的工厂类Executors里边提供的静态方法newFixedThreadPool生产一个指定数量的线程池；
        2、创建一个类，实现Runnable接口，重写run方法，设置线程任务；
        3、调用ExecutorService中的方法submit，传递线程任务（实现类），开启线程，执行run方法；
        4、调用ExecutorService中的方法shutdown销毁线程池（不建议执行，线程池应该保留）；

#### Lambda表达式

### 函数式编程思想：
    面向对象的思想： 做一件事情，好到可以解决这件事情的对象，再调用对象中的方法完成事情；
    函数式编程思想：只要能获取到结果，谁去做，怎么做等都不重要，重视的是结果，不重视过程；
    
    // 匿名内部类
    new Thread() {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName()+"新线程创建了");
        }
    }.start();
    
    // Lambda
    new Thread(() -> {
            System.out.println(Thread.currentThread().getName()+"新线程创建了");
        }
    ).start();

### Lambda表达式：是可以推导，可以省略
    省略的前提：
        1、使用Lambda必须具有接口，且接口中有且仅有一个抽象类方法；有且仅有一个抽象方法的接口，成为"函数式接口"；
        2、使用Lambda必须具有上下文推断；
    凡是根据上线文推导出来的内容，都可以省略书写：
        1、(参数列表):括号中草书列表的数据类型可以省略不写；
        2、(参数列表):括号中的参数如果只有一个，那么类型和()都可以省略；
        3、{一些代码}:如果{}中代码只有一行，如论是否有返回值，都可以省略({},return,;),要省略{},return时，分号也要一起省略；
    
    JDK1.7版本之前，创建集合对象必须噶前后的泛型都写上:
        ArrayList<String> list = new ArrayList<String>();
    JDK1.7版本之后，后边的泛型可以省略，因为后边的泛型可以根据前边的泛型推导出来:
        ArrayList<String> list = new ArrayList<String>();

###

#### FILE
    java.io.Rile 类
    文件和目录路径的抽象表示形式；
    java把电脑中的文件和文件夹（目录）封装到了一个File类，我们可以使用File类对文件和文件夹进行操作；
    我们可以使用File类的方法：
        创建一个文件/文件夹；
        删除文件/文件夹；
        获取文件/文件夹；
        判断文件/文件夹是否存在；
        对文件夹进行遍历；
        获取文件的大小；
    File类是一个与系统无关的类，任何系统都可以使用File类中的方法；
    file:文件   directory:文件夹/目录   path:路径

### File类的静态成员方法：
    1、static String pathSeparator  与系统有关的路径分隔符，为了方便，他被表示为一个字符串；
    2、static char pathSeparatorChar  与系统有关的路径分割符；
    3、static String separator  与系统有福安的默认名称分隔符，为了方便，他被表示为一个字符串；
    4、static char separatorChar  与系统有关的弄人名称分隔符；

### File 类的构造方法
    File file = new File();

### File 常用方法：
    1、获取功能的方法：
        a、public String getAbsolutePath()  绝对路径
        b、public String getPath()  路径字符串
        c、public String getName()  文件或者目录的名称
        d、public long length() 文件的大小 字节为单位
    2、判断功能的方法：
        a、public boolean exists()
        b、public boolean isDirectory()
        c、public boolean isFile()
    3、创建和删除功能的方法：
        a、public boolean createNewFile()
        b、public boolean delete()
        c、public boolean mkdir()
        d、public boolean mkdirs()
    4、目录的遍历
        a、public String[] list() 返回一个String数组，便是该File目录中的所有子文件或者目录
        b、public File[] listFiles() 返回一个File数组，便是该File目录中的所有子文件或者目录
    
    String name = file.getName();
    String path = file.getPath();
    String str = file.toString();
    str = str.toLowerCase();
    boolean b = str.endWith(".java");

### 过滤器
    在File类中有两个ListFiles重载的方法，方法的参数传递的就是过滤器；
    File[] listFiles(FileFilter fileter)
    java.io.FileFilter 接口：用于抽象路径名（File对象）的过滤器；
        用来过滤文件（File对象）
        用来过滤文件的方法（抽象方法）
            boolean accept(File pathname) 测试指定对象路径名是够应该包含在某个路径名列表中：
                参数：File pathname：使用ListFiles方法遍历目录，得到的每一个文件对象；
    File[] listFiles(FilenameFilter filter)
    java.io.FilenameFilter 接口：实现此接口的类实例可用于过滤器文件名；
        用于过滤文件名称；
        用来过滤文件的方法（抽象方法）：
            boolean accept(File dir, String name) 测试指定文件是够应该包含在某一文件列表中：
                参数：
                    File dir：构造方法中穿刺的被遍历的目录；
                    String name： 使用ListFiles方法遍历目录，获取每一个文件/文件夹的名称；
    注意：两个过滤器接口是没有实现类的，需要我们自己写实现类，重写过滤的方法accept，在方法中自己定义过滤器的规则；
    也可以使用匿名内部类 或者 Lambda表达式

###

#### IO

### IO
    Java中I/O操作主要是指java.io包下的内容，进行输入、输出操作。输入也叫做读取数据，输出也叫做写数据；
    i:input 输入(读取)：把硬盘中的数据读取到内存中使用；
    o:output 输出(写入)：把内存中的数据写入到硬盘中保存；
    输入和输出主体指的是内存，进入内存是输入，出内存是输出；
    流：数据（字节，字符）  1个字符 = 2个字节 = 8个二进制位
    输入流：把数据从其他设备上读取到内存中的流；
    输出流：把数据从内存中写出到其他设备上的流；
    格局数据的类型分为：字节流 和 字符流；
    
    顶级父类：这几个都是抽象类，无法直接使用，使用其子类；
    |----------|---------------|------------------|
    |          |      输入流    |       输出流      |
    |----------|---------------|------------------|
    |  字节流   |  InputStream  |   OutputStream   |
    |----------|---------------|------------------|
    |  字符流   |     Reader    |      Writer      |
    |----------|---------------|------------------|

### 字节流
    一切皆为字节：一切文件数据（文本、图片、视频等）在储存是，都是以二进制数组的形式保存，都是一个一个字节，传输时也是字节；
    字节流可以传输任意文件数据；无论使用什么样的流对象，底层传输的始终未二进制数据；

### 字节输出流 （OutputStream）
    java.io.OutputStream 抽象类书表示字节输出流的所有类的超类，将指定的字节信息写出到目的地；
    
    OutputStream 定义了一些子类共性的成员方法：
        public void close() : 关闭此输出流并释放与此流相关的任何系统资源；当完成流的操作时，必须调用此方法，释放系统资源；
        public void flush() : 刷新此输出流并强制任何缓冲的输出字节被写入；
        public void write(byte[] b) : 将b.length字节从指定的字节数组中写入此输出流；
        public void write(byte[] b, int off, int len) : 从指定的字节数组写入len字节，从偏移量off开始输出到此输出流；
        public abstract void write(int b) : 将指定的字节输出流；
    
    java.io.FileOutputStream extends OutputStream
    FileOutputStream ： 文件字节输出流；把内存中的数据写入到硬盘的文件中；
    
    构造方法：
        FileOutputStream(String name) : 创建一个向具有指定名称的文件中写入数据的输出文件流； String name: 目的地是一个文件的路径；
        FileOutputStream(File file) : 创建一个向指定File对象表示的文件中写入数据的文件输出流； File file: 目的地是一个文件；
    
    构造方法的作用：
        1、创建一个FileOutputStream对象；
        2、会根据构造方法中传递的文件/文件路径，创建一个空文件；
        3、会把FileOutputStream对象指向创建好的文件；
    
    写入数据的原理（内存 ---> 硬盘）
        java程序 --> JVM（java虚拟机） --> OS（操作系统） --> OS调用写数据的方法 --> 把数据写入到文件中
    
    字节输出流的使用步骤：
        1、创建一个FileOutputStream对象，构造方法中传递写入数据的目的地；FileOutputStream fos = new FileOutputStream("fos.txt");
        2、调用FileOutputStream对象中的方法write，把数据写入到文件中； fos.write(97);
        3、释放资源（流使用会占用一定的内存，使用完毕要把内存清空）；fos.close();
            // fos.write(98);
            // fos.write("你好".getBytes());
            // byte[] bytes = {97,98,99};
            // fos.write(bytes, 0, 2);
    
    任意的文本编辑器（记事本等）在打开文件的时候，都会查询编码表，把字节转换成字符表示：
        0-127 ： 查询ADCII表；
        其他值 ： 查询系统默认码表（中文系统GBK）；
    
    如果写入的第一个字节是正数（0-127），那么现实的时候会查询ASCII表；
    如果写入的第一个字节是负数，那第一个字节会和第二个字节组成一个中文现实，查询系统默认码表（GBK）；
    
    追加/续写：使用两个参数的构造方法：
        FileOutputStream(String name, boolean append) : 创建一个向具有指定名称的文件中写入数据的输出文件流； String name: 目的地是一个文件的路径；
        FileOutputStream(File file, boolean append) : 创建一个向指定File对象表示的文件中写入数据的文件输出流； File file: 目的地是一个文件；
            参数： boolean append : 追加开关；true表示追加，false表示覆盖；
    
    换行：Windows(\r\n)、Linux(\n)、Mac(\r)
    
        public static void main(String[] args) throws IOException {
            FileOutputStream fos = new FileOutputStream("test.txt", true);
            for (int i = 0; i < 5; i++) {
                fos.write(98);
                fos.write("你好".getBytes());
                byte[] bytes = {97,98,99};
                fos.write(bytes, 0, 2);
                fos.write("\r".getBytes());
            }
            fos.close();
        }

### 字节输入流 （InputStream）

    当使用字节流读取文本文件时，可能会有一个小问题，就是遇到中文字符时，可能不会显示完整的字符，
    那是因为一个中文字符可能占用多个字节存储。使用字符流（以字符为单位读写数据）可以解决；
    
    java.io.InputStream 抽象类 表示字节输入流的所有类的超类；
    
    InputStream 定义了一些子类共性的成员方法：
        int read() 从输入流读取数据的下一个字节；
        int read(byte[] b) 从输入流中读取一定数量的字节，并将其存储在缓存区b中；
            方法的参数byte[] 的作用：
                1、起到缓冲作用，存储每次读取到的多个字节；
                2、数组的长度一般定义为1024（1kb）或者1024的整数倍；byte[] bytes = new byte[1024];
            方法的返回值int是为什么：每次读取的有效字节个数；
        void close() 关闭此输入流并释放与该流关联的所有系统资源；
    
    java.io.FileInputStream extends InputStream
        FileInputStream： 文件字节输入流； 把硬盘文件中的数据，读取到内存中使用；
    
    构造方法：
        FileInputStream(String name)  String name：文件的路径
        FileInputStream(File file)  File file：文件
    构造方法的作用：
        1、会创建一个FileInputStream对象；
        2、会吧FileInputStream对象指定构造方法中要读取的文件；
    
    写入数据的原理（内存 ---> 硬盘）
        java程序 --> JVM（java虚拟机） --> OS（操作系统） --> OS调用写数据的方法 --> 把数据写入到文件中
    
    字节输出流的使用步骤：
        1、创建一个FileInputStream对象，构造方法中传递写入数据的目的地； FileInputStream fis = new FileInputStream("fos.txt");
        2、调用FileInputStream对象中的方法read，把数据写入到文件中； 一次读一个字节； 读取到文件末尾返回-1；
            int len = 0;
            while ((len = fis.read()) != -1) {
                System.out.println(len);
            }
    
            while (fis.rad() != -1) {
                System.out.println(fis.rad());   // 这种方法不对，因为read()方法一次读一个字节，此方法中有两个read()，必须要用一个变量接收
            }
        3、释放资源（流使用会占用一定的内存，使用完毕要把内存清空）； fis.close();
    
    字节输入流一次读取多个字节：
        FileInputStream fis = new FileInputStream("fos.txt");  // 可以是路径字符串或者File对象
        byte[] bytes = new byte[1024];
        int len = 0;
        while((len = fis.read(bytes)) != -1) {
            // String(byte[] bytes) : 把字节数组转换成字符串；
            // System.out.println(new String(bytes));  // 输出的字符串后面有很多空格，因为byte定义的长度为1024；
            // String(byte[], int offset, int length);
            // 把字节数组的一部分转换成字符串，offset：数组的开始索引， length：转换的字节个数；
            System.out.println(new String(bytes, 0, len));
        }
    
    // 复制 先读后写，先关闭写；
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("fos.txt");
        FileOutputStream fos = new FileOutputStream("foscopy.txt");
        byte[] bytes = new byte[1024];
        int len = 0;
        while ((len = fis.read(bytes)) != -1) {
            fos.write(bytes, 0, len);
        }
        fos.close();
        fis.close();
    }

### 字符流
    以字符为单位读写数据

### 字符输入流
    java.io.Reader ： 字符输入流，是字符输入流的最顶级的父类，是一个抽象类，定义了一些共性的成员方法：
        int read()  // 读取当个字符并返回；
        int read(char[] dbuf)   // 一次读取多个字符，将字符读入数组；
        void close()    // 关闭该流并释放与之关联的所有资源；
    
    java.io.FileReader extends InputStreamReader extends Reader
    FileReader：文件字符输入流：把硬盘文件中的数据以字符的方式读取到内存中；
    
    构造方法：
        FileReader(String fileName) // String fileName：文件的路径；
        FileReader(File file)   // File file：文件
    
        构造方法的作用：
            1、创建一个FileReader对象；
            2、会吧FileReader对象指向要读取的文件；
    
    字符输入流的使用步骤：
        1、创建FileReader对象，构造方法中绑定要读取的数据源； FileReader fr = new FileReader("fos.txt");
        2、使用FileReader对象中的read()方法读取文件；
            a、
            int len = 0;
            while ((len = fr.read()) != -1) {
                System.out.println((char)len);
            }
    
            b、
            int len = 0;
            char[] cs = new char[1024];
            while ((len = fr.read(cs)) != -1) {
                // String类的构造方法
                // String(char[] value) 把字符数组转为字符串；
                // String(char[] value, int offset, int count) 把字符数组中一部分转换为字符串 offset为数组的开始索引，count为转换的个数；
                System.out.println(new String(cs, 0, len));
            }
        3、释放资源；

### 字符输出流
    java.io.Writer: 字符输出流，是所有字符输出流的最顶层的父类，是一个抽象类，不能直接使用，要使用其子类；
    共性方法：
        1、void write(int c) 写入单个字符；
        2、void write(char[] cbuf) 写入字符数组；
        3、abstract void write(char[] cbuf, int off, int len) 写入字符数组的一部分，off数组的开始索引，len写的字符个数；
        4、void write(String str) 写入字符串；
        5、void write(String str, int off, int len) 写入字符串的某一部分，off为字符串的开始索引，len为写的字符个数；
        6、void flush() 刷新该流的缓冲；流对象可以继续使用；
        7、void close() 关闭此流，但要先刷新它；就对象不可以使用；
    
    java.io.FileWriter extends OutputStreamWrite extends Writer
    FileWriter: 文件字符输出流： 把内存中字符数据写入到文件中；
    
    构造方法：
        FileWriter(File file) 根据给定的File对象构造一个FileWriter对象；    File file：一个文件
        FileWriter(String fileName) 根据给定的文件名构造一个FileWriter对象；    String fileName：文件的路径
    
        构造方法的作用：
            1、会创建一个FileWriter对象；
            2、会根据构造方法中传递的文件/文件的路径，创建文件；
            3、会把FileWriter对象指向建好的文件；
    
    字符输出流的使用步骤：
        1、创建FileWriter对象，构造方法找那个绑定要写入数据的目的地；  FileWriter fw = new FileWriter("fw.txt");
        2、使用FileWriter中的方法write，把数据写入到内存缓冲区中（字符转换为字节的过程）；  fw.write(98);
        3、使用FileWriter中方法flush，把内存缓冲区中的数据，刷新到文件中；
        4、释放资源（会先把内存缓冲区找那个的数据刷新到文件中）；   fw.close();
    
    追加/续写：使用两个参数的构造方法：
    FileWriter(String name, boolean append) : 创建一个向具有指定名称的文件中写入数据的输出文件流； String name: 目的地是一个文件的路径；
    FileWriter(File file, boolean append) : 创建一个向指定File对象表示的文件中写入数据的文件输出流； File file: 目的地是一个文件；
        参数： boolean append : 追加开关；true表示追加，false表示覆盖；
    
    换行：Windows(\r\n)、Linux(\n)、Mac(\r)
    
    IO异常的处理：
        在JDK1.7之前使用try...catch...finally 处理流中的异常
    
        public static void main(String[] args) {
            FileWriter fw = null;
            try {
                fw = new FileWriter("fw.txt", true);
                for (int i = 0; i < 5; i++) {
                    fw.write("你好" + i + "\r");
                }
            } catch (IOException e) {
                e.printStackTrace();
            }finally {
                if (fw != null) {
                    try {
                        fw.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        }

### Properties  
    Properties集合是一个双列集合，key 和 value默认都是字符串;
    java.util.Properties 集合 extends HashTable<k, v> implements Map<k, v>
    Properties 类表示了一个持久的属性集，Properties 可保存在流中或者从流中加载；
    Properties 集合是一个唯一哈IO流相结合的集合；
        可以使用Properties集合中的方法store，把集合中的历史数据 持久化写入到硬盘中存储；
        可以使用Properties集合中的方法load，把硬盘中保存的文件（键值对） 读取到集合中使用；
    属性列表中每个键及其对应值都是一个字符串：
    
    使用Properties集合存储数据，遍历取出Properties集合中的数据；
    Properties集合是一个双列集合，key 和 value 默认都是字符串；
    Properties集合有一些操作字符串的特有方法：
        Object setProperty(String key, String value) 调用Hashtable的方法put()；
        String getProperty(String key) 通过key找到value值，此方法相当于Map集合中的get(key)方法；
        Set<String> stringPropertyNames() 返回此属性列表中的键值，其中该键机器对应值是字符串，此方法相当于Map集合中的keySet方法；
    
    使用Properties集合中的方法store，把集合中的临时数据 持久化写入到硬盘中存储；
        void store(OutputStream, String comments);
        void store(Write write, String comments);
        参数：
            OutputStream：字节输出流，不能写入中文；
            Writer writer：字符输出流，可以写中文；
            String comments：注释，用来解释说明保存文件是做什么用的，不能使用中文，一般使用空字符串；
    
        使用步骤：
            1、创建Properties集合对象，添加数据；
            2、创建字节输出流/字符输出流对象，构造方法中绑定要输入的目的地；
            3、使用Properties集合中的方法store，把集合中的临时数据，持久化写入到硬盘中存储；
            4、释放资源；
    
    使用Properties集合中的方法load，把硬盘中保存的文件（键值对），读取到集合中使用；
        void load(InputStream inStream)
        void load(Reader reader)
        参数：
            InputStream inStream：字节输出流，不能读取含有中文的键值对；
            Reader reader：字符输出流，能读取含有中文的键值对；
        
        使用步骤：
            1、创建Properties集合对象；
            2、使用Properties集合对象中的方法load()读取保存键值对的文件；
            3、遍历Properties集合；
        注意：
            1、存储键值对的文件中，键与值默认的连接符号可以使用 = ， 空格(其他符号)；
            2、存储键值对的文件中，可以使用 # 进行注释，备注是的键值对不会被读取；
            3、保存键与值默认都是字符串，不用再加引号；

### 缓冲流(高效流)对4个基本的FileXxx流的增强；
    原理：是创建流对象时，会创建一个内置的默认大小的缓冲区数组，通过缓冲区读写，减少系统IO次数，从而提高读写效率；
    字节缓冲流：BufferedInputStream、BufferedOutputStream；
    字符缓冲流：BufferedReader、BufferedWrite
    
    字节缓冲输出流： BufferedOutputStream；java.io.BufferedStream extends OutputStream
        继承父类的共性成员方法：
            public void close()
            public void flush()
            public void write(byte[] b)
            public void write(byte[], int off, int len)
            public abstract void write(int b)
        构造方法：
            BufferedOutputStream(OutputStream out)
            BufferedOutputStream(OutputStream out, int size)
        使用步骤：
            1、创建FileOutputStream对象，构造方法中绑定要输出的目的地；
            2、创建BufferedOutputStream对象，构造方法中传递FileOutputStream对象，提高FileOutputStream对象效率；
            3、使用BufferedOutputStream对象中的write() ，把数据写入到内部缓冲区中；
            4、使用BufferedOutputStream对象中的flush() ， 把内部缓冲区中的数据，刷新到文件中；
            5、释放资源close()；
    
    字节缓冲输出流：BufferedInputStream；java.io.BufferedInputStream extends InputStream
        继承父类的共性成员方法：
            1、int read()
            2、int read(byte[] b)
            3、void close()
        构造方法：
            BufferedInputStream(InputStream in)
            BufferedInputStream(InputStream in, int size)
        使用步骤：
            1、创建FileInputStream对象，构造方法中绑定要读取的数据源；
            2、创建BufferedInputStream对象，构造方法中传递FileInputStream对象，提高FileInputStream对象的读取效率；
            3、使用BufferedInputStream对象中的read()，读取文件；
            4、释放资源；
    
    字符缓冲输出流：BufferedWriter： java.io.BufferedWriter extends Writer
        继承父类的共性成员方法：
            void write(int c)
            void write(char[] cbuf)
            abstract void write(char[] cbuf, int off, int len)
            void write(String str)
            void write(String str, int off, int len)
            void flush()
            void close()
        构造方法：
            BuffereWriter(Writer out)
            BuffereWriter(Writer out, int size)
        特有成员方法：
            void newLine() 会根据不同的操作系统，获取不同的分隔符；
        使用步骤：
            1、创建字符缓冲输出流对象，构造方法中传递输出流；
            2、调用字节缓冲输出流中的write() 方法，把数据写入到内存缓冲区中；
            3、调用字符缓冲输入流中的flush() 方法，把内存缓冲区中的数据，刷新到文件中；
            4、释放资源；
    
    字符缓冲输入流： (BufferedReader) ；java.io.BufferedReader extends Reader；
        继承父类的共性方法：
            1、int read()
            2、int read(char[] cbuf)
            3、void close()
        构造方法：
            BufferedReader(Reader in)
            BufferedReader(Reader in, int sz)
        特有成员方法：
            String readLine() 读取一个文本行，读取一行数据，到达末尾，则返回null
        使用步骤：
            1、创建字符缓冲输入流对象，构造方法中传递字符输入流；
            2、使用字符缓冲输入流的方法read/readLint读取文本；
            3、释放资源；

### 















### 序列化 和 反序列化
    Java序列化  对象序列化  对象 => 字节序列(包括 对象的数据、有关对象类型的信息 以及 对象数据的类型)
    序列化 => 字节序列 => 写入文件 => 从文件提取 => 反序列化
        Java 提供了一种 对象序列化的机制，该机制中，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。
        将序列化对象写入文件之后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。
    
        序列化 整个过程 都是 Java虚拟机(JVM) 独立的，也就是说，在一个平台上序列化的对象可以在另一个完全不同的平台上反序列化该对象
    
        类 ObjectInputStream 和 ObjectOutputStream 是高层次的数据流，它们包含反序列化和序列化对象的方法。




###

#### 网络编程

### 网络编程：在一定的协议下，实现两台计算机的通信程序；
    C/S结构：（Client/Server) 是指客户端和服务器结构。QQ、迅雷等；
    B/S结构：（Brower/Server) 是指浏览器和服务器结构。火狐浏览器等；
    
    网络编程三要素：
        1、协议：
        2、IP地址：ipv4 4个字节；ipv6 16个字节；
        3、端口号：用两个字节表示的整数，唯一表示设备中的进程（应用程序）；0-65535，1024之前不能用；

### 网络通信
    网络通信协议：
        在计算机网络中，连接和通信的规则被称为网络协议；
        对数据的传输格式、传输速率、传输步骤等做了统一的规定；
        通信双方必须同时遵守才能完成数据交换；
    TCP/IP协议：传输控制协议/因特网互联协议（Transmission Control Protocol/Internet Protocol);
        Internet最基本、最广泛的协议；
    网络通信协议分类：
        UDP：用户数据报协议（User Datagram Protocol）：
            无连接通信协议；
            协议消耗资源小，通信效率高；
            通常用于音频、视频和普通数据的传输，安全性能不高；
            数据被限制在64kb以内，超出64kb就不能发送；
            数据报：网络传输的基本单位；
        TCP：传输控制协议（Transmission Controller Protocol）：
            面向连接的通信协议；
            三次握手：TCP协议中，在发送数据的准备阶段，客户端与服务器之间的三次交互，保证连接的可靠性；
            用途：浏览器下载，浏览网页等；

### TCP通讯程序
    TCP通信的客户端：向服务器发送连接请求，给服务器发送数据，读取服务器回写的数据；
        表示客户端类：
            java.net.Socket：此类实现客户端套接字（也可以叫“套接字”）。套接字是两台机器间通信的端点。
            套接字：包含了IP地址和端口号的网络单位；
        构造方法：
            Socket(String host, int port) 创建一个流套接字，并将其连接到指定主机上的指定端口号。
                String host：服务器主机的名称/服务器的IP地址；
                int port：服务器的端口号；
    
        成员方法：
            OutPutStream getOutputStream() 返回此套接字的输出流；
            InputStream getInputStream() 返回此套接字的输入流；
            void close() 关闭此套接字；
    
        实现步骤：
            1、创建一个客户端对象Socket，构造方法绑定服务器的IP地址和端口号；
            2、使用Socket对象中的方法getOutputStream() 获取网络字节输出流OutputStream对象；
            3、使用网络字节输出流OutputStream对象中的write() ，给服务器发送数据；
            4、使用Socket对象中的方法getInputStream()获取网络字节输入流InputStream对象；
            5、使用网络字节输出流InputStream对象中的read()，读取服务器回写的数据；
            6、释放资源（Socket）；
            注意：
                1、客户端和服务器端进行交互，必须使用Socket中提供的网络流，不能使用自己创建的流对象；
                2、当我们创建客户端对象Socket的时候，回去请求服务器和服务器经过3次握手建立连接通路；如果服务器没有启动，就会抛出异常；
    
    TCP通信的服务器端：接收客户端的请求，读取客户端发送的数据，给客户端回写数据
        表示服务器的类：
            java.net.ServerSocket：此类实现服务器套接字；
        构造方法：
            ServerSocket(int port) 创建绑定到特定端口的服务器套接字；
        服务器要明确一件事情，必须知道是哪个客户端请求的服务器：所以可以使用accept方法获取到请求的客户端对象Socket；
        成员方法：
            Socket accept() 侦听并接受到此套接字的连接；
    
        实现步骤：
            1、创建服务器ServerSocket对象和系统要指定的端口号；
            2、使用ServerSocket对象中的方法accept，获取到请求的客户端Socket；
            3、使用Socket对象中的getInputStream() 方法获取网络字节输入流InputStream对象；
            4、使用网络字节输入流InputStream对象中的read() 方法，读取客户端发送的数据；
            5、使用Socket对象中的方法getOutputStream() 获取网络字节输入流OutputStream对象；
            6、使用网络字节输出流OutputStream对象中的write() 方法，给客户端回写数据；
            7、释放资源（Socket、ServerSocket）；
    
    demo：
        // TCPClient
        public class TCPClient {
            public static void main(String[] args) throws IOException {
                // 1、创建一个客户端对象Socket，构造方法绑定服务器的IP地址和端口号；
                Socket socket = new Socket("127.0.0.1", 8888);
                // 2、使用Socket对象中的方法getOutputStream() 获取网络字节输出流OutputStream对象；
                OutputStream sos = socket.getOutputStream();
                // 3、使用网络字节输出流OutputStream对象中的write() ，给服务器发送数据；
                sos.write("你好服务器".getBytes());
                // 4、使用Socket对象中的方法getInputStream()获取网络字节输入流InputStream对象；
                InputStream is = socket.getInputStream();
                // 5、使用网络字节输出流InputStream对象中的read()，读取服务器回写的数据；
                byte[] bytes = new byte[1024];
                int len = is.read(bytes);
                System.out.println("我收到了服务器的响应：" + new String(bytes, 0, len));
                // 6、释放资源（Socket）；
                socket.close();
            }
        }
    
        // TCPServer
        public class TCPServer {
            public static void main(String[] args) throws IOException {
                // 1、创建服务器ServerSocket对象和系统要指定的端口号；
                ServerSocket server = new ServerSocket(8888);
                // 2、使用ServerSocket对象中的方法accept，获取到请求的客户端Socket；
                Socket socket = server.accept();
                // 3、使用Socket对象中的getInputStream() 方法获取网络字节输入流InputStream对象；
                InputStream is = socket.getInputStream();
                // 4、使用网络字节输入流InputStream对象中的read() 方法，读取客户端发送的数据；
                byte[] bytes = new byte[1024];
                int len = is.read(bytes);
                System.out.println("我收到了客户端的请求："+new String(bytes, 0, len));
                // 5、使用Socket对象中的方法getOutputStream() 获取网络字节输入流OutputStream对象；
                OutputStream os = socket.getOutputStream();
                // 6、使用网络字节输出流OutputStream对象中的write() 方法，给客户端回写数据；
                os.write("收到，谢谢".getBytes());
                // 7、释放资源（Socket、ServerSocket）；
                socket.close();
                server.close();
            }
        }

### 文件上传









### Java Number & Math 类
    System.out.println("90 度的正弦值：" + Math.sin(Math.PI/2));  
    System.out.println("0度的余弦值：" + Math.cos(0));  
    System.out.println("60度的正切值：" + Math.tan(Math.PI/3));  
    System.out.println("1的反正切值： " + Math.atan(1));  
    System.out.println("π/2的角度值：" + Math.toDegrees(Math.PI/2));  
    System.out.println(Math.PI); 
    
    xxxValue()  将 Number 对象转换为xxx数据类型的值并返回。
    compareTo() 将number对象与参数比较。
    equals()    判断number对象是否与参数相等。
    valueOf()   返回一个 Number 对象指定的内置数据类型
    toString()  以字符串形式返回值。
    parseInt()  将字符串解析为int类型。
    abs()       返回参数的绝对值。
    ceil()      返回大于等于( >= )给定参数的的最小整数，类型为双精度浮点型。
    floor()     返回小于等于（<=）给定参数的最大整数 。
    rint()      返回与参数最接近的整数。返回类型为double。
    round()     它表示四舍五入，算法为 Math.floor(x+0.5)，即将原来的数字加上 0.5 后再向下取整，所以，Math.round(11.5) 的结果为12，Math.round(-11.5) 的结果为-11。
    min()       返回两个参数中的最小值。
    max()       返回两个参数中的最大值。
    exp()       返回自然数底数e的参数次方。
    log()       返回参数的自然数底数的对数值。
    pow()       返回第一个参数的第二个参数次方。
    sqrt()      求参数的算术平方根。
    sin()       求指定double类型参数的正弦值。
    cos()       求指定double类型参数的余弦值。
    tan()       求指定double类型参数的正切值。
    asin()      求指定double类型参数的反正弦值。
    acos()      求指定double类型参数的反余弦值。
    atan()      求指定double类型参数的反正切值。
    atan2()     将笛卡尔坐标转换为极坐标，并返回极坐标的角度值。
    toDegrees() 将参数转化为角度。
    toRadians() 将角度转换为弧度。
    random()    返回一个随机数。

### Character 类
    Character 类用于对单个字符进行操作。
    Character 类在对象中包装一个基本类型 char 的值
    
    转义序列
        前面有反斜杠（\）的字符代表转义字符，它对编译器来说是有特殊含义的。
        下面列表展示了Java的转义序列：
        转义序列	描述
        \t	在文中该处插入一个tab键
        \b	在文中该处插入一个后退键
        \n	在文中该处换行
        \r	在文中该处插入回车
        \f	在文中该处插入换页符
        \'	在文中该处插入单引号
        \"	在文中该处插入双引号
        \\	在文中该处插入反斜杠
    
    Character 方法
        isLetter()      是否是一个字母
        isDigit()       是否是一个数字字符
        isWhitespace()  是否是一个空白字符
        isUpperCase()   是否是大写字母
        isLowerCase()   是否是小写字母
        toUpperCase()   指定字母的大写形式
        toLowerCase()   指定字母的小写形式
        toString()      返回字符的字符串形式，字符串的长度仅为1

### String 类
    字符串广泛应用 在 Java 编程中，在 Java 中字符串属于对象，Java 提供了 String 类来创建和操作字符串。
    1	char charAt(int index)
    返回指定索引处的 char 值。
    2	int compareTo(Object o)
    把这个字符串和另一个对象比较。
    3	int compareTo(String anotherString)
    按字典顺序比较两个字符串。
    4	int compareToIgnoreCase(String str)
    按字典顺序比较两个字符串，不考虑大小写。
    5	String concat(String str)
    将指定字符串连接到此字符串的结尾。
    6	boolean contentEquals(StringBuffer sb)
    当且仅当字符串与指定的StringBuffer有相同顺序的字符时候返回真。
    7	static String copyValueOf(char[] data)
    返回指定数组中表示该字符序列的 String。
    8	static String copyValueOf(char[] data, int offset, int count)
    返回指定数组中表示该字符序列的 String。
    9	boolean endsWith(String suffix)
    测试此字符串是否以指定的后缀结束。
    10	boolean equals(Object anObject)
    将此字符串与指定的对象比较。
    11	boolean equalsIgnoreCase(String anotherString)
    将此 String 与另一个 String 比较，不考虑大小写。
    12	byte[] getBytes()
    使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。
    13	byte[] getBytes(String charsetName)
    使用指定的字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。
    14	void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)
    将字符从此字符串复制到目标字符数组。
    15	int hashCode()
    返回此字符串的哈希码。
    16	int indexOf(int ch)
    返回指定字符在此字符串中第一次出现处的索引。
    17	int indexOf(int ch, int fromIndex)
    返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。
    18	int indexOf(String str)
    返回指定子字符串在此字符串中第一次出现处的索引。
    19	int indexOf(String str, int fromIndex)
    返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。
    20	String intern()
    返回字符串对象的规范化表示形式。
    21	int lastIndexOf(int ch)
    返回指定字符在此字符串中最后一次出现处的索引。
    22	int lastIndexOf(int ch, int fromIndex)
    返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。
    23	int lastIndexOf(String str)
    返回指定子字符串在此字符串中最右边出现处的索引。
    24	int lastIndexOf(String str, int fromIndex)
    返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。
    25	int length()
    返回此字符串的长度。
    26	boolean matches(String regex)
    告知此字符串是否匹配给定的正则表达式。
    27	boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)
    测试两个字符串区域是否相等。
    28	boolean regionMatches(int toffset, String other, int ooffset, int len)
    测试两个字符串区域是否相等。
    29	String replace(char oldChar, char newChar)
    返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。
    30	String replaceAll(String regex, String replacement)
    使用给定的 replacement 替换此字符串所有匹配给定的正则表达式的子字符串。
    31	String replaceFirst(String regex, String replacement)
    使用给定的 replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。
    32	String[] split(String regex)
    根据给定正则表达式的匹配拆分此字符串。
    33	String[] split(String regex, int limit)
    根据匹配给定的正则表达式来拆分此字符串。
    34	boolean startsWith(String prefix)
    测试此字符串是否以指定的前缀开始。
    35	boolean startsWith(String prefix, int toffset)
    测试此字符串从指定索引开始的子字符串是否以指定前缀开始。
    36	CharSequence subSequence(int beginIndex, int endIndex)
    返回一个新的字符序列，它是此序列的一个子序列。
    37	String substring(int beginIndex)
    返回一个新的字符串，它是此字符串的一个子字符串。
    38	String substring(int beginIndex, int endIndex)
    返回一个新字符串，它是此字符串的一个子字符串。
    39	char[] toCharArray()
    将此字符串转换为一个新的字符数组。
    40	String toLowerCase()
    使用默认语言环境的规则将此 String 中的所有字符都转换为小写。
    41	String toLowerCase(Locale locale)
    使用给定 Locale 的规则将此 String 中的所有字符都转换为小写。
    42	String toString()
    返回此对象本身（它已经是一个字符串！）。
    43	String toUpperCase()
    使用默认语言环境的规则将此 String 中的所有字符都转换为大写。
    44	String toUpperCase(Locale locale)
    使用给定 Locale 的规则将此 String 中的所有字符都转换为大写。
    45	String trim()
    返回字符串的副本，忽略前导空白和尾部空白。
    46	static String valueOf(primitive data type x)
    返回给定data type类型x参数的字符串表示形式。

### Java StringBuffer 和 StringBuilder 类
    当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。
    和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。
    StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。
    由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。
    然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。
    public class Test{
    public static void main(String args[]){
        StringBuffer sBuffer = new StringBuffer("菜鸟教程官网：");
        sBuffer.append("www");
        sBuffer.append(".runoob");
        sBuffer.append(".com");
        System.out.println(sBuffer);  
    }
    }
    # public StringBuffer append(String s)      将指定的字符串追加到此字符序列。
    # public StringBuffer reverse()             将此字符序列用其反转形式取代。
    # public delete(int start, int end)         移除此序列的子字符串中的字符。
    # public insert(int offset, int i)          将 int 参数的字符串表示形式插入此序列中。
    # replace(int start, int end, String str)   使用给定 String 中的字符替换此序列的子字符串中的字符。
    
    ## 下面的列表里的方法和 String 类的方法类似：
        # int capacity()    返回当前容量。
        # char charAt(int index)    返回此序列中指定索引处的 char 值。
        # void ensureCapacity(int minimumCapacity)  确保容量至少等于指定的最小值。
        # void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin) 将字符从此序列复制到目标字符数组 dst。
        # int indexOf(String str)   返回第一次出现的指定子字符串在该字符串中的索引。
        # int indexOf(String str, int fromIndex)    从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。
        # int lastIndexOf(String str)   返回最右边出现的指定子字符串在此字符串中的索引。
        # int lastIndexOf(String str, int fromIndex)    返回 String 对象中子字符串最后出现的位置。
        # int length()  返回长度（字符数）。
        # void setCharAt(int index, char ch)    将给定索引处的字符设置为 ch。
        # void setLength(int newLength) 设置字符序列的长度。
        # CharSequence subSequence(int start, int end)  返回一个新的字符序列，该字符序列是此序列的子序列。
        # String substring(int start)   返回一个新的 String，它包含此字符序列当前所包含的字符子序列。
        # String substring(int start, int end)  返回一个新的 String，它包含此序列当前所包含的字符子序列。
        # String toString() 返回此序列中数据的字符串表示形式。


###

#### Maven  jar包的管理过程，jar包仓库；

#### JDBC (Java DataBase Connectivity) Java数据库连接 java语言操作数据库；
    本质是官方（sun公司）定义的一套操作所有关系型数据库的规则，即接口，各个数据库厂商去实现这套接口，提供数据库驱动jar包。
    我们可以使用这套接口（JDBC）编程，真正执行的代码是驱动jar包中的实现类；
    
    快速入门：
        1、导入驱动jar包；
        2、注册驱动；
        3、获取数据库连接对象 Connection；
        4、定义SQL；
        5、获取执行SQL语句的对象 Statement；
        6、执行SQL，接受返回结果；
        7、处理结果；
        8、释放资源；

###

## 框架

### 三层架构

    1、表现层：用于展示数据接口的；
    2、业务层：处理业务需求；
    3、持久层：和数据库交互的；

![image-20210218163018310](/Users/zhangmenglei/Library/Application Support/typora-user-images/image-20210218163018310.png)

### mybatis

    mybatis 是一个优秀的基于java的持久层框架；
    mybatis 内部封装了jdbc操作的很多细节，我们只需要关注SQL语句本身，而无需关注加载驱动、创建连接、创建statement等繁杂的过程；
```
mybatis 通过xml或注解的方式将要执行的各种statement配置起来，并通过java对象和statement中sql的动态参数进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射为java对象并返回；
```

```
mybatis使用ORM思想实现了结果集的封装；
ORM：Object Relational Mappging 对象关系映射；就是把数据表中和实体类及其实体类的属性对应起来，操作实体类就可以实现操作数据库表；
create table user(
	`id` int not null auto_increment,
  `username` varchar(32) not null comment '用户名称',
  `birthday` datetime default null commnet '生日',
  `sex` char(1) default null comment '性别',
  `address` varchar(256) default null comment ' 地址',
  primary key(`id`) 
 )engine=innodb default charset=utf8;
```

#### 环境搭建注意事项

![image-20210219134702083](/Users/zhangmenglei/Library/Application Support/typora-user-images/image-20210219134702083.png)

#### 入门案例

![image-20210219140230063](/Users/zhangmenglei/Library/Application Support/typora-user-images/image-20210219140230063.png)

![image-20210219141448015](/Users/zhangmenglei/Library/Application Support/typora-user-images/image-20210219141448015.png)

