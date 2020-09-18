SpringCloud五大组件详解    https://blog.csdn.net/weixin_40910372/article/details/89466955
Spring Cloud系列--Feign整合(一)      https://www.jianshu.com/p/75178737ce91
https://www.runoob.com/java/java-loop.html


一个 Java 程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。下面简要介绍下类、对象、方法和实例变量的概念。

对象：对象是类的一个实例，有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
类：类是一个模板，它描述一类对象的行为和状态。
方法：方法就是行为，一个类可以有很多方法。逻辑运算、数据修改以及所有动作都是在方法中完成的。
实例变量：每个对象都有独特的实例变量，对象的状态由这些实例变量的值决定。

### 编写 Java 程序时，应注意以下几点：
## 大小写敏感：Java 是大小写敏感的，这就意味着标识符 Hello 与 hello 是不同的。
## 类名：对于所有的类来说，类名的首字母应该大写。如果类名由若干单词组成，那么每个单词的首字母应该大写，例如 MyFirstJavaClass 。
## 方法名：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写。
## 源文件名：源文件名必须和类名相同。当保存文件的时候，你应该使用类名作为文件名保存（切记 Java 是大小写敏感的），文件名的后缀为 .java。（如果文件名和类名不相同则会导致编译错误）。
## 主方法入口：所有的 Java 程序由 public static void main(String[] args) 方法开始执行。

### Java 标识符 (类名、变量名、方法名 都成为类名  大小写敏感  不能是关键字)
## Java 所有的组成部分都需要名字。类名、变量名 以及 方法名 都被称为 标识符。
## 关于 Java 标识符，有以下几点需要注意：
# 所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
# 首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
# 关键字不能用作标识符
# 标识符是大小写敏感的
# 合法标识符举例：age、$salary、_value、__1_value
# 非法标识符举例：123abc、-salary

### Java修饰符
## 像其他语言一样，Java可以使用修饰符来修饰类中方法和属性。主要有两类修饰符：
## 访问控制修饰符 : default, public , protected, private
## 非访问控制修饰符 : final, abstract, static, synchronized

### Java 变量
## Java 中主要有如下几种类型的、成员变量（非静态变量）

## 成员变量直接定义在类中，但是在方法之外；
## 成员方法不要写static关键字；

## Java 对象和类
## Java作为一种面向对象语言。支持以下基本概念：
#多态、继承、封装、抽象、类、对象、实例、方法、重载

### 对象：对象是类的一个实例（对象不是找个女朋友），有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
## 类：类是一个模板，它描述一类对象的行为和状态。

### 一个类可以包含以下类型变量：
## 局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。
## 成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。
## 类变量：类变量也声明在类中，方法体之外，但必须声明为 static 类型。

### 构造方法
## 每个类都有构造方法。如果没有显式地为类定义构造方法，Java 编译器将会为该类提供一个默认构造方法。
## 在创建一个对象的时候，至少要调用一个构造方法。构造方法的名称必须与类同名，一个类可以有多个构造方法。
## 构造方法是专门用来创建对象的方法，当我们通过关键字new来创建对象时，其实就是在调用构造方法。
public class Puppy{
    public Puppy(){
    }
    public Puppy(String name){
        // 这个构造器仅有一个参数：name
    }
}
## 注意事项：
# 构造方法名必须和所在的类名称完全一样；
# 构造方法不要写返回值，void 因为不写；
# 如果没有编写构造方法，那么编译器将会默认赠送一个构造方法，没有参数、方法体 什么都不做；
# 一旦编写至少一个构造方法，那么编译器将不再赠送；
# 构造方法也是可以进行重载， 重载：方法名称相同，参数列表不同；

### 创建对象
## 对象是根据类创建的。在Java中，使用关键字 new 来创建一个新的对象。创建对象需要以下三步：
# 声明：声明一个对象，包括对象名称和对象类型。
# 实例化：使用关键字 new 来创建一个对象。
# 初始化：使用 new 创建对象时，会调用构造方法初始化对象。
public class Puppy{
   public Puppy(String name){
      //这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name ); 
   }
   public static void main(String[] args){
      // 下面的语句将创建一个Puppy对象
      Puppy myPuppy = new Puppy( "tommy" );
   }
}

### 访问实例变量和方法
## 通过已创建的对象来访问成员变量和成员方法，如下所示：
# Object referenceVariable = new Constructor();  // 实例化对象
# referenceVariable.variableName;  // 访问类中的变量 
# referenceVariable.methodName();  // 访问类中的方法

public class Puppy{
   int puppyAge;
   public Puppy(String name){
      // 这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name ); 
   }
 
   public void setAge( int age ){
       puppyAge = age;
   }
 
   public int getAge( ){
       System.out.println("小狗的年龄为 : " + puppyAge ); 
       return puppyAge;
   }
 
   public static void main(String[] args){
      /* 创建对象 */
      Puppy myPuppy = new Puppy( "tommy" );
      /* 通过方法来设定age */
      myPuppy.setAge( 2 );
      /* 调用另一个方法获取age */
      myPuppy.getAge( );
      /*你也可以像下面这样访问成员变量 */
      System.out.println("变量值 : " + myPuppy.puppyAge ); 
   }
}

### 源文件声明规则
当在一个源文件中定义多个类，并且还有import语句和package语句时，要特别注意这些规则。
## 一个源文件中只能有一个 public 类
## 一个源文件可以有多个非 public 类
## 源文件的名称应该和 public 类的类名保持一致。例如：源文件中 public 类的类名是 Employee，那么源文件应该命名为Employee.java。
如果一个类定义在某个包中，那么 package 语句应该在源文件的首行。
如果源文件包含 import 语句，那么应该放在 package 语句和类定义之间。如果没有 package 语句，那么 import 语句应该在源文件中最前面。
import 语句和 package 语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。
类有若干种访问级别，并且类也分不同的类型：抽象类和 final 类等。这些将在访问控制章节介绍。

除了上面提到的几种类型，Java 还有一些特殊的类，如：内部类、匿名类。

### Java 包
包主要用来对类和接口进行分类。当开发 Java 程序时，可能编写成百上千的类，因此很有必要对类和接口进行分类。

### import 语句
## 在 Java 中，如果给出一个完整的限定名，包括包名、类名，那么 Java 编译器就可以很容易地定位到源代码或者类。
## import 语句就是用来提供一个合理的路径，使得编译器可以找到某个类。
例如，下面的命令行将会命令编译器载入 java_installation/java/io 路径下的所有类
import java.io.*;

### Java 基本数据类型
变量 就是 申请内存 来 存储值。也就是说，当创建变量的时候，需要在内存中申请空间。
内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。
因此，通过定义不同类型的变量，可以在内存中储存整数、小数或者字符。
Java 的两大数据类型:内置数据类型、引用数据类型

### 内置数据类型
    static boolean bool;
    static byte by;
    static char ch;
    static double d;
    static float f;
    static int i;
    static long l;
    static short sh;
    static String str;
    
### Java 变量类型
在Java语言中，所有的变量在使用前必须声明
int a, b, c;                // 声明三个int型整数：a、 b、c
int d = 3, e = 4, f = 5;    // 声明三个整数并赋予初值
byte z = 22;                // 声明并初始化 z
String s = "runoob";        // 声明并初始化字符串 s
double pi = 3.14159;        // 声明了双精度浮点型变量 pi
char x = 'x';               // 声明变量 x 的值是字符 'x'。

Java语言支持的变量类型有：

类变量：独立于方法之外的变量，用 static 修饰。
实例变量：独立于方法之外的变量，不过没有 static 修饰。
局部变量：类的方法中的变量。
实例
public class Variable{
    static int allClicks=0;    // 类变量
 
    String str="hello world";  // 实例变量
 
    public void method(){
 
        int i =0;  // 局部变量
 
    }
}

Java 局部变量
局部变量声明在方法、构造方法或者语句块中；
局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
访问修饰符不能用于局部变量；
局部变量只在声明它的方法、构造方法或者语句块中可见；
局部变量是在栈上分配的。
局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。

实例变量
实例变量声明在一个类中，但在方法、构造方法和语句块之外；
当一个对象被实例化之后，每个实例变量的值就跟着确定；
实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
实例变量可以声明在使用前或者使用后；
访问修饰符可以修饰实例变量；
实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName。

类变量（静态变量）
类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。
无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
静态变量除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。
静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量。
静态变量在第一次被访问时创建，在程序结束时销毁。
与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。
默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
静态变量可以通过：ClassName.VariableName的方式访问。
类变量被声明为public static final类型时，类变量名称一般建议使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。

### Java数据类型：内置数据类型、引用数据类型
## 妹纸数据类型
# Java提供了八种基本类型  六种数据类型（四个整数型、两个浮点型）、一种字符类型、一种布尔类型
# byte：数据类型是8位、有符号的，以二进制补码表示的整数；  -128 ~ 127
byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
# short 数据类型是 16 位、有符号的以二进制补码表示的整数   
Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
# int 数据类型是32位、有符号的以二进制补码表示的整数；
一般地整型变量默认为 int 类型；
# long 数据类型是 64 位、有符号的以二进制补码表示的整数；
# float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
float 在储存大型浮点数组的时候可节省内存空间；
默认值是 0.0f；
浮点数不能用来表示精确的值，如货币；
# double 数据类型是双精度、64 位、符合IEEE 754标准的浮点数；
浮点数的默认类型为double类型；
double类型同样不能表示精确的值，如货币；
默认值是 0.0d；
# boolean数据类型表示一位的信息；
只有两个取值：true 和 false；
这种类型只作为一种标志来记录 true/false 情况；
默认值是 false；
# char类型是一个单一的 16 位 Unicode 字符；
最小值是 \u0000（即为0）；
最大值是 \uffff（即为65,535）；
char 数据类型可以储存任何字符；


数据类型	默认值
byte	                0
short	                0
int	                    0
long	                0L
float	                0.0f
double	                0.0d
char	                'u0000'
String (or any object)	null
boolean	                false

## 引用数据类型
# 引用类型
对象、数组都是引用数据类型。
所有引用类型的默认值都是null。
  
## Java 常量
常量在程序运行时是不能被修改的。
虽然常量名也可以用小写，但为了便于识别，通常使用大写字母表示常量。
在 Java 中使用 final 关键字来修饰常量，声明方式和变量类似：
final double PI = 3.1415927;

Java语言支持一些特殊的转义字符序列。

符号	字符含义
\n	换行 (0x0a)
\r	回车 (0x0d)
\f	换页符(0x0c)
\b	退格 (0x08)
\0	空字符 (0x0)
\s	空格 (0x20)
\t	制表符
\"	双引号
\'	单引号
\\	反斜杠
\ddd	八进制字符 (ddd)
\uxxxx	16进制Unicode字符 (xxxx)

Java语言支持的变量类型有：

类变量：独立于方法之外的变量，用 static 修饰。
实例变量：独立于方法之外的变量，不过没有 static 修饰。
局部变量：类的方法中的变量。

int a, b, c;         // 声明三个int型整数：a、 b、c
int d = 3, e = 4, f = 5; // 声明三个整数并赋予初值
byte z = 22;         // 声明并初始化 z
String s = "runoob";  // 声明并初始化字符串 s
double pi = 3.14159; // 声明了双精度浮点型变量 pi
char x = 'x';        // 声明变量 x 的值是字符 'x'。

Java 修饰符
Java语言提供了很多修饰符，主要分为以下两类：
访问修饰符、非访问修饰符
修饰符用来定义类、方法或者变量，通常放在语句的最前端。

访问控制修饰符
Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。
default (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
public : 对所有类可见。使用对象：类、接口、变量、方法
protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。

## 非访问修饰符
为了实现一些其他的功能，Java 也提供了许多非访问修饰符。
# static 修饰符，用来修饰类方法和类变量。
静态变量：static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。
静态方法：static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。
对类变量和方法的访问可以直接使用 classname.variablename 和 classname.methodname 的方式访问。
# final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。
final 变量：
final 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。被 final 修饰的实例变量必须显式指定初始值。
final 修饰符通常和 static 修饰符一起使用来创建类常量。
public static final int BOXWIDTH = 6;
final 方法
父类中的 final 方法可以被子类继承，但是不能被子类重写。
声明 final 方法的主要目的是防止该方法的内容被修改。
public final void changeName(){}
final 类
final 类不能被继承，没有类能够继承 final 类的任何特性。
public final class Test {}
# abstract 修饰符，用来创建抽象类和抽象方法。
抽象类：
抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充。
一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。
抽象类可以包含抽象方法和非抽象方法。
抽象方法
抽象方法是一种没有任何实现的方法，该方法的的具体实现由子类提供。
抽象方法不能被声明成 final 和 static。
任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。
如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。
抽象方法的声明以分号结尾，例如：public abstract sample();。
# synchronized 和 volatile 修饰符，主要用于线程的编程。
synchronized 修饰符
synchronized 关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。
public synchronized void showDetails(){
    .......
}
transient 修饰符
序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。
该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。
public transient int limit = 55;   // 不会持久化
public int b; // 持久化
volatile 修饰符
volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。
而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。
一个 volatile 对象引用可能是 null。

### Java 运算符
计算机的最基本用途之一就是执行数学运算，作为一门计算机语言，Java也提供了一套丰富的运算符来操纵变量。我们可以把运算符分成以下几组：
算术运算符、关系运算符、位运算符、逻辑运算符、赋值运算符、其他运算符
## 算术运算符 + - * / % ++ --
## 关系运算符 > >= < <= == !=
## 位运算符 & | ^ ~ << >> >>>
## 逻辑运算符 && || !
## 赋值运算符 + += -= *= /= %= <<= >>= &= ^= |=
## 条件运算符（?:）   variable x = (expression) ? value if true : value if false
## instanceof 运算符  ( Object reference variable ) instanceof  (class/interface type)
## Java运算符优先级  

## Java 循环结构 - for, while 及 do...while
for(int x = 10; x < 20; x = x+1){}
Java 增强 for 循环
Java5 引入了一种主要用于数组的增强型 for 循环。
Java 增强 for 循环语法格式如下:
for(声明语句 : 表达式)
{
   //代码句子
}
声明语句：声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。
表达式：表达式是要访问的数组名，或者是返回值为数组的方法。
## break 关键字
break 主要用在循环语句或者 switch 语句中，用来跳出整个语句块。
break 跳出最里层的循环，并且继续执行该循环下面的语句。
## continue 关键字
continue 适用于任何循环控制结构中。作用是让程序立刻跳转到下一次循环的迭代。
在 for 循环中，continue 语句使程序立即跳转到更新语句。
在 while 或者 do…while 循环中，程序立即跳转到布尔表达式的判断语句。

### Java 条件语句
## if
## if...else
## if...else if...else if...else

### Java switch case 语句
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

### Java Character 类
Character 类用于对单个字符进行操作。
Character 类在对象中包装一个基本类型 char 的值

## 转义序列
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

## Character 方法
isLetter()      是否是一个字母
isDigit()       是否是一个数字字符
isWhitespace()  是否是一个空白字符
isUpperCase()   是否是大写字母
isLowerCase()   是否是小写字母
toUpperCase()   指定字母的大写形式
toLowerCase()   指定字母的小写形式
toString()      返回字符的字符串形式，字符串的长度仅为1

### Java String 类
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

### Java 数组
数组对于每一门编程语言来说都是重要的数据结构之一，当然不同语言对数组的实现及处理也不尽相同。
Java 语言中提供的数组是用来存储固定大小的同类型元素。
你可以声明一个数组变量，如 numbers[100] 来代替直接声明 100 个独立变量 number0，number1，....，number99。

## 声明数组变量
首先必须声明数组变量，才能在程序中使用数组。下面是声明数组变量的语法：
dataType[] arrayRefVar;   // 首选的方法
dataType arrayRefVar[];  // 效果相同，但不是首选方法

double[] myList;         // 首选的方法
double myList[];         //  效果相同，但不是首选方法

## 创建数组
Java语言使用new操作符来创建数组，语法如下：
arrayRefVar = new dataType[arraySize];
上面的语法语句做了两件事：
一、使用 dataType[arraySize] 创建了一个数组。
二、把新创建的数组的引用赋值给变量 arrayRefVar。
数组变量的声明，和创建数组可以用一条语句完成，如下所示：
dataType[] arrayRefVar = new dataType[arraySize];
另外，你还可以使用如下的方式创建数组。
dataType[] arrayRefVar = {value0, value1, ..., valuek};
数组的元素是通过索引访问的。数组索引从 0 开始，所以索引值从 0 到 arrayRefVar.length-1。















### Java 方法
System.out.println()
println() 是一个方法。
System 是系统类。
out 是标准输出对象。
这句话的用法是调用系统类 System 中的标准输出对象 out 中的方法 println()。
## 那么什么是方法呢？
Java方法是 语句的集合，它们在一起执行一个功能。

方法是解决 一类问题 的 步骤 的 有序组合
方法包含于 类 或 对象 中
方法在程序中 被创建，在其他地方被引用

## 方法的优点
1. 使 程序 变得 更简短 而清晰。
2. 有利于 程序维护。
3. 可以提高 程序开发的效率。
4. 提高了 代码的重用性。

## 方法的定义
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
    方法体
    ...
    return 返回值;
}
# 修饰符：修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。
# 返回值类型 ：方法可能会返回值。returnValueType 是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType 是关键字void。
# 方法名：是方法的实际名称。方法名和参数表共同构成方法签名。
# 参数类型：参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。
# 方法体：方法体包含具体的语句，定义该方法的功能。
static float interest(float principal, int year){...}

public static int max(int num1,int num2){
    return num1 > num2 ? num1 : num2;
}

### 方法调用
Java 支持 两种 调用方法的方式，根据方法 是否 返回值 来选择。
当程序调用一个方法时，程序的控制权交给了被调用的方法。当被调用方法的返回语句执行或者到达方法体闭括号时候交还控制权给程序。
1、当方法返回一个值的时候，方法调用通常被当做一个值。例如：
int larger = max(30, 40);
2、如果方法返回值是void，方法调用一定是一条语句。例如，方法println返回void。下面的调用是个语句：
System.out.println("欢迎访问菜鸟教程！");

### void 关键字

### 方法的重载

### 变量作用域

### 命令行参数的使用
有时候你希望运行一个程序时候再传递给它消息。这要靠传递命令行参数给main()函数实现。
命令行参数是在执行程序时候紧跟在程序名字后面的信息。

### 构造方法  构造方法没有返回值
当一个对象被创建时候，构造方法用来初始化该对象。构造方法和它所在类的名字相同，但 构造方法没有返回值。
通常会使用构造方法给一个类的实例变量赋初值，或者执行其它必要的步骤来创建一个完整的对象。
不管你是否自定义构造方法，所有的类都有构造方法，因为Java自动提供了一个默认构造方法，默认构造方法的访问修改符和类的访问修改符相同(类为 public，构造函数也为 public；类改为 protected，构造函数也改为 protected)。
一旦你定义了自己的构造方法，默认构造方法就会失效。

### 可变参数

### finalize() 方法
Java 允许定义这样的方法，它在对象被垃圾收集器析构(回收)之前调用，这个方法叫做 finalize( )，它用来清除回收对象。
例如，你可以使用 finalize() 来确保一个对象打开的文件被关闭了。
在 finalize() 方法里，你必须指定在对象销毁时候要执行的操作。
finalize() 一般格式是：
protected void finalize()
{
   // 在这里终结代码
}
关键字 protected 是一个限定符，它确保 finalize() 方法不会被该类以外的代码调用。
当然，Java 的内存回收可以由 JVM 来自动完成。如果你手动使用，则可以使用上面的方法。

### Java 流(Stream)、文件(File)和IO
Java.io包 几乎 包含了 所有操作输入、输出需要的类。所有这些流类代表了输入源和输出目标。
Java.io包 中的流支持很多种格式，比如：基本类型、对象、本地化字符集等等。
一个流可以理解为一个数据的序列。输入流 表示 从一个源 读取数据， 输出流 表示 向一个目标 写数据。
Java 为 I/O 提供了强大的而灵活的支持，使其更广泛地应用到文件传输和网络编程中。




### Java 继承  extends
继承是java面向对象编程技术的一块基石，因为它允许创建分等级层次的类。
继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
父类更通用，子类更具体。
class 父类 {  }
class 子类 extends 父类 {   }
## 继承的特性
子类拥有父类非 private 的属性、方法。
子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。
子类可以用自己的方式实现父类的方法。
Java 的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如 A 类继承 B 类，B 类继承 C 类，所以按照关系就是 C 类是 B 类的父类，B 类是 A 类的父类，这是 Java 继承区别于 C++ 继承的一个特性。
提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码独立性越差）。 
## 继承关键字
继承可以使用 extends 和 implements 这两个关键字来实现继承，而且所有的类都是继承于 java.lang.Object，当一个类没有继承的两个关键字，则默认继承object（这个类在 java.lang 包中，所以不需要 import）祖先类。
# extends关键字
在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。
# implements关键字
使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。
public interface A {
    public void eat();
    public void sleep();
}
public interface B {
    public void show();
}
public class C implements A,B {
}
# super 与 this 关键字
super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类。
this关键字：指向自己的引用。
# final关键字
final 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写：
声明类：
final class 类名 {//类体}
声明方法：
修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
注:实例变量也可以被定义为 final，被定义为 final 的变量不能被修改。被声明为 final 类的方法自动地声明为 final，但是实例变量并不是 final
# 构造器
子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表。
如果父类构造器没有参数，则在子类的构造器中不需要使用 super 关键字调用父类构造器，系统会自动调用父类的无参构造器。

通常情况下，一个类并不能直接使用，需要根据类创建一个对象，才能使用。
inport 包名称.类名称；
inport cn.itcast.day06.demo01.Student;
对于和当前类属于同一个包的情况，可以省略导包语句；
创建对象格式
类名称 对象名 = new 类名称()；
Student stu = new Student();
使用 分为两种情况
使用成员变量； 对象名.成员变量名；
使用成员方法； 对象名.成员方法名(参数)

### 一个标准的类通常要拥有下面四个组成部分：
## 1、所有的成员变量都是用private关键字修饰；
## 2、为每一个成员变量编写一对 Getter 和 Setter 方法；
## 3、编写一个无参数的构造方法；
## 4、编写一个全参数的构造方法；


### API (Application Programming Interface)
## Scanner      Scanner scan = new Scanner();
## Random       Random ran = new Random();
## ArrayList<>     集合   add get remove size
ArrayList<String> list = new ArrayList<>();  
list.add("张梦磊");
String name = list.get(2);
String name = list.remove(2);
int size = list.size();
集合也可以做方法参数  public static void printArray(ArrayList<String> list)
集合作为参数和返回值  public static ArrayList<Integer> getSmall(ArrayList<Integer> bigList)
基本类型------包装类
byte---------Byte
short--------Short
int----------Integer  *
long---------Long
float--------Float
double-------Double
char---------Character  * 
boolean------Boolean
## String java.lang.String类代表字符串
程序中的所有的双引号字符串，都是 String 类的对象（就算没有new也照样是）
字符串的特点：
1、字符串的内容用不可变，所以字符串是可以共享使用；
2、字符串效果上相当于是char[]字符数组，但是底层原理是byte[]字节数组；

创建字符串的常见3+1方法：
1、public String();  // 创建一个空白字符串，不含任何内容；
String str = new String();
2、public String(char[] array)   // 根据字符数组的内容，来创建对应的字符串
char[] charArray = {"A","B","C"};
String str = new String(charArray);
3、public String(byte[] array)   // 根据字节数组的内容，来创建对应的字符串
byte[] byteArray = {"97","98","99"};
String str = new String(byteArray);
4、String str = "Hello";    // 右边直接用双引号   直接写上双引号，就是字符串对象；

### Sting 常用的方法：
## length          public int length()                 // 获取字符串当中含有的字符串个数，拿到字符串长度；
str.length;  
## concat          public String concat(String str)    // 将当前字符串和参数字符串拼接成为返回值的新的字符串；
str1.concat(str2);
## charAt          public char charAt(int index)       // 获取指定索引位置的单个字符(索引从0开始)；
str.charAt(1);
## indexOf         public int indexOf(String str)      // 查找参数字符串在本字符串当中首次出现的索引位置，如果没有，返回 -1；
str.indexOf(str);
## substring       public String substring(int index);    public String substring(int begin,int end);    // 字符串截取
str.substring()
## toCharArray()   public char[] toCharArray();        // 将当前字符串拆分成字符数组作为返回值；
char[] chars = str.toCharArray();
## getBytes()      public byte[] getBytes();           // 获得当前字符串底层的字节数组
byte[] bytes = str1.getBytes();
## replace         public String replace(CharSequence oldString ,CharSequence)   // 字符串替换
str.replace();
## split()            public String[] split(String regex) // 字符串分割，split方法其实是一个正则表达式。  . =>  \\.

### static  静态变量，静态方法，静态代码  静态内容总是先入非静态
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

### arrays
toString(数组)    public static String toString(数组)  数组->字符串
String intStr = Arrays.toString(intArray)       
sort(数组)    public static void sort(数组)      数组升序排列

### Math
Math.abs();     绝对值
Math.ceil();    向上取整
Math.floor();   向下取整
Math.round();   四舍五入
Math.PI         圆周率

boolean equals(Object obj) 指示其他某个对象是否与此对象"相等"
equals 方法源码
    public boolean equals(Object obj){
        return(this == obj)
    }
boolean b = p1.equals(p2);
System.out.println(b);

## 异常
java.lang.Throwable:类是Java 语言中所有错误或者异常的超类。
    Exception:编译期异常，进行编译（写代码）Java程序出现问题
        RuntimeException：运行期异常，Java程序运行过程中出现的问题
        异常就相当于程序的了一个毛病，把异常处理掉，程序就可以继续执行。
    Error：错误
        错误就相当于程序得了一个无法治愈的毛病，必须修改源代码。

public class DemoException {
    public static void main(String[] args) /* throws ParseException*/ {
//        SimpleDateFormat sdf = new SimpleDateFormat(); // 用来格式化日期
//        Date date = null;
//        try {
//            date = sdf.parse("1992-06-21");
//        } catch (ParseException e) {
//            e.printStackTrace();
//        }
//        System.out.println(date);

//        int[] arr = {1,2,3};
//        try{
//            System.out.println(arr[3]);
//        }catch(Exception e){
//            System.out.println(e);
//        }

//        int[] arr = new int[1024*1024*1024];

//        System.out.println("后续代码");
    }
}


### 序列化 和 反序列化
## Java序列化  对象序列化  对象 => 字节序列(包括 对象的数据、有关对象类型的信息 以及 对象数据的类型)
## 序列化 => 字节序列 => 写入文件 => 从文件提取 => 反序列化
Java 提供了一种 对象序列化的机制，该机制中，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。
将序列化对象写入文件之后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。

序列化 整个过程 都是 Java虚拟机(JVM) 独立的，也就是说，在一个平台上序列化的对象可以在另一个完全不同的平台上反序列化该对象

类 ObjectInputStream 和 ObjectOutputStream 是高层次的数据流，它们包含反序列化和序列化对象的方法。

