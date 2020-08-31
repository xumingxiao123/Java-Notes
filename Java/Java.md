# JAVA基础

#### 1. 如何理解面向对象?

> 参考链接：[link1](https://www.zhihu.com/question/27468564)，[link2](http://www.360doc.com/content/18/1014/21/11935121_794742399.shtml)

**我认为可以从三个层面来解释：**

**第一个层面（基本概念）**：面向对象 ( Object Oriented ) 是将现实问题构建关系，然后抽象成 类 ( class )，给类定义属性和方法后，再将类实例化成 实例 ( instance ) ，通过访问实例的属性和调用方法来进行使用。

**第二个层面（三大特性）**：三大特性：封装，继承，多态（重载和重写）。

**第三个层面（设计模式）**：设计模式的六大原则可以更详细的去解释面向对象及其三大特性的规则。六大原则有：开闭原则，单一指责原则，里氏替换原则，依赖倒置原则，接口隔离原则，迪米特法则。

#### 2. Java和C++的区别?

>链接：https://www.nowcoder.com/discuss/406755

1. Java是解释型语言，所谓的解释型语言，就是源码会先经过一次编译，成为中间码，中间码再被解释器解释成机器码。对于Java而言，中间码就是字节码(.class)，而解释器在JVM中内置了。

2. C++是编译型语言，所谓编译型语言，就是源码一次编译，直接在编译的过程中链接了，形成了机器码。

3. C++比Java执行速度快，但是Java可以利用JVM跨平台。

4. Java是纯面向对象的语言，所有代码（包括函数、变量）都必须在类中定义。而C++中还有面向过程的东西，比如是全局变量和全局函数。

5. C++中有指针，Java中没有，但是有引用。

6. C++支持多继承，Java中类都是单继承的。但是继承都有传递性，同时Java中的接口是多继承，类对接口的实现也是多实现。

7. C++中，开发需要自己去管理内存，但是Java中JVM有自己的GC机制，虽然有自己的GC机制，但是也会出现OOM和内存泄漏的问题。C++中有析构函数，Java中Object的finalize方法。

8. C++运算符可以重载，但是Java中不可以。同时C++中支持强制自动转型，Java中不行，会出现ClassCastException（类型不匹配）。

**面向对象和面向过程有什么区别?**

面向对象和面向过程最本质的区别在于考虑问题的出发点不同，面向过程是以**事件流程**为考虑问题的出发点，而面向对象则是以**参与事件的角色**（对象）为考虑问题的出发点，所以面向对象在处理问题时更加灵活。目前，面向过程的语言更多被用于处理底层业务，而面向对象编程则更多用于实现一些业务逻辑复杂的大型系统。

>面向过程：摇（狗尾巴）
>面向对象：狗.摇尾巴（）
>
>面向过程是编年史。
>面向对象是纪传史。

#### 3. Java面向对象的三大特性?

**三大特性：封装，继承，多态（重载和重写）**

**封装**：把事物用**类**封装起来，保留特定的接口与外界联系，可减少耦合，隐藏细节；

**继承**：子类继承父类，子类可以拥有已知父类的行为和属性；通过继承创建的新类称为「子类」或「派生类」，被继承的类称为「基类」、「父类」或「超类」。

**多态**：多态性是允许你将父对象设置成为和一个或更多的他的子对象相等的技术，赋值之后，父对象就可以根据当前赋值给它的子对象的特性以不同的方式运作。简单说就是一句话：允许将子类类型的指针赋值给父类类型的指针。多态的本质就是一个程序中存在多个同名的不同方法，分为**重载**和**重写**。

[**【拓展】Java中实现多态的机制是什么？**](https://blog.csdn.net/github_37130188/article/details/89931885?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare)

多态就是指一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是**多态性**。

特点：

1. 指向子类的父类引用由于向上转型了，它只能访问父类中拥有的方法和属性，而对于子类中存在而父类中不存在的方法，该引用是不能使用的，尽管是重载该方法。
2. 若子类重写了父类中的某些方法，在调用该些方法的时候，必定是使用子类中定义的这些方法（动态连接、动态调用）。

Java实现多态有三个必要条件：继承、重写、向上转型。

调用的优先级方法，该优先级为：this.show(O)、super.show(O)、this.show((super)O)super.show((super)O)。**多态的实现原理**

Java 里对象方法的调用是依靠类信息里的方法表实现的。总体而言，当调用对象某个方法时，JVM查找该对象类的方法表以确定该方法的直接引用地址，有了地址后才真正调用该方法。Overriding该方法，那么调用时会指向父类的方法。如果Overrding该方法，那么指向该类的代码区。但是超类会存有父类的方法表。

我们知道java程序运行时，类的相关信息放在方法区，在这些信息中有个叫方法表的区域，该表包含有该类型所定义的所有方法的信息和指向这些方法实际代码的指针。

![img](https://img-blog.csdnimg.cn/20190507232434160.png)

当Bird、Cock、Parrot和CrazyParrot这四个类被加载到 Java 虚拟机之方法区后，方法区中就包含了这四个类的信息，下图示例了各个类的方法表。

![img](https://img-blog.csdnimg.cn/20190507232508677.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2dpdGh1Yl8zNzEzMDE4OA==,size_16,color_FFFFFF,t_70)

从图我们可以看到Cock、Parrot和CrazyParrot的类信息方法表包含了继承自Bird的方法。CrazyParrot的方法表包含了继承自Parrot的方法。此外各个类也有自己的方法。

注意看，方法表条目指向的具体方法代码区。对于多态Overriding的方法courtship()，虽然Cock、Parrot和CrazyParrot的方法表里的courtship()条目所在位置是属于继承自Bird方法表的部分，但指向不同的方法代码区了。

> **继承和多态有什么区别？**
>
> 继承是子类获得父类的成员，重写是继承后重新实现父类的方法，重载是在一个类里一系列参数不同名字相同的方法。多态则是为了避免在父类里大量重载引起代码臃肿且难于维护。

#### 4.   Java中重载和重写

**重载(overloading)**：**编译时多态**， 在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。

**重写(Override)**：**运行时多态**，如果一个子类继承了一个父类，子类中拥有和父类相同方法名称，返回值，参数类型的话，就是重写，会执行子类中的方法。

**重载：**

~~~java
public class 重载 {
    public static void sayhello(int s){
        System.out.println("这是int类型的参数");
    }
    public static void sayhello(char s){
        System.out.println("这是char类型的参数");
    }

    public static void main(String[] args) {
        sayhello(1);
        sayhello('a');
    }
}
~~~

**重写：**

~~~java
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}
 
class Dog extends Animal{
   public void move(){
      System.out.println("狗可以跑和走");
   }
}
 
public class TestDog{
   public static void main(String args[]){
      Animal a = new Animal(); // Animal 对象
      Animal b = new Dog(); // Dog 对象
 
      a.move();// 执行 Animal 类的方法
 
      b.move();//执行 Dog 类的方法
   }
}
~~~

以上实例编译运行结果如下：

> 动物可以移动
> 狗可以跑和走

在上面的例子中可以看到，尽管 b 属于 Animal 类型，但是它运行的是 Dog 类的 move方法。**这是由于在编译阶段，只是检查参数的引用类型**。然而在运行时，Java 虚拟机(JVM)指定对象的类型并且运行该对象的方法。因此在上面的例子中，之所以能编译成功，是因为 Animal 类中存在 move 方法，然而运行时，运行的是特定对象的方法。

**【拓展】多态的底层原理？**

重载编译时多态和重写运行时多态的解释：[link](https://blog.csdn.net/qq_38262968/article/details/82152449)，[link1](https://www.runoob.com/java/java-override-overload.html)，[link2](https://blog.csdn.net/qq_38262968/article/details/82152449)，[link3](https://blog.csdn.net/qq_35181209/article/details/77089724)

**【拓展】Java中重载和重写的规则？**

**方法的重载规则**

- 被重载的方法必须改变参数列表(参数个数或类型不一样)；
- 被重载的方法可以改变返回类型；
- 被重载的方法可以改变访问修饰符；
- 被重载的方法可以声明新的或更广的检查异常；
- 方法能够在同一个类中或者在一个子类中被重载。
- 无法以返回值类型作为重载函数的区分标准。

**方法的重写规则**

* 参数列表必须完全与被重写方法的相同。

* 返回类型与被重写方法的返回类型可以不相同，但是必须是父类返回值的派生类（java5 及更早版本返回类型要一样，java7 及更高版本可以不同）。

>父类返回值可能是复杂类型，如返回的是class A，那么重写返回值类型就要是class A或者是class A的子类

* **子类访问权限不能比父类中被重写的方法的访问权限更低**。例如：如果父类的一个方法被声明为 public，那么在子类中重写该方法就不能声明为 protected。

* 父类的成员方法只能被它的子类重写。

* 声明为 **final** 的方法不能被重写。

* 声明为 **static** 的方法不能被重写，但是能够被再次声明。

* 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为 private 和 final 的方法。

* 子类和父类不在同一个包中，那么子类只能够重写父类的声明为 public 和 protected 的非 final 方法。

* 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。

* 构造方法不能被重写。

* 如果不能继承一个方法，则不能重写这个方法。

> **为什么Java中子类重写方法的访问权限不能低于父类中权限?** [link](https://blog.csdn.net/Liebers/article/details/82697949?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.compare&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.compare)
>
> 该问题依赖于里氏代换原则, 先记录下该原则的原理，里氏代换原则(Liskov Substitution Principle LSP)面向对象设计的基本原则之一。 **里氏代换原则**中说，任何基类可以出现的地方，子类一定可以出现。

**重载重写规则对比**

| 区别点   | 重载方法 | 重写方法                                       |
| :------- | :------- | :--------------------------------------------- |
| 参数列表 | 必须修改 | 一定不能修改                                   |
| 返回类型 | 可以修改 | 一定不能修改                                   |
| 异常     | 可以修改 | 可以减少或删除，一定不能抛出新的或者更广的异常 |
| 访问     | 可以修改 | 一定不能做更严格的限制（可以降低限制）         |

方法的重写(Overriding)和重载(Overloading)是java多态性的不同表现，重写是父类与子类之间多态性的一种表现，重载可以理解成多态的具体表现形式。

- (1)方法重载是一个类中定义了多个方法名相同,而他们的参数的数量不同或数量相同而类型和次序不同,则称为方法的重载(Overloading)。
- (2)方法重写是在子类存在方法与父类的方法的名字相同,而且参数的个数与类型一样,返回值也一样的方法,就称为重写(Overriding)。
- (3)方法重载是一个类的多态性表现,而方法重写是子类与父类的一种多态性表现。

#### 5.  Java 中的访问修饰符

Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

- **public（公开）** :任何位置都可见。使用对象：类、接口、变量、方法
- **protected（受保护）** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。
- **default(默认）** : 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- **private（私有）** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**

| 修饰符      | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包)                                               | 其他包 |
| :---------- | :----- | :------- | :------------- | :----------------------------------------------------------- | :----- |
| `public`    | Y      | Y        | Y              | Y                                                            | Y      |
| `protected` | Y      | Y        | Y              | Y（[说明](https://www.runoob.com/java/java-modifier-types.html#protected-desc)） | N      |
| `default`   | Y      | Y        | Y              | N                                                            | N      |
| `private`   | Y      | N        | N              | N                                                            | N      |

[link](https://www.runoob.com/java/java-modifier-types.html)

#### 6.  Java的8种基本类型与封装类？

**整数类型**：字节型（byte/8位）、短整型（short/16位）、整型（int/32位）、长整型（long/64位）

**浮点类型**：单精度型（float/32位）和双精度类型（double/64位）

**字符类型**：字符类型（char/16位）

**布尔类型**：布尔类型（boolean/1位），常量只有“真（true）”和“假（false）”这两个状态

> **一个字节为8位**

------

**Java中的封装类：**

**8种基本类型按照类型划分：byte，short，int，long，float，double，boolean，char。**

**8种基本类型的封装类：Byte,Short,Integer,Long,Float,Double,Boolean,Character.**

* boolean类型占了单独使用是4个字节，在数组中又是1个字节
* 基本类型所占的存储空间是不变的。这种不变性也是Java具有可移植性的原因之一。
* 基本类型放在栈中，直接存储值。
* 所有数值类型都有正负号，没有无符号的数值类型。

**为什么需要封装类？**
因为泛型类包括预定义的集合，使用的参数都是对象类型，无法直接使用基本数据类型，所以Java又提供了这些基本类型的封装类。

**基本类型和对应的封装类由于本质的不同。具有一些区别**：
1.**基本类型只能按值传递，而封装类按引用传递**。
2.**基本类型会在栈中创建，而对于对象类型，对象在堆中创建，对象的引用在栈中创建**，基本类型由于在栈中，效率会比较高，但是可能存在内存泄漏的问题

>**包装类的缓存：**
>
>Boolean：全部缓存
>
>Byte：全部缓存
>
>Character：<= 127 缓存
>
>Short：-128 — 127 缓存
>
>Long：-128 — 127 缓存
>
>Integer：-128 — 127 缓存
>
>Float：没有缓存
>
>Doulbe：没有缓存

**自动装箱与自动拆箱**：[link](https://blog.csdn.net/yangyechi/article/details/82530447?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare)

#### 7.  Java中“==”和equals的区别？

1. ==是基本运算符，可以对基本类型进行比较，比较的是对象的引用是否指向同一块内存地址。
2. equals()是一个方法，它不可以可以对基本类型进行比较。见源码1，**equals()默认的方法中也使用了==，比较的也是对象的地址**。见源码2，只不过equals()是一个方法可以对其进行重写，像String、Date、Math、File、包装类等大部分类都重写了Object的equals()方法。重写后的equals()将每个值取出依次对比其内存地址，也可以把它理解为比较整体值是否相等。



>**重写hashCode遵循的五个条件**
>
> 在改写equals方法时，也要遵守他们的通用约定（equals方法实现了等价关系）：
>
>​    \1.   自反性：x.equals(x) = true;
>
>​    \2.   对称性：如果有x.equals(y) = true,那么一定有y.equals(x) = true;
>
>​    \3.   传递性：对任意的x,y,z。如果有x.equals(y) = y.equals(z) = true,那么一定有x.equals(z)= true;
>
>​    \4.   一致性：无论多少次调用，x.equals(y)总会返回相同的结果。
>
>​    \5.   非空性（暂定）：所有的对象都必须！=null;
>
> 上面的只是理论性的说法，更加具体的做法如下：
>
>​    \1.   使用==操作符检查“实参是否为指向对象的一个引用”，如果是则返回true；
>
>​    \2.   使用instanceof操作符检查“实参是否为正确的类型”，如果不是，则返回false;
>
>​    \3.   将实参装换为正确的类型；
>
>​    \4.   对于该类中的每一个关键域，检查实参中的域与当前对象中对应的域是否匹配。如果所有测试都成功，则返回true，否则返回false。
>
>​    \5.   方法完成之后，确定equals方法的对称性，传递性，一致性。
>
>**如何使用？**
>
>在java虚拟机中，基本类型存储在方法区中的常量池中，同属性同地址，用==即可。但是对于new出来的对象它们存储在堆中，==仅能比较其地址首相等。无法比较真正意义上的相等，用重写的equals方法即可。

~~~java
public boolean equals(Object obj) {
    return (this == obj);
}
~~~

**源码2. String类源码中重写的equals方法如下：**

~~~ java
public boolean equals(Object anObject) {
// 1. 检查是否为同一个对象的引用，如果是直接返回 true；
        if (this == anObject) {
            return true;
        }
/*2.判断anObject是否为String类的实例，如果不是直接返回false，如果是则取值比较大小。
注：instanceof 测试一个对象是否为一个类的实例
 **/
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
~~~

**为什么会出现以下现象？**

~~~java
        //1. 比较基本类型
        int m=1;
        int n=1;
        // System.out.println(m.equals(n)); // 报错
        System.out.println(m == n);  // true
        //System.out.println(m.hashCode());  // 报错
        //System.out.println(n.hashcode());  // 报错

        //2. 比较new出来的封装类型
        Integer x = new Integer(1);
        Integer y = new Integer(1);
        System.out.println(x.equals(y)); // true
        System.out.println(x == y);      // false

        //3. 比较非new封装类型 [-128, 127] 
        Integer x1 = 127;
        Integer y1 = 127;
        System.out.println(x1.equals(y1)); // true
        System.out.println(x1 == y1);      // true

        //4. 比较非new封装类型非[-128, 127] 
        Integer x2 = 128;
        Integer y2 = 128;
        System.out.println(x2.equals(y2)); // true
        System.out.println(x2 == y2);      // false
        
       //5. 比较非new字符串
        String s1="abc";
        String s2="abc";
        System.out.println(s1==s2);  // true
        System.out.println(s1.equals(s2));  // true

        //6. 比较new字符串
        String str1 = new String("hello");
        String str2 = new String("hello");
        System.out.println(str1.equals(str2)); //true
        System.out.println(str1==str2); //false

~~~

**1. 比较基本类型**
对于基本数据类型（byte，short，char，int，float，double，long，boolean）来说，他们是作为常量在方法区中的常量池里面以HashSet策略（HashSet中不允许有重复的元素）存储起来的。因此在常量池，一个常量只会对应一个地址。所以不管是再多的 1，其内存地址都为同一个。
 **2. 比较new出来的封装类型**
new String("hello")会在堆内存中创建一个实例，开辟新的内存空间，故==为falsie。但是源码2中，String类源码中重写了equals方法，对单个值的进行比较。
**3. 比较非new封装类型 [-128, 127]**
**4. 比较非new封装类型非[-128, 127]** 
对于两个非 new 生成的 Integer 对象进行比较时，如果两个变量的值在区间 [-128, 127] 之间，则比较结果为 true，否则为 false。Java 在编译 Integer i = 100 时，会编译成 Integer i = Integer.valueOf(100)，而 Integer 类型的 valueOf 的源码如下所示：

 ~~~java
public static Integer valueOf(int var0) {    
        return var0 >= -128 && var0 <= Integer.IntegerCache.high ? Integer.IntegerCache.cache[var0 + 128] : new Integer(var0);
}
 ~~~

从上面的代码中可以看出：Java 对于 [-128, 127] 之间的数会进行缓存，比如：Integer i = 127，会将 127 进行缓存，下次再写 Integer j = 127 的时候，就会直接从缓存中取出，而对于这个区间之外的数就需要 new 了。
**5. 比较字符串**
在Java执行时会维护一个String池（pool），对于一些可以共享的字符串对象，会先在String池中查找是否存在相同的String内容（字符相同），如果有就直接返回，不创建新对象。
**6. 比较非new字符串常量**
new String("hello")会在堆内存中创建一个实例，开辟新的内存空间，故==为falsie。但是，String类源码中重写了equals方法，对单个值的进行比较。

#### 8. 为什么重写equals一定要重写hashcode？

[link1](https://blog.csdn.net/xl_1803/article/details/80445481)，[link2](https://blog.csdn.net/weixin_40828249/article/details/96024288?depth_1-utm_source=distribute.pc_relevant.none-task-blog-OPENSEARCH-5&utm_source=distribute.pc_relevant.none-task-blog-OPENSEARCH-5)，[link3](https://blog.csdn.net/u013679744/article/details/57074669?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare)，[link4](https://blog.csdn.net/qq_35868412/article/details/89380409?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.compare&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.compare)，[link5](https://www.jianshu.com/p/5b7fe120bf94?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)，[link6](https://blog.csdn.net/u011583316/article/details/107129546/)

主要是**为了提升哈希表的性能**。因为HashMap 集合类使用了 hashCode() 方法来计算对象在哈希表中应该存储的位置，如果不重写hashcode值一样的对象。因为new出来的对象即使值相同，存储地址必不相同。不重写 hashCode会导致为值相同的对象分别了两个存储空间，导致了空间浪费。因此要重写。

**以下是关于hashcode的一些性质：**

>两个对象相等，hashcode一定相等
>
>两个对象不等，hashcode不一定不等
>
>hashcode相等，两个对象不一定相等
>
>hashcode不等，两个对象一定不等

#### 9. Java中抽象类和接口的区别？[link](https://cloud.tencent.com/developer/article/1517566)

从设计层面上看，抽象类提供了一种 IS-A 关系，需要满足里式替换原则，即子类对象必须能够替换掉所有父类对象。而接口更像是一种 LIKE-A 关系，它只是提供一种方法实现契约，并不要求接口和实现接口的类具有 IS-A 关系。**接口反应能力，抽象类提供默认实现，方便子类实现接口**。

（1）抽象类中可以定义构造函数，接口不能定义构造函数；

（2）接口可以被看作是抽象类的变体，接口中所有的方法都是抽象的（Java 1.8中可以定义default方法体）。

（3）**从使用上来看，一个类可以实现多个接口，但是不能继承多个抽象类**。

（4）**接口的字段只能是 static 和 final 类型的，而抽象类的字段没有这种限制**。

（5）**接口的成员只能是 public 的，而抽象类的成员除了不能被private修饰，可以有多种访问权限**。

> **共同点**：抽象类和接口都不能被实例化

> **什么是抽象类？什么是抽象方法？**
>
> **抽象类**：**抽象类就是不能使用new方法进行实例化的类**，即没有具体实例对象的类，抽象类有点类似于“模板”的作用,目的是根据其格式来创建和修改新的类，对象不能由抽象类直接创建，只可以通过抽象类派生出新的子类，再由其子类来创建对象，当一个类被声明为抽象类时，要在这个类前面加上修饰符abstract,在抽象类中的成员方法可以包括一般方法和抽象方法
>
> **抽象方法**：**抽象方法就是以abstract修饰的方法，这种方法只声明返回的数据类型，方法名称和所需要的参数，没有方法体**，也就是说抽象方法只需要声明而不需要事先，当一个方法为抽象方法时，意味着这个方法必须被子类的方法所重写，否则其子类的该方法仍然是abstract的，而这个子类也必须是抽象的，即声明为abstract。
>
> 原文链接：https://blog.csdn.net/dulijie/article/details/88256415
>
> **构造函数** ，是一种特殊的方法。主要用来在创建对象时初始化对象， 即为对象[成员变量](https://baike.baidu.com/item/成员变量)赋初始值，总与new[运算符](https://baike.baidu.com/item/运算符)一起使用在创建对象的语句中。特别的一个类可以有多个构造函数 ，可根据其参数个数的不同或参数类型的不同来区分它们 即构造函数的[重载](https://baike.baidu.com/item/重载)。

>**为什么接口中的成员变量非得是public static final的呢？**
>
>首先明白一个原理，就是接口的存在意义。接口就是为了实现多继承的抽象类，是一种高度抽象的模板、标准或者说协议。规定了什么东西该是这样，如果你继承了我这接口，就必须这样。比如USB接口，就是小方口，两根电源线和两根数据线，不能多不能少。
>
>**public**: 使接口的实现类可以使用这个常量
>**static**：static修饰就表示它属于类的，随的类的加载而存在的，如果是非static的话，就表示属于对象的，只有建立对象时才有它，而接口是不能建立对象的，所以接口的常量必须定义为static。
>**final**：final修饰就是保证接口定义的常量不能被实现类去修改，如果没有final的话，
>由子类随意去修改的话，接口建立这个常量就没有意义了。
>
>https://blog.csdn.net/u013682953/article/details/73699796
>
>https://blog.csdn.net/piyongduo3393/article/details/85225294

**举例说明：LinkedList**

>https://blog.csdn.net/qedgbmwyz/article/details/80108618

~~~java
public class LinkedList<E>
     extends AbstractSequentialList<E>
     implements List<E>, Deque<E>, Cloneable, java.io.Serializable
~~~

LinkedList 是一个继承于AbstractSequentialList的双向链表。它也可以被当作堆栈、队列或双端队列进行操作。
LinkedList 实现 List 接口，能对它进行队列操作。
LinkedList 实现 Deque 接口，即能将LinkedList当作双端队列使用。
LinkedList 实现了Cloneable接口，即覆盖了函数clone()，能克隆。
LinkedList 实现java.io.Serializable接口，这意味着LinkedList支持序列化，能通过序列化去传输。
LinkedList 是非同步的。

**为什么要继承自AbstractSequentialList ?**

AbstractSequentialList 实现了get(int index)、set(int index, E element)、add(int index, E element) 和 remove(int index)这些骨干性函数。降低了List接口的复杂度。这些接口都是随机访问List的，LinkedList是双向链表；既然它继承于AbstractSequentialList，就相当于已经实现了“get(int index)这些接口”。

此外，我们若需要通过AbstractSequentialList自己实现一个列表，只需要扩展此类，并提供 listIterator() 和 size() 方法的实现即可。若要实现不可修改的列表，则需要实现列表迭代器的 hasNext、next、hasPrevious、previous 和 index 方法即可。

#### 10. final finally finalize 区别及用法?

(https://www.cnblogs.com/wisefulman/p/10584515.html)

**final**：可以用来修饰类、方法、变量，分别有不同的意义，final修饰的class代表不可以继承扩展，final的变量是不可以修改的，而final的方法也是不可以重写的（override）。

**finally**：则是Java保证重点代码一定要被执行的一种机制。我们可以使用try-finally或者try-catch-finally来进行类似关闭JDBC连接、保证unlock锁等动作。

**finalize**：finalize()是Object中的方法，当垃圾回收器将要回收对象所占内存之前被调用，即当一个对象被虚拟机宣告死亡时会先调用它finalize()方法，让此**对象处理它生前的最后事情**（这个对象可以趁这个时机挣脱死亡的命运）。finalize机制现在已经不推荐使用，并且在JDK 9开始被标记为deprecated。
链接：https://www.jianshu.com/p/afaf54b9632e

https://baijiahao.baidu.com/s?id=1655232869611610920&wfr=spider&for=pc

**【拓展】finalize的原理：**

![img](https://pics5.baidu.com/feed/1e30e924b899a9010d34c78331bb0d7d0208f532.jpeg?token=cc6b19d8b9ecf5e0697042b70da81e1d&s=0D40EC12E18768EA584DA0CE0200D0A1)

1）对象在初始化的过程中会判断是否重写了**finalize**，方法是判断两个字段标志has_finalizer_flag和RegisterFinalizersAtInit。

2）如果重写了finalize，那就把当前对象注册到FinalizerThread的ReferenceQueue队列中。注册之后的对象就叫做Finalizer。方法是调用register_finalizer函数。此时java虚拟机一看当前有这个对象的引用，于是就不进行垃圾回收了。

3）对象开始被调用，FinalizerThread线程负责从ReferenceQueue队列中获取Finalizer对象。开始执行finalize方法，在执行之前，这个对象一直在堆中。

4）对象执行完毕之后，将这个Finalizer对象从队列中移除，java虚拟机一看对象没有引用了，就进行垃圾回收了。

这就是整个过程。不过在这里我们主要看的是finalize方法对垃圾回收的影响，其实就是在第三步，也就是这个对象含有finalize，进入了队列但一直没有被调用的这段时间，会一直占用内存。

> finalize流程：**当对象变成(GC Roots)不可达时，GC会判断该对象是否覆盖了finalize方法，若未覆盖，则直接将其回收。否则，若对象未执行过finalize方法，将其放入F-Queue队列，由一低优先级线程执行该队列中对象的finalize方法。执行finalize方法完毕后，GC会再次判断该对象是否可达，若不可达，则进行回收，否则，对象“复活”。**

#### 11. this和super的区别

https://www.cnblogs.com/newbie27/p/10437587.html

https://blog.csdn.net/lncsdn_123/article/details/79025525

**this**是自身的一个对象，代表对象本身，可以理解为：指向对象本身的一个指针；

**supe**r可以理解为是指向自己超（父）类对象的一个指针，而这个超类指的是离自己最近的一个父类。

#### 13 泛型

https://segmentfault.com/a/1190000014120746

**泛型：把类型明确的工作推迟到创建对象或调用方法之后**，简单来说，你有一个类，在使用时内部类型暂不确定，给使用给一个占位符给代替，在使用的时候可以给确定其定义的类型。例如HashMap等集合类中就用到了泛型：

~~~java
ArrayList<String> stringValues=new ArrayList<String>();
~~~

有了泛型以后：

* 代码更加简洁【不用强制转换】
* 程序更加健壮【只要编译时期没有警告，那么运行时期就不会出现ClassCastException异常】
* 可读性和稳定性【在编写集合的时候，就限定了类型】

https://www.jianshu.com/p/2bfbe041e6b7

**泛型底层如何实现？Java的泛型是使用类型擦除来实现的，意味着当你在使用泛型时，任何具体的类型信息都被擦除了，你唯一知道的就是你在使用一个对象**。

>泛型用于编译阶段，编译后的字节码文件不包含泛型类型信息，因为虚拟机没有泛型类型对象，所有对象都属于普通类。例如定义 `List<Object>` 或 `List<String>`，在编译后都会变成 `List` 。
>
>定义一个泛型类型，会自动提供一个对应原始类型，类型变量会被擦除。如果没有限定类型就会替换为 Object，如果有限定类型就会替换为第一个限定类型，例如 `<T extends A & B>` 会使用 A 类型替换 T。
>
>ava语言的泛型采用的是**擦除法**实现的**伪泛型**，泛型信息（类型变量、参数化类型）编译之后通通被除掉了。使用擦除法的好处就是实现简单、非常容易Backport，运行期也能够节省一些类型所占的内存空间。而擦除法的坏处就是，通过这种机制实现的泛型远不如真泛型灵活和强大。Java选取这种方法是一种折中，因为Java最开始的版本是不支持泛型的，为了兼容以前的库而不得不使用擦除法。

#### 14. 常用注解

https://www.cnblogs.com/yanze/p/9481915.html

> 注解提升了java语言的表达能力，有效实现了应该用功能和底层功能的分离。

**java内置注解**

@**Override**

覆盖父类方法

@**Deprecated**(不赞成)

用于方法，表明方法已过期，不建议使用

@**Suppvisewarning** 

忽略警告，例如当我们要使用已过时方法，有的编译器会出现警告，

@Suppvisewarning（"deprecation"）表示忽略此警告

**元注解**是自定义注解的注解，例如：

`@Target`：约束作用位置，值是 ElementType 枚举常量，包括 METHOD 方法、VARIABLE 变量、TYPE 类/接口、PARAMETER 方法参数、CONSTRUCTORS 构造方法和 LOACL_VARIABLE 局部变量等。

`@Rentention`：约束生命周期，值是 RetentionPolicy 枚举常量，包括 SOURCE 源码、CLASS 字节码和 RUNTIME 运行时。

`@Documented`：表明这个注解应该被 javadoc 记录。

#### 15.  JDK1.8中有哪些新特性？[link](https://www.cnblogs.com/jacksontao/p/8608291.html)

- **Lambda表达式**：Lambda允许把函数作为一个方法的参数（函数作为参数传递到方法中）。
- **方法引用**：方法引用提供了非常有用的语法，可以直接引用已有Java类或对象（实例）的方法或构造器。与lambda联合使用，方法引用可以使语言的构造更紧凑简洁，减少冗余代码。
- **默认方法**：默认方法就是一个在接口里面有了一个实现的方法。
- **新工具**：新的编译工具，如：Nashorn引擎 jjs、 类依赖分析器jdeps。
- **Stream API**：新添加的Stream API（java.util.stream） 把真正的函数式编程风格引入到Java中。
- **Date Time API**：加强对日期与时间的处理。
- **Optional类**：Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常。
- **Nashorn，JavaScript引擎**：JDK1.8提供了一个新的Nashorn javascript引擎，它允许我们在JVM上运行特定的javascript应用。

#### 16. Java对象的hashCode方法理解

**概念：**Object类中有一个方法: `public native int hashCode();` Java中的hashCode方法就是根据一定的规则将与对象相关的信息（比如对象的存储地址，对象的字段等）映射成一个数值，这个数值称作为散列值。

**作用：**

1. 用于查找的快捷性。如HashMap，hashCode值用于散列来确定对象hash到哪个slot
2. 减少equals方法的调用次数，从而提高程序效率。如在集合中两个对象相等判断时，先比较hashCode方法的值，**相等再调用equals方法**，所以在对象不相等时直接hashCode不等判断结束，减少equals方法的调用。当然也存在对象不相等但hashCide值相等的情况，如:`"wzd".hashCode()=="x[d".hashCode()`

**HashCode约定：**

- 在程序执行期间，只要equals方法的比较操作用到的信息没有被修改，那么对这同一个对象调用多次，hashCode方法必须始终如一地返回同一个整数。
- 如果两个对象根据equals方法比较是相等的，那么调用两个对象的hashCode方法必须返回相同的整数结果。
- 如果两个对象根据equals方法比较是不等的，则hashCode方法不一定要返回不同的整数。但是，为不相等的对象生成不同hashCode可以提高hash的性能，减少冲突。

#### 17.Object o=new object()在中占用多少字节？

https://blog.csdn.net/weixin_42864905/article/details/104966716

![å°å§å§é®ï¼Object obj=new Object()ç©¶ç«å å¤å°å­èåï¼](https://imgconvert.csdnimg.cn/aHR0cDovL3AzLnBzdGF0cC5jb20vbGFyZ2UvZGZpYy1pbWFnZWhhbmRsZXIvM2Q5ZGJjZTYtNmYwZC00MjdhLWIwYjctODk3ZTUyMDc3M2Q0?x-oss-process=image/format,png)



![å°å§å§é®ï¼Object obj=new Object()ç©¶ç«å å¤å°å­èåï¼](https://imgconvert.csdnimg.cn/aHR0cDovL3AxLnBzdGF0cC5jb20vbGFyZ2UvZGZpYy1pbWFnZWhhbmRsZXIvMGVhYjRhNDAtY2RmNy00YzdmLWFhYjYtNzI2YmI4NDMxZWMy?x-oss-process=image/format,png)

![å°å§å§é®ï¼Object obj=new Object()ç©¶ç«å å¤å°å­èåï¼](https://imgconvert.csdnimg.cn/aHR0cDovL3AxLnBzdGF0cC5jb20vbGFyZ2UvZGZpYy1pbWFnZWhhbmRsZXIvNjhmZjY1ZmYtYWRiZS00OGUzLWJkY2UtMmQwYjIwNGM1NmM0?x-oss-process=image/format,png)

**Klass Word** 这里其实是虚拟机设计的一个oop-klass model模型，这里的OOP是指Ordinary Object Pointer（普通对象指针），看起来像个指针实际上是藏在指针里的对象。而 klass 则包含 元数据和方法信息，用来描述 Java 类。它在64位虚拟机开启压缩指针的环境下占用 32bits 空间。

**Mark Word** 是我们分析的重点，这里也会设计到锁的相关知识。Mark Word 在64位虚拟机环境下占用 64bits 空间。整个Mark Word的分配有几种情况：

1. 未锁定（Normal）： 哈希码（identity_hashcode）占用31bits，分代年龄（age）占用4 bits，偏向模式（biased_lock）占用1 bits，锁标记（lock）占用2 bits，剩余26bits 未使用(也就是全为0)

2. 可偏向（Biased）： 线程id 占54bits，epoch 占2 bits，分代年龄（age）占用4 bits，偏向模式（biased_lock）占用1 bits，锁标记（lock）占用2 bits，剩余 1bit 未使用。

3. 轻量锁定（Lightweight Locked）： 锁指针占用62bits，锁标记（lock）占用2 bits。

4. 重量级锁定（Heavyweight Locked）：锁指针占用62bits，锁标记（lock）占用2 bits。

5. GC 标记：标记位占2bits，其余为空（也就是填充0）
   以上就是我们对Java对象头内存模型的解析，只要是Java对象，那么就肯定会包括对象头，也就是说这部分内存占用是避免不了的。所以，在笔者64位虚拟机，Jdk1.8（开启了指针压缩）的环境下，任何一个对象，啥也不做，只要声明一个类，那么它的内存占用就至少是96bits，也就是至少12字节。

**内存对齐**：4个字节，保证可以被8整除。内存对齐
想要知道为什么虚拟机要填充4个字节，我们需要了解什么是内存对齐？

我们程序员看内存是这样的：



 ![å°å§å§é®ï¼Object obj=new Object()ç©¶ç«å å¤å°å­èåï¼](https://imgconvert.csdnimg.cn/aHR0cDovL3AzLnBzdGF0cC5jb20vbGFyZ2UvZGZpYy1pbWFnZWhhbmRsZXIvYWEwNzM0NjYtYTMzZS00ZmRmLWE4YmYtMjQ2NjliNWIzYThi?x-oss-process=image/format,png)

上图表示一个坑一个萝卜的内存读取方式。但实际上 CPU 并不会以一个一个字节去读取和写入内存。相反 CPU 读取内存是一块一块读取的，块的大小可以为 2、4、6、8、16 字节等大小。块大小我们称其为内存访问粒度。如下图：

![å°å§å§é®ï¼Object obj=new Object()ç©¶ç«å å¤å°å­èåï¼](https://imgconvert.csdnimg.cn/aHR0cDovL3A5LnBzdGF0cC5jb20vbGFyZ2UvZGZpYy1pbWFnZWhhbmRsZXIvMzJiOWRjZjctMDNmNC00YzlkLWE1MzQtZWI5MzA4MGFhNTE0?x-oss-process=image/format,png)

 

假设一个32位平台的 CPU，那它就会以4字节为粒度去读取内存块。那为什么需要内存对齐呢？主要有两个原因：

平台（移植性）原因：不是所有的硬件平台都能够访问任意地址上的任意数据。例如：特定的硬件平台只允许在特定地址获取特定类型的数据，否则会导致异常情况。
性能原因：若访问未对齐的内存，将会导致 CPU 进行两次内存访问，并且要花费额外的时钟周期来处理对齐及运算。而本身就对齐的内存仅需要一次访问就可以完成读取动作。
我用图例来说明 CPU 访问非内存对齐的过程：

![å°å§å§é®ï¼Object obj=new Object()ç©¶ç«å å¤å°å­èåï¼](https://imgconvert.csdnimg.cn/aHR0cDovL3AxLnBzdGF0cC5jb20vbGFyZ2UvZGZpYy1pbWFnZWhhbmRsZXIvNzg3N2U0MjktYWIwZS00NDY5LTlmNTctNTU5MDhkMmZkZDVk?x-oss-process=image/format,png)

 

在上图中，假设CPU 是一次读取4字节，在这个连续的8字节的内存空间中，如果我的数据没有对齐，存储的内存块在地址1，2，3，4中，那CPU的读取就会需要进行两次读取，另外还有额外的计算操作：

1. CPU 首次读取未对齐地址的第一个内存块，读取 0-3 字节。并移除不需要的字节 0。
2. CPU 再次读取未对齐地址的第二个内存块，读取 4-7 字节。并移除不需要的字节 5、6、7 字节。
3. 合并 1-4 字节的数据。
4. 合并后放入寄存器。

所以，没有进行内存对齐就会导致CPU进行额外的读取操作，并且需要额外的计算。如果做了内存对齐，CPU可以直接从地址0开始读取，一次就读取到想要的数据，不需要进行额外读取操作和运算操作，节省了运行时间。我们用了空间换时间，这就是为什么我们需要内存对齐。

回到Java空对象填充了4个字节的问题，因为原字节头是12字节，64位机器下，内存对齐的话还需要填充4个字节就是128位，也就是**16字节**。

**数组：最小是24个字节 8+4+4+4+8**

**非空对象占用内存计算**：TestNotNull的类占用空间是24字节，其中头部占用12字节，变量a是int类型，占用4字节,变量nullObject是引用，占用了4字节，最后填充了4个字节，总共是24个字节，与我们之前的预测一致。但是，因为我们实例化了NullObject,这个对象一会存在于内存中，所以我们还需要加上这个对象的内存占用16字节，那总共就是24bytes+16bytes=40bytes。我们图中最后的统计打印结果也是40字节，所以我们的分析正确。

#### 18.  JDK, JRE 和JVM的区别

https://www.cnblogs.com/xiaofeixiang/p/4085159.html

**JDK（Java Development Kit）简单理解就是Java开发工具包，JRE(Java Runtime Enviroment)是Java的运行环境，JVM( java virtual machine)也就是常常听到Java虚拟机。JDK是面向开发者的，JRE是面向使用JAVA程序的用户。**

**Java 开发工具包 (JDK)**

Java开发工具包是Java环境的核心组件，并提供编译、调试和运行一个Java程序所需的所有工具，可执行文件和二进制文件。JDK是一个平台特定的软件，有针对Windows，Mac和Unix系统的不同的安装包。可以说JDK是JRE的超集，它包含了JRE的Java编译器，调试器和核心类。目前JDK的版本号是1.7，也被称为Java 7。

**Java虚拟机(JVM)**

JVM是Java编程语言的核心。当我们运行一个程序时，JVM负责将字节码转换为特定机器代码。JVM也是平台特定的，并提供核心的Java方法，例如内存管理、垃圾回收和安全机制等。JVM 是可定制化的，我们可以通过Java 选项(java options)定制它，比如配置JVM 内存的上下界。JVM之所以被称为虚拟的是因为它提供了一个不依赖于底层操作系统和机器硬件的接口。这种独立于硬件和操作系统的特性正是Java程序可以一次编写多处执行的原因。

**Java运行时环境(JRE)**

JRE是JVM的实施实现，它提供了运行Java程序的平台。JRE包含了JVM、Java二进制文件和其它成功执行程序的类文件。JRE不包含任何像Java编译器、调试器之类的开发工具。如果你只是想要执行Java程序，你只需安装JRE即可，没有安装JDK的必要。

**JDK, JRE 和JVM的区别**

- JDK是用于开发的而JRE是用于运行Java程序的。
- JDK和JRE都包含了JVM，从而使得我们可以运行Java程序。
- JVM是Java编程语言的核心并且具有平台独立性。

**即时编译器(JIT)**

有时我们会听到JIT这个概念，并说它是JVM的一部分，这让我们很困惑。JIT是JVM的一部分，它可以在同一时间编译类似的字节码来优化将字节码转换为机器特定语言的过程相似的字节码，从而将优化字节码转换为机器特定语言的过程，这样减少转换过程所需要花费的时间。

#### 19. IO流？

主要分为**字符流**和**字节流**，字符流一般用于文本文件，字节流一般用于图像或其他文件。

字符流包括了字符输入流 Reader 和字符输出流 Writer，字节流包括了字节输入流 InputStream 和字节输出流 OutputStream。字符流和字节流都有对应的缓冲流，字节流也可以包装为字符流，缓冲流带有一个 8KB 的缓冲数组，可以提高流的读写效率。除了缓冲流外还有过滤流 FilterReader、字符数组流 CharArrayReader、字节数组流 ByteArrayInputStream、文件流 FileInputStream 等。

![ioæµå¾ç](https://img-blog.csdn.net/20170523222107234?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWXVlX0NoZW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

------

#### 20. 序列化和反序列化是什么？

Java 对象 JVM 退出时会全部销毁，如果需要将对象及状态持久化，就要通过序列化实现，将内存中的对象保存在二进制流中，需要时再将二进制流反序列化为对象。对象序列化保存的是对象的状态，因此属于类属性的静态变量不会被序列化。

常见的序列化有三种：

- **Java 原生序列化**

  实现 `Serializabale` 标记接口，Java 序列化保留了对象类的元数据（如类、成员变量、继承类信息）以及对象数据，兼容性最好，但不支持跨语言，性能一般。序列化和反序列化必须保持序列化 ID 的一致，一般使用 `private static final long serialVersionUID` 定义序列化 ID，如果不设置编译器会根据类的内部实现自动生成该值。如果是兼容升级不应该修改序列化 ID，防止出错，如果是不兼容升级则需要修改。

- **Hessian 序列化**

  Hessian 序列化是一种支持动态类型、跨语言、基于对象传输的网络协议。Java 对象序列化的二进制流可以被其它语言反序列化。Hessian 协议的特性：① 自描述序列化类型，不依赖外部描述文件，用一个字节表示常用基础类型，极大缩短二进制流。② 语言无关，支持脚本语言。③ 协议简单，比 Java 原生序列化高效。Hessian 会把复杂对象所有属性存储在一个 Map 中序列化，当父类和子类存在同名成员变量时会先序列化子类再序列化父类，因此子类值会被父类覆盖。

- **JSON 序列化**

  JSON 序列化就是将数据对象转换为 JSON 字符串，在序列化过程中抛弃了类型信息，所以反序列化时只有提供类型信息才能准确进行。相比前两种方式可读性更好，方便调试。

序列化通常会使用网络传输对象，而对象中往往有敏感数据，容易遭受攻击，Jackson 和 fastjson 等都出现过反序列化漏洞，因此不需要进行序列化的敏感属性传输时应加上 transient 关键字。transient 的作用就是把变量生命周期仅限于内存而不会写到磁盘里持久化，变量会被设为对应数据类型的零值。

#### 21 Object类方法

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200809102813199.png" alt="image-20200809102813199" style="zoom: 67%;" />

二、 方法详解

1. **registerNatives()**
   这是一个native方法，说明这个方法的实现不是在java中，而是由C/C++实现，并编译成.dll文件，由java调用。registerNatives主要是将C/C++的方法映射到java中的native方法，实现方法命名的解耦。了解即可，知道是注册，细节暂时不研究。
2. **clone方法**
   clone方法是native方法，native方法的效率远高于非native方法，因此还是使用clone方法去做对象的拷贝而不是使用new的方法，copy。**此方法被protected修饰。这就意味着想要使用，必须继承它**（废话，默认都是继承的）。然后重载它，如果想要使得其他类能使用这个类，需要设置成public。**返回值是一个Object对象**，所以要强制转换才行。
   保护方法，实现对象的浅复制，只有实现了 Cloneable 接口才可以调用该方法，否则抛出 CloneNotSupportedException 异常。
3. **getClass 方法**
   final 方法，获得运行时类的类型。
4. **toString 方法**
   返回一个 String 对象，用来标识自己。该方法用得比较多，一般子类都有覆盖。
5. **finalize 方法**
   该方法用于释放资源。因为无法确定该方法什么时候被调用，很少使用。
6. **equals 方法**
   该方法是非常重要的一个方法。一般 equals 和 == 是不一样的，但是在 Object 中两者是一样的。子类一般都要重写这个方法。
7. **hashCode 方法**
   该方法用于哈希查找，重写了 equals 方法一般都要重写 hashCode 方法。这个方法在一些具有哈希功能的 Collection 中用到。
8. **wait 方法**
   wait 方法就是使当前线程等待该对象的锁，当前线程必须是该对象的拥有者，也就是具有该对象的锁。wait() 方法一直等待，直到获得锁或者被中断。wait(long timeout) 设定一个超时间隔，如果在规定时间内没有获得锁就返回。
   调用该方法后当前线程进入睡眠状态，直到以下事件发生。
   （1）其他线程调用了该对象的 notify 方法。
   （2）其他线程调用了该对象的 notifyAll 方法。
   （3）其他线程调用了 interrupt 中断该线程。
   （4）时间间隔到了。
   此时该线程就可以被调度了，如果是被中断的话就抛出一个InterruptedException 异常。
9. **notify 方法**
   该方法唤醒在该对象上等待的某个线程。
10. **notifyAll 方法**
    该方法唤醒在该对象上等待的所有线程。

#### 22 创建对象的四种方式

1.使用**new**创建对象

　　使用new关键字创建对象应该是最常见的一种方式，但我们应该知道，使用new创建对象会增加耦合度。无论使用什么框架，都要减少new的使用以降低耦合度。

```java
package yunche.test;

/**
 * @ClassName: Hello
 * @Description: 待创建的类
 * @author: yunche
 * @date: 2018/08/24
 */
public class Hello
{
    public void sayWorld()
    {
        System.out.println("Hello world!");
    }

}
```

```java
package yunche.test;

/**
 * @ClassName: NewClass
 * @Description: 使用new关键字创建对象
 * @author: yunche
 * @date: 2018/08/24
 */
public class NewClass
{
    public static void main(String[] args)
    {
        Hello h = new Hello();
        h.sayWorld();
    }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://images2018.cnblogs.com/blog/1305509/201808/1305509-20180824160442284-1166030475.png)

2.使用反射的机制创建对象

 使用Class类的newInstance方法，Hello类的代码不变，NewClass类的代码如下：

```java
package yunche.test;

/**
 * @ClassName: NewClass
 * @Description: 使用Class类的newInstance方法
 * @author: yunche
 * @date: 2018/08/24
 */
public class NewClass
{
    public static void main(String[] args)
    {
        try
        {
           Class heroClass = Class.forName("yunche.test.Hello");
           Hello h =(Hello) heroClass.newInstance();
           h.sayWorld();
        }
        catch (ClassNotFoundException e)
        {
            e.printStackTrace();
        }
        catch (IllegalAccessException e)
        {
            e.printStackTrace();
        }
        catch (InstantiationException e)
        {
            e.printStackTrace();
        }

    }
}
```

 使用Constructor类的newInstance方法

```java
package yunche.test;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

/**
 * @ClassName: NewClass
 * @Description: 使用Constructor类的newInstance方法
 * @author: yunche
 * @date: 2018/08/24
 */
public class NewClass
{
    public static void main(String[] args)
    {
        try
        {
            //获取类对象
           Class heroClass = Class.forName("yunche.test.Hello");

           //获取构造器
           Constructor constructor = heroClass.getConstructor();
           Hello h =(Hello) constructor.newInstance();
           h.sayWorld();
        }
        catch (NoSuchMethodException e)
        {
            e.printStackTrace();
        }
        catch (InvocationTargetException e)
        {
            e.printStackTrace();
        }
        catch (IllegalAccessException e)
        {
            e.printStackTrace();
        }
        catch (InstantiationException e)
        {
            e.printStackTrace();
        }
        catch (ClassNotFoundException e)
        {
            e.printStackTrace();
        }

    }
}
```

3.采用clone

　　clone时，需要已经有一个分配了内存的源对象，创建新对象时，首先应该分配一个和源对象一样大的内存空间。要调用clone方法需要实现*Cloneable*接口，由于clone方法是protected的，所以修改Hello类。

```java
package yunche.test;

/**
 * @ClassName: Hello
 * @Description: 待创建的类
 * @author: yunche
 * @date: 2018/08/24
 */
public class Hello implements Cloneable
{
    public void sayWorld()
    {
        System.out.println("Hello world!");

    }

    public static void main(String[] args)
    {
        Hello h1 = new Hello();
        try
        {
            Hello h2 = (Hello)h1.clone();
            h2.sayWorld();
        }
        catch (CloneNotSupportedException e)
        {
            e.printStackTrace();
        }
    }
}
```

**4.采用反序列化机制**

　　使用序列化时，要实现实现Serializable接口，将一个对象序列化到磁盘上，而采用反序列化可以将磁盘上的对象信息转化到内存中。

```
package yunche.test;

import java.io.*;

/**
 * @ClassName: Serialize
 * @Description: 序列化与反序列化对象
 * @author: yunche
 * @date: 2018/08/24
 */
public class Serialize
{
    public static void main(String[] args)
    {
        Hello h = new Hello();

        //准备一个文件用于存储该对象的信息
        File f = new File("hello.obj");

        try(FileOutputStream fos = new FileOutputStream(f);
            ObjectOutputStream oos = new ObjectOutputStream(fos);
            FileInputStream fis = new FileInputStream(f);
            ObjectInputStream ois = new ObjectInputStream(fis)
            )
        {
            //序列化对象，写入到磁盘中
            oos.writeObject(h);
            //反序列化对象
            Hello newHello = (Hello)ois.readObject();

            //测试方法
            newHello.sayWorld();
        }
        catch (FileNotFoundException e)
        {
            e.printStackTrace();
        }
        catch (IOException e)
        {
            e.printStackTrace();
        }
        catch (ClassNotFoundException e)
        {
            e.printStackTrace();
        }
    }
}
```

#### 23 构造方法

构造方法是一种特殊的方法，具有以下特点。
（1）构造方法的**方法名必须与类名**相同。
（2）构造方法**没有返回类型**，也不能定义为void，在方法名前面不声明方法类型。
（3）构造方法的主要作用是完成对象的初始化工作，它能够把定义对象时的参数传给对象的域。
（4）构造方法不能由编程人员调用，而要系统调用。
（5）一个类可以定义多个构造方法，如果在定义类时没有定义构造方法，则编译系统会自动插入一个无参数的默认构 造器，这个构造器不执行任何代码。
（6）构造方法可以重载，以参数的个数，类型，或排列顺序区分。 
其实英文翻译其实为构造器，根本就不是一个方法，所以没有返回值。



#### 14  short i = 1 ； i=i+1；

short s1 = 1; s1 = s1 + 1; （s1+1运算结果是int型，需要强制转换类型）
short s1 = 1; s1 += 1;（可以正确编译）

对于short i =1;i = i+1;由于1是int类型，因此i+1运算结果也是int类型(**向上转型)**，需要强制转换类型才能赋值给short类型；而short i = 1；i+=1;可以正确编译，因为i+=1；相当于i=(short)(i+1);其中有隐含的强制类型转换。拓展：short i = 1;i++;也是正确的。需要注意的是，**整数都默认为int类型，除非你将其定义为short类型**，因此1+short类型的i还是int类型，所以会报错；而i++并没有经过i+1赋值语句，因此不会报错，而i+=1等价于i++，所以也不会报错。

#### 【克隆】

##### [1] 深克隆和浅克隆的区别？

**浅拷贝**：**浅克隆只是复制了对象的引用地址**。是将原始对象中的数据型字段拷贝到新对象中去，将引用型字段的“引用”复制到新对象中去，不把“引用的对象”复制进去，所以原始对象和新对象引用同一对象，新对象中的引用型字段发生变化会导致原始对象中的对应字段也发生变化。

**深拷贝**：**深拷贝是将对象及值复制过来，两个对象修改其中任意的值另一个值不会改变**。是在引用方面不同，深拷贝就是创建一个新的和原始字段的内容相同的字段，是两个一样大的数据段，所以两者的引用是不同的，之后的新对象中的引用型字段发生改变，不会引起原始对象中的字段发生改变。

##### [2] **如何实现对象的克隆？**

（1）实现 Cloneable 接口并重写 Object 类中的 clone() 方法；

（2）实现 Serializable 接口，通过对象的序列化和反序列化实现克隆，可以实现真正的深克隆。

##### [3] 数组的四种拷贝方式对比

https://blog.csdn.net/weixin_42220532/article/details/84200634

![image-20200628205703300](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200628205703300.png)

**对于基本数据类型来说可以理解为是深拷贝，对于引用类型来说是浅拷贝，它们拷贝的是引用，和被拷贝的引用指向同一个对象。**

[link1](https://blog.csdn.net/QQ2899349953/article/details/80143746)，[link2](https://blog.csdn.net/you_never_alone/article/details/79904947?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)

##### [4] 数组的四种拷贝方式实现

~~~Java
package 其他;

import java.util.Arrays;

public class 数组的四种拷贝方式 {
    public static void main(String[] args) {
        for_copy();
        clone_copy();
        arraycopy_copy();
        ArrayscopyOf_copy();
    }

    /**
     * for循环拷贝数组
     */
    public static void for_copy() {
        //一维数组的拷贝
        int[] array1={1,2,3,4,5,6,7};
        int[] array2=new int[array1.length];

        for(int i = 0;i < array1.length;i++){
            array2[i] = array1[i];
        }
        System.out.println(Arrays.toString(array2));

        //二维数组的拷贝
        int[][] array3= {{1,2,3},{4,5,6}};
        int[][] array4 = new int[2][3];

        for(int i = 0;i < array3.length;i++){
            for(int j = 0;j < array3[i].length;j++){
                array4[i][j] = array3[i][j];
            }
        }
        System.out.println(Arrays.deepToString(array4));
    }

    /**
     * clone拷贝数组
     */
    public static void clone_copy() {
        //一维数组的拷贝
        int[] array1={1,2,3,5,9,8,7};
        int[] array2=new int[array1.length];
        array2=array1.clone();
        System.out.println(Arrays.toString(array2));


        //二维数组的拷贝
        int[][] array3={{1,2,3,4},{5,6,7}};
        int[][] array4=new int[2][];

        for(int i = 0;i < array3.length;i++){
            array4[i] = array3[i].clone();
        }
        for(int i=0;i<array3.length;i++){
            System.out.print(Arrays.toString(array4[i]));
        }

    }

    /**
     * System.arraycopy拷贝数组
     */
    public static void arraycopy_copy() {
        //一维数组的拷贝
        int[] array = {1,2,3,4,5};
        int[] array2 = new int[array.length];
        System.arraycopy(array, 0, array2, 0, array.length);//(被复制的数组，从几号下标开始复制，复制到哪个数组，复制到新数组第几号下标，复制长度)
        System.out.println(Arrays.toString(array2));

        //二维数组的拷贝
        int[][] array1={{1,2,3,5,9},{2,3,36,5,7}};
        int[][] array3=new int[2][5];
        for(int i=0;i<array1.length;i++){
            System.arraycopy(array1[i], 0, array3[i], 0, array1[i].length);
        }
        System.out.println(Arrays.deepToString(array3));
    }

    /**
     * Arrays.copyOf拷贝数组
     */
    public static void ArrayscopyOf_copy() {
        //一维数组的拷贝
        int[] array=new int[4];
        System.out.println(Arrays.toString(array));
        int[] array1 = new int[4];
        array1 = Arrays.copyOf(array,array.length);//将数组array拷贝到数组brr,拷贝长度为array.length
        System.out.println(Arrays.toString(array1));

        //一维数组的拷贝
        int[][] array2={{1,2,3,4},{2,6,7,5}};
        int[][] array3=new int[2][4];
        array3=Arrays.copyOf(array2, array2.length);
        System.out.println(Arrays.deepToString(array3));
    }

}
~~~

#### 【static】

##### [1] static关键词的原理？

<img src="https://pics3.baidu.com/feed/024f78f0f736afc33409f1471839eec1b74512b4.jpeg?token=33db0ecbe211c671b69179720b8e41d4&amp;s=ED9CAA528ACE3EC846392E6303003066" alt="img" style="zoom: 67%;" />



我们可以一句话来概括：**方便在没有创建对象的情况下来进行调用，被他修饰的会在java虚拟机的方法区内，被static关键字修饰的不需要创建对象去调用，直接根据类名就可以去访问**。静态变量存放在方法区中，并且是被所有线程所共享的。

##### [2] Java中static关键词的作用？

（1）**静态变量**：又称为类变量，也就是说这个变量属于类的，类所有的实例都共享静态变量，可以直接通过类名来访问它。静态变量在内存中只存在一份；

（2）**静态方法**：可以直接通过类名来进行调用。静态方法在类加载的时候就存在了，它不依赖于任何实例。所以静态方法必须有实现，也就是说它不能是抽象方法。**只能访问所属类的静态字段和静态方法**(因为非静态方法是随着对象实例化才有的，调用它可能会出现错误)，**方法中不能有 this 和 super 关键字**；

> main 方法就是静态方法

（3）**静态内部类**：static关键字修饰类，普通类是不允许声明为静态的，只有内部类才可以。非静态内部类依赖于外部类的实例，而静态内部类不需要。**静态内部类不能访问外部类的非静态的变量和方法**；

（4）**静态语句块**：静态语句块在类初始化时运行一次；

> **初始化顺序**：静态变量和静态语句块优先于实例变量和普通语句块，静态变量和静态语句块的初始化顺序取决于它们在代码中的顺序。

>https://baijiahao.baidu.com/s?id=1636927461989417537&wfr=spider&for=pc
>
>https://www.cnblogs.com/w-wfy/p/7118494.html 

##### [3] 为什么静态成员和方法中不能用this和super关键字？

1. 因为this代表的是调用这个函数的对象的引用,而静态方法是属于类的,不属于对象,静态方法成功加载后,对象还不一定存在

2. super的用法跟this类似，this代表对本类对象的引用，指向本类已经创建的对象；而super代表对父类对象的引用，指向父类对象；
   2.静态优先于对象存在；

3. 因为静态优先于对象存在，所以方法被静态修饰之后方法先存在，而方法里面要用到super指向的父类对象，但是所需的父类引用对象晚于该方法出现，也就是super所指向的对象没有，当然就会出错。

#### 【异常处理】

##### [1] try和catch

https://blog.csdn.net/qq_34427165/article/details/83929470

try catch：自己处理异常

~~~java
try { 
可能出现异常的代码
} catch（异常类名A e）{ 
如果出现了异常类A类型的异常，那么执行该代码
} ...（catch可以有多个）
finally { 
最终肯定必须要执行的代码（例如释放资源的代码）
}
~~~

**代码执行的顺序：**
1.try内的代码从出现异常的那一行开始，中断执行
2.执行对应的catch块内的代码
3.继续执行try catch结构之后的代码
**注意点：**
1.如果catch内的异常类存在子父类的关系，那么子类应该在前，父类在后
2。如果最后中有返回语句，那么最后返回的结果肯定以最终中的返回值为准
3。如果最后语句中有回报，那么没有被处理的异常将会被吞掉
**重写的注意点：**
1.儿子不能比父亲的本事大
2.儿子要比父亲开放
3.儿子不能比父亲惹更大的麻烦（子类的异常的类型不能是父类的异常的父类型）

##### **[2] Error 和 Exception 的区别？**

Error 类和 Exception 类的父类都是 Throwable 类。主要区别如下：

Error 类： 一般是指与虚拟机相关的问题，如：系统崩溃、虚拟机错误、内存空间不足、方法调用栈溢出等。这类错误将会导致应用程序中断，仅靠程序本身无法恢复和预防；

Exception 类：分为运行时异常和受检查的异常。

##### **[3]  运行时异常与受检异常有何异同？**

运行时异常：如：空指针异常、指定的类找不到、数组越界、方法传递参数错误、数据类型转换错误。可以编译通过，但是一运行就停止了，程序不会自己处理；

受检查异常：要么用 try … catch… 捕获，要么用 throws 声明抛出，交给父类处理。

##### **[4] throw 和 throws 的区别？**

（1）throw：在方法体内部，表示抛出异常，由方法体内部的语句处理；throw 是具体向外抛出异常的动作，所以它抛出的是一个异常实例；

（2）throws：在方法声明后面，表示如果抛出异常，由该方法的调用者来进行异常的处理；表示出现异常的可能性，并不一定会发生这种异常。

##### **[5] 常见的异常类有哪些？**

NullPointerException：当应用程序试图访问空对象时，则抛出该异常。

SQLException：提供关于数据库访问错误或其他错误信息的异常。

IndexOutOfBoundsException：指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。

FileNotFoundException：当试图打开指定路径名表示的文件失败时，抛出此异常。

IOException：当发生某种 I/O 异常时，抛出此异常。此类是失败或中断的 I/O 操作生成的异常的通用类。

ClassCastException：当试图将对象强制转换为不是实例的子类时，抛出该异常。

IllegalArgumentException：抛出的异常表明向方法传递了一个不合法或不正确的参数。

##### [补充]

所有异常都是 Throwable 的子类，分为 **Error** 和 **Exception**。

**Error** 是 Java 运行时系统的内部错误和资源耗尽错误，例如 StackOverFlowError 和 OutOfMemoryError，这种异常程序无法处理。

**Exception** 分为受检异常和非受检异常，受检异常需要在代码中显式处理，否则会编译出错，非受检异常是运行时异常，继承自 RuntimeException。

**受检异常**：① 无能为力型，如字段超长导致的 SQLException。② 力所能及型，如未授权异常 UnAuthorizedException，程序可跳转权限申请页面。常见受检异常还有 FileNotFoundException、ClassNotFoundException、IOException等。

**非受检异常**：① 可预测异常，例如 IndexOutOfBoundsException、NullPointerException、ClassCastException 等，这类异常应该提前处理。② 需捕捉异常，例如进行 RPC 调用时的远程服务超时，这类异常客户端必须显式处理。③ 可透出异常，指框架或系统产生的且会自行处理的异常，例如 Spring 的 NoSuchRequestHandingMethodException，Spring 会自动完成异常处理，将异常自动映射到合适的状态码。

#### 【反射】

##### [1] 为什么有反射机制？

程序运行时，允许改变程序结构或变量类型，这种语言称为[动态语言](https://baike.baidu.com/item/动态语言)，像是python。JAVA的反射机制就是为了实现这种功能。

##### [2] 什么是反射机制？

 **反射机制**是指在一个类在**运行中**，对于任意一个类，都能够知道这个类的所有属性和方法，且都能够调用它的任意一个方法和属性。即**动态获取信息和动态调用对象方法的功能**称为反射机制。

##### [3] **反射如何实现的？**

每个类都有一个 **Class 对象，包含了与类有关的信息**。当编译一个新类时，会产生一个同名的 .class 文件，该文件内容保存着 Class 对象。类加载相当于 Class 对象的加载。

#####  **[4] 如何获取 Class 对象**

①  `类名.class` 。②对象的 `getClass`方法。③ `Class.forName(类的全限定名)`。

（1）通过**类名称.class**来获取Class类对象：

```java
Class c = int.class；
Class c = int[ ].class；
Class c = String.class
```

（2）通过**对象.getClass( )**方法来获取Class类对象：

```java
Class c = obj.getClass( );
```

（3）通过类名称加载类**Class.forName( )**，只要有类名称就可以得到Class：

```java
Class c = Class.forName(“cn.ywq.Demo”);
```

##### [5] 反射机制的作用

- 在运行时判断任意一个对象所属的类
- 在运行时构造一个类的对象
- 在运行时判断任意一个类所具有的成员变量和方法
- 在运行时调用任意一个对象的方法，生成动态代（dai）理

##### **[6] 反射相关的类**

**反射可以提供运行时的类信息，并且这个类可以在运行时才加载进来，甚至在编译时期该类的 .class 不存在也可以加载进来**。Class 和 java.lang.reflect 一起对反射提供了支持，java.lang.reflect 类库主要包含了以下三个类：

（1）Field ：可以使用 get() 和 set() 方法读取和修改 Field 对象关联的字段；

（2）Method ：可以使用 invoke() 方法调用与 Method 对象关联的方法；

（3）Constructor ：可以用 Constructor 创建新的对象。

##### [7] **反射的优缺点？**

**优点：**运行期类型的判断，class.forName() 动态加载类，提高代码的灵活度；

**缺点：**尽管反射非常强大，但也不能滥用。如果一个功能可以不用反射完成，那么最好就不用。在我们使用反射技术时，下面几条内容应该牢记于心。

（1）**性能开销** ：反射涉及了动态类型的解析，所以 JVM 无法对这些代码进行优化。因此，反射操作的效率要比那些非反射操作低得多。我们应该避免在经常被执行的代码或对性能要求很高的程序中使用反射。

（2）**安全限制** ：使用反射技术要求程序必须在一个没有安全限制的环境中运行。如果一个程序必须在有安全限制的环境中运行，如 Applet，那么这就是个问题了。

（3）**内部暴露**：由于反射允许代码执行一些在正常情况下不被允许的操作（比如：访问私有的属性和方法），所以使用反射可能会导致意料之外的副作用，这可能导致代码功能失调并破坏可移植性。反射代码破坏了抽象性，因此当平台发生改变的时候，代码的行为就有可能也随着变化。

  (4)  **破坏了封装性以及泛型约束**

#### 【代理】

>[link](https://gitee.com/moxi159753/LearningNotes/tree/master/%E6%A0%A1%E6%8B%9B%E9%9D%A2%E8%AF%95/%E5%9F%BA%E7%A1%80%E9%9D%A2%E8%AF%95%E9%A2%98/5_JDK%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86%E5%92%8CCGLIB%E5%8A%A8%E6%80%81%E4%BB%A3%E7%90%86)

##### [1] 什么是代理模式？

代理是一种设计模式，它的核心思想，是将对目标的访问转移到代理对象上。这样做的好处就是，目标对象在不改变代码的情况下，可以通过代理对象加一些额外的功能。这是一种编程思想，在不改变原有代码的情况下，通过代理增加一些扩展功能。

代理过程如图所示，用户访问代理对象，代理对象通过访问目标对象，来达到用户访问目标对象的目的



<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200708105330591.png" alt="image-20200708105330591" style="zoom:50%;" />

代理模式包含一下三个角色：

- **ISubject：接口对象**，该接口是对象和它的代理共用的接口。
- **TargetSubject：目标对象**，是实现抽象主题接口的类。
- **Proxy：代理角色**，内部含有对目标对象TargetSubject的引用，从而可以操作真实对象。代理对象提供与目标对象相同的接口，以便在任何时刻都能代替目标对象。同时，代理对象可以在执行目标对象操作时，附加其他的操作，相当于对真实对象进行封装。

常见的代理模式分为**静态代理**和**动态代理**，动态代理在Java中的实现分为**JDK动态代理**和**cglib代理**。

##### [2] 什么是静态代理？

[1](https://blog.csdn.net/u014589856/article/details/79551155)，[2](https://blog.csdn.net/mulinsen77/article/details/84730087)，[3](https://blog.csdn.net/jiankunking/article/details/52143504?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare[)，[**4**](https://www.jianshu.com/p/f56e123817b5)

**静态代理**：由程序员创建或工具生成代理类的源码，再编译代理类，即代理类和委托类的关系再程序运行前就已经存在。

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723220002255.png" alt="image-20200723220002255" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723215753123.png" alt="image-20200723215753123" style="zoom:67%;" />



<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723215927039.png" alt="image-20200723215927039" style="zoom: 67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723220121882.png" alt="image-20200723220121882" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723220209671.png" alt="image-20200723220209671" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723220250127.png" alt="image-20200723220250127" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723220329379.png" alt="image-20200723220329379" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723220404912.png" alt="image-20200723220404912" style="zoom:67%;" />

##### [3] 什么是动态代理？如何实现？

**动态代理**：在运行期间使用动态生成字节码形式，动态创建代理类。使用的工具有 jdkproxy、cglibproxy 等。

动态代理的实现方式是借助java.lang.Reflect.**Proxy**进行反射实现的，其步骤如下：
 a、编写一个委托类接口，对应的静态代理的Subject接口
 b、编写一个委托类接口的实现类，对应的是静态代理的RealSubject
 c、创建动态代理类方法调用处理程序，实现InvocationHandler接口，并重写invoke方法
 d、在测试类中生成动态代理对象
链接：https://www.jianshu.com/p/85d181d7d09a

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723221145721.png" alt="image-20200723221145721" style="zoom: 67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723221221631.png" alt="image-20200723221221631" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723221309631.png" alt="image-20200723221309631" style="zoom:67%;" />

##### [4] 静态代理和动态代理有什么区别？

![å¨è¿éæå¥å¾çæè¿°](https://img-blog.csdnimg.cn/20181203155827793.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L211bGluc2VuNzc=,size_16,color_FFFFFF,t_70)

动态代理的应用：Spring 的 AOP 、加事务、加权限、加日志。

##### [5] **怎么实现动态代理？**

https://cloud.tencent.com/developer/article/1009203

**Jdk动态对象**

Jdk的动态代理由**Proxy**这个类来生成，注意该方法是在Proxy类中是静态方法,且接收的三个参数依次为:

- `ClassLoader loader,`:指定当前目标对象使用**类加载器**,获取加载器的方法是固定的
- `Class<?>[] interfaces,`:目标对象实现的**接口的类型**,使用泛型方式确认类型
- `InvocationHandler h`:**事件处理,**执行目标对象的方法时,会触发事件处理器的方法,会把当前执行目标对象的方法作为参数传入

**CGLib动态代理**

CGLib采用了非常底层的字节码技术，其原理是通过字节码技术为一个类创建子类，并在子类中采用方法拦截的技术拦截所有父类方法的调用，顺势织入横切逻辑。

上面的静态代理和动态代理模式都是要求目标对象是实现一个接口的目标对象,**但是有时候目标对象只是一个单独的对象,并没有实现任何的接口,这个时候就可以使用以目标对象子类的方式类实现代理,这种方法就叫做:Cglib代理**

也叫作子类代理,它是在内存中构建一个子类对象从而实现对目标对象功能的扩展.

- JDK的动态代理有一个限制,就是使用动态代理的对象必须实现一个或多个接口,如果想代理没有实现接口的类,就可以使用Cglib实现.
- Cglib是一个强大的高性能的代码生成包,它可以在运行期扩展java类与实现java接口.它广泛的被许多AOP的框架使用,例如Spring AOP和synaop,为他们提供方法的interception(拦截)
- Cglib包的底层是通过使用一个小而块的字节码处理框架ASM来转换字节码并生成新的类.不鼓励直接使用ASM,因为它要求你必须对JVM内部结构包括class文件的格式和指令集都很熟悉.

> https://cloud.tencent.com/developer/article/1524189

**Cglib子类代理实现方法:**
1.需要引入cglib的jar文件,但是Spring的核心包中已经包括了Cglib功能,所以直接引入`pring-core-3.2.5.jar`即可.
2.引入功能包后,就可以在内存中动态构建子类
3.代理的类不能为final,否则报错
4.目标对象的方法如果为final/static,那么就不会被拦截,即不会执行目标对象额外的业务方法.

**Jdk动态对象和CGLib动态代理区别**

Jdk SDK面向的是一组接口，他为这些接口创建了一个实现类。cglib代理面对的是一个具体类，搭配创建了一个新类，继承了该类重写了该方法。

##### [6] 动态代理的应用


链接：https://www.zhihu.com/question/40536038/answer/676236311

动态代理在代码界可是有非常重要的意义，我们开发用到的许多框架都使用到了这个概念。我所知道的就有：Spring AOP、Hibernate、Struts 使用到了动态代理。

- **Spring AOP。**Spring 最重要的一个特性是 AOP（Aspect Oriented Programming 面向切面编程），利用 Spring AOP 可以快速地实现权限校验、安全校验等公用操作。而 Spring AOP 的原理则是通过动态代理实现的，**默认情况下 Spring AOP 会采用 Java 动态代理实现，而当该类没有对应接口时才会使用 CGLib 动态代理实现**。
- **Hibernate。**Hibernate 是一个常用的 ORM 层框架，在获取数据时常用的操作有：get() 和 load() 方法，它们的区别是：get() 方法会直接获取数据，而 load() 方法则会延迟加载，等到用户真的去取数据的时候才利用代理类去读数据库。
- **Struts。**Struts 现在虽然因为其太多 bug 已经被抛弃，但是曾经用过 Struts 的人都知道 Struts 中的拦截器。拦截器有非常强的 AOP 特性，仔细了解之后你会发现 Struts 拦截器其实也是用动态代理实现的。

##### [7] Spring如何实现AOP？

https://cloud.tencent.com/developer/article/1524189

1. AnnotationAwareAspectJAutoProxyCreator是AOP核心处理类
2. AnnotationAwareAspectJAutoProxyCreator实现了BeanProcessor，其中postProcessAfterInitialization是核心方法。
3. 核心实现分为2步 getAdvicesAndAdvisorsForBean获取当前bean匹配的增强器 createProxy为当前bean创建代理
4. getAdvicesAndAdvisorsForBean核心逻辑如下 a. 找所有增强器，也就是所有@Aspect注解的Bean b. 找匹配的增强器，也就是根据@Before，@After等注解上的表达式，与当前bean进行匹配，暴露匹配上的。 c. 对匹配的增强器进行扩展和排序，就是按照@Order或者PriorityOrdered的getOrder的数据值进行排序，越小的越靠前。
5. createProxy有2种创建方法，JDK代理或CGLIB a. 如果设置了proxyTargetClass=true，一定是CGLIB代理 b. 如果proxyTargetClass=false，目标对象实现了接口，走JDK代理 c. 如果没有实现接口，走CGLIB代理

##### [8] 面试

**1. 解释一下代理？**

代理是一种设计模式，**目标对象在不改变代码的情况下，可以通过代理对象加一些扩展功能，同时将目标的访问转移到代理对象上**。常见的代理模式分为**静态代理**和**动态代理**，动态代理在Java中的实现分为**JDK动态代理**和**cglib代理**。

> CGLib (Code Generation Library) 是一个强大的,高性能,高质量的Code生成类库。它可以在运行期扩展Java类与实现Java接口。Hibernate用它来实现PO字节码的动态生成。CGLib 比 Java 的 java.lang.reflect.Proxy 类更强的在于它不仅可以接管接口类的方法，还可以接管普通类的方法。

**2. 解释一下静态代理和动态代理？**

**静态代理**：需要自己写代理类，而且代理类需要实现与目标对象相同的接口

**动态代理**：不需要自己编写代理类(是动态生成的)，**JDK动态代理**需要类有接口，实现依赖于**反射**。而**cglib代理**不需要类有接口实现，以来的是底层的字节码的拦截技术。

**3.JDK SDK和cglib动态代理的区别？**

Jdk SDK面向的是一组接口，他为这些接口创建了一个实现类。cglib代理面对的是一个具体类，搭配创建了一个新类，继承了该类重写了该方法。

**4. 动态代理的应用**

Spring AOP、Hibernate、Struts 使用到了动态代理。

##### [9] 知乎的优秀总结

 https://www.zhihu.com/question/40536038/answer/658146278

# JAVA集合

#### [【HashMap问答】](https://blog.csdn.net/weixin_41796401/article/details/104321419?utm_source=app&from=groupmessage)

**[图解 Java8 HashMap 常用方法源码](https://www.jianshu.com/p/45474a025c50)**

![img](https://img-blog.csdn.net/20180620164825363?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dhbmRlcmx1c3RMZWU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![img](https://upload-images.jianshu.io/upload_images/17362740-2e95f8e7cdb91264.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

##### [1] HashMap是什么？

 HashMap是map接口下常用的集合，它具有查询快，插入删除方便的优点。

 ##### [2]  HashMap的底层是怎样的？

 HashMap的底层是在JDK1.7的时候，是**数组+链表**；在JDK1.8的时候，**底层是数组+链表+红黑树**。

##### [3]  HashMap的树化及其链表化机制及其原因？

**一、链表树化的条件是：哈希桶数组的长度大于等于64且链表中节点的个数大于等于8，不满足哈希桶数组的长度大于等于64时执行扩容操作**

1.链表长度大于8，官方源码如下：

~~~java
if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
    treeifyBin(tab, hash);
~~~

2.当满足条件1以后调用treeifyBin方法转化红黑树。该方法中，数组如果长度小于MIN_TREEIFY_CAPACITY（64）就选择扩容，而不是转化为红黑树。

~~~java
if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
    resize();
~~~

>**原因：**
>
>1. **通过复杂度分析**，我们都知道，链表取元素是从头结点一直遍历到对应的结点，这个过程的复杂度是O(N) ，而红黑树基于二叉树的结构，查找元素的复杂度为O(logN) ，通过他们的曲线也可以看出来，数据越多红黑树查询次数越低，性能也就越高。所以，当元素个数过多时，用红黑树存储可以提高搜索的效率。
>
>2. **也可以通过泊松分布**，我们应该在保证查询性能的情况下尽可能不要树化。冲突后的拉链长度和概率结果如下，可以看到第8个节点几率是滴7个节点的1/14。
>
>  0:    0.60653066
>  1:    0.30326533
>  2:    0.07581633
>  3:    0.01263606
>  4:    0.00157952
>  5:    0.00015795
>  6:    0.00001316
>  7:    0.00000094
>  8:    0.00000006
>
>**既然红黑树的效率高，那怎么不一开始就用红黑树存储呢？**
>
>这其实是基于空间和时间平衡的考虑，JDK的源码里已经对这个问题做了解释：
>
>```
>* Because TreeNodes are about twice the size of regular nodes, we
>* use them only when bins contain enough nodes to warrant use
>* (see TREEIFY_THRESHOLD). And when they become too small (due to
>* removal or resizing) they are converted back to plain bins.  
>```
>
>看注释里的前面四行就不难理解，单个 TreeNode 需要占用的空间大约是普通 Node 的两倍，所以只有当包含足够多的 Nodes 时才会转成 TreeNodes，这个足够多的标准就是由 TREEIFY_THRESHOLD 的值（默认值8）决定的。而当桶中节点数由于移除或者 resize (扩容) 变少后，红黑树会转变为普通的链表，这个阈值是 UNTREEIFY_THRESHOLD（默认值6）
>
>

**树链表化的条件是：树中节点数小于等于6。**

>**原因：**主要是一个过渡，避免链表和红黑树之间频繁的转换。如果阈值是7的话，删除一个元素红黑树就必须退化为链表，增加一个元素就必须树化，来回不断的转换结构无疑会降低性能，所以阈值才不设置的那么临界。

##### [4] HashMap的扩容机制是怎样的？

HashMap初始容量是16。

 HashMap会使用size记录当前数组的占用个数，当size大于扩容阈值threshold时，将会使用resize（）方法进行扩容操作，扩容增量是原容量的1倍（在put方法结束后就有这个函数）。

~~~java
 if (++size > threshold)//特别注意，此处的size是指键值对的个数，而不是当前哈希表的长度
            resize();   //特别注意，此处的threshold=capacity*loadFactor，阀值=桶长*负载因子
~~~

**举个例子：**初始情况下，HashMap的初始容量（capacity）16，加载因子（loadFactor）为0.75，那么当前的扩容阀值（threshold）为16*0.75=12。当前键值对的个数（size）大于扩容阀值（threshold），扩容成原容量的2倍，即从16扩容到32、64、128 ... 但是他不会无限制扩容下去，扩充阈值参数为Integer.MAX_VAULE=1 << 30;  。

##### [5] 为什么HashMap初始容量是16？

首先，length为2的整数次幂的话，h&(length-1)相当于对length取模，既保证了散列均匀，又提升了效率。

##### [6] 为什么HashMap加载因子（loadFactor）为0.75？

HashMap加载因子时真实数据和数组长度的比值。如果加载因子太小，就会造成过多的hash冲突，致使效率降低。太小，就会频繁扩容，浪费空间，降低效率。所以它不能太大也不能太小，为什么取（loadFactor）为0.75？与离散数学中的泊松分布有关。

>* 加载因子过高，例如为1，虽然减少了空间开销，提高了空间利用率，hash冲突太多。但同时也增加了查询时间成本；
>
>* 加载因子过低，例如0.5，虽然可以减少查询时间成本，但是空间利用率很低，同时提高了rehash操作的次数。在设置初始容量时应该考虑到映射中所需的条目数及其加载因子，以便最大限度地减少rehash操作次数，所以，一般在使用HashMap时建议根据预估值设置初始容量，减少扩容操作。

**什么是泊松分布**？

泊松分布是统计学和概率学常见的离散概率分布，适用于**描述单位时间内随机事件发生的次数的概率分布**。

<img src="https://img-blog.csdnimg.cn/20200411155246722.png#pic_center" alt="å¨è¿éæå¥å¾çæè¿°" style="zoom: 50%;" />

等号的左边，P 表示概率，N表示某种函数关系，t 表示时间，n 表示数量。等号的右边，λ 表示事件的频率。

在理想情况下，使用随机哈希码，**在扩容阈值（加载因子）为0.75的情况下，节点出现在频率在Hash桶（表）中遵循参数平均为0.5的泊松分布**。忽略方差，即X = λt，P(λt = k)，其中λt = 0.5的情况，按公式：

<img src="https://img-blog.csdnimg.cn/20200411155231550.png#pic_center" alt="å¨è¿éæå¥å¾çæè¿°" style="zoom:50%;" />

计算结果如上述的列表所示，当一个bin中的链表长度达到8个元素的时候，概率为0.00000006，几乎是一个不可能事件。所以我们可以知道，其实常数0.5是作为参数代入泊松分布来计算的，而加载因子0.75是作为一个条件，当HashMap长度为length/size ≥ 0.75时就扩容，在这个条件下，冲突后的拉链长度和概率结果为：

0:    0.60653066
1:    0.30326533
2:    0.07581633
3:    0.01263606
4:    0.00157952
5:    0.00015795
6:    0.00001316
7:    0.00000094
8:    0.00000006
从上面的表中可以看到当桶中元素到达8个的时候，概率已经变得非常小，也就是说用0.75作为加载因子，每个碰撞位置的链表长度超过８个是几乎不可能的。

**那么为什么不可以是0.8或者0.6呢？**
HashMap中除了哈希算法之外，有两个参数影响了性能：初始容量和加载因子。初始容量是哈希表在创建时的容量，加载因子是哈希表在其容量自动扩容之前可以达到多满的一种度量。

**在维基百科来描述加载因子：**对于开放定址法，加载因子是特别重要因素，应严格限制在0.7-0.8以下。超过0.8，查表时的CPU缓存不命中（cache missing）按照指数曲线上升。因此，一些采用开放定址法的hash库，如Java的系统库限制了加载因子为0.75，超过此值将resize散列表。

在设置初始容量时应该考虑到映射中所需的条目数及其加载因子，以便最大限度地减少扩容rehash操作次数，所以，一般在使用HashMap时建议根据预估值设置初始容量，以便减少扩容操作。

**选择0.75作为默认的加载因子，完全是时间和空间成本上寻求的一种折衷选择。**

##### [7] 为什么桶数组的长度是2^n

因为在计算元素该存放的位置的时候，用到的算法是将元素的hashcode与当前map长度-1进行与运算**(i=（n-1）&hash)**。如果map长度为2的幂次，那n-1的二进制一定为11111...的形式。这可以保证每一位参与有有意义的与运算，即可以把结果i控制在0~n-1之间。**能够充分利用数组，有效减少哈希冲突**。

 ##### [8] HashMap线程安全吗？为什么？[link](https://www.zhihu.com/question/28516433)，[link](https://blog.csdn.net/swpu_ocean/article/details/88917958?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-3)

https://blog.csdn.net/swpu_ocean/article/details/88917958

https://blog.csdn.net/swpu_ocean/article/details/88917958

`HashMap`的线程不安全主要体现在下面两个方面：

1. **在JDK1.7中，当并发执行扩容操作时会造成死链和数据丢失的情况。**

**在扩容时产生死链：**。`HashMap`的线程不安全主要是发生在扩容函数中，即根源是在**transfer函数**。`HashMap`的扩容操作，重新定位每个桶的下标，并采用头插法将元素迁移到新数组中。头插法会将链表的顺序翻转，这也是形成死循环的关键点。假设两个线程同时进行resize, A->B 第一线程在处理过程中比较慢，第二个线程已经完成了倒序完成了B-A 那么就出现了循环，B->A->B.

**在扩容时数据丢失：**当多个线程同时进来，检测到总数量超过门限值的时候就会同时调用 resize 操作，各自生成新的数组并 rehash 后赋给该 map 底层的数组，结果最终只有最后一个线程生成的新数组被赋给该 map 底层，其他线程的均会丢失。

2. **在JDK1.8中，在并发执行put操作时会发生数据覆盖的情况。**

**数据覆盖导致的数据丢失**：在JDK1.7中，hashmap的链表采用了尾插法。如果有两个线程A和B，都进行插入数据，刚好这两条不同的数据经过哈希计算后得到的哈希码是一样的，且该位置还没有其他的数据。假设一种情况，线程A通过if判断，该位置没有哈希冲突，进入了if语句，还没有进行数据插入，这时候CPU就把资源让给了线程B，线程A停在了if语句里面，线程B判断该位置没有哈希冲突（线程A的数据还没插入），也进入了if语句，线程B执行完后，轮到线程A执行，现在线程A直接在该位置插入而不用再判断。这时候，你会发现线程A把线程B插入的数据给覆盖了。发生了线程不安全情况。本来在HashMap中，发生哈希冲突是可以用链表法或者红黑树来解决的，但是在多线程中，可能就直接给覆盖了。

##### [9]  关于HashMap的key值的数据类型不能为基础类型的原因？

HashMap是利用HashCode()来区别两个不同的对象。而HashCode()是本地方法，是用C或C++来实现的，即该方法是直接返回对象的内存地址。

~~~java
 final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
        if (oldCap > 0) {
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
~~~

##### [10] 其他总结

**HashMap 有什么特点？**

JDK8 之前底层实现是数组 + 链表，JDK8 改为数组 + 链表/红黑树，节点类型从Entry 变更为 Node。主要成员变量包括存储数据的 table 数组、元素数量 size、加载因子 loadFactor。

table 数组记录 HashMap 的数据，每个下标对应一条链表，所有哈希冲突的数据都会被存放到同一条链表，Node/Entry 节点包含四个成员变量：key、value、next 指针和 hash 值。

HashMap 中数据以键值对的形式存在，键对应的 hash 值用来计算数组下标，如果两个元素 key 的 hash 值一样，就会发生哈希冲突，被放到同一个链表上，为使查询效率尽可能高，键的 hash 值要尽可能分散。

HashMap 默认初始化容量为 16，扩容容量必须是 2 的幂次方、最大容量为 1<< 30 、默认加载因子为 0.75。

------

**HashMap 相关方法的源码**

**JDK8 之前**

**hash：计算元素 key 的散列值**

① 处理 String 类型时，调用 `stringHash32` 方法获取 hash 值。

② 处理其他类型数据时，提供一个相对于 HashMap 实例唯一不变的随机值 hashSeed 作为计算初始量。

③ 执行异或和无符号右移使 hash 值更加离散，减小哈希冲突概率。

**indexFor：计算元素下标**

将 hash 值和数组长度-1 进行与操作，保证结果不会超过 table 数组范围。

**get：获取元素的 value 值**

① 如果 key 为 null，调用 `getForNullKey` 方法，如果 size 为 0 表示链表为空，返回 null。如果 size 不为 0 说明存在链表，遍历 table[0] 链表，如果找到了 key 为 null 的节点则返回其 value，否则返回 null。

② 如果 key 为 不为 null，调用 `getEntry` 方法，如果 size 为 0 表示链表为空，返回 null 值。如果 size 不为 0，首先计算 key 的 hash 值，然后遍历该链表的所有节点，如果节点的 key 和 hash 值都和要查找的元素相同则返回其 Entry 节点。

③ 如果找到了对应的 Entry 节点，调用 `getValue` 方法获取其 value 并返回，否则返回 null。

**put：添加元素**

① 如果 key 为 null，直接存入 table[0]。

② 如果 key 不为 null，计算 key 的 hash 值。

③ 调用 `indexFor` 计算元素存放的下标 i。

④ 遍历 table[i] 对应的链表，如果 key 已存在，就更新 value 然后返回旧 value。

⑤ 如果 key 不存在，将 modCount 值加 1，使用 `addEntry` 方法增加一个节点并返回 null。

**resize：扩容数组**

① 如果当前容量达到了最大容量，将阈值设置为 Integer 最大值，之后扩容不再触发。

② 否则计算新的容量，将阈值设为 `newCapacity x loadFactor` 和 `最大容量 + 1` 的较小值。

③ 创建一个容量为 newCapacity 的 Entry 数组，调用 `transfer` 方法将旧数组的元素转移到新数组。

**transfer：转移元素**

① 遍历旧数组的所有元素，调用 `rehash` 方法判断是否需要哈希重构，如果需要就重新计算元素 key 的 hash 值。

② 调用 `indexFor` 方法计算元素存放的下标 i，利用头插法将旧数组的元素转移到新数组。

**JDK8**

**hash：计算元素 key 的散列值**

如果 key 为 null 返回 0，否则就将 key 的 `hashCode` 方法返回值高低16位异或，让尽可能多的位参与运算，让结果的 0 和 1 分布更加均匀，降低哈希冲突概率。

**put：添加元素**

① 调用 `putVal` 方法添加元素。

② 如果 table 为空或长度为 0 就进行扩容，否则计算元素下标位置，不存在就调用 `newNode` 创建一个节点（node节点内存储的属性有hash，key，value，next）。

③ 如果存在且是链表，如果首节点和待插入元素的 hash 和 key 都一样，更新节点的 value。

④ 如果首节点是 TreeNode 类型，调用 `putTreeVal` 方法增加一个树节点，每一次都比较插入节点和当前节点的大小，待插入节点小就往左子树查找，否则往右子树查找，找到空位后执行两个方法：`balanceInsert` 方法，插入节点并调整平衡、`moveRootToFront` 方法，由于调整平衡后根节点可能变化，需要重置根节点。

⑤ 如果都不满足，遍历链表，根据 hash 和 key 判断是否重复，决定更新 value 还是新增节点。如果遍历到了链表末尾则添加节点，如果达到建树阈值 7，还需要调用 `treeifyBin` 把链表重构为红黑树。

⑥ 存放元素后将 modCount 加 1，如果 `++size > threshold` ，调用 `resize` 扩容。

**get ：获取元素的 value 值**

① 调用 `getNode` 方法获取 Node 节点，如果不是 null 就返回其 value 值，否则返回 null。

② `getNode` 方法中如果数组不为空且存在元素，先比较第一个节点和要查找元素的 hash 和 key ，如果都相同则直接返回。

③ 如果第二个节点是 TreeNode 类型则调用 `getTreeNode` 方法进行查找，否则遍历链表根据 hash 和 key 查找，如果没有找到就返回 null。

**resize：扩容数组**

重新规划长度和阈值，如果长度发生了变化，部分数据节点也要重新排列。

**重新规划长度**

① 如果当前容量 `oldCap > 0` 且达到最大容量，将阈值设为 Integer 最大值，return 终止扩容。

② 如果未达到最大容量，当 `oldCap << 1` 不超过最大容量就扩大为 2 倍。

③ 如果都不满足且当前扩容阈值 `oldThr > 0`，使用当前扩容阈值作为新容量。

④ 否则将新容量置为默认初始容量 16，新扩容阈值置为 12。

**重新排列数据节点**

① 如果节点为 null 不进行处理。

② 如果节点不为 null 且没有next节点，那么通过节点的 hash 值和 `新容量-1` 进行与运算计算下标存入新的 table 数组。

③ 如果节点为 TreeNode 类型，调用 `split` 方法处理，如果节点数 hc 达到6 会调用 `untreeify` 方法转回链表。

④ 如果是链表节点，需要将链表拆分为 hash 值超出旧容量的链表和未超出容量的链表。对于`hash & oldCap == 0` 的部分不需要做处理，否则需要放到新的下标位置上，新下标 = 旧下标 + 旧容量。

------

**Q3：HashMap 为什么线程不安全？**

JDK7 存在死循环和数据丢失问题。

**数据丢失：**

- **并发赋值被覆盖：** 在 `createEntry` 方法中，新添加的元素直接放在头部，使元素之后可以被更快访问，但如果两个线程同时执行到此处，会导致其中一个线程的赋值被覆盖。
- **已遍历区间新增元素丢失：** 当某个线程在 `transfer` 方法迁移时，其他线程新增的元素可能落在已遍历过的哈希槽上。遍历完成后，table 数组引用指向了 newTable，新增元素丢失。
- **新表被覆盖：** 如果 `resize` 完成，执行了 `table = newTable`，则后续元素就可以在新表上进行插入。但如果多线程同时 `resize` ，每个线程都会 new 一个数组，这是线程内的局部对象，线程之间不可见。迁移完成后`resize` 的线程会赋值给 table 线程共享变量，可能会覆盖其他线程的操作，在新表中插入的对象都会被丢弃。

**死循环：** 扩容时 `resize` 调用 `transfer` 使用头插法迁移元素，虽然 newTable 是局部变量，但原先 table 中的 Entry 链表是共享的，问题根源是 Entry 的 next 指针并发修改，某线程还没有将 table 设为 newTable 时用完了 CPU 时间片，导致数据丢失或死循环。

JDK8 在 `resize` 方法中完成扩容，并改用尾插法，不会产生死循环，但并发下仍可能丢失数据。可用 ConcurrentHashMap 或 `Collections.synchronizedMap` 包装成同步集合。

#### 【String】

##### [1] String为什么设计成final的？

String 类和其存储数据的成员变量 value 字节数组都是 final 修饰的，final 修饰类则此类不可被继承，修饰数组则数组不可变。这是为了保证它的线程安全。

##### [2] String 是不可变类为什么值可以修改？

对一个 String 对象的任何修改实际上都是创建一个新 String 对象，再引用该对象。只是修改 String 变量引用的对象，没有修改原 String 对象的内容。

##### [3] 字符串拼接的方式有哪些？

1. 直接用 `+` ，底层用 StringBuilder 实现。只适用小数量，如果在循环中使用 `+` 拼接，相当于不断创建新的 StringBuilder 对象再转换成 String 对象，效率极差。

2. 使用 String 的 concat 方法，该方法中使用 `Arrays.copyOf` 创建一个新的字符数组 buf 并将当前字符串 value 数组的值拷贝到 buf 中，buf 长度 = 当前字符串长度 + 拼接字符串长度。之后调用 `getChars` 方法使用 `System.arraycopy` 将拼接字符串的值也拷贝到 buf 数组，最后用 buf 作为构造参数 new 一个新的 String 对象返回。效率稍高于直接使用 `+`。

3. 使用 StringBuilder 或 StringBuffer，两者的 `append` 方法都继承自 AbstractStringBuilder，该方法首先使用 `Arrays.copyOf`  确定新的字符数组容量，再调用 `getChars` 方法使用 `System.arraycopy` 将新的值追加到数组中。StringBuilder 是 JDK5 引入的，效率高但线程不安全。StringBuffer 使用 synchronized 保证线程安全。

##### [4] String a = "a" + new String("b")  创建了几个对象？

常量和常量拼接仍是常量，结果在常量池，只要有变量参与拼接结果就是**变量**，存在堆。

使用字面量时只创建一个常量池中的常量，使用 new 时如果常量池中没有该值就会在常量池中新创建，再在堆中创建一个对象引用常量池中常量。因此 `String a = "a" + new String("b")` 会创建四个对象，常量池中的 a 和 b，堆中的 b 和堆中的 ab。

##### [5] String、StringBuilder、StringBuffer的区别？

**String**：不可变，故线程不安全

**StringBuilder**：可变，线程不安全

**StringBuffer**：可变，内部使用 **synchronized** 进行同步，线程安全

##### [5] String a="ab" 与String a = new String("ab");

new String新建的对象是保存在堆中的，但对中的对象的value还是指向常量池的。而String str = “hello”就是直接指向常量池

**这两个值，A,B 是否相等，如果都往HashSet里面放，能放下吗？**

(a)A==B 的判断为false; (b)A.equals(B)为true ；因为值相等，所以都往HashSet里面放不下，只能放一个

>String A = "ABC";内存会去查找永久代(常量池) ，如果没有的话，在永久代中中开辟一块儿内存空间，把地址付给栈指针，如果已经有了"ABC"的内存，直接把地址赋给栈指针； 因此 
>String str1="aa";
>Srting str2="aa";
>String Str3="aa";
>....
>这样下去，str1==Str2==str3;会一直相等下去，(a) ==的判断， (b) equals()的判断；都相等，因为他们的地址都相等，因此只在常量池中有一份内存空间，地址全部相同； 
>而String str = new String("a");是根据"a"这个String对象再次构造一个String对象;在堆中从新new一块儿内存，把指针赋给栈， 将新构造出来的String对象的引用赋给str。 因此 只要是new String()，则，栈中的地址都是指向最新的new出来的堆中的地址

#### 1. 集合常用的有哪几种？

![å¨è¿éæå¥å¾çæè¿°](https://img-blog.csdnimg.cn/20200324100421645.png#pic_center)

>从map，list，set三大接口下分类别回答

* map接口下的：

1. HashMap(首先想起最常用的hashmap，**无序**，**线程不安全**，底层是**数组加链表加红黑树**)，
2. HashTable(然后想起**线程安全**的hashtable)，
3. HashTree(然后想起**有序**的hashtree，底层是**红黑树**)，
4. LinkedHashMap(然后想起**有序**的hashtree，底层是**红黑树**)，
5. ConcurrentHashMap(然后想起**有序**的hashtree，底层是**双向链表加数组加链表加红黑树**，线程安全)

>ConcurrentHashMap结合了HashMap和Hashtable二者的优势

* List接口下的：

1. ArrayList(底层为**数组**的arraylist，线程不安全)，
 2. LinkedList(底层为**链表**的的LinkedList，线程不安全)，
 3. Stack（常用的栈，继承自Vector，底层是通过**数组**实现的，线程安全）
 4. Vector（底层是通过**数组**实现的，线程安全）

  * Set接口下的：

    1. HashSet(HashSet底层使用了**Hash表**实现)，
    2. TreeSet(TreeSet底层使用了**红黑树**来实现)，
     3. LinkedHashSet( LinkedHashSet是具有可预知迭代顺序的Set接口的**哈希表**和**链接列表**实现)

   #### 2. 集合里哪些是线程安全的？

 **vector（syn锁）**， **stack（syn锁）**， **hashtable（syn锁）**，**ConcurrentHashMap（segment分段锁或者细粒度锁）**。

   #### 3. list，set有什么区别？

   　最主要的区别，**list包含重复元素，set不包含重复元素**。

#### 4 HashMap， HashTable有什么区别？

1. **跟HashMap相比Hashtable是线程安全的，适合在多线程的情况下使用，但是他在对数据操作的时候都会上synchronzied锁，所以效率比较低下。**

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200718091749716.png" alt="image-20200718091749716" style="zoom: 50%;" />

2. **Hashtable 是不允许键或值为 null 的，HashMap 的键值则都可以为 null。**这是因为Hashtable使用的是**安全失败机制（fail-safe）**，这种机制会使你此次读到的数据不一定是最新的数据。如果你使用null值，就会使得其无法判断对应的key是不存在还是为空，因为你无法再调用一次contain(key）来对key是否存在进行判断，ConcurrentHashMap同理。
3. **实现方式不同**：Hashtable 继承了 Dictionary类，而 HashMap 继承的是 AbstractMap 类。Dictionary 是 JDK 1.0 添加的，貌似没人用过这个，我也没用过。
4. **初始化容量不同**：HashMap 的初始容量为：16，Hashtable 初始容量为：11，两者的负载因子默认都是：0.75。
5. **扩容机制不同**：当现有容量大于总容量负载因子时，HashMap 扩容规则为当前容量翻倍，Hashtable 扩容规则为当前容量翻倍 + 1。
6. **迭代器不同**：HashMap 中的 Iterator 迭代器是 fail-fast 的，而 Hashtable 的 Enumerator 不是 fail-fast 的。
   所以，当其他线程改变了HashMap 的结构，如：增加、删除元素，将会抛出ConcurrentModificationException 异常，而 Hashtable 则不会。

> **fail-fast是啥？**
>
> **快速失败（fail—fast）**是java集合中的一种机制， 在用迭代器遍历一个集合对象时，如果遍历过程中对集合对象的内容进行了修改（增加、删除、修改），则会抛出Concurrent Modification Exception。
>
> **他的原理是啥？**
>
> 迭代器在遍历时直接访问集合中的内容，并且在遍历过程中使用一个 modCount 变量。集合在被遍历期间如果内容发生变化，就会改变modCount的值。每当迭代器使用hashNext()/next()遍历下一个元素之前，都会检测modCount变量是否为expectedmodCount值，是的话就返回遍历；否则抛出异常，终止遍历。
>
> **Tip**：这里异常的抛出条件是检测到 modCount！=expectedmodCount 这个条件。如果集合发生变化时修改modCount值刚好又设置为了expectedmodCount值，则异常不会抛出。
>
> 因此，不能依赖于这个异常是否抛出而进行并发操作的编程，这个异常只建议用于检测并发修改的bug。
>
> **说说他的场景？**
>
> java.util包下的集合类都是快速失败的，不能在多线程下发生并发修改（迭代过程中被修改）算是一种安全机制吧。

#### 5. ArrayList，LinkedList有什么区别？

ArrayList底层是数组，方便查找，不方便增加删除元素。LinkedList底层是链表，方便增删，但是查找不方便。

>从名字可以推想出底层
>从底层可以推想出其特点

**Q1: 说一说 ArrayList**

**ArrayList** 是容量可变的非线程安全列表，使用数组实现，集合扩容时会创建更大的数组，把原有数组复制到新数组。支持对元素的快速随机访问，但插入与删除速度很慢。ArrayList 实现了 RandomAcess 标记接口，如果一个类实现了该接口，那么表示使用索引遍历比迭代器更快。

**elementData**是 ArrayList 的数据域，被 transient 修饰，序列化时会调用 writeObject 写入流，反序列化时调用 readObject 重新赋值到新对象的 elementData。原因是 elementData 容量通常大于实际存储元素的数量，所以只需发送真正有实际值的数组元素。

**size** 是当前实际大小，elementData 大小大于等于 size。

**modCount **记录了 ArrayList 结构性变化的次数，继承自 AbstractList。所有涉及结构变化的方法都会增加该值。**expectedModCount** 是迭代器初始化时记录的 modCount 值，每次访问新元素时都会检查 modCount 和 expectedModCount 是否相等，不相等就会抛出异常。这种机制叫做 fail-fast，所有集合类都有这种机制。

------

**Q2：说一说 LinkedList**

**LinkedList** 本质是双向链表，与 ArrayList 相比插入和删除速度更快，但随机访问元素很慢。除继承 AbstractList 外还实现了 Deque 接口，这个接口**具有队列和栈**的性质。成员变量被 transient 修饰，原理和 ArrayList 类似。

LinkedList 包含三个重要的成员：size、first 和 last。size 是双向链表中节点的个数，first 和 last 分别指向首尾节点的引用。

LinkedList 的优点在于可以将零散的内存单元通过附加引用的方式关联起来，形成按链路顺序查找的线性结构，内存利用率较高。

#### 6. HashSet，TreeSet是怎么保证元素唯一性的？

* HashSet利用的是hashmap中的key不能唯一的原则。通过判断元素的**hashCode值是否相同**。如果相同，还会继续判断元素的equals方法，是否为true。
* TreeSet底层保证元素唯一性是**通过Comparable或者Comparator接口**实现。

#### 7. HashSet底层原理？

**1. add(Object obj)方法**：用于向Set集合中添加元素，添加成功返回true，否则返回false。

~~~java
    public boolean add(E e) {
        //map中put方法，如果添加成功返回null，添加失败返回oldValue（旧值）。
        return map.put(e, PRESENT)==null;
    }
~~~

**在add方法中，实际上是HashMap对象在调用put方法，而在put方法中其实把我们在add方法中传入的元素赋给了HashMap对象中的key，而对于HashMap对象key不能重复，因此add方法无法添加重复的对象**。

~~~java
public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }    
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }
~~~

**2. iterator()**：返回在此Set中的元素上进行迭代的迭代器。

~~~java
    public Iterator<E> iterator() {
        return map.keySet().iterator();
    }
~~~

**3. hashset为什么没有put方法**

因为它不能重复，你不能保证你不会存入相同的数据，那么当放入两个相同的数据时，顺序就乱了，所以无法通过下标索引，如果你想判断内部是否有元素时，可以用contains方法。

~~~java
    public boolean contains(Object o) {
        return map.containsKey(o);
    }
~~~

#### 7. TreeMap底层原理？

　1.TreeMap实现了**SortedMap接口**，保证了**有序性**。默认的排序是根据key值进行升序排序，也可以重写**comparator方法来根据value进行排序**具体取决于使用的构造方法。不允许有null值null键。TreeMap是线程不安全的。

　2. TreeMap基于**红黑树**（Red-Black tree）实现。TreeMap的基本操作 containsKey、get、put 和 remove 的时间复杂度是 log(n) 。

~~~java
    public void putAll(Map<? extends K, ? extends V> map) {
        int mapSize = map.size();
        if (size==0 && mapSize!=0 && map instanceof SortedMap) {
            Comparator<?> c = ((SortedMap<?,?>)map).comparator();
            if (c == comparator || (c != null && c.equals(comparator))) {
                ++modCount;
                try {
                    buildFromSorted(mapSize, map.entrySet().iterator(),
                                    null, null);
                } catch (java.io.IOException cannotHappen) {
                } catch (ClassNotFoundException cannotHappen) {
                }
                return;
            }
        }
        super.putAll(map);
    }
~~~

#### 8. LinkedHashMap 底层原理？

> https://www.cnblogs.com/xiaowangbangzhu/p/10445574.html

针对LinkedHashMap 的总结有一下几点

　　1.LinkedHashMap 继承自 HashMap，所以它的底层仍然是基于拉链式散列结构。该结构由**数组和链表+红黑树** 在此基础上LinkedHashMap 增加了一条**双向链表**，保持遍历顺序和插入顺序一致的问题。

　　2. 在实现上，LinkedHashMap 很多方法直接继承自 HashMap（比如put remove方法就是直接用的父类的），仅为维护双向链表覆写了部分方法（get（）方法是重写的）。

　　3.LinkedHashMap使用的键值对节点是Entity 他继承了hashMap 的Node,并新增了两个引用，分别是 before 和 after。这两个引用的用途不难理解，也就是用于维护双向链表.

　　4.链表的建立过程是在插入键值对节点时开始的，初始情况下，让 LinkedHashMap 的 head 和 tail 引用同时指向新节点，链表就算建立起来了。随后不断有新节点插入，通过将新节点接在 tail 引用指向节点的后面，即可实现链表的更新

　　5.LinkedHashMap **允许使用null值和null键，** 线程是不安全的，虽然底层使用了双线链表，但是增删相快了。因为他底层的Entity 保留了hashMap node 的next 属性。

　　6.如何实现迭代有序？

　　重新定义了数组中保存的元素Entry（继承于HashMap.node)，该Entry除了保存当前对象的引用外，还保存了其上一个元素before和下一个元素after的引用，从而在哈希表的基础上又构成了双向链接列表。仍然保留next属性，所以既可像HashMap一样快速查找，

　　用next获取该链表下一个Entry，也可以通过双向链接，通过after完成所有数据的有序迭代.

　　7.竟然inkHashMap 的put 方法是直接调用父类hashMap的，但在 HashMap 中，put 方法插入的是 HashMap 内部类 Node 类型的节点，该类型的节点并不具备与 LinkedHashMap 内部类 Entry 及其子类型节点组成链表的能力。那么，LinkedHashMap 是怎样建立链表的呢？

　　　*虽然linkHashMap* 调用的是hashMap中的put 方法，但是linkHashMap 重写了，了一部分方法，其中就有 

~~~java
newNode(int hash, K key, V value, Node<K,V> e)
linkNodeLast(LinkedHashMap.Entry<K,V> p)
~~~

　　　这两个方法就是 第一个方法就是新建一个 linkHasnMap 的Entity 方法，而 linkNodeLast 方法就是为了把Entity 接在链表的尾部。

　　8.链表节点的删除过程

　　　与插入操作一样，LinkedHashMap 删除操作相关的代码也是直接用父类的实现，但是LinkHashMap 重写了`removeNode()方法 afterNodeRemoval（）方法，该removeNode方法在hashMap 删除的基础上有调用了afterNodeRemoval 回调方法。完成删除。`

　　删除的过程并不复杂，上面这么多代码其实就做了三件事：

1. 根据 hash 定位到桶位置
2. 遍历链表或调用红黑树相关的删除方法
3. 从 LinkedHashMap 维护的双链表中移除要删除的节点

#### 9.[ArrayList 扩容原理](https://www.cnblogs.com/SunArmy/p/9844022.html)

> https://blog.csdn.net/u010890358/article/details/80515284

```java
newCapacity = oldCapacity + (oldCapacity >> 1);
//Arrays.copyOf底层调用system.arraycopy，返回一个新数组
elementData = Arrays.copyOf(elementData, newCapacity);
```

ArrayList扩容的核心方法grow()，下面将针对三种情况对该方法进行解析：

1. 当前数组是由默认构造方法生成的空数组并且第一次添加数据。此时minCapacity等于默认的容量（10）那么根据下面逻辑可以看到最后数组的容量会从0扩容成10。而后的数组扩容才是按照当前容量的1.5倍进行扩容；
2. 当前数组是由自定义初始容量构造方法创建并且指定初始容量为0。此时minCapacity等于1那么根据下面逻辑可以看到最后数组的容量会从0变成1。这边可以看到一个严重的问题，一旦我们执行了初始容量为0，那么根据下面的算法前四次扩容每次都 +1，在第5次添加数据进行扩容的时候才是按照当前容量的1.5倍进行扩容。
3. 当扩容量（newCapacity）大于ArrayList数组定义的最大值后会调用hugeCapacity来进行判断。如果minCapacity已经大于Integer的最大值（溢出为负数）那么抛出OutOfMemoryError（内存溢出）否则的话根据与MAX_ARRAY_SIZE的比较情况确定是返回Integer最大值还是MAX_ARRAY_SIZE。这边也可以看到ArrayList允许的最大容量就是Integer的最大值（-2的31次方~2的31次方减1）。

# JAVA并发编程

#### 1. 多线程环境下的线程安全体现在哪些方面？

答：多线程环境下的线程安全主要体现在原子性，可见性与有序性方面。

1. **原子性**是一组操作要么完全发生，要么没有发生，其余线程不会看到中间过程的存在。

   > 对于涉及到共享变量访问的操作，若该操作从执行线程以外的任意线程来看是不可分割的，那么该操作就是原子操作，该操作具有原子性。即，其它线程不会“看到”该操作执行了部分的中间结果。
   >
   > **举例：**银行转账流程中，A账户减少了100元，那么B账户就会多100元，这两个动作是一个原子操作。我们不会看到A减少了100元，但是B余额保持不变的中间结果。
   >
   > **Java原子性的实现方式：**
   >
   > - 利用**锁的排他性**，保证同一时刻只有一个线程在操作一个共享变量
   > - 利用**CAS（Compare And Swap）**保证
   > - Java**语言规范中**，保证了除long和double型以外的任何变量的写操作都是原子操作
   >
   > ##### 关于原子性，你应该注意的地方：
   >
   > - 原子性针对的是多个线程的共享变量，所以对于局部变量来说不存在共享问题，也就无所谓是否是原子操作
   > - 单线程环境下讨论是否是原子操作没有意义
   > - volatile关键字仅仅能保证变量写操作的原子性，不保证复合操作，比如说读写操作的原子性

2. **可见性**是指一个线程对共享变量的更新对于另外一个线程是否可见的问题。

   >**定义：**可见性是指一个线程对于共享变量的更新，对于后续访问该变量的线程是否可见的问题。
   >
   >为了阐述可见性问题，我们先来简单介绍**处理器缓存**的概念。
   >
   >现代处理器处理速度远大于主内存的处理速度，所以在主内存和处理器之间加入了寄存器，高速缓存，写缓冲器以及无效化队列等部件来加速内存的读写操作。也就是说，我们的处理器可以和这些部件进行读写操作的交互，这些部件可以称为处理器缓存。
   >
   >处理器对内存的读写操作，其实仅仅是与处理器缓存进行了交互。一个处理器的缓存上的内容无法被另外一个处理器读取，所以另外一个处理器必须通过缓存一致性协议来读取的其他处理器缓存中的数据，并且同步到自己的处理器缓存中，这样保证了其余处理器对该变量的更新对于另外处理器是可见的。
   >
   >**在单处理器中，为什么也会出现可见性的问题呢？**
   >
   >单处理器中，由于是多线程并发编程，所以会存在线程的上下文切换，线程会将对变量的更新当作上下文存储起来，导致其余线程无法看到该变量的更新。所以单处理器下的多线程并发编程也会出现可见性问题的。
   >
   ><img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200518151721340.png" alt="image-20200518151721340" style="zoom:50%;" />
   >
   >

3. **有序性**是指一个线程对共享变量的更新在其余线程看起来是按照什么顺序执行的问题。

   >**定义：**有序性是指一个处理器上运行的线程所执行的内存访问操作在另外一个处理器上运行的线程来看是否有序的问题。
   >
   >**重排序：**
   >为了提高程序执行的性能，Java编译器在其认为不影响程序正确性的前提下，可能会对源代码顺序进行一定的调整，导致程序运行顺序与源代码顺序不一致。
   >
   >重排序是对内存读写操作的一种优化，在单线程环境下不会导致程序的正确性问题，但是多线程环境下可能会影响程序的正确性。
   >
   >**重排序举例：**
   >**Instance instance = new Instance()都发生了啥？**
   >**具体步骤如下所示三步：**
   >
   >- 在堆内存上分配对象的内存空间
   >- 在堆内存上初始化对象
   >- 设置instance指向刚分配的内存地址
   >
   >第二步和第三步可能会发生重排序，导致引用型变量指向了一个不为null但是也不完整的对象。（**在多线程下的单例模式中，我们必须通过volatile来禁止指令重排序**）

>##### [5] 什么是重排序?
>
>为了提高性能，编译器和处理器常常会对既定的代码执行顺序进行指令重排序。
>
>**重排序的类型有哪些呢？源码到最终执行会经过哪些重排序呢？**
>
>![image-20200518153028933](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200518153028933.png)
>
>一个好的内存模型实际上会放松对处理器和编译器规则的束缚，也就是说软件技术和硬件技术都为同一个目标，而进行奋斗：在不改变程序执行结果的前提下，尽可能提高执行效率。
>
>JMM对底层尽量减少约束，使其能够发挥自身优势。
>
>因此，在执行程序时，为了提高性能，编译器和处理器常常会对指令进行重排序。
>
>一般重排序可以分为如下三种：
>
>- 编译器优化的重排序。编译器在不改变单线程程序语义的前提下，可以重新安排语句的执行顺序;
>- 指令级并行的重排序。现代处理器采用了指令级并行技术来将多条指令重叠执行。如果不存在数据依赖性，处理器可以改变语句对应机器指令的执行顺序;
>- 内存系统的重排序。由于处理器使用缓存和读/写缓冲区，这使得加载和存储操作看上去可能是在乱序执行的。
>
>这里还得提一个概念，`as-if-serial`。
>
>不管怎么重排序，单线程下的执行结果不能被改变。编译器、runtime和处理器都必须遵守as-if-serial语义。

      4. 总结：

> - **原子性**是一组操作要么完全发生，要么没有发生，其余线程不会看到中间过程的存在。注意，**原子操作+原子操作不一定还是原子操作。**
> - **可见性**是指一个线程对共享变量的更新**对于另外一个线程是否可见**的问题。
> - **有序性**是指一个线程对共享变量的更新在其余线程看起来是**按照什么顺序执行**的问题。
> - 可以这么认为，**原子性 + 可见性 -> 有序性**
>
> 缘可续

#### 2. 创建线程的方式及其区别？

**方法一，继承** **Thread类**

~~~java
// 创建线程对象
Thread t = new Thread() {
 public void run() {
 // 要执行的任务
 }
};
// 启动线程
t.start();
~~~

例如：

~~~java
package cn.mycast;

import lombok.extern.slf4j.Slf4j;

@Slf4j(topic= "c.创建一个线程")
public class 创建一个线程 {
    public static void main(String[] args)  {
        Thread t1 =new Thread("t1"){
            @Override
            public void run() {
                log.debug("hello");
            }
        };
        t1.start();
    }
}
~~~

结果

~~~verilog
15:33:39.617 c.创建一个线程 [t1] - hello
~~~

**方法二，实现 Runnable 接口**

把【线程】和【任务】（要执行的代码）分开

* Thread 代表线程

* Runnable 可运行的任务（线程要执行的代码）

~~~java
Runnable runnable = new Runnable() {
 public void run(){
 // 要执行的任务
 }
};
// 创建线程对象
Thread t = new Thread( runnable );
// 启动线程
t.start();
~~~

例如：

~~~java
// 创建任务对象
Runnable task2 = new Runnable() {
 @Override
 public void run() {
 log.debug("hello");
 }
};
// 参数1 是任务对象; 参数2 是线程名字，推荐
Thread t2 = new Thread(task2, "t2");
t2.start();
~~~

输出：

~~~java
9:19:00 [t2] c.ThreadStarter - hello
~~~

Java 8 以后可以使用 lambda 精简代码

~~~java
// 创建任务对象
Runnable task2 = () -> log.debug("hello");
// 参数1 是任务对象; 参数2 是线程名字，推荐Thread t2 = new Thread(task2, "t2");
t2.start();
~~~

**区别：**

方法1 是把线程和任务合并在了一起，方法2 是把线程和任务分开了

* 用 Runnable 更容易与线程池等高级 API 配合

* 用 Runnable 让任务类脱离了 Thread 继承体系，更灵活（java不能实现多继承的补偿）

**方法三，实现Callable接口**

FutureTask 能够接收 Callable 类型的参数，用来处理有返回结果的情况

~~~java
// 创建任务对象
FutureTask<Integer> task3 = new FutureTask<>(() -> {
        log.debug("hello");     return 100});
// 参数1 是任务对象; 参数2 是线程名字，推荐
new Thread(task3, "t3").start();
// 主线程阻塞，同步等待 task 执行完毕的结果
Integer result = task3.get();
log.debug("结果是:{}", result);
~~~

**方法四：使用线程池创建**

#### 3. 说一下从Java API层面上的6种线程状态

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200624161618240.png" alt="image-20200624161618240" style="zoom:67%;" />

1. **新建（New）**：这是属于一个已经创建的线程，但是还没有调用**start方法**启动的线程所处的状态。
2. **可运行（Runnable）**：该状态包含两种可能。有可能正在运行，或者正在等待CPU资源。包含了操作系统线程状态种的运行，可运行状态和阻塞状态（由于 BIO 导致的线程阻塞，在 Java 里无法区分，仍然认为是可运行）；
3. **阻塞（Blocked）**：阻塞状态，当线程准备进入synchronized同步块或同步方法（排它锁）的时候，需要申请一个监视器锁而进行的等待，会使线程进入BLOCKED状态。如果其线程释放了锁就会结束此状态；
4. **等待（Waiting）**：该状态的出现是因为调用了**方法1**。处于该状态下的线程在等待另一个线程 执行一些其余action来将其唤醒。等待其他线程显式唤醒，否则不会再被分配CPU时间片；
5. **限期等待（Timed Waiting）**：该状态和上一个状态其实是一样的，调用了**方法2**是不过其等待的时间是明确的。
6. **死亡（TERMINATED）**：消亡状态比较容易理解，那就是线程执行结束了，run方法执行结束表示线程处于消亡状态了。

**方法1：**

| 进入方法                                   | 退出方法                             |
| ------------------------------------------ | ------------------------------------ |
| 没有设置 Timeout 参数的 Object.wait() 方法 | Object.notify() / Object.notifyAll() |
| 没有设置 Timeout 参数的 Thread.join() 方法 | 被调用的线程执行完毕                 |
| LockSupport.park() 方法                    | LockSupport.unpark(Thread)           |

调用 Thread.sleep() 方法使线程进入限期等待状态时，常常用“使一个线程睡眠”进行描述。调用 Object.wait() 方法使线程进入限期等待或者无限期等待时，常常用“挂起一个线程”进行描述。睡眠和挂起是用来描述行为，而阻塞和等待用来描述状态。

**方法2：**

| 进入方法                                 | 退出方法                                        |
| ---------------------------------------- | ----------------------------------------------- |
| Thread.sleep() 方法                      | 时间结束                                        |
| 设置了 Timeout 参数的 Object.wait() 方法 | 时间结束 / Object.notify() / Object.notifyAll() |
| 设置了 Timeout 参数的 Thread.join() 方法 | 时间结束 / 被调用的线程执行完毕                 |
| LockSupport.parkNanos() 方法             | LockSupport.unpark(Thread)                      |
| LockSupport.parkUntil() 方法             | LockSupport.unpark(Thread）                     |

#### **4 线程状态转换**

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200624161618240.png" alt="image-20200624161618240" style="zoom:67%;" />

假设有线程 Thread t
**情况 1 NEW --> RUNNABLE**

* 当调用 t.start() 方法时，由 NEW --> RUNNABLE

**情况 2 RUNNABLE <--> WAITING**
t 线程用 synchronized(obj) 获取了对象锁后

* 调用 obj.wait() 方法时，t 线程从 RUNNABLE --> WAITING
* 调用 obj.notify() ， obj.notifyAll() ， t.interrupt() 时
  + 竞争锁成功，t 线程从  WAITING --> RUNNABLE
  + 竞争锁失败，t 线程从  WAITING --> BLOCKED 

**情况 3 RUNNABLE <--> WAITING**

* 当前线程调用 t.join() 方法时，当前线程从 RUNNABLE --> WAITING
  + 注意是当前线程在t 线程对象的监视器上等待
* t 线程运行结束，或调用了当前线程的 interrupt() 时，当前线程从 WAITING --> RUNNABLE

**情况 4  RUNNABLE <--> WAITING**

* 当前线程调用 LockSupport.park() 方法会让当前线程从 RUNNABLE --> WAITING

* 调用 LockSupport.unpark(目标线程) 或调用了线程 的 interrupt() ，会让目标线程从 WAITING --> RUNNABLE

**情况** **5** **RUNNABLE <--> TIMED_WAITING**

**t** **线程**用 synchronized(obj) 获取了对象锁后

* 调用 obj.wait(long n) 方法时，**t** **线程**从 RUNNABLE --> TIMED_WAITING

* **t** **线程**等待时间超过了 n 毫秒，或调用 obj.notify() ， obj.notifyAll() ， t.interrupt() 时
  + 竞争锁成功，**t** **线程**从 TIMED_WAITING --> RUNNABLE
  + 竞争锁失败，**t** **线程**从 TIMED_WAITING --> BLOCKED

**情况** **6** **RUNNABLE <--> TIMED_WAITING**

+ **当前线程**调用 t.join(long n) 方法时，**当前线程**从 RUNNABLE --> TIMED_WAITING

注意是**当前线程**在**t** **线程对象**的监视器上等待

+  **当前线程**等待时间超过了 n 毫秒，或**t** **线程**运行结束，或调用了**当前线程**的 interrupt() 时，**当前线程**从TIMED_WAITING --> RUNNABLE

**情况** **7** **RUNNABLE <--> TIMED_WAITING**

* 当前线程调用 Thread.sleep(long n) ，当前线程从 RUNNABLE --> TIMED_WAITING

* **当前线程**等待时间超过了 n 毫秒，**当前线程**从 TIMED_WAITING --> RUNNABLE

**情况** **8** **RUNNABLE <--> TIMED_WAITING**

* 当前线程调用 LockSupport.parkNanos(long nanos) 或 LockSupport.parkUntil(long millis) 时，**当前线程**从 RUNNABLE --> TIMED_WAITING

* 调用 LockSupport.unpark(目标线程) 或调用了线程 的 interrupt() ，或是等待超时，会让目标线程从TIMED_WAITING--> RUNNABLE

**情况** **9** **RUNNABLE <--> BLOCKED**

* **t** **线程**用 synchronized(obj) 获取了对象锁时如果竞争失败，从 RUNNABLE --> BLOCKED持 obj 锁线程的同步代码块执行完毕，会唤醒该对象上所有 BLOCKED 的线程重新竞争，如果其中 **t** **线程**竞争成功，从 BLOCKED --> RUNNABLE ，其它失败的线程仍然 BLOCKED

**情况** **10** **RUNNABLE <--> TERMINATED**

* 当前线程所有代码运行完毕，进入 TERMINATED

#### 5 final原理

**final实现原理：**https://www.cnblogs.com/hexinwei1/p/10025840.html

> https://www.jianshu.com/p/1f4b0f98cbf1

对于final域，编译器和处理器要遵守**两个重排序规则**：

1. 在构造函数内对一个final域的写入，与随后把这个被构造对象的引用赋值给一个引用变量，这两个操作之间不能重排序。（先写入final变量，后调用该对象引用）

    **原因：**编译器会在final域的写之后，插入一个**StoreStore**屏障

2. 初次读一个包含final域的对象的引用，与随后初次读这个final域，这两个操作之间不能重排序（先读对象的引用，后读final变量）

   **原因：**编译器会在读final域操作的前面插入一个**LoadLoad**屏障 

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200807202047375.png" alt="image-20200807202047375" style="zoom:50%;" /> 

#### 6 ThreadLocal有了解吗？

**答：**使用ThreadLocal维护变量时，其为每个使用该变量的线程提供独立的变量副本，所以每一个线程都可以独立的改变自己的副本，而不会影响其他线程对应的副本。

**ThreadLocal内部实现机制：**

- 每个线程内部都会维护一个类似HashMap的对象，称为**ThreadLocalMap**，里边会包含若干了**Entry（K-V键值对）**，相应的线程被称为这些Entry的属主线程
- **Entry的Key是一个ThreadLocal实例，Value是一个线程特有对象**。Entry的作用是为其属主线程建立起一个ThreadLocal实例与一个线程特有对象之间的对应关系
- **Entry对Key的引用是弱引用**；**Entry对Value的引用是强引用**。

#### 7  synchronized 和Lock区别

> https://blog.csdn.net/qq_29373285/article/details/85964460

###### 1. 在实现上

**synchronized**是一个关键字，它基于JVM。它有锁升级过程，从偏向锁，轻量级锁，到重量级锁。

**Lock**是一个接口，它是基于JDK，它实现的主要实现类是ReentrantLock，它的使用也离不开AQS。

###### 2. 在使用上

**synchronized**是隐式锁，加锁解锁对使用者是隐藏的，可以作用于方法，代码块和类。

**Lock**是显示锁，需要手动上锁和释放锁（lock和unlock）

###### **3. 在功能上**

* **Lock和synchronized**都是互斥锁且支持可重入

* **Lock**支持默认非公平锁，但支持公平锁，**synchronized**只支持非公平锁

* **lock**的condition支持多个条件变量，但是**synchronized**

* **Lock** 可中断，而 **synchronized** 不行

<img src="https://upload-images.jianshu.io/upload_images/17248722-56beaaf0bc5256ea.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp" alt="img" style="zoom:67%;" />



![image-20200725094645345](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200725094645345.png)



#### 8  as-if-serial与happens-before

**as-if-serial规则：**

>不论怎么排序，单线程的执行结果都不能被改变

**as-if-serial**语义的意思指：**不管怎么重排序**（编译器和处理器为了提高并行度），（单线程）程序的执行结果不能被改变。编译器，runtime 和处理器都必须遵守as-if-serial语义。

**happens-before(发生-前面)：**

> 前一个变量相对于后一个发生变量是可见的

JMM可以通过happens-before关系向程序员提供跨线程的**内存可见性保证**（如果A线程的写操作a与B线程的读操作b之间存在happens-before关系，尽管a操作和b操作在不同的线程中执行，但JMM向程序员保证a操作将对b操作可见）。具体的定义为：

1）如果一个操作happens-before另一个操作，那么第一个操作的执行结果将对第二个操作可见，而且第一个操作的执行顺序排在第二个操作之前。

2）两个操作之间存在happens-before关系，并不意味着Java平台的具体实现必须要按照happens-before关系指定的顺序来执行。如果重排序之后的执行结果，与按happens-before关系来执行的结果一致，那么这种重排序并不非法（也就是说，JMM允许这种重排序）。

**下面来比较一下as-if-serial和happens-before：**

1. as-if-serial语义保证单线程内程序的执行结果不被改变，happens-before关系保证正确同步的多线程程序的执行结果不被改变。
2. as-if-serial语义给编写单线程程序的程序员创造了一个幻境：单线程程序是按程序的顺序来执行的。happens-before关系给编写正确同步的多线程程序的程序员创造了一个幻境：正确同步的多线程程序是按happens-before指定的顺序来执行的。
3. as-if-serial语义和happens-before这么做的目的，都是为了在不改变程序执行结果的前提下，尽可能地提高程序执行的并行度

#### 9 [sleep()和wait()的区别](https://www.cnblogs.com/lyx210019/p/9427146.html)

**一. 查看API**

**sleep**是Thread类的方法，导致此线程暂停执行指定时间，给其他线程执行机会，但是依然保持着监控状态，过了指定时间会自动恢复，调用sleep方法不会释放锁对象。当调用sleep方法后，当前线程进入**阻塞**状态。目的是让出CPU给其他线程运行的机会。但是由于sleep方法不**会释放锁对象**，所以在一个同步代码块中调用这个方法后，线程虽然休眠了，但其他线程无法访问它的锁对象。这是因为sleep方法拥有CPU的执行权，它可以自动醒来无需唤醒。而当sleep()结束指定休眠时间后，这个线程不一定立即执行，因为此时其他线程可能正在运行。

**wait方法是Object**类里的方法，当一个线程执行到wait()方法时，它就进入到一个和该对象相关的等待池中，同时释放了锁对象，等待期间可以调用里面的同步方法，其他线程可以访问，等待时不拥有CPU的执行权，否则其他线程无法获取执行权。当一个线程执行了wait方法后，**必须调用notify或者notifyAll方法**才能唤醒，而且是**随机唤醒**，若是被其他线程抢到了CPU执行权，该线程会继续进入等待状态。**由于锁对象可以时任意对象**，所以wait方法必须定义在Object类中，因为Obeject类是所有类的基类。

**二. 是否可以传入参数**

sleep()方法**必须传入参数**，参数就是休眠时间，时间到了就会自动醒来。

wait()方法**可以传入参数也可以不传入参数**，传入参数就是在参数结束的时间后开始等待，不穿如参数就是直接等待。

**三. 是否需要捕获异常**

**sleep方法必须要捕获异常，而wait方法不需要捕获异常**。sleep方法属于Thread类中方法，表示让一个线程进入睡眠状态，等待一定的时间之后，自动醒来进入到可运行状态，不会马上进入运行状态，因为线程调度机制恢复线程的运行也需要时间，一个线程对象调用了sleep方法之后，并不会释放他所持有的所有对象锁，所以也就不会影响其他进程对象的运行。但在sleep的过程中过程中有可能被其他对象调用它的interrupt(),产生InterruptedException异常，如果你的程序不捕获这个异常，线程就会异常终止，进入TERMINATED状态，如果你的程序捕获了这个异常，那么程序就会继续执行catch语句块(可能还有finally语句块)以及以后的代码。

wait属于Object的成员方法，一旦一个对象调用了wait方法，必须要采用notify()和notifyAll()方法唤醒该进程;如果线程拥有某个或某些对象的同步锁，那么在调用了wait()后，这个线程就会释放它持有的所有同步资源，而不限于这个被调用了wait()方法的对象。wait()方法也同样会在wait的过程中有可能被其他对象调用interrupt()方法而产生。

**四. 作用范围**

wait、notify和notifyAll方法只能在同步方法或者同步代码块中使用，而sleep方法可以在任何地方使用。但是注意sleep是静态方法，也就是说它只对当前对象有效。通过对象名.sleep()想让该对象线程进入休眠是无效的，它只会让当前线程进入休眠。

**五. 调用者的区别**

**首先为什么wait、notify和notifyAll方法要和synchronized关键字一起使用？**

因为wait方法是使一个线程进入等待状态，并且释放其所持有的锁对象，notify方法是通知等待该锁对象的线程重新获得锁对象，然而**如果没有获得锁对象，wait方法和notify方法都是没有意义**的，因此必须先获得锁对象再对锁对象进行进一步操作于是才要把wait方法和notify方法写到同步方法和同步代码块中了。

由此可知，wait和notify、notifyAll方法是由确定的对象即锁对象来调用的，锁对象就像一个传话的人，他对某个线程说停下来等待，然后对另一个线程说你可以执行了（实质上是被捕获了），这一过程是**线程通信**。sleep方法是让某个线程暂停运行一段时间，其控制范围是由当前线程决定，运行的主动权是由当前线程来控制（拥有CPU的执行权）。其实两者的区别都是让线程暂停运行一段时间，但本质的区别一个是**线程的运行状态控制**，一个是**线程间的通信**。

#### 10 为什么wait()和notify()或notifyAll()需要搭配synchronized关键字使用

> [link](https://blog.csdn.net/lengxiao1993/article/details/52296220?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)

- 从语义角度来讲， 一个线程调用了`wait()`之后， 必然需要由另外一个线程调用`notify()`来唤醒该线程， 所以本质上， `wait()`与`notify()`的成对使用， 是一种线程间的通信手段。
- 进一步分析， `wait()` 操作的调用必然是在等待某种条件的成立， 而条件的成立必然是由其他的线程来完成的。

#### 11 消费者生产者模型

~~~java
//仓库代码 主要处理同步问题
public class Storage {
    private final int MAX_SIZE = 100;//仓库最大容量
    private List list = new LinkedList();//产品存储在这里
    
    public void produce(int num) {//生产num个产品
        synchronized (list) {
            //一定是while，因为wait被唤醒后需要判断是不是满足生产条件
            while(list.size()+num > MAX_SIZE) {
                System.out.println("暂时不能执行生产任务");
                try{
                    list.wait();
                } catch ( InterruptedException e) {
                    e.printStackTrace();
                }
            }
           //满足生产条件开始生产
            for(int i = 0; i < num; i++) {
                list.add(new Object());
            }
            System.out.println("已生产产品数"+num+" 仓库容量"+list.size());
            list.notifyAll();
        }
    }

    public void consume(int num) {//消费num个产品
        synchronized (list) {
            while(list.size() < num) {
                System.out.println("暂时不能执行消费任务");
                try{
                    list.wait();
                } catch ( InterruptedException e) {
                    e.printStackTrace();
                }
            }
            //满足消费条件开始消费
            for(int i = 0; i < num; i++) {
                list.remove();
            }
            System.out.println("已消费产品数"+num+" 仓库容量"+list.size());
            list.notifyAll();
        }
    }
}
~~~

### 【同步的方式】

> https://www.cnblogs.com/Terry-Wu/p/10788663.html

**为何要使用同步？** 

java允许多线程并发控制，当多个线程同时操作一个可共享的资源变量时（如数据的增删改查）， 将会导致数据不准确，相互之间产生冲突，因此加入同步锁以避免在该线程没有完成操作之前，被其他线程的调用， 
**从而保证了该变量的唯一性和准确性**。 

##### [1] **synchronized同步方法** 

即有synchronized关键字修饰的方法。 由于java的每个对象都有一个内置锁，当用此关键字修饰方法时， 

内置锁会保护整个方法。在调用该方法前，需要获得内置锁，否则就处于阻塞状态。

代码如： 

```java
public synchronized void save(){}
```

注： *synchronized关键字也可以修饰静态方法，此时如果调用该静态方法，将会锁住整个类* 

##### [2 **synchronized同步代码块**

即有synchronized关键字修饰的语句块。 被该关键字修饰的语句块会自动被加上内置锁，从而实现同步。

代码如： 

```java
synchronized(object){ }
```

注：同步是一种高开销的操作，因此应该尽量减少同步的内容。 
通常没有必要同步整个方法，使用synchronized代码块同步关键代码即可。 

```java
package com.xhj.thread;
 
    /**
     * 线程同步的运用
     *
     * @author XIEHEJUN
     *
     */
    public class SynchronizedThread {
 
        class Bank {
 
            private int account = 100;
 
            public int getAccount() {
                return account;
            }
 
            /**
             * 用同步方法实现
             *
             * @param money
             */
            public synchronized void save(int money) {
                account += money;
            }
 
            /**
             * 用同步代码块实现
             *
             * @param money
             */
            public void save1(int money) {
                synchronized (this) {
                    account += money;
                }
            }
        }
 
        class NewThread implements Runnable {
            private Bank bank;
 
            public NewThread(Bank bank) {
                this.bank = bank;
            }
 
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    // bank.save1(10);
                    bank.save(10);
                    System.out.println(i + "账户余额为：" + bank.getAccount());
                }
            }
 
        }
 
        /**
         * 建立线程，调用内部类
         */
        public void useThread() {
            Bank bank = new Bank();
            NewThread new_thread = new NewThread(bank);
            System.out.println("线程1");
            Thread thread1 = new Thread(new_thread);
            thread1.start();
            System.out.println("线程2");
            Thread thread2 = new Thread(new_thread);
            thread2.start();
        }
 
        public static void main(String[] args) {
            SynchronizedThread st = new SynchronizedThread();
            st.useThread();
        }
 
    }
```

##### **[3] 使用volatile实现线程同步**

-  volatile关键字为域变量的**访问**提供了一种免锁机制， 
-  使用volatile修饰域相当于告诉虚拟机该域可能会被其他线程更新， 
-  因此每次使用该域就要重新计算，而不是使用寄存器中的值 
-  volatile不会提供任何原子操作，它也不能用来修饰final类型的变量 

 例如： 在上面的例子当中，只需在account前面加上volatile修饰，即可实现线程同步。 

代码实例： 

```java
//只给出要修改的代码，其余代码与上同
        class Bank {
            //需要同步的变量加上volatile
            private volatile int account = 100;
 
            public int getAccount() {
                return account;
            }
            //这里不再需要synchronized
            public void save(int money) {
                account += money;
            }
        ｝
```

注：多线程中的非同步问题主要出现在对域的读写上，如果让域自身避免这个问题，则就不需要修改操作该域的方法。 用final域，有锁保护的域和volatile域可以避免非同步的问题。

##### **[4] 使用 ReentrantLock实现线程同步** 

在JavaSE5.0中新增了一个java.util.concurrent包来支持同步。 ReentrantLock类是可重入、互斥、实现了Lock接口的锁， 它与使用synchronized方法和快具有相同的基本行为和语义，并且扩展了其能力。

ReenreantLock类的常用方法有：

- ReentrantLock() : 创建一个ReentrantLock实例 
- lock() : 获得锁 
- unlock() : 释放锁  

注：ReentrantLock()还有一个可以创建公平锁的构造方法，但由于能大幅度降低程序运行效率，不推荐使用 

例如： 在上面例子的基础上，改写后的代码为: 代码实例： 

```java
//只给出要修改的代码，其余代码与上同
        class Bank {
            //需要同步的变量加上volatile
            private volatile int account = 100;
 
            public int getAccount() {
                return account;
            }
            //这里不再需要synchronized
            public void save(int money) {
                account += money;
            }
        ｝
```

注：关于Lock对象和synchronized关键字的选择： 

- 最好两个都不用，使用一种java.util.concurrent包提供的机制, 能够帮助用户处理所有与锁相关的代码。 
- 如果synchronized关键字能满足用户的需求，就用synchronized，因为它能简化代码 
- 如果需要更高级的功能，就用ReentrantLock类，此时要注意及时释放锁，否则会出现死锁，通常在finally代码释放锁 　

##### **[5]  使用ThreadLocal实现线程同步**   

如果**使用ThreadLocal（局部变量）管理变量**，则每一个使用该变量的线程都获得该变量的副本， 副本之间相互独立，这样每一个线程都可以随意修改自己的变量副本，而不会对其他线程产生影响。

**ThreadLocal 类的常用方法**

- ThreadLocal() : 创建一个线程本地变量 
- get() : 返回此线程局部变量的当前线程副本中的值 
- initialValue() : 返回此线程局部变量的当前线程的"初始值" 
- set(T value) : 将此线程局部变量的当前线程副本中的值设置为value
  在上面例子基础上，修改后的代码为： 

```java
//只改Bank类，其余代码与上同
        public class Bank{
            //使用ThreadLocal类管理共享变量account
            private static ThreadLocal<Integer> account = new ThreadLocal<Integer>(){
                @Override
                protected Integer initialValue(){
                    return 100;
                }
            };
            public void save(int money){
                account.set(account.get()+money);
            }
            public int getAccount(){
                return account.get();
            }
        }
```

注：ThreadLocal与同步机制 

-  a.ThreadLocal与同步机制都是为了解决多线程中相同变量的访问冲突问题。 
-  b.前者采用以"空间换时间"的方法，后者采用以"时间换空间"的方式

##### **[6]  使用LinkedBlockingQueue实现线程同步**

前面5种同步方式都是在底层实现的线程同步，但是我们在实际开发当中，应当尽量远离底层结构。 使用javaSE5.0版本中新增的java.util.concurrent包将有助于简化开发。 本小节主要是使LinkedBlockingQueue<E>来实现线程的同步 LinkedBlockingQueue<E>是一个基于已连接节点的，范围任意的blocking queue。 
队列是先进先出的顺序（FIFO），关于队列以后会详细讲解~ 

**LinkedBlockingQueue 类常用方法**

- LinkedBlockingQueue() : 创建一个容量为Integer.MAX_VALUE的LinkedBlockingQueue 
- put(E e) : 在队尾添加一个元素，如果队列满则阻塞 
- size() : 返回队列中的元素个数 
- take() : 移除并返回队头元素，如果队列空则阻塞 

**代码实例：**
实现商家生产商品和买卖商品的同步

```java
package com.xhj.thread;
 
import java.util.Random;
import java.util.concurrent.LinkedBlockingQueue;
 
/**
 * 用阻塞队列实现线程同步 LinkedBlockingQueue的使用
 *
 * @author XIEHEJUN
 *
 */
public class BlockingSynchronizedThread {
    /**
     * 定义一个阻塞队列用来存储生产出来的商品
     */
    private LinkedBlockingQueue<Integer> queue = new LinkedBlockingQueue<Integer>();
    /**
     * 定义生产商品个数
     */
    private static final int size = 10;
    /**
     * 定义启动线程的标志，为0时，启动生产商品的线程；为1时，启动消费商品的线程
     */
    private int flag = 0;
 
    private class LinkBlockThread implements Runnable {
        @Override
        public void run() {
            int new_flag = flag++;
            System.out.println("启动线程 " + new_flag);
            if (new_flag == 0) {
                for (int i = 0; i < size; i++) {
                    int b = new Random().nextInt(255);
                    System.out.println("生产商品：" + b + "号");
                    try {
                        queue.put(b);
                    } catch (InterruptedException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                    }
                    System.out.println("仓库中还有商品：" + queue.size() + "个");
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                    }
                }
            } else {
                for (int i = 0; i < size / 2; i++) {
                    try {
                        int n = queue.take();
                        System.out.println("消费者买去了" + n + "号商品");
                    } catch (InterruptedException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                    }
                    System.out.println("仓库中还有商品：" + queue.size() + "个");
                    try {
                        Thread.sleep(100);
                    } catch (Exception e) {
                        // TODO: handle exception
                    }
                }
            }
        }
    }
 
    public static void main(String[] args) {
        BlockingSynchronizedThread bst = new BlockingSynchronizedThread();
        LinkBlockThread lbt = bst.new LinkBlockThread();
        Thread thread1 = new Thread(lbt);
        Thread thread2 = new Thread(lbt);
        thread1.start();
        thread2.start();
 
    }
 
}
```

注：BlockingQueue<E>定义了阻塞队列的常用方法，尤其是三种添加元素的方法，我们要多加注意，当队列满时：

- add()方法会抛出异常
- offer()方法返回false
- put()方法会阻塞

##### **[7] 使用原子变量实现线程同步**

需要使用线程同步的根本原因在于对普通变量的操作不是原子的。**那么什么是原子操作呢？**
原子操作就是指将读取变量值、修改变量值、保存变量值看成一个整体来操作，即-这几种行为要么同时完成，要么都不完成。在java的**util.concurrent.atomic包中提供了创建了原子类型变量的工具类**，使用该类可以简化线程同步。其中**AtomicInteger** 表可以用原子方式更新int的值，可用在应用程序中(如以原子方式增加的计数器)，
但不能用于替换Integer；可扩展Number，允许那些处理机遇数字类的工具和实用工具进行统一访问。

**AtomicInteger类常用方法：**

- AtomicInteger(int initialValue) : 创建具有给定初始值的新的AtomicInteger
- addAddGet(int dalta) : 以原子方式将给定值与当前值相加
- get() : 获取当前值


**代码实例：**
只改Bank类，其余代码与上面第一个例子同

```java
class Bank {
        private AtomicInteger account = new AtomicInteger(100);
 
        public AtomicInteger getAccount() {
            return account;
        }
 
        public void save(int money) {
            account.addAndGet(money);
        }
    }
```

**补充--原子操作主要有：**

- 对于引用变量和大多数原始变量(long和double除外)的读写操作；
- 对于所有使用volatile修饰的变量(包括long和double)的读写操作。

### 【锁】

> [JAVA锁有哪些种类，以及区别（转）](https://www.cnblogs.com/lxmyhappy/p/7380073.html)

1. 实现上

`Synchronized`

`ReentrantLock`

`CAS`

`Volatile`

2 类型上

- 公平锁/非公平锁 : 
- 可重入锁
- 独享锁/共享锁
- 互斥锁/读写锁
- 乐观锁/悲观锁
- 分段锁
- 偏向锁/轻量级锁/重量级锁
- 自旋锁

上面是很多锁的名词，这些分类并不是全是指锁的状态，有的指锁的特性，有的指锁的设计，下面总结的内容是对每个锁的名词进行一定的解释

##### **[1] 公平锁/非公平锁**

* **介绍：**

公平锁是指多个线程按照申请锁的顺序来获取锁，

非公平锁是指多个线程获取锁的顺序并不是按照申请锁的顺序，有可能后申请的线程比先申请的线程优先获取锁。

* **优缺点：**

公平锁可以防止线程饥饿。

非公平锁的优点在于吞吐量比公平锁大，有可能会造成优先级反转或者饥饿现象。

* **实现：**

对于Java `ReentrantLock`而言，默认是非公平锁。，但是支持公平锁。

对于`Synchronized`而言，也是一种非公平锁。由于其并不像`ReentrantLock`是通过AQS的来实现线程调度，所以并没有任何办法使其变成公平锁。

**1. 公平调度方式：**

按照**申请的先后顺序**授予资源的独占权。

**2. 非公平调度方式：**

在该策略中，资源的持有线程释放该资源的时候，等待队列中一个线程会被唤醒，而该线程从被唤醒到其继续执行可能需要一段时间。在该段时间内，**新来的线程（活跃线程）**可以先被授予该资源的独占权。

如果新来的线程占用该资源的时间不长，那么它完全有可能在被唤醒的线程继续执行前释放相应的资源，从而不影响该被唤醒的线程申请资源。

**公平调度和非公平调度方式优缺点分析**

**非公平调度策略：**

- 优点：吞吐率较高，单位时间内可以为更多的申请者调配资源
- 缺点：资源申请者申请资源所需的时间偏差可能较大，并可能出现线程饥饿的现象

**公平调度策略：**

- 优点：线程申请资源所需的时间偏差较小；**不会出现线程饥饿的现象**；适合在资源的持有线程占用资源的时间相对长或者资源的平均申请时间间隔相对长的情况下，或者对资源申请所需的时间偏差有所要求的情况下使用；
- 缺点：吞吐率较小

接下来，我们一起来看看JVM对synchronized内部锁的调度方式吧。

**JVM对synchronized内部锁的调度**

JVM对内部锁的调度是一种**非公平的调度方式**，JVM会给每个内部锁分配一个**入口集（Entry Set）**，用于记录等待获得相应内部锁的线程。当锁被持有的线程释放的时候，该锁的入口集中的任意一个线程将会被唤醒，从而得到再次申请锁的机会。被唤醒的线程等待占用处理器运行时可能还有其他新的活跃线程与该线程抢占这个被释放的锁.

##### **[2] 可重入锁**

* **介绍：**

可重入锁又名递归锁，是指在同一个线程在外层方法获取锁的时候，在进入内层方法会自动获取锁。

* **优缺点：**

可重入锁的一个好处是可一定程度避免死锁。

* **实现：**

对于Java `ReentrantLock`而言, 他的名字就可以看出是一个可重入锁，其名字是`Re entrant Lock`重新进入锁。
对于`Synchronized`而言,也是一个可重入锁。

 **synchronized可重入锁的实现：**

之前谈到过，每个锁关联一个线程持有者和一个计数器。当计数器为0时表示该锁没有被任何线程持有，那么任何线程都都可能获得该锁而调用相应方法。当一个线程请求成功后，JVM会记下持有锁的线程，并将计数器计为1。此时其他线程请求该锁，则必须等待。而该持有锁的线程如果再次请求这个锁，就可以再次拿到这个锁，同时计数器会递增。当线程退出一个synchronized方法/块时，计数器会递减，如果计数器为0则释放该锁。

```java
synchronized void setA() throws Exception{
    Thread.sleep(1000);
    setB();
}

synchronized void setB() throws Exception{
    Thread.sleep(1000);
}
```

##### **[3] 独享锁/共享锁（互斥锁/读写锁）**

* **介绍：**

独享锁是指该锁一次只能被一个线程所持有。读锁的共享锁可保证并发读是非常高效的，读写，写读 ，写写的过程是互斥的。
共享锁是指该锁可被多个线程所持有。独享锁与共享锁也是通过AQS来实现的，通过实现不同的方法，来实现独享或者共享。

* **实现：**

上面讲的独享锁/共享锁就是一种广义的说法，互斥锁/读写锁就是具体的实现。
互斥锁在Java中的具体实现就是`ReentrantLock`和`Synchronized`
读写锁在Java中的具体实现就是`ReadWriteLock`

对于`Synchronized`而言，当然是独享锁。

##### **[4] 乐观锁/悲观锁**

* **介绍：**

乐观锁与悲观锁不是指具体的什么类型的锁，而是指看待并发同步的角度。
悲观锁认为对于同一个数据的并发操作，一定是会发生修改的，哪怕没有修改，也会认为修改。因此对于同一个数据的并发操作，悲观锁采取加锁的形式。悲观的认为，不加锁的并发操作一定会出问题。悲观锁适合写操作非常多的场景
乐观锁则认为对于同一个数据的并发操作，是不会发生修改的。在更新数据的时候，会采用尝试更新，不断重新的方式更新数据。乐观的认为，不加锁的并发操作是没有事情的。乐观锁适合读操作非常多的场景，不加锁会带来大量的性能提升。

* **优缺点：**

从悲观锁适合写操作非常多的场景

乐观锁适合读操作非常多的场景，不加锁会带来大量的性能提升。

* **实现：**

悲观锁在Java中的使用，就是利用各种锁。
乐观锁在Java中的使用，是无锁编程，常常采用的是CAS算法，典型的例子就是原子类，通过CAS自旋实现原子操作的更新。

##### **[5] 分段锁**

* **介绍：**

分段锁其实是一种锁的设计，并不是具体的一种锁，对于`ConcurrentHashMap`而言，其并发的实现就是通过分段锁的形式来实现高效的并发操作。

* **实现：**

我们以`ConcurrentHashMap`来说一下分段锁的含义以及设计思想，`ConcurrentHashMap`中的分段锁称为Segment，它即类似于HashMap（JDK7与JDK8中HashMap的实现）的结构，即内部拥有一个Entry数组，数组中的每个元素又是一个链表；同时又是一个ReentrantLock（Segment继承了ReentrantLock)。
当需要put元素的时候，并不是对整个hashmap进行加锁，而是先通过hashcode来知道他要放在那一个分段中，然后对这个分段进行加锁，所以当多线程put的时候，只要不是放在一个分段中，就实现了真正的并行的插入。
但是，在统计size的时候，可就是获取hashmap全局信息的时候，就需要获取所有的分段锁才能统计。
分段锁的设计目的是细化锁的粒度，当操作不需要更新整个数组的时候，就仅仅针对数组中的一项进行加锁操作。

##### **[6] 偏向锁/轻量级锁/重量级锁**

* **介绍：**

这三种锁是指锁的状态，并且是针对`Synchronized`。在Java 5通过引入锁升级的机制来实现高效`Synchronized`。这三种锁的状态是通过对象监视器在对象头中的字段来表明的。

* **实现：**

偏向锁是指一段同步代码一直被一个线程所访问，那么该线程会自动获取锁。降低获取锁的代价。
轻量级锁是指当锁是偏向锁的时候，被另一个线程所访问，偏向锁就会升级为轻量级锁，其他线程会通过自旋的形式尝试获取锁，不会阻塞，提高性能。
重量级锁是指当锁为轻量级锁的时候，另一个线程虽然是自旋，但自旋不会一直持续下去，当自旋一定次数的时候，还没有获取到锁，就会进入阻塞，该锁膨胀为重量级锁。重量级锁会让其他申请的线程进入阻塞，性能降低。

##### **[7] 自旋锁**

* **介绍：**

在Java中，自旋锁是指尝试获取锁的线程不会立即阻塞，而是采用循环的方式去尝试获取锁。

* **优缺点**

好处是减少线程上下文切换的消耗，缺点是循环会消耗CPU造成ABA问题。

* **实现：**

典型的自旋锁实现的例子，可以参考[自旋锁的实现](http://ifeve.com/java_lock_see1/)

##### [8] 可中断锁/不可中断锁/超时时间

可中断锁：顾名思义，就是可以相应中断的锁。**不会无限制等待下去，是避免死锁的一种方式。**在Java中，synchronized就不是可中断锁，而Lock是可中断锁。

如果某一线程A正在执行锁中的代码，另一线程B正在等待获取该锁，可能由于等待时间过长，线程B不想等待了，想先处理其他事情，我们可以让它中断自己或者在别的线程中中断它，这种就是可中断锁。**如果是不可中断模式，那么即使使用了 interrupt 也不会让等待中断**

**超时时间**：中断是被动的打断，而设置超时时间**是主动的打断**，可以避免死锁。

##### [9] 显式锁/隐式锁

synchronized加锁是隐式加锁，使用者不会看到其加锁解锁过程锁升级过程·。

ReentrantLock 加锁和解锁是显示的。如果 ReentrantLock 调用lock方法加锁， unlock 方法解锁，否则会造成死锁。

##### [10] 条件变量

synchronized 中也有条件变量，就是我们讲原理时那个 waitSet 休息室，当条件不满足时进入 waitSet 等待

ReentrantLock 的条件变量比 synchronized 强大之处在于，它是支持多个条件变量的，这就好比

synchronized 是那些不满足条件的线程都在一间休息室等消息

**而 ReentrantLock 支持多间休息室，有专门等烟的休息室、专门等早餐的休息室、唤醒时也是按休息室来唤**

**醒**

使用要点：

* await 前需要获得锁

await 执行后，会释放锁，进入 conditionObject 等待

await 的线程被唤醒（或打断、或超时）取重新竞争 lock 锁

竞争 lock 锁成功后，从 await 后继续执行

##### **[11] AQS**

AQS是AbustactQueuedSynchronizer（队列同步器）的简称，它是一个Java提供的底层同步工具类，用一个int类型的变量表示同步状态，并提供了一系列的CAS操作来管理这个同步状态。

AQS的主要作用是为Java中的**并发同步组件提供统一的底层支持**，例如ReentrantLock，CountdowLatch就是基于AQS实现的，用法是通过**继承AQS实现其模版方法**，然后将**子类作为同步组件的内部类**。

AQS中可重写的方法分为独占式与共享式的



![img](https://pic3.zhimg.com/80/v2-7f39146a987be0ac9a459e8bd03d8b4b_720w.jpg)



可以直接调用的模板方法有



![img](https://pic2.zhimg.com/80/v2-6391ce83f9f66d8687b3098a4238e342_720w.jpg)



同步器提供的如下3个方法来访问或修改同步状态。 ·getState()：获取当前同步状态。 ·setState(int newState)：设置当前同步状态。 ·compareAndSetState(int expect,int update)：使用CAS设置当前状态，该方法能够保证状态设置的原子性。

**2.2 实现**

**2.2.1 同步队列**

同步队列是AQS很重要的组成部分，它是一个**双端队列**，遵循FIFO原则，主要作用是用来存放在锁上阻塞的线程，当一个线程尝试获取锁时，如果已经被占用，**获取锁失败**那么当前线程就会**被构造成一个Node节点**加入到同步队列的尾部，队列的**头节点是成功获取锁的节点**，当头节点线程释放锁时，会**唤醒后面的节点并释放当前头节点的引用**

同步队列中的节点（Node）用来保存获取同步状态失败的线程引用、等待状态以及前驱和 后继节点



![img](https://pic1.zhimg.com/80/v2-fe00dbe612ec5ab59c6524b50513b41b_720w.jpg)



使用CAS将节点插入到尾部，并用tail指向该结点

**2.2.2 独占锁的获取和释放流程**

**获取**

- 调用入口方法acquire(arg)
- 调用模版方法tryAcquire(arg)尝试获取锁，若成功则返回，若失败则走下一步
- 将当前线程构造成一个Node节点，并利用addWaiter(Node node) 将其加入到同步队列尾部
- 调用acquireQueued(Node node,int arg)方法，使得该 节点以“死循环”的方式获取同步状态
- 自旋时，首先判断其**前驱节点为头节点且释放&是否成功获取同步状态**，两个条件都成立，则将当前线程的节设置为头节点，如果不是，则利用**LockSupport.park(this)将当前线程挂起 ,等待前驱节点释放唤醒自己**，之后继续判断。

**释放**

- 调用入口方法release(arg)
- 调用模版方法tryRelease(arg)释放同步状态
- 利用LockSupport.unpark(currentNode.next.thread)唤醒后继节点（接获取的第五步）



**2.2.3 共享锁的获取和释放流程**

**共享式获取与独占式获取最主要的区别在于同一时刻能否有多个线程同时获取到同步状态**



**获取锁**

- 在acquireShared(int arg)方法中，同步器调用tryAcquireShared(int arg)方法尝试获取同步状态
- tryAcquireShared(int arg)方法返回值为int类型，当返回值大于等于0时，表示能够获取到同步状态。因此，在共享式获取的自旋过程中，成功获取到同步状态并退出自旋的条件就是 **tryAcquireShared(int arg)方法返回值大于等于0**。
- 可以看到，在doAcquireShared(int arg)方法的自 旋过程中，如果当前节点的前驱为头节点时，尝试获取同步状态，如果返回值大于等于0，表示该次获取同步状态成功并从自旋过程中退出。



**释放锁**

- 调用releaseShared(arg)模版方法释放同步状态
- 调用模版方法tryReleaseShard(arg)释放同步状态
- 如果释放成功，则**遍历整个队列，利用LockSupport.unpark(nextNode.thread)唤醒所有后继节点**
- 与独占式区别在于**线程安全释放，通过循环和CAS保证**，因为释放同步状态的操作会同时来自多个线程



**2.2.4 独占锁和共享锁在实现上的区别**

- 独占锁的同步状态值为1，即同一时刻只能有一个线程成功获取同步状态
- 共享锁的同步状态>1，取值由上层同步组件确定
- 独占锁队列中头节点运行完成后释放它的直接后继节点
- 共享锁队列中头节点运行完成后释放它后面的所有节点
- 共享锁中会出现多个线程（即同步队列中的节点）同时成功获取同步状态的情况



**2.2.5 重入锁**

重入锁指的是当前线程成功获取锁后，如果再次访问该临界区，则不会对自己产生互斥行为。Java中ReentrantLock和synchronized都是可重入锁，synchronized由JVM偏向锁实现可重入锁，ReentrantLock可重入性基于AQS实现。

重入锁的基本原理是**判断上次获取锁的线程是否为当前线程**(`current == getExclusiveOwnerThread()`)，如果是则可再次进入临界区，如果不是，则阻塞。

```java
 final boolean nonfairTryAcquire(int acquires) {
     //获取当前线程
     final Thread current = Thread.currentThread();
     //通过AQS获取同步状态
     int c = getState();
     //同步状态为0，说明临界区处于无锁状态，
     if (c == 0) {
         //修改同步状态，即加锁
         if (compareAndSetState(0, acquires)) {
             //将当前线程设置为锁的owner
             setExclusiveOwnerThread(current);
             return true;
         }
     }
     //如果临界区处于锁定状态，且上次获取锁的线程为当前线程
     else if (current == getExclusiveOwnerThread()) {
         //则递增同步状态
         int nextc = c + acquires;
         if (nextc < 0) // overflow
             throw new Error("Maximum lock count exceeded");
         setState(nextc);
         return true;
     }
     return false;
 }
 
```

如果是获取锁的线程再次请求，则将同步状态值进行增加并返回 true，表示获取同步状态成功。

成功获取锁的线程再次获取锁，只是增加了同步状态值，这也就要求ReentrantLock在释放 同步状态时减少同步状态值



**2.2.6 公平锁和非公平锁**

对于非公平锁，只要CAS设置 同步状态成功，则表示当前线程获取了锁，而公平锁则不同

```java
 protected final boolean tryAcquire(int acquires) {
     final Thread current = Thread.currentThread();
     int c = getState();
     if (c == 0) {
         //此处为公平锁的核心，即判断同步队列中当前节点是否有前驱节点
         if (!hasQueuedPredecessors() &&
             compareAndSetState(0, acquires)) {
             setExclusiveOwnerThread(current);
             return true;
         }
     }
     else if (current == getExclusiveOwnerThread()) {
         int nextc = c + acquires;
         if (nextc < 0)
             throw new Error("Maximum lock count exceeded");
         setState(nextc);
         return true;
     }
     return false;
 }
```

该方法与nonfairTryAcquire(int acquires)比较，唯一不同的位置为判断条件多了 hasQueuedPredecessors()方法，即加入了**同步队列中当前节点是否有前驱节点的判断**，如果该 方法返回true，则表示有线程比当前线程更早地请求获取锁，因此需要等待前驱线程获取并释放锁之后才能继续获取锁。



**2.2.7 读写锁**

Java提供了一个基于AQS到读写锁实现`ReentrantReadWriteLock`，该读写锁到实现原理是：**将同步变量state按照高16位和低16位进行拆分，高16位表示读锁，低16位表示写锁**。

**写锁的获取与释放** 写锁是一个独占锁，所以我们看一下ReentrantReadWriteLock中tryAcquire(arg)的实现：

```java
     protected final boolean tryAcquire(int acquires) {
             Thread current = Thread.currentThread();
             int c = getState();
             int w = exclusiveCount(c);
             if (c != 0) {
                 if (w == 0 || current != getExclusiveOwnerThread())
                     return false;
                 if (w + exclusiveCount(acquires) > MAX_COUNT)
                     throw new Error("Maximum lock count exceeded");
                 // Reentrant acquire
                 setState(c + acquires);
                 return true;
             }
             if (writerShouldBlock() ||
                 !compareAndSetState(c, c + acquires))
                 return false;
             setExclusiveOwnerThread(current);
             return true;
         }
 
```

上述代码的处理流程已经非常清晰：

- 获取同步状态，并从中分离出低16为的写锁状态
- 如果同步状态不为0，说明存在读锁或写锁
- 如果存在读锁（c ！=0 && w == 0），则不能获取写锁（保证写对读的可见性）
- 如果当前线程不是上次获取写锁的线程，则不能获取写锁（写锁为独占锁）
- 如果以上判断均通过，则在低16为写锁同步状态上利用CAS进行修改（增加写锁同步状态，实现可重入） 将当前线程设置为写锁的获取线程



写锁的释放过程与独占锁基本相同：

```java
     protected final boolean tryRelease(int releases) {
             if (!isHeldExclusively())
                 throw new IllegalMonitorStateException();
             int nextc = getState() - releases;
             boolean free = exclusiveCount(nextc) == 0;
             if (free)
                 setExclusiveOwnerThread(null);
             setState(nextc);
             return free;
         }
 
```

在释放的过程中，不断减少读锁同步状态，只为同步状态为0时，写锁完全释放。



**读锁的获取与释放**

读锁是一个共享锁，获取读锁的步骤如下：

- 获取当前同步状态
- 计算高16为读锁状态+1后的值
- 如果大于能够获取到的读锁的最大值，则抛出异常
- 如果存在写锁并且当前线程不是写锁的获取者，则获取读锁失败
- 如果上述判断都通过，则利用CAS重新设置读锁的同步状态



读锁的释放步骤与写锁类似，即不断的释放写锁状态，直到为0时，表示没有线程获取读锁。



**三、使用AQS与Lock自定义一个锁**

```java
 class Mutex implements Lock {    
     
     // 静态内部类，自定义同步器    
     private static class Sync extends AbstractQueuedSynchronizer {            
         
         // 是否处于占用状态            
         protected boolean isHeldExclusively() {                    
             return getState() == 1;            
         }            
         
         // 当状态为0的时候获取锁            
         public boolean tryAcquire(int acquires) {                    
             if (compareAndSetState(0, 1)) {   
                 setExclusiveOwnerThread(Thread.currentThread()); 
                 return true;                    
             }                    
             return false;            
         }            
         
         // 释放锁，将状态设置为0            
         protected boolean tryRelease(int releases) {                    
             if (getState() == 0) 
                 throw new IllegalMonitorStateException();            
             setExclusiveOwnerThread(null);                    
             setState(0);                    
             return true;            
         }            
         
         // 返回一个Condition，每个condition都包含了一个condition队列            
         Condition newCondition() { 
             return new ConditionObject(); 
         }    
     }    
     
     // 仅需要将操作代理到Sync上即可    
     private final Sync sync = new Sync();
     
     public void lock() { 
         sync.acquire(1); 
     }
     
     public boolean tryLock() { 
         return sync.tryAcquire(1); 
     }
     
     public void unlock() { 
         sync.release(1); 
     }    
     
     public Condition newCondition() { 
         return sync.newCondition(); 
     }
     
     public boolean isLocked() { 
         return sync.isHeldExclusively(); 
     }
     
     public boolean hasQueuedThreads() { 
         return sync.hasQueuedThreads(); 
     }
     
     public void lockInterruptibly() throws InterruptedException {            
         sync.acquireInterruptibly(1);    
     }
     
     public boolean tryLock(long timeout, TimeUnit unit) throws InterruptedException{ 
         return sync.tryAcquireNanos(1, unit.toNanos(timeout));    
     } 
 }
```

流程：

- 这个自定义类Mutex首先实现了Lock接口，
- 内部静态类Sync继承了AQS抽象类，并重写了独占式的tryAcquire和tryRelease方法，
- 接着Mutex实例化Sync内部类，
- Mutex类重写Lock接口的方法，如lock、tryLock、unlock等方法，具体实现是通过调用Sync类中的重写的方法（tryAcquire）以及模板方法（acquire）等
- 用户使用Mutex时调用Mutex提供的方法，在Mutex的实现中，调用同步器的模板方法acquire(int args)

### 【<锁的属性>】

##### [1] 为什么要加锁之临界区

多个线程访问共享资源时，在多个线程对共享资源读写操作时发生指令交错，就会出现问题。一段代码块内如果存在对共享资源的多线程读写操作，称这段代码块为临界区。

多个线程在临界区内执行，由于代码的执行序列不同而导致结果无法预测，称之为发生了**竞态条件**。

##### **[2] 实现一个锁需要考虑哪些方面?**

实现一个锁，主要需要考虑2个问题

1. 如何线程安全的修改锁状态位？
2. 得不到锁的线程，如何排队？

### 【<锁升级>】

##### [1] Java对象头

我们以 Hotspot 虚拟机为例，Hopspot 对象头主要包括两部分数据：`Mark Word（标记字段） 和 Klass Pointer（类型指针）`

**Mark Word**：默认存储对象的HashCode，分代年龄和锁标志位信息。这些信息都是与对象自身定义无关的数据，所以Mark Word被设计成一个非固定的数据结构以便在极小的空间内存存储尽量多的数据。它会根据对象的状态复用自己的存储空间，也就是说在运行期间Mark Word里存储的数据会随着锁标志位的变化而变化。

**Klass Point**：对象指向它的类元数据的指针，虚拟机通过这个指针来确定这个对象是哪个类的实例。

在上面中我们知道了，`synchronized`	用的锁是存在Java对象头里的，那么具体是存在对象头哪里呢？答案是：**存在锁对象的对象头的Mark Word中**，那么MarkWord在对象头中到底长什么样，它到底存储了什么呢？

**在64位的虚拟机中：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200606113746579.png)
**在32位的虚拟机中：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200606113736103.png)

![image-20200714200304212](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714200304212.png)

![image-20200714200322099](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714200322099.png)

![image-20200714200339932](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714200339932.png)

https://stackoverflow.com/questions/26357186/what-is-in-java-object-header

##### [2] Mark word 结构

**默认（Normal）**：hashcode（地址码）；age（分代中的年龄）；biased—lock（是不是偏向锁），01（加锁状态：表示没有和任何monitor关联）

**重量级锁（Normal）**：ptr_to_heavyweight_moniter(指向锁的地址)，10（加锁状态：已经与monitor关联）轻**轻量级锁（Normal）**：ptr_to_lock_record(锁记录的地址)，00（加锁状态：轻量级锁）

| 锁状态   | 存储内容                                              | 标志位 |
| -------- | ----------------------------------------------------- | ------ |
| 无锁     | 对象的hashCode、对象分代年龄、是否是偏向锁(0)         | 01     |
| 偏向锁   | 偏向线程ID、偏向时间戳、对象分代年龄、是否是偏向锁(1) | 01     |
| 轻量级锁 | 指向栈中锁记录的指针                                  | 00     |
| 重量级锁 | 指向互斥量的指针                                      | 11     |

![image-20200714201707252](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714201707252.png)

##### [3] Monitor

Monitor 被翻译为**监视器**或**管程** 。**每个 Java 对象都可以关联一个 Monitor 对象，如果使用 synchronized 给对象上锁（重量级）之后，该对象头的Mark Word 中就被设置指向 Monitor 对象的指针**。

使用**monitorenter**和**monitorexit**两个指令实现同步：

大致含义如下：

* **monitorenter**

> 每个对象都会与一个monitor相关联，当某个monitor被拥有之后就会被锁住，当线程执行到monitorenter指令时，就会去尝试获得对应的monitor。步骤如下：
>
> 1. 每个monitor维护着一个记录着拥有次数的计数器。未被拥有的monitor的该计数器为0，当一个线程获得monitor（执行monitorenter）后，该计数器自增变为 1 。
>    - 当同一个线程再次获得该monitor的时候，计数器再次自增；
>    - 当不同线程想要获得该monitor的时候，就会被阻塞。
> 2. 当同一个线程释放 monitor（执行monitorexit指令）的时候，计数器再自减。当计数器为0的时候。monitor将被释放，其他线程便可以获得monitor。

- **monitorexit**

> 当线程执行monitorexit指令时，会去讲monitor的计数器减一，如果结果是0，则该线程将不再拥有该monitor。其他线程就可以获得该monitor了。

![image-20200714200132363](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714200132363.png)

* 刚开始 Monitor 中 Owner 为 null

* 当 Thread-2 执行 synchronized(obj) 就会将 Monitor 的所有者 Owner 置为 Thread-2，

* 在 Thread-2 上锁的过程中，如果 Thread-3，Thread-4，Thread-5 也来执行 synchronized(obj)，就会进入

EntryList BLOCKED (**Monitor中只能有一个 Owner**)

* Thread-2 执行完同步代码块的内容，然后唤醒 EntryList 中等待的线程来竞争锁，竞争时是非公平的

* 图中 WaitSet 中的 Thread-0，Thread-1 是之前获得过锁，但条件不满足进入 WAITING 状态的线程，后面讲

wait-notify 时会分析

https://www.jianshu.com/p/c3313dcf2c23

>① owner：初始时为NULL。当有线程占有该monitor时，owner标记为该线程的唯一标识。当线程释放monitor时，owner又恢复为NULL。owner是一个临界资源，JVM是通过CAS操作来保证其线程安全的。
>② _cxq：竞争队列，所有请求锁的线程首先会被放在这个队列中（单向链接）。_cxq是一个临界资源，JVM通过CAS原子指令来修改_cxq队列。修改前_cxq的旧值填入了node的next字段，_cxq指向新值（新线程）。因此_cxq是一个后进先出的stack（栈）。
>③ _EntryList：_cxq队列中有资格成为候选资源的线程会被移动到该队列中
>④ _WaitSet：因为调用wait方法而被阻塞的线程会被放在该队列中
>
>synchronized 必须是进入同一个对象的 monitor 才有上述的效果
>
>不加 synchronized 的对象不会关联监视器，不遵从以上规则

##### [4] synchronized锁升级

###### **无锁**

不通过阻塞的方式来访问并修改资源。**如果有多个线程修改同一个值，必定会有一个线程能修改成功，而其他修改失败的线程会不断重试直到修改成功**，CAS就是一个无锁的形式。

###### 偏向锁（可关闭）

偏向锁是指一段同步代码仅仅被一个线程所访问时，那么会给对象加偏向锁。简单来说：第一次使用时，使用CAS将线程ID存储到mark word上，之后测试这个锁是自己的就不需要再竞争了。

**加锁**：

1. 访问Mark Word中偏向锁的标识，如果锁标志位（biased_lock）是为0，则说明无锁。将对象头的markword当前线程ID，并执行同步代码块。
2. 如果锁标志位是否为01，为可偏向状态，则测试将Mark Word中线程ID是否指向当前线程 。
   * 如果是，执行同步代码；
   * 如果否，则通过CAS操作竞争偏向锁。如果竞争成功，则将Mark Word中线程ID设置为当前线程ID，然后执行同步代码块，如果竞争失败，则说明有其他线程在使用，执行撤销操作。

**撤销**：有竞争时进行撤销，一旦有了竞争就升级为轻量级锁，他会当到达全局安全点（safepoint）时获得偏向锁的线程被挂起，撤销偏向锁的时候会导致stop the word操作。

**关闭**：有锁的竞争时，偏向锁会多做很多额外操作，尤其是撤销偏向所的时候会导致进入安全点，安全点会导致stw，导致性能下降，这种情况下应当禁用；

- 开启偏向锁：-XX:+UseBiasedLocking -XX:BiasedLockingStartupDelay=0 
- 关闭偏向锁：-XX:-UseBiasedLocking

![](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715094211946.png)

###### 轻量级锁

是指当锁是偏向锁的时候，被另外的线程所访问，偏向锁就会升级为轻量级锁，其他线程会通过自旋的形式尝试获取锁，不会阻塞，从而提高性能。若当前只有一个等待线程，则该线程通过自旋进行等待。但是当自旋超过一定的次数，或者一个线程在持有锁，一个在自旋，又有第三个来访时，轻量级锁升级为重量级锁。

**加锁**：这里涉及到一个锁记录的概念，线程在执行同步代码块之前，每个的栈桢都新建一个锁记录的结构，提前将对象的markword复制到锁记录中，官方称为displaced mark word。然后尝试使用CAS（displaced mark word==markword）将对象头的Markword替换为指向锁记录的指针。

* 如果成功，则执行代码块
* 如果失败，则使用CAS自旋操作来获取锁

**解锁**：使用原子操作的CAS将displaced mark word替换回对象头

* 如果成功，则表示没有竞争发生

  如果失败，则表明当前存在竞争，则升级

![image-20200715100154850](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715100154850.png)

###### 重量级锁

升级为重量级锁时，锁标志的状态值变为“10”，此时Mark Word中存储的是指向重量级锁的指针，此时等待锁的线程都会进入阻塞状态。**详细见monitor**。

![image-20200715100210104](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715100210104.png)



##### [5] synchronized锁升级图解

**偏向锁**

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715102152254.png" alt="image-20200715102152254" style="zoom: 67%;" />

**轻量级**



<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714212157405.png" alt="image-20200714212157405" style="zoom:50%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714212215112.png" alt="image-20200714212215112" style="zoom:50%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714212230614.png" alt="image-20200714212230614" style="zoom: 50%;" />



<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714212256240.png" alt="image-20200714212256240" style="zoom: 50%;" />

![image-20200714212342392](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714212342392.png)

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714212414734.png" alt="image-20200714212414734" style="zoom:50%;" />

**重量级锁**

![image-20200715102846140](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715102846140.png)

![image-20200714221534816](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714221534816.png)



<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714222334799.png" alt="image-20200714222334799" style="zoom: 67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714222358769.png" alt="image-20200714222358769" style="zoom: 67%;" />

##### [6] synchronized锁流程

![å¨è¿éæå¥å¾çæè¿°](https://img-blog.csdnimg.cn/20200603161323889.png)

##### **[7] synchronized锁对比**

| 锁       | 优点                                                         | 缺点                                           | 适用场景                           |
| -------- | ------------------------------------------------------------ | ---------------------------------------------- | ---------------------------------- |
| 偏向锁   | 加锁和解锁不需要额外的消耗，和执行非同步方法相比仅存在纳秒级的差距 | 如果线程间存在锁竞争，会带来额外的锁撤销的消耗 | 适用于只有一个线程访问同步块场景   |
| 轻量级锁 | 竞争的线程不会阻塞，提高了程序的响应速度                     | 如果始终得不到索竞争的线程，使用自旋会消耗CPU  | 追求响应速度，同步块执行速度非常快 |
| 重量级锁 | 线程竞争不使用自旋，不会消耗CPU                              | 线程阻塞，响应时间缓慢                         | 追求吞吐量，同步块执行速度较慢     |

### 【<[CAS](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=_1-cas)>】

##### [1] [什么是CAS?](https://segmentfault.com/q/1010000021946513/a-1020000021946725?sort=created)

**CAS，英文全称compare-and-swap，即比较并交换，是一种乐观锁的思想。**CAS的思想很简单：三个参数，一个当前内存值V、旧的预期值A、即将更新的值B，当且仅当预期值A和内存值V相同时，将内存值修改为B并返回true，否则什么都不做，并返回false。

> 工作内存首先会读取当前内存中将要修改的值，即预期值。然后计算结果值，在修改结果值之前将当前工作内存中的值与预期值对比，如果相等则修改并返回ture，不相等，返回false。（**自旋状态失败下**：从读取预期值开始重复上述步骤。）
>
> **cas里面比较E和当前新值相等后，在修改前有被其他线程修改了怎么办？ 即这里怎么保证这两步之间的原子性的？**
>
> 有个lock指令（**lock cmpxchg**）保证在CPU操作一个格子时其他CPU不能操作它，再底层是lock指令后时候锁定一个北桥电信号,并非总线指令。
>
> https://www.cnblogs.com/yungyu16/p/13200626.html

##### [2] 什么是自旋锁?

**cas**是一种乐观锁机制，cas可以不用自旋机制，失败也可以直接返回false。只是一般应用场景下，cas都会带有重试机制（while和for实现空转，不断尝试）。

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714183000846.png" alt="image-20200714183000846" style="zoom: 33%;" />

~~~java
 //CAS模拟实现
    public class SimulatedCAS {
        private int value;
    
        public synchronized int get() {
            return value;
        }
    
        public synchronized int compareAndSwap(int expectedValue, int newValue) {
            int oldValue = value;
            if (oldValue == expectedValue) {
                value = newValue;
            }
            return oldValue;
        }
    
        public synchronized boolean compareAndSet(int expectedValue, int newValue) {
            return (expectedValue == compareAndSwap(expectedValue, newValue));
        }
    }
~~~

##### **[3] CAS可能出现的问题有什么？**

- **ABA 问题：在读取预期值到将其与现在的值比较的在这段时间里，另一个线程将旧的预期值改为其他值，然后又改回 A（即A->B->A）。那 CAS 操作就会误认为它从来没有被修改过。这个问题被称为 CAS 操作的 "ABA" 问题。**

> ABA问题的解决思路就是使用**版本号机制**，每次更新就把版本号加1，那么**原来的A->B->A就会变为A1->B2->A3**，根据**版本号（时间戳，布尔值）**二次确认值是否被修改过。
>
> JDK 1.5 以后的AtomicStampedReference 类就提供了此种能力，其中的 compareAndSet 方法就是首先检查当前引用是否等于预期引用，并且当前标志是否等于预期标志，如果全部相等，则以原子方式将该引用和该标志的值设置为给定的更新值。
>
> **ABA可能产生问题，也可能不产生问题。**https://blog.csdn.net/superfjj/article/details/106465175

- **循环时间长开销大：自旋 CAS（也就是不成功就一直循环执行直到成功）如果长时间不成功，会给 CPU 带来非常大的执行开销。**

> 如果 JVM 能支持处理器提供的 pause 指令那么效率会有一定的提升，pause 指令有两个作用，第一：它可以延迟流水线执行指令（de-pipeline），使 CPU 不会消耗过多的执行资源，延迟的时间取决于具体实现的版本，在一些处理器上延迟时间是零。第二：它可以避免在退出循环的时候因内存顺序冲突（memory order violation）而引起 CPU 流水线被清空（CPU pipeline flush），从而提高 CPU 的执行效率。

- **只能保证一个共享变量的原子操作：CAS 只对单个共享变量有效，当操作涉及跨多个共享变量时 CAS 无效**。

> 但是从 JDK 1.5 开始，提供了 AtomicReference 类来保证引用对象之间的原子性，你可以把多个变量放在一个对象里来进行 CAS 操作。所以我们**可以使用锁或者利用 AtomicReference 类把多个共享变量合并成一个共享变量来操作（比如i=2，j=a，合并一下ij=2a）。**

##### [4] 哪里有用到CAS？

* **ReenterLock内部的AQS**
* **各种Atomic开头的原子类**
* **synchronized中轻量级锁的加锁和解锁都用到了 CAS 操作。**

##### [5] CAS 和volatile如何实现无锁并发？

CAS 必须借助 volatile 才能读取到共享变量的最新值来实现【**比较并交换**】的效果。

结合 CAS 和 volatile 可以实现无锁并发，适用于线程数少、多核 CPU 的场景下。

CAS 是基于乐观锁的思想：最乐观的估计，不怕别的线程来修改共享变量，就算改了也没关系，我吃亏点再重试呗。
synchronized 是基于悲观锁的思想：最悲观的估计，得防着其它线程来修改共享变量，我上了锁你们都别想改，我改完了解开锁，你们才有机会。
CAS 体现的是无锁并发、无阻塞并发，请仔细体会这两句话的意思。

因为没有使用 synchronized，所以线程不会陷入阻塞，这是效率提升的因素之一但如果竞争激烈，可以想到重试必然频繁发生，反而效率会受影响。

### 【<死锁>】

原文链接：https://blog.csdn.net/hd12370/article/details/82814348

##### [1] 什么是死锁

**死锁，是指多个进程在运行过程中因争夺资源而造成的一种僵局**，当进程处于这种僵持状态时，若无外力作用，它们都将无法再向前推进。 因此我们举个例子来描述，如果此时有一个线程A，按照先锁a再获得锁b的的顺序获得锁，而在此同时又有另外一个线程B，按照先锁b再锁a的顺序获得锁。如下图所示：

<img src="https://img-blog.csdn.net/20180922173936964?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hkMTIzNzA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" alt="img" style="zoom: 67%;" />

##### [2] 产生死锁的原因？

可归结为如下两点：

a. **竞争资源**

系统中的资源可以分为两类：

1. 可剥夺资源，是指某进程在获得这类资源后，该资源可以再被其他进程或系统剥夺，CPU和主存均属于可剥夺性资源；
2. 另一类资源是不可剥夺资源，当系统把这类资源分配给某进程后，再不能强行收回，只能在进程用完后自行释放，如磁带机、打印机等。
   产生死锁中的竞争资源之一指的是竞争不可剥夺资源（例如：系统中只有一台打印机，可供进程P1使用，假定P1已占用了打印机，若P2继续要求打印机打印将阻塞）
   产生死锁中的竞争资源另外一种资源指的是竞争临时资源（临时资源包括硬件中断、信号、消息、缓冲区内的消息等），通常消息通信顺序进行不当，则会产生死锁

 b.  **进程间推进顺序非法**

若P1保持了资源R1,P2保持了资源R2，系统处于不安全状态，因为这两个进程再向前推进，便可能发生死锁
例如，当P1运行到P1：Request（R2）时，将因R2已被P2占用而阻塞；当P2运行到P2：Request（R1）时，也将因R1已被P1占用而阻塞，于是发生进程死锁

##### [3]  死锁的产生必须满足的四个必要条件

死锁是最常见的一种线程活性故障。死锁的起因是**多个线程之间相互等待对方而被永远暂停**（处于Runnable）。死锁的产生必须满足如下**四个必要条件：**

- **资源互斥**：一个资源每次只能被一个线程使用。即进程要求对所分配的资源进行排它性控制，即在一段时间内某资源仅为一进程所占用。
- **请求与保持条件**：一个线程因请求资源而阻塞时，对已获得的资源保持不放，
- **不剥夺条件**：线程已经获得的资源，在未使用完之前，不能强行剥夺，即只能由获得该资源的进程自己来释放（只能是主动释放)。
- **循环等待条件**：若干线程之间形成一种头尾相接的循环等待资源关系

> **总结**：死锁只能发生在像 synchronized 的同步代码块中，一个资源只能被一个线程占用。而且占用资源的锁不会因为请求其他资源失败而主动释放当前锁，已经持有的锁也不能被其他进程剥夺。另外还需要形成一个循环等待的结构，否则它申请的锁有可能被释放。

##### [4] 解决死锁的基本方法

1. **预防死锁----- 确保系统永远不会进入死锁状态**

  产生死锁需要四个条件，那么，只要这四个条件中至少有一个条件得不到满足，就不可能发生死锁了。由于互斥条件是非共享资源所必须的，不仅不能改变，还应加以保证，所以，主要是破坏产生死锁的其他三个条件。
**a、破坏“占有且等待”条件**
     方法1：所有的进程在开始运行之前，必须一次性地申请其在整个运行过程中所需要的全部资源。
         优点：简单易实施且安全。
         缺点：因为某项资源不满足，进程无法启动，而其他已经满足了的资源也不会得到利用，严重降低了资源的利用率，造成资源浪费。
                  使进程经常发生饥饿现象。
     方法2：该方法是对第一种方法的改进，允许进程只获得运行初期需要的资源，便开始运行，在运行过程中逐步释放掉分配到的已经使用完毕的资源，然后再去请求新的资源。这样的话，资源的利用率会得到提高，也会减少进程的饥饿问题。
**b、破坏“不可抢占”条件**
      当一个已经持有了一些资源的进程在提出新的资源请求没有得到满足时，它必须释放已经保持的所有资源，待以后需要使用的时候再重新申请。这就意味着进程已占有的资源会被短暂地释放或者说是被抢占了。
      该种方法实现起来比较复杂，且代价也比较大。释放已经保持的资源很有可能会导致进程之前的工作实效等，反复的申请和释放资源会导致进程的执行被无限的推迟，这不仅会延长进程的周转周期，还会影响系统的吞吐量。
**c、破坏“循环等待”条件**
     可以通过定义资源类型的线性顺序来预防，可将每个资源编号，当一个进程占有编号为i的资源时，那么它下一次申请资源只能申请编号大于i的资源。如图所示：

![img](https://img-blog.csdn.net/2018051322430635)

这样虽然避免了循环等待，但是这种方法是比较低效的，资源的执行速度回变慢，并且可能在没有必要的情况下拒绝资源的访问，比如说，进程c想要申请资源1，如果资源1并没有被其他进程占有，此时将它分配个进程c是没有问题的，但是为了避免产生循环等待，该申请会被拒绝，这样就降低了资源的利用率
————————————————
原文链接：https://blog.csdn.net/guaiguaihenguai/article/details/80303835

2. **避免死锁----- 在使用前进行判断，只允许不会产生死锁的进程申请资源**

预防死锁的几种策略，会严重地损害系统性能。因此在避免死锁时，要施加较弱的限制，从而获得 较满意的系统性能。由于在避免死锁的策略中，允许进程动态地申请资源。因而，系统在进行资源分配之前预先计算资源分配的安全性。若此次分配不会导致系统进入不安全状态，则将资源分配给进程；否则，进程等待。其中最具有代表性的避免死锁算法是银行家算法。

死锁避免是利用额外的检验信息，在分配资源时判断是否会出现死锁，只在不会出现死锁的情况下才分配资源。
两种避免办法：
    1、如果一个进程的**请求**会导致死锁，则不启动该进程
    2、如果一个进程的**增加资源请求**会导致死锁 ，则拒绝该申请。

 **银行家算法**：首先需要定义**状态**和**安全状态**的概念。系统的状态是当前给进程分配的资源情况。因此，状态包含两个向量Resource（系统中每种资源的总量）和Available（未分配给进程的每种资源的总量）及两个矩阵Claim（表示进程对资源的需求）和Allocation（表示当前分配给进程的资源）。安全状态是指至少有一个资源分配序列不会导致死锁。当进程请求一组资源时，假设同意该请求，从而改变了系统的状态，然后确定其结果是否还处于安全状态。如果是，同意这个请求；如果不是，阻塞该进程知道同意该请求后系统状态仍然是安全的。

>**a、银行家算法的相关数据结构**
>**可利用资源向量Available**：用于表示系统里边各种资源剩余的数目。由于系统里边拥有的资源通常都是有很多种（假设有m种），所以，我们用一个有m个元素的数组来表示各种资源。数组元素的初始值为系统里边所配置的该类全部可用资源的数目，其数值随着该类资源的分配与回收动态地改变。
>**最大需求矩阵Max**：用于表示各个进程对各种资源的额最大需求量。进程可能会有很多个（假设为n个），那么，我们就可以用一个nxm的矩阵来表示各个进程多各种资源的最大需求量
>**分配矩阵Allocation**：顾名思义，就是用于表示已经分配给各个进程的各种资源的数目。也是一个nxm的矩阵。
>**需求矩阵Need**：用于表示进程仍然需要的资源数目，用一个nxm的矩阵表示。系统可能没法一下就满足了某个进程的最大需求（通常进程对资源的最大需求也是只它在整个运行周期中需要的资源数目，并不是每一个时刻都需要这么多），于是，为了进程的执行能够向前推进，通常，系统会先分配个进程一部分资源保证进程能够执行起来。那么，进程的最大需求减去已经分配给进程的数目，就得到了进程仍然需要的资源数目了。

**银行家算法通过对进程需求、占有和系统拥有资源的实时统计，确保系统在分配给进程资源不会造成死锁才会给与分配。**
**死锁避免的优点**：不需要死锁预防中的抢占和重新运行进程，并且比死锁预防的限制要少。
**死锁避免的限制**：
    必须事先声明每个进程请求的最大资源量
    考虑的进程必须无关的，也就是说，它们执行的顺序必须没有任何同步要求的限制
    分配的资源数目必须是固定的。
    在占有资源时，进程不能退出
————————————————
原文链接：https://blog.csdn.net/guaiguaihenguai/article/details/80303835

>##### 5. 如何避免死锁的发生？
>
>- **粗锁法：**使用一个粒度粗的锁来消除“请求与保持条件”，缺点是会明显降低程序的并发性能并且会导致资源的浪费。
>- **锁排序法：（必须回答出来的点）指定获取锁的顺序**，比如某个线程只有获得A锁和B锁，才能对某资源进行操作
>
>##### 6. 在多线程条件下，如何避免死锁？
>
>通过指定锁的获取顺序，比如规定，只有获得A锁的线程才有资格获取B锁，按顺序获取锁就可以避免死锁。这通常被认为是解决死锁很好的一种方法。
>
>- 使用**显式锁**中的**ReentrantLock.try(long,TimeUnit)**来申请锁。

3. **检测死锁**

首先为每个进程和每个资源指定一个唯一的号码；

然后建立资源分配表和进程等待表

4. **解除死锁**

**当发现有进程死锁后，便应立即把它从死锁状态中解脱出来**，常采用的方法有：

**剥夺资源**：从其它进程剥夺足够数量的资源给死锁进程，以解除死锁状态；

**撤消进程**：**可以直接撤消死锁进程或撤消代价最小的进程**，直至有足够的资源可用，死锁状态.消除为止；所谓代价是指优先级、运行代价、进程的重要性和价值等。
————————————————
原文链接：https://blog.csdn.net/Beyond_2016/article/details/81363361

##### [5] 说下对悲观锁和乐观锁的理解？

- **悲观锁**

总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁（共享资源每次只给一个线程使用，其它线程阻塞，用完后再把资源转让给其它线程）。传统的关系型数据库里边就用到了很多这种锁机制，比如：行锁、表锁、读锁、写锁等，都是在做操作之前先上锁。Java 中 synchronized 和 ReentrantLock 等独占锁就是悲观锁思想的实现。

- **乐观锁**

总是假设最好的情况，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号机制和 CAS 算法实现。乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库提供的类似于 write_condition 机制，其实都是提供的乐观锁。在 Java 中 java.util.concurrent.atomic 包下面的原子变量类就是使用了乐观锁的一种实现方式 CAS 实现的。

- **两种锁的使用场景**

从上面对两种锁的介绍，我们知道两种锁各有优缺点，不可认为一种好于另一种，像乐观锁适用于写比较少的情况下（多读场景），即冲突真的很少发生的时候，这样可以省去了锁的开销，加大了系统的整个吞吐量。但如果是多写的情况，一般会经常产生冲突，这就会导致上层应用会不断的进行 retry，这样反倒是降低了性能，所以一般多写的场景下用悲观锁就比较合适。

##### [6] 乐观锁常见的两种实现方式是什么？

乐观锁一般会使用版本号机制或者 CAS 算法实现。

- **版本号机制**

  一般是在数据表中加上一个数据版本号 version 字段，表示数据被修改的次数，当数据被修改时，version 值会加 1。当线程 A 要更新数据值时，在读取数据的同时也会读取 version 值，在提交更新时，若刚才读取到的 version 值为当前数据库中的 version 值相等时才更新，否则重试更新操作，直到更新成功。

- **CAS 算法**

  即 compare and swap（比较与交换），是一种有名的无锁算法。无锁编程，即不使用锁的情况下实现多线程之间的变量同步，也就是在没有线程被阻塞的情况下实现变量的同步，所以也叫非阻塞同步（Non-blocking Synchronization）。CAS 算法涉及到三个操作数：

1、需要读写的内存值 V

2、进行比较的值 A

3、拟写入的新值 B

当且仅当 V 的值等于 A 时，CAS 通过原子方式用新值 B 来更新 V 的值，否则不会执行任何操作（比较和替换是一个原子操作）。一般情况下是一个自旋操作，即不断的重试。

### 【<线程锁死>】

##### [1] 什么是线程锁死

线程锁死是另一种常见的线程活性故障，与线程死锁不可以混为一谈。**线程锁死的定义如下：**

**线程锁死是指等待线程由于唤醒其所需的条件永远无法成立，或者其他线程无法唤醒这个线程而一直处于非运行状态（线程并未终止）导致其任务 一直无法进展。**

线程死锁和线程锁死的外部表现是一致的，即故障线程一直处于非运行状态使得其所执行的任务没有进展。但是锁死的产生条件和线程死锁不一样，即使产生死锁的4个必要条件都没有发生，线程锁死仍然可能已经发生。

##### [2] 线程锁死分为哪两种

- **信号丢失锁死：**

信号丢失锁死是因为没有对应的通知线程来将等待线程唤醒，导致等待线程一直处于等待状态。

**典型例子**是等待线程在执行Object.wait( )/Condition.await( )前**没有对保护条件进行判断，而此时保护条件实际上可能已经成立**，此后可能并无其他线程更新相应保护条件涉及的共享变量使其成立并通知等待线程，这就使得等待线程一直处于等待状态，从而使其任务一直无法进展。

- **嵌套监视器锁死：**

嵌套监视器锁死是由于嵌套锁导致等待线程永远无法被唤醒的一种故障。

比如一个线程，只释放了内层锁Y.wait()，但是没有释放外层锁X; 但是通知线程必须先获得外层锁X，才可以通过 Y.notifyAll()来唤醒等待线程，这就导致出现了嵌套等待现象。

##### [3] 活锁

活锁是一种特殊的线程活性故障。当一个线程一直处于运行状态，但是其所执行的任务却没有任何进展称为活锁。比如，一个线程一直在申请其所需要的资源，但是却无法申请成功。

##### [3] 线程饥饿

线程饥饿是指线程一直无法获得其所需的资源导致任务一直无法运行的情况。线程调度模式有公平调度和非公平调度两种模式。**在线程的非公平调度模式下**，就可能出现线程饥饿的情况。

##### [5] 线程活性故障总结

- **线程饥饿发生时，如果线程处于可运行状态，也就是其一直在申请资源，那么就会转变为活锁**
- 只要存在一个或多个线程因为获取不到其所需的资源而无法进展就是线程饥饿，所以**线程死锁其实也算是线程饥饿**

### 【<多线程常用方法>】

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200624193120172.png" alt="image-20200624193120172" style="zoom: 67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200624193146170.png" alt="image-20200624193146170" style="zoom:67%;" />

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200624193216676.png" alt="image-20200624193216676" style="zoom:67%;" />

#####  [1] start 与 run

> https://www.cnblogs.com/agilestyle/p/11421515.html

**start**：用**start方法来启动线程**，真正实现了多线程运行，这时无需等待run方法体代码执行完毕而直接继续执行下面的代码。通过调用Thread类的start()方法来启动一个线程，这时此线程处于就绪（可运行）状态，并没有运行，一旦得到cpu时间片，就开始执行run()方法，这里方法run()称为线程体，它包含了要执行的这个线程的内容，run方法运行结束，此线程随即终止。

 **run** ：**run()方法只是类的一个普通方法**而已，如果直接调用Run方法，程序中依然只有主线程这一个线程，其程序执行路径还是只有一条，还是要顺序执行，还是要等待run方法体执行完毕后才可继续执行下面的代码，这样就没有达到写线程的目的。

>https://blog.csdn.net/kwame211/article/details/79030255
>
>1. 使用**start()方法**，是真的启动了相应的线程0-9，而使用run()方法并没有真的启动线程，而是由一个叫main的主线程去调用的run()方法。
>2. 所以，正确启动线程的方式是使用**start()**方法。

##### [2] sleep 与 yield

**sleep()**

1.	调用 sleep 会让当前线程从 Running  进入 Timed Waiting 状态（阻塞）
2.	其它线程可以使用  interrupt 方法打断正在睡眠的线程，这时 sleep 方法会抛出 InterruptedException
3.	睡眠结束后的线程未必会立刻得到执行
4.	建议用 TimeUnit 的 sleep 代替 Thread 的 sleep 来获得更好的可读性

**yield()**：

对静态方法 Thread.yield() 的调用声明了当前线程已经完成了生命周期中最重要的部分，可以切换给其它线程来执行。该方法只是对线程调度器的一个建议，而且也只是**建议具有相同优先级的其它线程可以运行**。

1.	调用 yield 会让当前线程从 Running 进入 Runnable  就绪状态，然后调度执行其它线程
2.	具体的实现依赖于操作系统的任务调度器

>线程优先级会提示（hint）调度器优先调度该线程，但它仅仅是一个提示，调度器可以忽略它如果 cpu 比较忙，那么优先级高的线程会获得更多的时间片，但 cpu 闲时，优先级几乎没作用

##### [3] sleep 和 wait 

- **sleep方法：**是Thread类的静态方法，当前线程将睡眠n毫秒，线程进入阻塞状态。当睡眠时间到了，会解除阻塞，进入可运行状态，等待CPU的到来。睡眠不释放锁（如果有的话）。
- **wait方法：**是Object的方法，必须与synchronized关键字一起使用，线程进入阻塞状态，当notify或者notifyall被调用后，会解除阻塞。但是，只有**重新占用互斥锁**之后才会进入可运行状态。睡眠时，会释放互斥锁。

##### [4] **Daemon**

默认情况下，Java 进程需要等待所有线程都运行结束，才会结束。有一种特殊的线程叫做守护线程，只要其它非守护线程运行结束了，即使守护线程的代码没有执行完，也会强制结束。

~~~java
package cn.mycast;

import lombok.extern.slf4j.Slf4j;

import static cn.itcast.n2.util.Sleeper.sleep;


@Slf4j(topic= "c.守护线程")
public class 守护线程 {
    public static void main(String[] args) {
        //方法1
        Thread t1 = new Thread(()-> {
                sleep(2);
                log.debug("hello");
        });
        t1.setDaemon(true);
        t1.start();
        sleep(1);
        log.debug("运行结束...");
    }
}
~~~

##### [5] join和yield 

**join 方法：**当前线程调用，则其它线程全部停止，等待当前线程执行完毕，接着执行（**即调用此方法的线程必须加入**）。

**yield 方法：**该方法使得线程放弃当前分得的 CPU 时间。但是不使线程阻塞，即线程仍处于可执行状态，随时可能再次分得 CPU 时间。yield()做的是让当前运行线程回到可运行状态，以允许具有相同优先级的其他线程获得运行机会。因此，使用yield()的目的是让相同优先级的线程之间能适当的轮转执行。
**但是，实际中无法保证yield()达到让步目的，因为让步的线程还有可能被线程调度程序再次选中。**
所以，该方法只是对线程调度器的一个建议，而且也只是**建议具有相同优先级的其它线程可以运行**。

##### [6] wait() notify() notifyAll()

调用 wait() 使得线程等待某个条件满足，线程在等待时会被挂起，当其他线程的运行使得这个条件满足时，其它线程会调用 notify() 或者 notifyAll() 来唤醒挂起的线程。

> 注意：
>
> 1. 它们都属于 Object 的一部分，而不属于 Thread。
> 2. 只能用在同步方法或者同步控制块中使用，否则会在运行时抛出 IllegalMonitorStateException。
> 3. 使用 wait() 挂起期间，线程会释放锁。这是因为，**如果没有释放锁，那么其它线程就无法进入对象的同步方法或者同步控制块中，那么就无法执行 notify() 或者 notifyAll() 来唤醒挂起的线程，造成死锁**。

##### [7] await() signal() signalAll()

**await() signal() signalAll()--多线程的协调**。java.util.concurrent 类库中提供了 Condition 类来实现线程之间的协调，可以在 Condition 上调用 await() 方法使线程等待，其它线程调用 signal() 或 signalAll() 方法唤醒等待的线程。

相比于 wait() 这种等待方式，**await() 可以指定等待的条件**，因此更加灵活。

使用 Lock 来获取一个 Condition 对象。

##### [8] InterruptedException

**InterruptedException--中断机制**，通过调用一个线程的 interrupt() 来中断该线程，如果该线程处于**阻塞、限期等待或者无限期等待状态**，那么就会抛出 InterruptedException，从而提前结束该线程。但是不能中断 I/O 阻塞和 synchronized 锁阻塞。

对于以下代码，在 main() 中启动一个线程之后再中断它，由于线程中调用了 Thread.sleep() 方法，因此会抛出一个 InterruptedException，从而提前结束线程，不执行之后的语句。

~~~java
try {
                Thread.sleep(2000);
                System.out.println("Thread run");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
~~~

##### [9] interrupted()

**interrupted()--中断机制**，如果一个线程的 run() 方法执行一个无限循环，并且没有执行 sleep() 等会抛出 InterruptedException 的操作，那么调用线程的 interrupt() 方法就无法使线程提前结束。

但是调用 interrupt() 方法会设置线程的中断标记，此时调用 interrupted() 方法会返回 true。因此可以**在循环体中**使用 interrupted() 方法来判断线程是否处于中断状态，从而提前结束线程。

##### [10] Executor

Executor 管理多个异步任务的执行，而无需程序员显式地管理线程的生命周期。这里的异步是指多个任务的执行互不干扰，不需要进行同步操作。主要有三种 Executor：

- CachedThreadPool：一个任务创建一个线程；
- FixedThreadPool：所有任务只能使用固定大小的线程；
- SingleThreadExecutor：相当于大小为 1 的 FixedThreadPool。

##### [11] CopyOnWriteArrayList

CopyOnWriteArraySet 是它的马甲 底层实现采用了 **写入时拷贝** 的思想，增删改操作会将底层数组拷贝一份，修改完毕后，再原子性时候修改共享访问的变量，让它指向新的对象。更改操作在新数组上执行，这时不影响其它线程的并发读，读写分离。

### 【ReentrantLock】

Java 提供了两种锁机制来控制多个线程对共享资源的互斥访问，第一个是 JVM 实现的 synchronized，而另一个是 JDK 实现的 ReentrantLock。

ReentrantLock ，re: 可重新  entrant：进入  Lock：锁 ，所以他就是可冲入锁

##### [1] ReentrantLock简介

ReentrantLock 是 java.util.concurrent（J.U.C）包中的锁。相对于 synchronized 它具备如下特点：

* **可重入（）**：是指同一个线程如果首次获得了这把锁，那么因为它是这把锁的拥有者，因此有权利再次获取这把锁如果是不可重入锁，那么第二次获得锁时，自己也会被锁挡住
* **可中断**：如果是不可中断模式，那么即使使用了 interrupt 也不会让等待中断
* **可以设置超时时间**
* **可以设置为公平锁**
* **支持多个条件变量**：synchronized 中也有条件变量，就是我们讲原理时那个 waitSet 休息室，当条件不满足时进入 waitSet 等待ReentrantLock 的条件变量比 synchronized 强大之处在于，它是支持多个条件变量的。

~~~java
public class LockExample {

    private Lock lock = new ReentrantLock();

    public void func() {
        lock.lock();
        try {
            for (int i = 0; i < 10; i++) {
                System.out.print(i + " ");
            }
        } finally {
            lock.unlock(); // 确保释放锁，从而避免发生死锁。
        }
    }
}
~~~



##### [2] ReentrantLock方法

* **加锁**

  ReentrantLock 类提供了最基本的加锁和解锁方法：

  ~~~java
  public void lock();
  ~~~

  ~~~java
  class Counter {
      private static int counter = 0;
      private static ReentrantLock lock = new ReentrantLock();
  
      public static int getCounter() {
          return counter;
      }
  
      public static void increase() {
          try {
              lock.lock();
              counter++;
          } finally {
              lock.unlock();
          }
      }
  
      private Counter() {};
  }
  ~~~

  这个方法保证了线程安全，他和 synchronized 关键字实现了相同的效果：

  ~~~java
  class Counter {
      private static int counter = 0;
  
      public static int getCounter() {
          return counter;
      }
  
      public synchronized static void increase() {
          counter++;
      }
  
      private Counter() {};
  }
  ~~~

  显然，synchronized 关键字的实现更为简洁和清晰，同时，如果 ReentrantLock 忘记调用 unlock 方法将会造成死锁，这是必须要注意的一点

  因此，如果仅仅是想要进行上面代码中这样的加锁和解锁，synchronized 还是最好的选择

* **可重入**

  默认可重入

* **可中断**

  ~~~java
  public void lockInterruptibly()	// 可中断锁，调用线程 interrupt 方法，则锁方法抛出 InterruptedException
  ~~~

* **可以设置超时时间**

  ~~~java
  public boolean tryLock(long timeout, TimeUnit unit)	// 尝试获取锁，最多等待 timeout 时长
  ~~~

* **可以设置为公平锁**：

  使用 synchronized 锁是不保证等待的线程获取到锁的顺序的，这就是非公平锁，除了默认的非公平锁构造方法外，ReentrantLock 还提供了一个带有 boolean 参数的构造方法：

  ~~~java
  public ReentrantLock(boolean fair);
  ~~~

  如果传入参数为 true，则会创建公平锁，所谓的公平锁，就是保证了先进入等待的线程一定先获取到锁

  可以通过 isFair 方法查询 ReentrantLock 对象是否是公平锁：

  ~~~java
  public final boolean isFair();
  ~~~

* **支持多个条件变量**

​      通过 newCondition 方法，可以创建出 Condition 对象

​      Condition 接口提供了如下的方法：

~~~java
void await();								// 可被中断的等待
boolean await(long time, TimeUnit unit);	// 最多等待 time 时长的可中断等待
long awaitNanos(long nanosTimeout);			// 最多等待 nanosTimeout 毫秒的可中断等待
boolean awaitUntil(Date deadline);			// 等待直到指定时间的可中断等待
void awaitUninterruptibly();				// 不可中断的等待
void signal();								// 唤醒一个线程
void signalAll();							// 唤醒所有等待中的线程
~~~

上面的五个等待方法中，除了 awaitUninterruptibly 方法，其他四个都可以被 interrupt 方法中断，而 signal 和 signalAll 方法可以中断上述所有等待方法

但是，signal 和 signalAll 方法只能唤醒通过当前 Condition 对象调用过等待方法的线程

基于上述特性，我们可以精准的控制让某个指定的线程被唤醒，而 Object 的 notify、notifyAll 方法的唤醒则是随机的，同一个 ReentrantLock 每次调用 newCondition 方法都将获得不同的 Condition 对象

* **查询接口**

~~~java
int getHoldCount();		// 获取当前线程持有该锁的次数
boolean isHeldByCurrentThread();	// 判断当前线程是否持有该锁
boolean isLocked();		// 获取锁状态是否为加锁状态
boolean isFair();		// 当前锁是否是公平锁
Thread getOwner();		// 获取持有锁的线程
boolean hasQueuedThreads();			// 判断当前锁是否有线程在等待
boolean hasQueuedThread(Thread thread);	// 判断指定线程是否在等待该锁
int getQueueLength();	// 获取正在等待该锁的线程数量
boolean hasWaiters(Condition condition);	// 判断是否有线程等待在该 Condition 对象上
int getWaitQueueLength(Condition condition);	// 获取等待在该 Condition 对象的线程数
~~~

##### [3] ReentrantLock实战

**加锁及其解锁：**

```java
class Counter {
    private static int counter = 0;
    private static ReentrantLock lock = new ReentrantLock();
public static int getCounter() {
    return counter;
}

public static void increase() {
    try {
        lock.lock();
        counter++;
    } finally {
        lock.unlock();
    }
}

private Counter() {};
    }
```

https://baijiahao.baidu.com/s?id=1648624077736116382&wfr=spider&for=pc

**可重入**：可重入是指同一个线程如果首次获得了这把锁，那么因为它是这把锁的拥有者，因此有权利再次获取这把锁

如果是不可重入锁，那么第二次获得锁时，自己也会被锁挡住

~~~java
static ReentrantLock lock = new ReentrantLock();
public static void main(String[] args) {
 method1();
}
public static void method1() {
 lock.lock();
 try {
 log.debug("execute method1");
 method2();
 } finally {
 lock.unlock();
 }
}
public static void method2() {
 lock.lock();
 try {
 log.debug("execute method2");
 method3();
 } finally {
 lock.unlock();
 }
}
public static void method3() {
 lock.lock();
 try {
 log.debug("execute method3");
 } finally {
 lock.unlock();
 }
}
~~~

![image-20200716080920156](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716080920156.png)

**可打断**：

~~~java
ReentrantLock lock = new ReentrantLock();
Thread t1 = new Thread(() -> {
北京市昌平区建材城西路金燕龙办公楼一层 电话：400-618-9090
 log.debug("启动...");
 try {
 lock.lockInterruptibly();
 } catch (InterruptedException e) {
 e.printStackTrace();
 log.debug("等锁的过程中被打断");
 return;
 }
 try {
 log.debug("获得了锁");
 } finally {
 lock.unlock();
 }
}, "t1");
lock.lock();
log.debug("获得了锁");
t1.start();
try {
 sleep(1);
 t1.interrupt();
 log.debug("执行打断");
} finally {
 lock.unlock();
}
~~~

![image-20200716080945053](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716080945053.png)

可超时：

~~~java
ReentrantLock lock = new ReentrantLock();
Thread t1 = new Thread(() -> {
 log.debug("启动...");
 if (!lock.tryLock()) {
 log.debug("获取立刻失败，返回");
 return;
 }
 try {
 log.debug("获得了锁");
 } finally {
 lock.unlock();
 }
}, "t1");
lock.lock();
log.debug("获得了锁");
t1.start();
try {
 sleep(2);
} finally {
 lock.unlock();
}
~~~

![image-20200716080851608](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716080851608.png)

**公平锁：**

~~~java
ReentrantLock lock = new ReentrantLock(false);
lock.lock();
for (int i = 0; i < 500; i++) {
 new Thread(() -> {
 lock.lock();
 try {
 System.out.println(Thread.currentThread().getName() + " running...");
 } finally {
 lock.unlock();
 }
 }, "t" + i).start();
}
// 1s 之后去争抢锁
Thread.sleep(1000);
new Thread(() -> {
 System.out.println(Thread.currentThread().getName() + " start...");
 lock.lock();
 try {
 System.out.println(Thread.currentThread().getName() + " running...");
 } finally {
 lock.unlock();
 }
}, "强行插入").start();
lock.unlock()
~~~

![image-20200716080827688](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716080827688.png)

**条件变量**

synchronized 中也有条件变量，就是我们讲原理时那个 waitSet 休息室，当条件不满足时进入 waitSet 等待

ReentrantLock 的条件变量比 synchronized 强大之处在于，它是支持多个条件变量的，这就好比

synchronized 是那些不满足条件的线程都在一间休息室等消息

**而 ReentrantLock 支持多间休息室，有专门等烟的休息室、专门等早餐的休息室、唤醒时也是按休息室来唤**

**醒**

使用要点：

await 前需要获得锁

await 执行后，会释放锁，进入 conditionObject 等待

await 的线程被唤醒（或打断、或超时）取重新竞争 lock 锁

竞争 lock 锁成功后，从 await 后继续执行

~~~java
static ReentrantLock lock = new ReentrantLock();
static Condition waitCigaretteQueue = lock.newCondition();
static Condition waitbreakfastQueue = lock.newCondition();
static volatile boolean hasCigrette = false;
static volatile boolean hasBreakfast = false;
public static void main(String[] args) {
 new Thread(() -> {
 try {
 lock.lock();
 while (!hasCigrette) {
      try {
 waitCigaretteQueue.await();
 } catch (InterruptedException e) {
 e.printStackTrace();
 }
 }
 log.debug("等到了它的烟");
 } finally {
 lock.unlock();
 }
 }).start();
 new Thread(() -> {
 try {
 lock.lock();
 while (!hasBreakfast) {
 try {
 waitbreakfastQueue.await();
 } catch (InterruptedException e) {
 e.printStackTrace();
 }
 }
 log.debug("等到了它的早餐");
 } finally {
 lock.unlock();
 }
 }).start();
 sleep(1);
 sendBreakfast();
 sleep(1);
 sendCigarette();
}
private static void sendCigarette() {
 lock.lock();
 try {
 log.debug("送烟来了");
 hasCigrette = true;
 waitCigaretteQueue.signal();
 } finally {
 lock.unlock();
 }
}
private static void sendBreakfast() {
 lock.lock();
 try {
 log.debug("送早餐来了");
 hasBreakfast = true;
 waitbreakfastQueue.signal();
 } finally {
 lock.unlock();
      }
}

~~~

![image-20200716080757372](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716080757372.png)

##### [4] ReentrantLock原理

**如何实现一个锁?**

实现一个锁，主要需要考虑2个问题

1. **如何线程安全的修改锁状态位？**
2. **得不到锁的线程，如何排队？**

带着这2个问题，我们看一下JUC中的ReentrantLock是如何做的？

ReentrantLock类的大部分逻辑，都是其均继承自AQS的内部类Sync实现的

**如何线程安全的修改锁状态位？**

**锁状态位的修改主要通过，内部类Sync实现的，们可以发现线程安全的关键在于：<font color="#dd0000">volatile变量</font>和<font color="#dd0000">CAS原语</font>的配合使用**

```java
    public abstract class AbstractQueuedSynchronizer{
         //锁状态标志位：volatile变量（多线程间通过此变量判断锁的状态）
          private volatile int state;
         
          protected final int getState() {
                 return state;
          }

 
         protected final void setState(int newState) {
              state = newState;
         }

    }
  
    abstract static  Sync extends AbstractQueuedSynchronizer {
    
        
         final boolean nonfairTryAcquire(int acquires) {
            final Thread current = Thread.currentThread();
            //volatile读，确保了锁状态位的内存可见性
            int c = getState();
            //锁还没有被其他线程占用
            if (c == 0) {
                //此时，如果多个线程同时进入，CAS操作会确保，只有一个线程修改成功
                if (compareAndSetState(0, acquires)) {
                    //设置当前线程拥有独占访问权
                    setExclusiveOwnerThread(current);
                    return true;
                }
            }
            //当前线程就是拥有独占访问权的线程，即锁重入
            else if (current == getExclusiveOwnerThread()) {
                //重入锁计数+1
                int nextc = c + acquires;
                if (nextc < 0) //溢出
                    throw new Error("Maximum lock count exceeded");
                //只有获取锁的线程，才能进入此段代码，因此只需要一个volatile写操作，确保其内存可见性即可
                setState(nextc);
                return true;
            }
            return false;
        }
        
        //只有获取锁的线程才会执行此方法，因此只需要volatile读写确保内存可见性即可
        protected final boolean tryRelease(int releases) {
            //锁计数器-1
            int c = getState() - releases;
            if (Thread.currentThread() != getExclusiveOwnerThread())
                throw new IllegalMonitorStateException();
            boolean free = false;
            //锁计数器为0，说明锁被释放
            if (c == 0) {
                free = true;
                setExclusiveOwnerThread(null);
            }
            setState(c);
            return free;
        }
    }
   
```

**得不到锁的线程，如何排队？**

JUC中锁的排队策略，是基于CLH队列的变种实现的。因此，我们先看看啥是CLH队列

![img](https:////upload-images.jianshu.io/upload_images/6283837-a868311ecafbc2b4.png?imageMogr2/auto-orient/strip|imageView2/2/w/844/format/webp)



如上图所示，**获取不到锁的线程，会进入队尾，然后自旋，直到其前驱线程释放锁。**

 这样做的好处：假设有1000个线程等待获取锁，锁释放后，只会通知队列中的第一个线程去竞争锁，减少了并发冲突。（ZK的分布式锁，为了避免惊群效应，也使用了类似的方式：获取不到锁的线程只监听前一个节点）

为什么说JUC中的实现是基于CLH的“变种”，因为原始CLH队列，一般用于实现自旋锁。而JUC中的实现，获取不到锁的线程，一般会时而阻塞，时而唤醒。



##### [11] ReentrantLock如何实现可重入锁？

可重入锁的实现原理：

**如果当前锁的状态不为0，表示有线程占有该锁。再判断如果当前线程就是占有这个锁的线程，修改当前线程的同步状态值，同步状态加1，这样就实现了可重入。**
**每次重新获取都会对同步状态进行加一的操作，那么释放的时候处理思路是怎样的了？释放锁会调用unlock方法，内部有一个tryRelease方法，每释放一次锁同步状态减1，只有当同步状态为0时，锁成功被释放，返回true。**

~~~java
static final class NonfairSync extends Sync {
 // ...
 
 // Sync 继承过来的方法, 方便阅读, 放在此处
 final boolean nonfairTryAcquire(int acquires) {
 final Thread current = Thread.currentThread();
 int c = getState();
 if (c == 0) {
 if (compareAndSetState(0, acquires)) {
 setExclusiveOwnerThread(current);
 return true;
 }
 }
 // 如果已经获得了锁, 线程还是当前线程, 表示发生了锁重入
 else if (current == getExclusiveOwnerThread()) {
 // state++
 int nextc = c + acquires;
 if (nextc < 0) // overflow
 throw new Error("Maximum lock count exceeded");
 setState(nextc);
 return true;
 }
 return false;
 }
 
 // Sync 继承过来的方法, 方便阅读, 放在此处
 protected final boolean tryRelease(int releases) {
 // state-- 
 int c = getState() - releases;
 if (Thread.currentThread() != getExclusiveOwnerThread())
 throw new IllegalMonitorStateException();
 boolean free = false;
 // 支持锁重入, 只有 state 减为 0, 才释放成功
 if (c == 0) {
 free = true;
 setExclusiveOwnerThread(null);
 }
 setState(c);
 return free;
 }
}
~~~

##### [12] ReentrantLock如何实现公平锁和非公平锁？

总结：公平锁和非公平锁**(默认)**只有两处不同：

**非公平：**

1. 调用lock()方法时，首先去通过CAS尝试设置锁资源的state变量，如果设置成功，则设置当前持有锁资源的线程为当前请求线程
2. 调用tryAcquire方法时，首先获取当前锁资源的state变量，如果为0，则通过CAS去尝试设置state，如果设置成功，则设置当前持有锁资源的线程为当前请求线程

**以上两步都属于插队现象，可以提高系统吞吐量**

**公平：**
1.调用lock()方法时，不进行CAS尝试
2.调用tryAcuqire方法时，首先获取当前锁资源的state变量，如果为0，则**判断该节点是否是头节点可以去获取锁资源，如果可以才通过CAS去尝试设置state**

上面通过判断该线程是否是队列的头结点，从而保证公平性

```
public ReentrantLock() {
    sync = new NonfairSync();
}
public ReentrantLock(boolean fair) {
    sync = fair ? new FairSync() : new NonfairSync();
}
```

公平锁的 lock 方法：

```
static final class FairSync extends Sync {
    final void lock() {
        acquire(1);
    }
    // AbstractQueuedSynchronizer.acquire(int arg)
    public final void acquire(int arg) {
        if (!tryAcquire(arg) &&
            acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
            selfInterrupt();
    }
    protected final boolean tryAcquire(int acquires) {
        final Thread current = Thread.currentThread();
        int c = getState();
        if (c == 0) {
            // 1. 和非公平锁相比，这里多了一个判断：是否有线程在等待
            if (!hasQueuedPredecessors() &&
                compareAndSetState(0, acquires)) {
                setExclusiveOwnerThread(current);
                return true;
            }
        }
        else if (current == getExclusiveOwnerThread()) {
            int nextc = c + acquires;
            if (nextc < 0)
                throw new Error("Maximum lock count exceeded");
            setState(nextc);
            return true;
        }
        return false;
    }
}
```

非公平锁的 lock 方法：

```
static final class NonfairSync extends Sync {
    final void lock() {
        // 2. 和公平锁相比，这里会直接先进行一次CAS，成功就返回了
        if (compareAndSetState(0, 1))
            setExclusiveOwnerThread(Thread.currentThread());
        else
            acquire(1);
    }
    // AbstractQueuedSynchronizer.acquire(int arg)
    public final void acquire(int arg) {
        if (!tryAcquire(arg) &&
            acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
            selfInterrupt();
    }
    protected final boolean tryAcquire(int acquires) {
        return nonfairTryAcquire(acquires);
    }
}
/**
 * Performs non-fair tryLock.  tryAcquire is implemented in
 * subclasses, but both need nonfair try for trylock method.
 */
final boolean nonfairTryAcquire(int acquires) {
    final Thread current = Thread.currentThread();
    int c = getState();
    if (c == 0) {
        if (compareAndSetState(0, acquires)) {
            setExclusiveOwnerThread(current);
            return true;
        }
    }
    else if (current == getExclusiveOwnerThread()) {
        int nextc = c + acquires;
        if (nextc < 0) // overflow
            throw new Error("Maximum lock count exceeded");
        setState(nextc);
        return true;
    }
    return false;
}
```

##### [8] 条件变量Condition实现原理？

**Condition的作用和Object.wait()和Object.notify()的作用相同，可以使当前线程阻塞和唤醒。只不过condition需要与reentrantlock配合使用，而wait/notify需要与snychronized配合使用。**

通过Lock接口（重入锁实现了这一接口）的new Condition()方法可以生成一个与当前重入锁绑定的Condition实例，**每个条件变量其实就对应着一个等待队列**，其实现类是 ConditionObject。

**condition常用的方法：**

* await()方法会使当前线程等待，同时释放当前锁,当其他线程中使用signal()或signalAll()方法时，线程会重新获得锁并继续执行。或者当其他线程被中断时，也能跳出等待。这和Object.wait()很相似。
* awaitUninterruptibly()与await()方法基本相同，但他并不会在中断过程中响应中断。
* signal()方法用于唤醒一个在等待中的线程。相对的signalAll()方法会唤醒所有在等待中的线程。这和Object.notifyAll()很类似。

**await** **流程**：

![image-20200716144925408](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716144925408.png)

![image-20200716144941742](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716144941742.png)

![image-20200716145003743](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716145003743.png)

![image-20200716145017143](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716145017143.png)

![](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716145225664.png)

![image-20200716145341008](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716145341008.png)

![image-20200716145416997](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716145416997.png)

~~~java
public class ConditionObject implements Condition, java.io.Serializable {
 private static final long serialVersionUID = 1173984872572414699L;
 
 // 第一个等待节点
 private transient Node firstWaiter;
 
 // 最后一个等待节点
 private transient Node lastWaiter;
 public ConditionObject() { }
 // ㈠ 添加一个 Node 至等待队列
 private Node addConditionWaiter() {
 Node t = lastWaiter;
 // 所有已取消的 Node 从队列链表删除, 见 ㈡
 if (t != null && t.waitStatus != Node.CONDITION) {
 unlinkCancelledWaiters();
 t = lastWaiter;
 }
 // 创建一个关联当前线程的新 Node, 添加至队列尾部
 Node node = new Node(Thread.currentThread(), Node.CONDITION);
 if (t == null)
 firstWaiter = node;
 else
 t.nextWaiter = node;
 lastWaiter = node;
 return node;
 }
 // 唤醒 - 将没取消的第一个节点转移至 AQS 队列
 private void doSignal(Node first) {
 do {
 // 已经是尾节点了
 if ( (firstWaiter = first.nextWaiter) == null) {
 lastWaiter = null;
 }
 first.nextWaiter = null;
 } while (
 // 将等待队列中的 Node 转移至 AQS 队列, 不成功且还有节点则继续循环 ㈢
 !transferForSignal(first) &&
 // 队列还有节点
 (first = firstWaiter) != null
 );
 }
 
 // 外部类方法, 方便阅读, 放在此处
 // ㈢ 如果节点状态是取消, 返回 false 表示转移失败, 否则转移成功
 final boolean transferForSignal(Node node) {
 // 如果状态已经不是 Node.CONDITION, 说明被取消了
 if (!compareAndSetWaitStatus(node, Node.CONDITION, 0))
 return false;
 // 加入 AQS 队列尾部
 Node p = enq(node);
 int ws = p.waitStatus;
 if (
 // 上一个节点被取消
 ws > 0 ||
 // 上一个节点不能设置状态为 Node.SIGNAL
 !compareAndSetWaitStatus(p, ws, Node.SIGNAL) 
 ) {
 // unpark 取消阻塞, 让线程重新同步状态
 LockSupport.unpark(node.thread);
 }
 return true;
 }
 // 全部唤醒 - 等待队列的所有节点转移至 AQS 队列
北京市昌平区建材城西路金燕龙办公楼一层 电话：400-618-9090
 private void doSignalAll(Node first) {
 lastWaiter = firstWaiter = null;
 do {
 Node next = first.nextWaiter;
 first.nextWaiter = null;
 transferForSignal(first);
 first = next;
 } while (first != null);
 }
 
 // ㈡
 private void unlinkCancelledWaiters() {
 // ...
 }
 // 唤醒 - 必须持有锁才能唤醒, 因此 doSignal 内无需考虑加锁
 public final void signal() {
 if (!isHeldExclusively())
 throw new IllegalMonitorStateException();
 Node first = firstWaiter;
 if (first != null)
 doSignal(first);
 }
 // 全部唤醒 - 必须持有锁才能唤醒, 因此 doSignalAll 内无需考虑加锁
 public final void signalAll() {
 if (!isHeldExclusively())
 throw new IllegalMonitorStateException();
 Node first = firstWaiter;
 if (first != null)
 doSignalAll(first);
 }
 // 不可打断等待 - 直到被唤醒
 public final void awaitUninterruptibly() {
 // 添加一个 Node 至等待队列, 见 ㈠
 Node node = addConditionWaiter();
 // 释放节点持有的锁, 见 ㈣
 int savedState = fullyRelease(node);
 boolean interrupted = false;
 // 如果该节点还没有转移至 AQS 队列, 阻塞
 while (!isOnSyncQueue(node)) {
 // park 阻塞
 LockSupport.park(this);
 // 如果被打断, 仅设置打断状态
 if (Thread.interrupted())
 interrupted = true;
 }
 // 唤醒后, 尝试竞争锁, 如果失败进入 AQS 队列
 if (acquireQueued(node, savedState) || interrupted)
 selfInterrupt();
 }
 
北京市昌平区建材城西路金燕龙办公楼一层 电话：400-618-9090
 // 外部类方法, 方便阅读, 放在此处
 // ㈣ 因为某线程可能重入，需要将 state 全部释放
 final int fullyRelease(Node node) {
 boolean failed = true;
 try {
 int savedState = getState();
 if (release(savedState)) {
 failed = false;
 return savedState;
 } else {
 throw new IllegalMonitorStateException();
 }
 } finally {
 if (failed)
 node.waitStatus = Node.CANCELLED;
 }
 }
 // 打断模式 - 在退出等待时重新设置打断状态
 private static final int REINTERRUPT = 1;
 // 打断模式 - 在退出等待时抛出异常
 private static final int THROW_IE = -1;
 // 判断打断模式
 private int checkInterruptWhileWaiting(Node node) {
 return Thread.interrupted() ?
 (transferAfterCancelledWait(node) ? THROW_IE : REINTERRUPT) :
 0;
 }
 // ㈤ 应用打断模式
 private void reportInterruptAfterWait(int interruptMode)
 throws InterruptedException {
 if (interruptMode == THROW_IE)
 throw new InterruptedException();
 else if (interruptMode == REINTERRUPT)
 selfInterrupt();
 }
 // 等待 - 直到被唤醒或打断
 public final void await() throws InterruptedException {
 if (Thread.interrupted()) {
 throw new InterruptedException();
 }
 // 添加一个 Node 至等待队列, 见 ㈠
 Node node = addConditionWaiter();
 // 释放节点持有的锁
 int savedState = fullyRelease(node);
 int interruptMode = 0;
 // 如果该节点还没有转移至 AQS 队列, 阻塞
 while (!isOnSyncQueue(node)) {
 // park 阻塞
 LockSupport.park(this);
北京市昌平区建材城西路金燕龙办公楼一层 电话：400-618-9090
 // 如果被打断, 退出等待队列
 if ((interruptMode = checkInterruptWhileWaiting(node)) != 0)
 break;
 }
 // 退出等待队列后, 还需要获得 AQS 队列的锁
 if (acquireQueued(node, savedState) && interruptMode != THROW_IE)
 interruptMode = REINTERRUPT;
 // 所有已取消的 Node 从队列链表删除, 见 ㈡
 if (node.nextWaiter != null) 
 unlinkCancelledWaiters();
 // 应用打断模式, 见 ㈤
 if (interruptMode != 0)
 reportInterruptAfterWait(interruptMode);
 }
 // 等待 - 直到被唤醒或打断或超时
 public final long awaitNanos(long nanosTimeout) throws InterruptedException {
 if (Thread.interrupted()) {
 throw new InterruptedException();
 }
 // 添加一个 Node 至等待队列, 见 ㈠
 Node node = addConditionWaiter();
 // 释放节点持有的锁
 int savedState = fullyRelease(node);
 // 获得最后期限
 final long deadline = System.nanoTime() + nanosTimeout;
 int interruptMode = 0;
 // 如果该节点还没有转移至 AQS 队列, 阻塞
 while (!isOnSyncQueue(node)) {
 // 已超时, 退出等待队列
 if (nanosTimeout <= 0L) {
 transferAfterCancelledWait(node);
 break;
 }
 // park 阻塞一定时间, spinForTimeoutThreshold 为 1000 ns
 if (nanosTimeout >= spinForTimeoutThreshold)
 LockSupport.parkNanos(this, nanosTimeout);
 // 如果被打断, 退出等待队列
 if ((interruptMode = checkInterruptWhileWaiting(node)) != 0)
 break;
 nanosTimeout = deadline - System.nanoTime();
 }
 // 退出等待队列后, 还需要获得 AQS 队列的锁
 if (acquireQueued(node, savedState) && interruptMode != THROW_IE)
 interruptMode = REINTERRUPT;
 // 所有已取消的 Node 从队列链表删除, 见 ㈡
 if (node.nextWaiter != null)
 unlinkCancelledWaiters();
 // 应用打断模式, 见 ㈤
 if (interruptMode != 0)
 reportInterruptAfterWait(interruptMode);
 return deadline - System.nanoTime();
 }
 // 等待 - 直到被唤醒或打断或超时, 逻辑类似于 awaitNanos
 public final boolean awaitUntil(Date deadline) throws InterruptedException {
 // ...
 }
 // 等待 - 直到被唤醒或打断或超时, 逻辑类似于 awaitNanos
 public final boolean await(long time, TimeUnit unit) throws InterruptedException {
 // ...
 }
 // 工具方法 省略 ...
}
~~~



##### [11] **谈谈 synchronized 和 ReenTrantLock 的区别？**

1. **synchronized 是和 for、while 一样的关键字，ReentrantLock 是类，这是二者的本质区别**。既然 ReentrantLock 是类，那么它就提供了比 synchronized 更多更灵活的特性：**等待可中断、可实现公平锁、可实现选择性通知**（锁可以绑定多个条件）、性能已不是选择标准。

2. **synchronized 依赖于 JVM 而 ReenTrantLock 依赖于 API。synchronized 是依赖于 JVM 实现的**，JDK1.6 为 synchronized 关键字进行了很多优化，但是这些优化都是在虚拟机层面实现的，并没有直接暴露给我们。ReenTrantLock 是 JDK 层面实现的（也就是 API 层面，需要 lock() 和 unlock 方法配合 try/finally 语句块来完成），所以我们可以通过查看它的源代码，来看它是如何实现的。

>1. 锁的实现：synchronized 是 JVM 实现的，而 ReentrantLock 是 JDK 实现的。
>2. 性能：新版本 Java 对 synchronized 进行了很多优化，例如自旋锁等，synchronized 与 ReentrantLock 大致相同。
>3. 等待可中断：当持有锁的线程长期不释放锁的时候，正在等待的线程可以选择放弃等待，改为处理其他事情。ReentrantLock 可中断，而 synchronized 不行。
>4. 公平锁：公平锁是指多个线程在等待同一个锁时，必须按照申请锁的时间顺序来依次获得。synchronized 中的锁是非公平的，ReentrantLock 默认情况下也是非公平的，但是也可以是公平的。
>5. 锁绑定多个条件：一个 ReentrantLock 可以同时绑定多个 Condition 对象。

>**答：**ReentrantLock**是显示锁**，其提供了一些内部锁不具备的特性，但并不是内部锁的替代品。**显式锁支持公平和非公平的调度方式**，默认采用非公平调度。
>
>**synchronized 内部锁简单，但是不灵活。显示锁支持在一个方法内申请锁，并且在另一个方法里释放锁。**显示锁定义了一个tryLock（）方法，尝试去获取锁**，成功返回true，失败并不会导致其执行的线程被暂停而是直接返回false，即可以**避免死锁**。**

### 【< volatile 关键字专题>】

##### [1] 谈一下你对 volatile 关键字的理解？

**答：**volatile 关键字是用来保证有序性和可见性的。

1. 保证了不同线程对该变量操作的内存可见性;
2. 禁止指令重排序。

> 我们所写的代码，不一定是按照我们自己书写的顺序来执行的，编译器会做重排序，CPU 也会做重排序的，这样做是为了减少流水线阻塞，提高 CPU 的执行效率。这就需要有一定的顺序和规则来保证，不然程序员自己写的代码都不知道对不对了，所以有 happens-before 规则，其中有条就是 volatile 变量规则：对一个变量的写操作先行发生于后面对这个变量的读操作、有序性实现的是通过插入内存屏障来保证的。

**解析：**

- volatile 可以保证**主内存和工作内存直接产生交互**，进行读写操作，保证可见性
- volatile 仅能保证变量**写操作的原子性**，不能保证读写操作的原子性。
- volatile可以**禁止指令重排序**（通过插入内存屏障），典型案例是在单例模式中使用。

**volatile变量的开销：**

volatile不会导致线程上下文切换，但是其读取变量的成本较高，因为其每次都需要从高速缓存或者主内存中读取，无法直接从寄存器中读取变量。

##### [2]Volatile如何保证可见性和有序性？

> https://blog.csdn.net/duzhe2905/article/details/106038681?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.compare
>
> https://blog.csdn.net/qq_35590091/article/details/106986536
>
> 》https://www.jianshu.com/p/08a0a8c984ab

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200518151004751.png" alt="image-20200518151004751" style="zoom:67%;" />



###### **1. 可见性**

>**主内存与工作内存**
>
>java内存模型规定了所有的变量都存储在主内存。每条线程还有自己的工作内存，线程的工作内存中保存了被改线程使用到的变量的主内存副本拷贝。线程对变量的所有操作都必须在工作内存中进行，而不能直接读写主内存中的变量。不同线程之间也无法直接访问对方工作内存中的变量，线程间变量传递均需要通过主内存来完成。当多个线程操作的变量涉及到同一个主内存区域，将可能导致各自的工作线程数据不一致，这样就导致变量同步回主内存的时候可能冲突导致数据丢失。
>原文链接：https://blog.csdn.net/y124675160/article/details/78310121

![å¨è¿éæå¥å¾çæè¿°](https://img-blog.csdnimg.cn/20200510191415431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1emhlMjkwNQ==,size_16,color_FFFFFF,t_70)

**volatile修饰的共享变量进行写操作的时候多出一条带lock前缀的指令**，lock前缀的指令在多核处理器下会引发两件事情：

1. **将当前处理器缓存行的数据写回到系统内存**。
2. **这个写回内存的操作会使在其他CPU里缓存了该内存地址的数据无效**。

为了提高处理速度，处理器不直接和内存进行通信，而是先将系统内存的数据读到内部缓存后再进行操作，但是操作完了不知道什么时候写回内存。而对声明了volatile关键字的变量进行写操作，JVM会向处理器发送一条**lock前缀**的指令，将这个变量所在的缓存行立即写回系统内存。并且**为了保证各个处理器的缓存是一致的，实现了缓存一致性协议，各个处理通过嗅探在总线上传播的数据来检查自己缓存的值是不是过期了**，当处理器发现自己缓存行对应的内存地址被修改，就会将当前处理器的缓存行设置成无效状态，那么下次对这个数据进行操作，就会重新从系统内存中获取最新的值。对应JMM来说就是：

1. **Lock前缀的指令让线程工作内存中的值写回主内存中**；
2. **通过缓存一致性协议，其他线程如果工作内存中存了该共享变量的值，就会失效**；
3. **其他线程会重新从主内存中获取最新的值**；


原文链接：https://blog.csdn.net/y124675160/article/details/78310121

###### **2.有序性**

> https://www.jianshu.com/p/64240319ed60
>
> > https://baijiahao.baidu.com/s?id=1666283243240041852&wfr=spider&for=pc

> 为了性能优化，JVM会在不改变数据依赖性的情况下，允许编译器和处理器对指令序列进行重排序，而有序性问题指的就是程序代码执行的顺序与程序员编写程序的顺序不一致，导致程序结果不正确的问题。而加了volatile修饰的共享变量，则通过内存屏障解决了多线程下有序性问题。

**内存屏障指令**（Memory Barrier）：

写内存屏障（Store Memory Barrier）：处理器将存储缓存值**写回主存**（阻塞方式）。

读内存屏障（Load Memory Barrier）：处理器，处理**失效队列**（阻塞方式）。

**内次屏障分为以下4类：**

![image-20200723232539965](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200723232539965.png)
为了实现volatile的内存语义，编译器在生成字节码时，会在指令序列中插入内存屏障来禁止特定类型的处理器重排序，下面是基于保守策略的JMM内存平展插入策略。

* 在每个volatile写操作的前面插入一个StoreStore(**存储存储**)屏障，可以保证前面普通的写操作已经对任意处理器可见。
* 在每个volatile写操作的后面插入一个StoreLoad屏障，可以保证前面普通的写操作已经对任意处理器可见。
* 在每个volatile读操作的后面插入一个LoadLoad屏障，确保前面的数据先于后面的指令写入工作内存。
* 在每个volatile读操作的后面插入一个LoadStore屏障，确保前面的数据先于后面的指令写入工作内存。

volatile在写操作前后插入了内存屏障后生成的指令序列，示意图如下：

<img src="https://img-blog.csdnimg.cn/20200510202203789.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1emhlMjkwNQ==,size_16,color_FFFFFF,t_70#pic_center" alt="å¨è¿éæå¥å¾çæè¿°" style="zoom: 50%;" />

volatile在读操作后面插入了内存屏障后生成的指令序列示意图如下：

<img src="https://img-blog.csdnimg.cn/20200510202533262.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R1emhlMjkwNQ==,size_16,color_FFFFFF,t_70#pic_center" alt="å¨è¿éæå¥å¾çæè¿°" style="zoom: 50%;" />

##### **[3] volatile在什么情况下可以替代锁？**

> 理解volatile和CAS配合使用原理：https://blog.csdn.net/liaoxiaolin520/article/details/93711623

volatile是一个轻量级的锁，适合多个线程**共享一个状态变量**，锁适合多个线程**共享一组状态变量**。可以**将多个线程共享的一组状态变量合并成一个对象**，用一个volatile变量来引用该对象，从而替代锁。

### 【< synchronized专题>】

![image-20200518105440632](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200518105440632.png)

##### [1] synchronized 关键字？

**synchronized是Java中的一个关键字，通常用于多线程环境下，在同一时刻只允许有一个线程访问共享变量。它会根据情况，将锁升级为不同状态，如偏向锁（可以关掉），轻量级锁（无锁/自旋锁/自适应锁），重量级锁。重量级锁会调用操作系统层面的minotor，这时候获得不到线程的对象会被阻塞在队列中。这也是经常被称为一个重量级锁原因。**

**另外它可以保证原子性，可见性和有序性。支持可重入，但不可中断（Lock的tryLock方法是可以被中断的）。**

> **内部锁底层实现：**
>
> - 进入时，执行**monitorenter**，将计数器+1，释放锁**monitorexit**时，计数器-1
> - 当一个线程判断到计数器为0时，则当前锁空闲，可以占用；反之，当前线程进入等待状态

![img](https://pic4.zhimg.com/80/v2-f49568a1f5dea1a636db74e4ca50bfb0_1440w.jpg?source=1940ef5c)

https://www.zhihu.com/question/57794716/answer/606126905

##### [2] synchronized 关键字使用场景

~~~java
package synchronizedTest;

public class SynchronizedTest {
    // 作用于方法上（或者静态方法上）
    public synchronized void test(){
        System.out.println("synchronized test!!!");
    }
    // 作用于代码块内
    public void testBlock(){
        synchronized (this) {
            System.out.println("synchronized test!!!");
        }
    }
}
//作用于一个类上
class ClassName {
    public void method() {
       synchronized(ClassName.class) {
          // todo
       }
    }
 }
~~~

1.  无论synchronized关键字加在方法上还是对象上，如果它作用的对象是非静态的，则它取得的锁是对象；**如果synchronized作用的对象是一个静态方法或一个类，则它取得的锁是对类，该类所有的对象同一把锁**。 因为静态方法是属于类的而不属于对象的 。同样的， synchronized修饰的静态方法锁定的是这个类的所有对象，所有类用它都会有锁的效果。
2. 每个对象只有一个锁（lock）与之相关联，谁拿到这个锁谁就可以运行它所控制的那段代码。
3.  实现同步是要很大的系统开销作为代价的，甚至可能造成死锁，所以尽量避免无谓的同步控制。
   同步关键字锁的是对象

##### [3] synchronized 内部字节码指令

synchronized 内部字节码指令可以保证出现异常时正常解锁。

~~~java
static final Object lock = new Object();
static int counter = 0;
public static void main(String[] args) {
 synchronized (lock) {
 counter++;
 }
}
~~~

~~~java
public static void main(java.lang.String[]);
 descriptor: ([Ljava/lang/String;)V
 flags: ACC_PUBLIC, ACC_STATIC
 Code:
 stack=2, locals=3, args_size=1
 0: getstatic #2 // <- lock引用 （synchronized开始）
 3: dup
 4: astore_1 // lock引用 -> slot 1 <解锁时候用>
 5: monitorenter // 将 lock对象 MarkWord 置为 Monitor 指针 <c实现的>
 6: getstatic #3 // <- i
 9: iconst_1 // 准备常数 1
 10: iadd // +1
 11: putstatic #3 // -> i 
 14: aload_1 // <- lock引用   <解锁>
 15: monitorexit // 将 lock对象 MarkWord 重置, 唤醒 EntryList
 16: goto 24
//19-23: Exception table还在检测范围内检测异常，6 16 19如果6-16出现异常们就会到19行。19行到最后可以保证在异常发生时正常解锁
 19: astore_2 // e -> slot 2 
 20: aload_1 // <- lock引用
 21: monitorexit // 将 lock对象 MarkWord 重置, 唤醒 EntryList 
 22: aload_2 // <- slot 2 (e)    
 23: athrow // throw e
 24: return
 Exception table:  
 from to target type
 6 16 19 any
 19 22 19 any
 LineNumberTable:
 line 8: 0
 line 9: 6
 line 10: 14
 line 11: 24
 LocalVariableTable:
 Start Length Slot Name Signature
 0 25 0 args [Ljava/lang/String;
 StackMapTable: number_of_entries = 2
 frame_type = 255 /* full_frame */
 offset_delta = 19
 locals = [ class "[Ljava/lang/String;", class java/lang/Object ]
 stack = [ class java/lang/Throwable ]
 frame_type = 250 /* chop */
 offset_delta = 4
~~~

> 方法

##### [4] synchronized如何保证有序性、可见性、原子性?

> https://blog.csdn.net/qq_35590091/article/details/106986641

###### 1. 原子性

​     synchronized经过编译之后，对应的是class文件中的**monitorenter和monitorexit**这两个字节码指令。这两个字节码对应的内存模型的操作是**lock（上锁）和unlock（解锁**）。因为这两个操作之间运行的都是原子的（这个操作保证了变量为一个线程独占的，也就是说只有获得锁的线程才能够操作被锁定的内存区域），所synchronized也具有原子性。

 > 这两个字节码都需要一个对象来作为锁。因此，
 >
 > 1、如果synchronized修饰的是实例方法，则会传入this作为参数，
 >
 > 2、如果修饰的是静态方法，则会传入class类对象作为参数。
 >
 > 3、如果只是一个同步块，那么锁就是括号里配置的对象。
 >
 > 执行monitorenter字节码时，如果这个对象没有被上锁，或者当前线程已经持有了该锁，那么锁的计数器会+1，而在执行monitorexit字节码时，锁的计数器会-1，当计数器为0时，锁被释放。如果获取对象的锁失败，那么该线程会被阻塞等待，直到之前把这个对象上锁的线程释放这个锁为止。
 >
 > 每个对象都有一个monitor（监视器）与之关联，所谓的上锁，就是获得对象的monitor的独占权（因为只用获得monitor才能访问这个对象）。执行monitorenter字节码的时候，线程就会尝试获得monitor的所有权，也就是尝试获得对象的锁。只有获得了monitor，才能进入同步块，或者执行同步方法。独占对象的本质是独占对象的monitor。

###### 2. 可见性

**lock（上锁时）**清空工作内存中共享变量的值，从而使用共享变量时需要从主内存中重新获取最新的值；

**unlock (解锁)**：这个操作规定，放开对某个变量的锁的之前，需要把这个变量从缓存更新到主内存。

###### 3. 有序性

 为什么synchronized无法禁止指令重排，却能保证有序性？因为在一个线程内部，他不管怎么指令重排，他都是as if serial的，也就是说单线程即使重排序之后的运行结果和串行运行的结果是一样的，是类似串行的语义。**而当线程运行到同步块时，会加锁，其他线程无法获得锁，也就是说此时同步块内的方法是单线程的，根据as if serial，可以认为他是有序的。**而指令重排序导致线程不安全是多线程运行的时候，不是单线程运行的时候，因此多线程运行时静止指令重排序也可以实现有序性，这就是as if seria。

> **原子性 + 可见性 -> 有序性，即使内部重排序，也不会有影响，可以说是多线程的serif**

##### [5] synchronized 关键字锁升级过程？

锁的状态总共有四种，级别由低到高依次为：**无锁、偏向锁、轻量级锁、重量级锁**，四种状态会随着竞争的情况逐渐升级，而且是不可逆的过程。目的是为了提高获得锁和释放锁的效率。

**偏向锁**：大多数情况下，锁总是由同一个线程多次获得。当一个线程访问同步块并获取锁时，会在对象头和栈帧中的锁记录里存储锁偏向的线程ID，**偏向锁是一个可重入的锁**。如果锁对象头的Mark Word里存储着指向当前线程的偏向锁，无需重新进行CAS操作来加锁和解锁。当有其他线程尝试竞争偏向锁时，持有偏向锁的线程（不处于活动状态）才会释放锁。**偏向锁无法使用自旋锁**优化，因为一旦有其他线程申请锁，就破坏了偏向锁的假定进而升级为轻量级锁。

> 对于同一时刻只有一个线程访问时，每次进入锁是检查是否是自己的锁，是则执行，不是则升级

**轻量级锁**：减少无实际竞争情况下，使用重量级锁产生的性能消耗。JVM会现在当前线程的栈桢中创建用于存储锁记录的空间 LockRecord，将对象头中的 Mark Word 复制到 LockRecord 中并将 LockRecord 中的 Owner 指针指向锁对象。然后线程会尝试使用CAS将对象头中的Mark Word替换为指向锁记录的指针，成功则当前线程获取到锁，失败则表示其他线程竞争锁当前线程则**尝试使用自旋的方式获取锁**。自旋获取锁失败则锁膨胀升级为重量级锁。

>在少量线程访问同步代码快时，使用CAS操作实现无🔒，如果获取到则存入旧状态值，如果成功则使用自旋来获取锁，如果

**重量级锁**：通过对象内部的监视器(monitor)实现，其中monitor的本质是依赖于底层操作系统的Mutex Lock实 现，操作系统实现线程之间的切换需要从用户态到内核态的切换，切换成本非常高。线程竞争不使用自旋，不会消耗CPU。但是线程会进入阻塞等待被其他线程被唤醒，响应时间缓慢。

>会调用操作系统层面的moniter

##### [[5] JVM 对 synchronized 的锁优化](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=十二、锁优化)

**[1. 自旋锁](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=自旋锁)**

让不满足条件的线程等待一会看能不能获得锁，通过占用处理器的时间来避免线程切换带来的开销。自旋等待的时间或次数是有一个限度的，如果自旋超过了定义的时间仍然没有获取到锁，则该线程应该被挂起。在 JDK1.6 之后，引入了**自适应自旋锁**，自适应意味着自旋的次数不是固定不变的，而是根据前一次在同一个锁上自旋的时间以及锁的拥有者的状态来决定。如果在同一个锁对象上，自旋等待刚刚成功获得过锁，并且持有锁的线程正在运行中，那么虚拟机就会认为这次自旋也是很有可能再次成功，进而它将允许自旋等待持续相对更长的时间。如果对于某个锁，自旋很少成功获得过，那在以后尝试获取这个锁时将可能省略掉自旋过程，直接阻塞线程，避免浪费处理器资源。

**[2. 锁消除](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=锁消除)**

**锁消除是指对于被检测出不可能存在竞争的共享数据的锁进行消除。**

锁消除主要是通过逃逸分析来支持，如果堆上的共享数据不可能逃逸出去被其它线程访问到，那么就可以把它们当成私有数据对待，也就可以将它们的锁进行消除。

对于一些看起来没有加锁的代码，其实隐式的加了很多锁。例如下面的字符串拼接代码就隐式加了锁：

```java
public static String concatString(String s1, String s2, String s3) {
    return s1 + s2 + s3;
}Copy to clipboardErrorCopied
```

String 是一个不可变的类，编译器会对 String 的拼接自动优化。在 JDK 1.5 之前，会转化为 StringBuffer 对象的连续 append() 操作：

```java
public static String concatString(String s1, String s2, String s3) {
    StringBuffer sb = new StringBuffer();
    sb.append(s1);
    sb.append(s2);
    sb.append(s3);
    return sb.toString();
}Copy to clipboardErrorCopied
```

每个 append() 方法中都有一个同步块。虚拟机观察变量 sb，很快就会发现它的动态作用域被限制在 concatString() 方法内部。也就是说，sb 的所有引用永远不会逃逸到 concatString() 方法之外，其他线程无法访问到它，因此可以进行消除。

**[3.锁粗化](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=锁粗化)**

**如果一系列的连续操作都对同一个对象反复加锁和解锁，频繁的加锁操作就会导致性能损耗。**

上一节的示例代码中连续的 append() 方法就属于这类情况。如**果虚拟机探测到由这样的一串零碎的操作都对同一个对象加锁，将会把加锁的范围扩展（粗化）到整个操作序列的外部**。对于上一节的示例代码就是扩展到第一个 append() 操作之前直至最后一个 append() 操作之后，这样只需要加锁一次就可以了。

##### [8] synchronized 和 volatile 的区别是什么？

1. volatile 本质是在告诉 JVM当前变量在寄存器（工作内存）中的值是不确定的，需要从主存中读取；synchronized 则是锁定当前变量，只有当前线程可以访问该变量，其他线程被阻塞住。

2. volatile 仅能使用在变量级别；synchronized 则可以使用在变量、方法、和类级别的。

3. volatile 仅能实现变量的修改可见性，不能保证原子性；而 synchronized 则可以保证变量的修改可见性和原子性。

4. **volatile 不会造成线程的阻塞**；synchronized 可能会造成线程的阻塞。

5. volatile 标记的变量不会被编译器优化；synchronized 标记的变量可以被编译器优化。

### 【< AQS>】

##### **[1]** 什么是AQS 

[AQS](https://www.jianshu.com/p/0f876ead2846) 全称是 AbstractQueuedSynchronizer，是阻塞式锁和相关的同步器工具的框架。

**AQS分为独占式同步状态获取与释放，共享式同步状态获取与释放，独占式超时获取同步状态。接下来我先简单介绍下第一种：独占式同步状态获取与释放。AQS从数据结构上说，通过一个int成员变量state来控制同步状态，内部的同步队列(先进先出（FIFO）的双向链表队列)完成 对同步状态(state)的管理。**

> **state**：当state = 0时，说明没有任何线程占有共享资源的锁； state = 1时，则说明有线程目前正在使用共享变量

**具体实现为同步器的acquire方法，该方法对中断不敏感：**

1. **首先调用自定义同步器实现的tryAcquire(int arg)方法，尝试获取同步状态**。

   > **tryAcquire(int arg)方法**，以独占式获取同步状态，实现该方法需要查询当前状态state，然后再使用CAS设置当前状态。**无参方法tryAcquire（）的作用是尝试的获得1个许可，如果getstate！=0，则说明，此时已经被占用无法获取，返回false，如果getstate==0，则说明，此时共享变量是空闲的，使用CAS(判断当前状态是否为0)设置锁状态为1，并返回ture。**

2. **如果获取成功，则直接退出，如果同步状态获取失败，则构造同步节点（）并通过addWaiter(Node node)方法将该节点加入到同步队列的尾部，并阻塞当前线程**。

   >**同步节点**：独占式node,同一时刻只有一个线程可以获得同步状态；
   >
   >**addWaiter(Node node)**：首先使用CAS尝试快速在队尾插入，如果入队失败了，则调用enq()，[link](https://www.jianshu.com/p/c806dd7f60bc)
   >
   >**compareAndSetTail(pred, node)**：确保节点可以被线程安全的添加。如果多个线程同时使用添加节点，最终可能导致节点数量和顺序变化。compareAndSetTail会比较pred和tail是否指向同一个节点，如果是，才将tail更新为node。虽然当前线程在声明pred时，为pred赋值了tail，但tail可能会被其他线程改变，而当前线程的本地变量pred是不会感知到这个改变的。
   >
   >**enq(final Node node)方法**，同步器通过“死循环”来保证节点的正确添加，在“死循环”中只有通过CAS将节点设置成为尾节点之后，当前线程才能从该方法返回，否则，当前线程不断地尝试设置。

3. **然后调用acquireQueued(Node node,int arg)方法，使得该节点以“死循环”的方式获取同步状态。如果获取不到则节点中的线程则会被阻塞，而被阻塞线程的唤醒主要依靠前驱节点的出队或阻塞线程被中断来实现。**

> 在acquireQueued(final Node node,int arg)方法中，当前**线程在“死循环”中尝试获取同步状态，而只有前驱节点是头节点才能够尝试获取同步状态。**首先是维护了先进先出原则，再就是后面节点需要“死循环”来判断自己是否是头结点。

![img](https://img-blog.csdn.net/20180520130953567?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



**AQS核心思想：**

* **如果被请求的共享资源空闲，则将当前请求资源的线程设置为有效的工作线程，并且将共享资源设置为锁定状态。内部通过一个int成员变量state来控制同步状态**。
  * 当state = 0时，说明没有任何线程占有共享资源的锁；
  * state = 1时，则说明有线程目前正在使用共享变量，其他线程必须加入同步队列进行等待，当然state也 可以继续执行+1操作，比如可重入锁。
* **AQS同步器的实现依赖于内部的同步队列(FIFO的双向链表队列)完成 对同步状态(state)的管理**。
  * 当前线程获取锁(同步状态)失败时，AQS会将该线程以及相关等待信息包装成 一个节点(Node)并将其加入同步队列，同时会阻塞当前线程
  * 当同步状态释放时，会将头结点head中的线程唤醒，让其尝试获取同步状态。简单来说，就是同步状态。

**AQS实现：**

* getState - 获取 state 状态
* setState - 设置 state 状态
* compareAndSetState - cas 机制设置 state 状态
* 独占模式是只有一个线程能够访问资源，而共享模式可以允许多个线程访问资源
* 提供了基于 FIFO 的等待队列，类似于 Monitor 的 EntryList
* 条件变量来实现等待、唤醒机制，支持多个条件变量，类似于 Monitor 的 WaitSet

**AQS功能：**

* 阻塞版本获取锁 acquire 和非阻塞的版本尝试获取锁 tryAcquire
* 获取锁超时机制
* 通过打断取消机制
* 独占机制及共享机制
* 条件不满足时的等待机制

**子类主要实现这样一些方法**（默认抛出 UnsupportedOperationException）

* tryAcquire

* tryRelease

* tryAcquireShared

* tryReleaseShared

* isHeldExclusively

##### **[2]** LCK队列源码及其实现

我们来看看AbstractQueuedSynchronizer类中的acquire方法实现

```java
    public final void acquire(int arg) {
        //尝试获取锁
        if (!tryAcquire(arg) &&
            //获取不到,则进入等待队列，返回是否中断
            acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
            //如果返回中断，则调用当前线程的interrupt()方法
            selfInterrupt();
    }
```

**1. 入队** ：如果线程调用tryAcquire（其最终实现是调用上面分析过的nonfairTryAcquire方法）获取锁失败。调用addWaiter(Node.EXCLUSIVE)方法，将自己加入CLH队列的尾部。

* **tryAcquire(int arg)方法**，以独占式获取同步状态，实现该方法需要查询当前状态state，然后再使用CAS设置当前状态。**无参方法tryAcquire（）的作用是尝试的获得1个许可，如果getstate！=0，则说明，此时已经被占用无法获取，返回false，如果getstate==0，则说明，此时共享变量是空闲的，使用CAS(判断当前状态是否为0)设置锁状态为1，并返回ture。**

* **同步节点**：独占式node,同一时刻只有一个线程可以获得同步状态；

* **addWaiter(Node node)**：首先使用CAS尝试快速在队尾插入，如果入队失败了，则调用enq()，[link](https://www.jianshu.com/p/c806dd7f60bc)

* **compareAndSetTail(pred, node)**：确保节点可以被线程安全的添加。如果多个线程同时使用添加节点，最终可能导致节点数量和顺序变化。compareAndSetTail会比较pred和tail是否指向同一个节点，如果是，才将tail更新为node。虽然当前线程在声明pred时，为pred赋值了tail，但tail可能会被其他线程改变，而当前线程的本地变量pred是不会感知到这个改变的。

* **enq(final Node node)方法**，同步器通过“死循环”来保证节点的正确添加，在“死循环”中只有通过CAS将节点设置成为尾节点之后，当前线程才能从该方法返回，否则，当前线程不断地尝试设置。

~~~java
final boolean nonfairTryAcquire(int acquires) {
            final Thread current = Thread.currentThread();
            int c = getState();
            if (c == 0) {
                if (compareAndSetState(0, acquires)) {
                    setExclusiveOwnerThread(current);
                    return true;
                }
            }
            else if (current == getExclusiveOwnerThread()) {
                int nextc = c + acquires;
                if (nextc < 0) // overflow
                    throw new Error("Maximum lock count exceeded");
                setState(nextc);
                return true;
            }
            return false;
        }
~~~

```java
    private Node addWaiter(Node mode) {
        //线程对应的Node
        Node node = new Node(Thread.currentThread(), mode);
        // Try the fast path of enq; backup to full enq on failure
        Node pred = tail;
        //尾节点不为空
        if (pred != null) {
            //当前node的前驱指向尾节点
            node.prev = pred;
            //将当前node设置为新的尾节点
            //如果cas操作失败，说明线程竞争
            if (compareAndSetTail(pred, node)) {
                pred.next = node;
                return node;
            }
        }
        //lockfree的方式插入队尾
        enq(node);
        return node;
    }
    private Node enq(final Node node) {
        //经典的lockfree算法：循环+CAS
        for (;;) {
            Node t = tail;
            //尾节点为空
            if (t == null) { // Must initialize
                //初始化头节点
                if (compareAndSetHead(new Node()))
                    tail = head;
            } else {
                node.prev = t;
                if (compareAndSetTail(t, node)) {
                    t.next = node;
                    return t;
                }
            }
        }
    }
```

入队过程，入下图所示

1  T0持有锁时，其CLH队列的头尾指针为NULL 

![img](https:////upload-images.jianshu.io/upload_images/6283837-329b55b2aef3cfed.png?imageMogr2/auto-orient/strip|imageView2/2/w/492/format/webp)

2 线程T1，此时请求锁，由于锁被T0占有。因此加入队列尾部。具体过程如下所示：

 (1) 初始化头节点

 (2) 初始化T1节点，入队，尾指针指向T1



![img](https:////upload-images.jianshu.io/upload_images/6283837-44b561cadb816d53.png?imageMogr2/auto-orient/strip|imageView2/2/w/638/format/webp)



3 此时如果有一个T10线程先于T1入队，则T1执行compareAndSetTail(t, node)会失败，然后回到for循环开始处，重新入队。



![img](https:////upload-images.jianshu.io/upload_images/6283837-f7eff474bd1f2d8c.png?imageMogr2/auto-orient/strip|imageView2/2/w/738/format/webp)

image.png

**2.  由自旋到阻塞**

入队后，调用acquireQueued方法，时而自旋，时而阻塞，直到获取锁（或被取消）。

* 在acquireQueued(final Node node,int arg)方法中，当前**线程在“死循环”中尝试获取同步状态，而只有前驱节点是头节点才能够尝试获取同步状态。**首先是维护了先进先出原则，再就是后面节点需要“死循环”来判断自己是否是头结点。

```java
  final boolean acquireQueued(final Node node, int arg) {
        boolean failed = true;
        try {
            boolean interrupted = false;
            for (;;) {
                final Node p = node.predecessor();
                //其前驱是头结点，并且再次调用tryAcquire成功获取锁
                if (p == head && tryAcquire(arg)) {
                    //将自己设为头结点
                    setHead(node);
                    p.next = null; // help GC
                    failed = false;
                    //成功获取锁，返回
                    return interrupted;
                }
                //没有得到锁时：
                //shouldParkAfterFailedAcquire方法：返回是否需要阻塞当前线程
                //parkAndCheckInterrupt方法：阻塞当前线程，当线程再次唤醒时，返回是否被中断
                if (shouldParkAfterFailedAcquire(p, node) &&
                    parkAndCheckInterrupt())
                    //修改中断标志位
                    interrupted = true;
            }
        } finally {
            if (failed)
                //获取锁失败，则将此线程对应的node的waitStatus改为CANCEL
                cancelAcquire(node);
        }
    }
    
    private void setHead(Node node) {
        head = node;
        node.thread = null;
        node.prev = null;
    }
    
      /**
     * 获取锁失败时，检查并更新node的waitStatus。
     * 如果线程需要阻塞，返回true。
     */
    private static boolean shouldParkAfterFailedAcquire(Node pred, Node node) {
        int ws = pred.waitStatus;
        
        //前驱节点的waitStatus是SIGNAL。
        if (ws == Node.SIGNAL)
            /* 
             * SIGNAL状态的节点，释放锁后，会唤醒其后继节点。
             * 因此，此线程可以安全的阻塞（前驱节点释放锁时，会唤醒此线程)。
             */
            return true;
            
        //前驱节点对应的线程被取消
        if (ws > 0) {
            do {
                //跳过此前驱节点
                node.prev = pred = pred.prev;
            } while (pred.waitStatus > 0);
            pred.next = node;
        } else {
            /*
               此时，需要将前驱节点的状态设置为SIGNAL。
             * waitStatus must be 0 or PROPAGATE.  Indicate that we
             * need a signal, but don't park yet.  Caller will need to
             * retry to make sure it cannot acquire before parking.
             */
            compareAndSetWaitStatus(pred, ws, Node.SIGNAL);
        }
        return false;
    }
     //当shouldParkAfterFailedAcquire方法返回true，则调用parkAndCheckInterrupt方法阻塞当前线程
    private final boolean parkAndCheckInterrupt() {
        LockSupport.park(this);
        return Thread.interrupted();
    }
```

自旋过程，入下图所示

![img](https:////upload-images.jianshu.io/upload_images/6283837-878b80c3bb792a5a.png?imageMogr2/auto-orient/strip|imageView2/2/w/598/format/webp)

image.png

![img](https:////upload-images.jianshu.io/upload_images/6283837-7bf0c19c620a3be3.png?imageMogr2/auto-orient/strip|imageView2/2/w/618/format/webp)

image.png

![img](https:////upload-images.jianshu.io/upload_images/6283837-7d476066c368ab54.png?imageMogr2/auto-orient/strip|imageView2/2/w/580/format/webp)

image.png

![img](https:////upload-images.jianshu.io/upload_images/6283837-e06abbefaaeb75d5.png?imageMogr2/auto-orient/strip|imageView2/2/w/504/format/webp)

image.png

![img](https:////upload-images.jianshu.io/upload_images/6283837-712ccd351e24b328.png?imageMogr2/auto-orient/strip|imageView2/2/w/668/format/webp)

image.png



 然后线程T2,加入了请求锁的队列，尾指针后移。


![img](https:////upload-images.jianshu.io/upload_images/6283837-17e7fabaa90e7e95.png?imageMogr2/auto-orient/strip|imageView2/2/w/630/format/webp)

image.png

![img](https:////upload-images.jianshu.io/upload_images/6283837-5fd5ff276db53efb.png?imageMogr2/auto-orient/strip|imageView2/2/w/606/format/webp)

image.png

![img](https:////upload-images.jianshu.io/upload_images/6283837-84c2841b593c2746.png?imageMogr2/auto-orient/strip|imageView2/2/w/642/format/webp)

image.png

终上所述，每个得不到锁的线程，都会讲自己封装成Node，加入队尾，或自旋或阻塞，直到获取锁（为简化问题，不考虑取消的情况）

**3. 锁的释放**

前文提到，T1,T2在阻塞之前，都回去修改其前驱节点的waitStatus=-1。这是为什么？
 我们看下锁释放的代码，便一目了然

```java
    public final boolean release(int arg) {
        //修改锁计数器，如果计数器为0,说明锁被释放
        if (tryRelease(arg)) {
            Node h = head;
            //head节点的waitStatus不等于0，说明head节点的后继节点对应的线程，正在阻塞，等待被唤醒
            if (h != null && h.waitStatus != 0)
                //唤醒后继节点
                unparkSuccessor(h);
            return true;
        }
        return false;
    }
    
   
    private void unparkSuccessor(Node node) {
        /*
         * If status is negative (i.e., possibly needing signal) try
         * to clear in anticipation of signalling.  It is OK if this
         * fails or if status is changed by waiting thread.
         */
        int ws = node.waitStatus;
        if (ws < 0)
            compareAndSetWaitStatus(node, ws, 0);

      
        //后继节点
        Node s = node.next;
        //如果s被取消，跳过被取消节点
        if (s == null || s.waitStatus > 0) {
            s = null;
            for (Node t = tail; t != null && t != node; t = t.prev)
                if (t.waitStatus <= 0)
                    s = t;
        }
        if (s != null)
            //唤醒后继节点
            LockSupport.unpark(s.thread);
    }
```

如代码所示，waitStatus=-1的作用，主要是告诉释放锁的线程：后面还有排队等待获取锁的线程，请唤醒他！

释放锁的过程，如图所示：

![img](https:////upload-images.jianshu.io/upload_images/6283837-a94cd5ee0547df1c.png?imageMogr2/auto-orient/strip|imageView2/2/w/784/format/webp)

![img](https:////upload-images.jianshu.io/upload_images/6283837-83ee3de9fad63814.png?imageMogr2/auto-orient/strip|imageView2/2/w/740/format/webp)

**总结**

实现锁的关键在于：

1. 通过CAS操作与volatile变量互相配合，线程安全的修改锁标志位
2. 基于CLH队列，实现锁的排队策略

##### [3] 独占式同步状态获取

通过调用同步器的acquire(int arg)方法可以获取同步状态，该方法对中断不敏感，也就是由于线程获取同步状态失败后进入同步队列中，后续对线程进行中断操作时，线程不会从同步队列中移出，该方法代码如下：

![image-20200716092220731](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716092220731.png)

上述代码主要完成了同步状态获取、节点构造、加入同步队列以及在同步队列中自旋等待的相关工作，其主要逻辑是：**首先调用自定义同步器实现的tryAcquire(int arg)方法，该方法保证线程安全的获取同步状态，如果同步状态获取失败，则构造同步节点（独占式node,同一时刻只有一个线程可以获得同步状态）并通过addWaiter(Node node)方法将该节点加入到同步队列的尾部，最后调用acquireQueued(Node node,int arg)方法，使得该节点以“死循环”的方式获取同步状态。如果获取不到则阻塞节点中的线程，而被阻塞线程的唤醒主要依靠前驱节点的出队或阻塞线程被中断来实现。**

我们看下同步器的**addWaiter**和enq的实现代码如下：

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200716092454978.png" alt="image-20200716092454978" style="zoom: 67%;" />

上述代码通过使用compareAndSetTail(Node expect,Node update)方法来确保节点能够被线程安全添加。

**在enq(final Node node)方法中，同步器通过“死循环”来保证节点的正确添加，在“死循环”中只有通过CAS将节点设置成为尾节点之后，当前线程才能从该方法返回，否则，当前线程不断地尝试设置。**

 **节点进入同步队列之后，就进入了一个自旋的过程（acquireQueued方法），每个节点（或者说每个线程）都在自省地观察，当条件满足，获取到了同步状态，就可以从这个自旋过程中退出，否则依旧留在这个自旋过程中（并会阻塞节点的线程）**，如代码所示：

![img](https://img-blog.csdn.net/20180520130822922?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

在acquireQueued(final Node node,int arg)方法中，当前**线程在“死循环”中尝试获取同步状态，而只有前驱节点是头节点才能够尝试获取同步状态。**首先是维护了先进先出原则，再就是后面节点需要“死循环”来判断自己是否是头结点。

![img](https://img-blog.csdn.net/20180520130915614?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

独占式同步状态获取流程，也就是acquire(int arg)方法调用流程，如图所示：

![img](https://img-blog.csdn.net/20180520130953567?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

下面看下如何释放释放同步状态的：

![img](https://img-blog.csdn.net/2018052013112053?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

****

 该方法执行时，会唤醒头节点的后继节点线程，unparkSuccessor(Node node)方法使用LockSupport（这里不做介绍）来唤醒处于等待状态的线程。

**适当做个总结：在获取同步状态时，同步器维护一个同步队列，获取状态失败的线程都会被加入到队列中并在队列中进行自旋；移出队列（或停止自旋）的条件是前驱节点为头节点且成功获取了同步状态。在释放同步状态时，同步器调用tryRelease(int arg)方法释放同步状态，然后唤醒头节点的后继节点。**

##### [4] 共享式同步状态获取与释放

   **共享式获取与独占式获取最主要的区别在于同一时刻能否有多个线程同时获取到同步状态。**

​    通过调用同步器的acquireShared(int arg)方法可以共享式地获取同步状态，该方法代码如下:

![img](https://img-blog.csdn.net/20180520131522163?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

  在acquireShared(int arg)方法中，**同步器调用tryAcquireShared(int arg)方法尝试获取同步状态，tryAcquireShared(int arg)方法返回值为int类型，当返回值大于等于0时，表示能够获取到同步状态。因此，在共享式获取的自旋过程中，成功获取到同步状态并退出自旋的条件就是tryAcquireShared(int arg)方法返回值大于等于0。可以看到，在doAcquireShared(int arg)方法的自旋过程中，如果当前节点的前驱为头节点时，尝试获取同步状态，如果返回值大于等于0，表示该次获取同步状态成功并从自旋过程中退出.**

 与独占式一样，共享式获取也需要释放同步状态，通过调用releaseShared(int arg)方法可以释放同步状态，该方法代码:

![img](https://img-blog.csdn.net/20180520131707401?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 该方法在释放同步状态之后，将会唤醒后续处于等待状态的节点。对于能够支持多个线程同时访问的并发组件（比如Semaphore），它和独占式主要区别在于tryReleaseShared(int arg)方法必须确保同步状态（或者资源数）线程安全释放，一般是通过循环和CAS来保证的，因为释放同步状态的操作会同时来自多个线程

#####  [5] 独占式超时获取同步状态

​     通过调用同步器的doAcquireNanos(int arg,long nanosTimeout)方法可以超时获取同步状态，即在指定的时间段内获取同步状态，如果获取到同步状态则返回true，否则，返回false。该方法提供了传统Java同步操作（比如synchronized关键字）所不具备的特性。

   超时获取同步状态过程可以被视作响应中断获取同步状态过程的“增强版”，doAcquireNanos(int arg,long nanosTimeout)方法在支持响应中断的基础上，增加了超时获取的特性。针对超时获取，主要需要计算出需要睡眠的时间间隔nanosTimeout，为了防止过早通知，nanosTimeout计算公式为：nanosTimeout-=now-lastTime，其中now为当前唤醒时间，lastTime为上次唤醒时间，如果nanosTimeout大于0则表示超时时间未到，需要继续睡眠nanosTimeout纳秒，反之，表示已经超时.具体代码这里就不贴出来了。大致的流程图如下：

<img src="https://img-blog.csdn.net/20180520132130147?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" alt="img" style="zoom:67%;" />

独占式超时获取同步状态doAcquireNanos(int arg,long nanosTimeout)和独占式获取同步状态acquire(int args)在流程上非常相似，其主要区别在于未获取到同步状态时的处理逻辑。**acquire(int args)在未获取到同步状态时，将会使当前线程一直处于等待状态，而doAcquireNanos(int arg,long nanosTimeout)会使当前线程等待nanosTimeout纳秒，如果当前线程在nanosTimeout纳秒内没有获取到同步状态，将会从等待逻辑中自动返回。**

##### [5] AQS的思想

![image-20200714235957417](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200714235957417.png)



![image-20200715000018721](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715000018721.png)

![image-20200715000051324](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715000051324.png)

![image-20200715000112746](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715000112746.png)

![image-20200715000131770](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715000131770.png)

![image-20200715000156543](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715000156543.png)





### 【< J.U.C>】

##### **[1]** AQS 

**见专题**

##### [2] ReentrantLock 

**见专题**

##### [3] ReentrantReadWriteLock

https://www.cnblogs.com/xiaoxi/p/9140541.html

现实中有这样一种场景：**对共享资源有读和写的操作，且写操作没有读操作那么频繁。**在没有写操作的时候，多个线程同时读一个资源没有任何问题，所以应该允许多个线程同时读取共享资源；但是如果一个线程想去写这些共享资源，就不应该允许其他线程对该资源进行读和写的操作了。

　**针对这种场景，JAVA的并发包提供了读写锁ReentrantReadWriteLock，它表示两个锁（ReadLock和WriteLock），一个是读操作相关的锁，称为共享锁；一个是写相关的锁，称为排他锁**，描述如下：

* **线程进入读锁（共享）的前提条件：**

没有其他线程的写锁，

没有写请求或者**有写请求，但调用线程和持有锁的线程是同一个。**

* **线程进入写锁（互斥）的前提条件：**

没有其他线程的读锁

没有其他线程的写锁

* **而读写锁有以下六个重要的特性：**

（1）公平选择性：支持非公平（默认）和公平的锁获取方式，吞吐量还是非公平优于公平。

（2）重进入：读锁和写锁都支持线程重进入。

（3）**锁降级**：遵循获取写锁、获取读锁再释放写锁的次序，写锁能够降级成为读锁

（4）不支持锁升级：为了保证内存可见性

 （5） 不支持conditon函数

（6） 读写锁允许多个读线程访问，但是写线程时，不允许其他线程。

**1. 读写状态的设计**

**如何用一个state值来表示读写两种状态呢？**

  同步状态在重入锁的实现中是表示被同一个线程重复获取的次数，即一个整型变量来维护，但是之前的那个表示仅仅表示是否锁定，而不用区分是读锁还是写锁。而读写锁需要在同步状态（一个整形变量）上维护多个读线程和一个写线程的状态。

   **读写锁对于同步状态的实现是在一个整形变量上通过“按位切割使用”：将变量切割成两部分，高16位表示读，低16位表示写。**

![http://static.open-open.com/lib/uploadImg/20151031/20151031223319_397.png](http://static.open-open.com/lib/uploadImg/20151031/20151031223319_397.png)

假设当前同步状态值为S，get和set的操作如下：

（1）获取写状态：

  S&0x0000FFFF:将高16位全部抹去

（2）获取读状态：

  S>>>16:无符号补0，右移16位

（3）写状态加1：

   S+1

（4）读状态加1：

　　S+（1<<16）即S + 0x00010000

在代码层的判断中，如果S不等于0，当写状态（S&0x0000FFFF），而读状态（S>>>16）大于0，则表示该读写锁的读锁已被获取。

**4、写锁的获取与释放**

看下WriteLock类中的lock和unlock方法：

```
public void lock() {
    sync.acquire(1);
}

public void unlock() {
    sync.release(1);
}
```

可以看到就是调用的独占式同步状态的获取与释放，因此真实的实现就是Sync的 tryAcquire和 tryRelease。

**写锁的获取，看下tryAcquire：**

```java
 1 protected final boolean tryAcquire(int acquires) {
 2     //当前线程
 3     Thread current = Thread.currentThread();
 4     //获取状态
 5     int c = getState();
 6     //写线程数量（即获取独占锁的重入数）
 7     int w = exclusiveCount(c);
 8     
 9     //当前同步状态state != 0，说明已经有其他线程获取了读锁或写锁
10     if (c != 0) {
11         // 当前state不为0，此时：如果写锁状态为0说明读锁此时被占用返回false；
12         // 如果写锁状态不为0且写锁没有被当前线程持有返回false
13         if (w == 0 || current != getExclusiveOwnerThread())
14             return false;
15         
16         //判断同一线程获取写锁是否超过最大次数（65535），支持可重入
17         if (w + exclusiveCount(acquires) > MAX_COUNT)
18             throw new Error("Maximum lock count exceeded");
19         //更新状态
20         //此时当前线程已持有写锁，现在是重入，所以只需要修改锁的数量即可。
21         setState(c + acquires);
22         return true;
23     }
24     
25     //到这里说明此时c=0,读锁和写锁都没有被获取
26     //writerShouldBlock表示是否阻塞
27     if (writerShouldBlock() ||
28         !compareAndSetState(c, c + acquires))
29         return false;
30     
31     //设置锁为当前线程所有
32     setExclusiveOwnerThread(current);
33     return true;
34 }
```

其中exclusiveCount方法表示占有写锁的线程数量，源码如下：

```
static int exclusiveCount(int c) { return c & EXCLUSIVE_MASK; }
```

说明：直接将状态state和（2^16 - 1）做与运算，其等效于将state模上2^16。写锁数量由state的低十六位表示。

从源代码可以看出，获取写锁的步骤如下：

（1）首先获取c、w。c表示当前锁状态；w表示写线程数量。然后判断同步状态state是否为0。如果state!=0，说明已经有其他线程获取了读锁或写锁，执行(2)；否则执行(5)。

（2）如果锁状态不为零（c != 0），而写锁的状态为0（w = 0），说明读锁此时被其他线程占用，所以当前线程不能获取写锁，自然返回false。或者锁状态不为零，而写锁的状态也不为0，但是获取写锁的线程不是当前线程，则当前线程也不能获取写锁。

（3）判断当前线程获取写锁是否超过最大次数，若超过，抛异常，反之更新同步状态（此时当前线程已获取写锁，更新是线程安全的），返回true。

（4）如果state为0，此时读锁或写锁都没有被获取，判断是否需要阻塞（公平和非公平方式实现不同），在非公平策略下总是不会被阻塞，在公平策略下会进行判断（判断同步队列中是否有等待时间更长的线程，若存在，则需要被阻塞，否则，无需阻塞），如果不需要阻塞，则CAS更新同步状态，若CAS成功则返回true，失败则说明锁被别的线程抢去了，返回false。如果需要阻塞则也返回false。

（5）成功获取写锁后，将当前线程设置为占有写锁的线程，返回true。

方法流程图如下：

![img](https://images2018.cnblogs.com/blog/249993/201806/249993-20180607130802005-1386429088.png)

**写锁的释放，tryRelease方法：**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
 1 protected final boolean tryRelease(int releases) {
 2     //若锁的持有者不是当前线程，抛出异常
 3     if (!isHeldExclusively())
 4         throw new IllegalMonitorStateException();
 5     //写锁的新线程数
 6     int nextc = getState() - releases;
 7     //如果独占模式重入数为0了，说明独占模式被释放
 8     boolean free = exclusiveCount(nextc) == 0;
 9     if (free)
10         //若写锁的新线程数为0，则将锁的持有者设置为null
11         setExclusiveOwnerThread(null);
12     //设置写锁的新线程数
13     //不管独占模式是否被释放，更新独占重入数
14     setState(nextc);
15     return free;
16 }
```

  写锁的释放过程还是相对而言比较简单的：首先查看当前线程是否为写锁的持有者，如果不是抛出异常。然后检查释放后写锁的线程数是否为0，如果为0则表示写锁空闲了，释放锁资源将锁的持有线程设置为null，否则释放仅仅只是一次重入锁而已，并不能将写锁的线程清空。

  说明：此方法用于释放写锁资源，首先会判断该线程是否为独占线程，若不为独占线程，则抛出异常，否则，计算释放资源后的写锁的数量，若为0，表示成功释放，资源不将被占用，否则，表示资源还被占用。其方法流程图如下。

![img](https://images2018.cnblogs.com/blog/249993/201806/249993-20180607131006282-1633551158.png)

**5、读锁的获取与释放**

类似于写锁，读锁的lock和unlock的实际实现对应Sync的 tryAcquireShared 和 tryReleaseShared方法。

**读锁的获取，看下tryAcquireShared方法**

```
 1 protected final int tryAcquireShared(int unused) {
 2     // 获取当前线程
 3     Thread current = Thread.currentThread();
 4     // 获取状态
 5     int c = getState();
 6     
 7     //如果写锁线程数 != 0 ，且独占锁不是当前线程则返回失败，因为存在锁降级
 8     if (exclusiveCount(c) != 0 &&
 9         getExclusiveOwnerThread() != current)
10         return -1;
11     // 读锁数量
12     int r = sharedCount(c);
13     /*
14      * readerShouldBlock():读锁是否需要等待（公平锁原则）
15      * r < MAX_COUNT：持有线程小于最大数（65535）
16      * compareAndSetState(c, c + SHARED_UNIT)：设置读取锁状态
17      */
18      // 读线程是否应该被阻塞、并且小于最大值、并且比较设置成功
19     if (!readerShouldBlock() &&
20         r < MAX_COUNT &&
21         compareAndSetState(c, c + SHARED_UNIT)) {
22         //r == 0，表示第一个读锁线程，第一个读锁firstRead是不会加入到readHolds中
23         if (r == 0) { // 读锁数量为0
24             // 设置第一个读线程
25             firstReader = current;
26             // 读线程占用的资源数为1
27             firstReaderHoldCount = 1;
28         } else if (firstReader == current) { // 当前线程为第一个读线程，表示第一个读锁线程重入
29             // 占用资源数加1
30             firstReaderHoldCount++;
31         } else { // 读锁数量不为0并且不为当前线程
32             // 获取计数器
33             HoldCounter rh = cachedHoldCounter;
34             // 计数器为空或者计数器的tid不为当前正在运行的线程的tid
35             if (rh == null || rh.tid != getThreadId(current)) 
36                 // 获取当前线程对应的计数器
37                 cachedHoldCounter = rh = readHolds.get();
38             else if (rh.count == 0) // 计数为0
39                 //加入到readHolds中
40                 readHolds.set(rh);
41             //计数+1
42             rh.count++;
43         }
44         return 1;
45     }
46     return fullTryAcquireShared(current);
47 }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 其中sharedCount方法表示占有读锁的线程数量，源码如下：

```
static int sharedCount(int c)    { return c >>> SHARED_SHIFT; }
```

说明：直接将state右移16位，就可以得到读锁的线程数量，因为state的高16位表示读锁，对应的第十六位表示写锁数量。

  读锁获取锁的过程比写锁稍微复杂些，首先判断写锁是否为0并且当前线程不占有独占锁，直接返回；否则，判断读线程是否需要被阻塞并且读锁数量是否小于最大值并且比较设置状态成功，若当前没有读锁，则设置第一个读线程firstReader和firstReaderHoldCount；若当前线程线程为第一个读线程，则增加firstReaderHoldCount；否则，将设置当前线程对应的HoldCounter对象的值。流程图如下。

![img](https://images2018.cnblogs.com/blog/249993/201806/249993-20180607131704903-887096141.png)

注意：更新成功后会在firstReaderHoldCount中或readHolds(ThreadLocal类型的)的本线程副本中记录当前线程重入数（23行至43行代码），这是为了实现jdk1.6中加入的getReadHoldCount()方法的，这个方法能获取当前线程重入共享锁的次数(state中记录的是多个线程的总重入次数)，加入了这个方法让代码复杂了不少，但是其原理还是很简单的：如果当前只有一个线程的话，还不需要动用ThreadLocal，直接往firstReaderHoldCount这个成员变量里存重入数，当有第二个线程来的时候，就要动用ThreadLocal变量readHolds了，每个线程拥有自己的副本，用来保存自己的重入数。

fullTryAcquireShared方法：

```
final int fullTryAcquireShared(Thread current) {

    HoldCounter rh = null;
    for (;;) { // 无限循环
        // 获取状态
        int c = getState();
        if (exclusiveCount(c) != 0) { // 写线程数量不为0
            if (getExclusiveOwnerThread() != current) // 不为当前线程
                return -1;
        } else if (readerShouldBlock()) { // 写线程数量为0并且读线程被阻塞
            // Make sure we're not acquiring read lock reentrantly
            if (firstReader == current) { // 当前线程为第一个读线程
                // assert firstReaderHoldCount > 0;
            } else { // 当前线程不为第一个读线程
                if (rh == null) { // 计数器不为空
                    // 
                    rh = cachedHoldCounter;
                    if (rh == null || rh.tid != getThreadId(current)) { // 计数器为空或者计数器的tid不为当前正在运行的线程的tid
                        rh = readHolds.get();
                        if (rh.count == 0)
                            readHolds.remove();
                    }
                }
                if (rh.count == 0)
                    return -1;
            }
        }
        if (sharedCount(c) == MAX_COUNT) // 读锁数量为最大值，抛出异常
            throw new Error("Maximum lock count exceeded");
        if (compareAndSetState(c, c + SHARED_UNIT)) { // 比较并且设置成功
            if (sharedCount(c) == 0) { // 读线程数量为0
                // 设置第一个读线程
                firstReader = current;
                // 
                firstReaderHoldCount = 1;
            } else if (firstReader == current) {
                firstReaderHoldCount++;
            } else {
                if (rh == null)
                    rh = cachedHoldCounter;
                if (rh == null || rh.tid != getThreadId(current))
                    rh = readHolds.get();
                else if (rh.count == 0)
                    readHolds.set(rh);
                rh.count++;
                cachedHoldCounter = rh; // cache for release
            }
            return 1;
        }
    }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

说明：在tryAcquireShared函数中，如果下列三个条件不满足（读线程是否应该被阻塞、小于最大值、比较设置成功）则会进行fullTryAcquireShared函数中，它用来保证相关操作可以成功。其逻辑与tryAcquireShared逻辑类似，不再累赘。



```
 1 protected final boolean tryReleaseShared(int unused) {
 2     // 获取当前线程
 3     Thread current = Thread.currentThread();
 4     if (firstReader == current) { // 当前线程为第一个读线程
 5         // assert firstReaderHoldCount > 0;
 6         if (firstReaderHoldCount == 1) // 读线程占用的资源数为1
 7             firstReader = null;
 8         else // 减少占用的资源
 9             firstReaderHoldCount--;
10     } else { // 当前线程不为第一个读线程
11         // 获取缓存的计数器
12         HoldCounter rh = cachedHoldCounter;
13         if (rh == null || rh.tid != getThreadId(current)) // 计数器为空或者计数器的tid不为当前正在运行的线程的tid
14             // 获取当前线程对应的计数器
15             rh = readHolds.get();
16         // 获取计数
17         int count = rh.count;
18         if (count <= 1) { // 计数小于等于1
19             // 移除
20             readHolds.remove();
21             if (count <= 0) // 计数小于等于0，抛出异常
22                 throw unmatchedUnlockException();
23         }
24         // 减少计数
25         --rh.count;
26     }
27     for (;;) { // 无限循环
28         // 获取状态
29         int c = getState();
30         // 获取状态
31         int nextc = c - SHARED_UNIT;
32         if (compareAndSetState(c, nextc)) // 比较并进行设置
33             // Releasing the read lock has no effect on readers,
34             // but it may allow waiting writers to proceed if
35             // both read and write locks are now free.
36             return nextc == 0;
37     }
38 }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

  说明：此方法表示读锁线程释放锁。首先判断当前线程是否为第一个读线程firstReader，若是，则判断第一个读线程占有的资源数firstReaderHoldCount是否为1，若是，则设置第一个读线程firstReader为空，否则，将第一个读线程占有的资源数firstReaderHoldCount减1；若当前线程不是第一个读线程，那么首先会获取缓存计数器（上一个读锁线程对应的计数器 ），若计数器为空或者tid不等于当前线程的tid值，则获取当前线程的计数器，如果计数器的计数count小于等于1，则移除当前线程对应的计数器，如果计数器的计数count小于等于0，则抛出异常，之后再减少计数即可。无论何种情况，都会进入无限循环，该循环可以确保成功设置状态state。其流程图如下。

![img](https://images2018.cnblogs.com/blog/249993/201806/249993-20180607132608771-1291388784.png)

  在读锁的获取、释放过程中，总是会有一个对象存在着，同时该对象在获取线程获取读锁是+1，释放读锁时-1，该对象就是HoldCounter。

  要明白HoldCounter就要先明白读锁。前面提过读锁的内在实现机制就是共享锁，对于共享锁其实我们可以稍微的认为它不是一个锁的概念，它更加像一个计数器的概念。一次共享锁操作就相当于一次计数器的操作，获取共享锁计数器+1，释放共享锁计数器-1。只有当线程获取共享锁后才能对共享锁进行释放、重入操作。所以HoldCounter的作用就是当前线程持有共享锁的数量，这个数量必须要与线程绑定在一起，否则操作其他线程锁就会抛出异常。

先看读锁获取锁的部分：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
if (r == 0) {//r == 0，表示第一个读锁线程，第一个读锁firstRead是不会加入到readHolds中
    firstReader = current;
    firstReaderHoldCount = 1;
} else if (firstReader == current) {//第一个读锁线程重入
    firstReaderHoldCount++;    
} else {    //非firstReader计数
    HoldCounter rh = cachedHoldCounter;//readHoldCounter缓存
    //rh == null 或者 rh.tid != current.getId()，需要获取rh
    if (rh == null || rh.tid != current.getId())    
        cachedHoldCounter = rh = readHolds.get();
    else if (rh.count == 0)
        readHolds.set(rh);  //加入到readHolds中
    rh.count++; //计数+1
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

  这里为什么要搞一个firstRead、firstReaderHoldCount呢？而不是直接使用else那段代码？这是为了一个效率问题，firstReader是不会放入到readHolds中的，如果读锁仅有一个的情况下就会避免查找readHolds。可能就看这个代码还不是很理解HoldCounter。我们先看firstReader、firstReaderHoldCount的定义：

```
private transient Thread firstReader = null;
private transient int firstReaderHoldCount;
```

这两个变量比较简单，一个表示线程，当然该线程是一个特殊的线程，一个是firstReader的重入计数。

HoldCounter的定义：

```
static final class HoldCounter {
    int count = 0;
    final long tid = Thread.currentThread().getId();
}
```

  在HoldCounter中仅有count和tid两个变量，其中count代表着计数器，tid是线程的id。但是如果要将一个对象和线程绑定起来仅记录tid肯定不够的，而且HoldCounter根本不能起到绑定对象的作用，只是记录线程tid而已。

  诚然，在java中，我们知道如果要将一个线程和对象绑定在一起只有ThreadLocal才能实现。所以如下：

```
static final class ThreadLocalHoldCounter
    extends ThreadLocal<HoldCounter> {
    public HoldCounter initialValue() {
        return new HoldCounter();
    }
}
 ThreadLocalHoldCounter继承ThreadLocal，并且重写了initialValue方法。
```

  故而，HoldCounter应该就是绑定线程上的一个计数器，而ThradLocalHoldCounter则是线程绑定的ThreadLocal。从上面我们可以看到ThreadLocal将HoldCounter绑定到当前线程上，同时HoldCounter也持有线程Id，这样在释放锁的时候才能知道ReadWriteLock里面缓存的上一个读取线程（cachedHoldCounter）是否是当前线程。这样做的好处是可以减少ThreadLocal.get()的次数，因为这也是一个耗时操作。需要说明的是这样HoldCounter绑定线程id而不绑定线程对象的原因是避免HoldCounter和ThreadLocal互相绑定而GC难以释放它们（尽管GC能够智能的发现这种引用而回收它们，但是这需要一定的代价），所以其实这样做只是为了帮助GC快速回收对象而已。

**总结**

  通过上面的源码分析，我们可以发现一个现象：

  **在线程持有读锁的情况下，该线程不能取得写锁(因为获取写锁的时候，如果发现当前的读锁被占用，就马上获取失败，不管读锁是不是被当前线程持有)。**

  **在线程持有写锁的情况下，该线程可以继续获取读锁（获取读锁时如果发现写锁被占用，只有写锁没有被当前线程占用的情况才会获取失败）**。

  仔细想想，这个设计是合理的：**因为当线程获取读锁的时候，可能有其他线程同时也在持有读锁，因此不能把获取读锁的线程“升级”为写锁；而对于获得写锁的线程，它一定独占了读写锁，因此可以继续让它获取读锁，当它同时获取了写锁和读锁后，还可以先释放写锁继续持有读锁，这样一个写锁就“降级”为了读锁。**

综上：

**一个线程要想同时持有写锁和读锁，必须先获取写锁再获取读锁；写锁可以“降级”为读锁；读锁不能“升级”为写锁。**

##### [4] StampedLock

一、StampedLock类简介

StampedLock类，在JDK1.8时引入，是对读写锁ReentrantReadWriteLock的增强，该类提供了一些功能，优化了读锁、写锁的访问，同时使读写锁之间可以互相转换，更细粒度控制并发。

首先明确下，该类的设计初衷是作为一个内部工具类，用于辅助开发其它线程安全组件，用得好，该类可以提升系统性能，用不好，容易产生死锁和其它莫名其妙的问题。

1.1 StampedLock的引入

> 先来看下，为什么有了ReentrantReadWriteLock，还要引入StampedLock？

ReentrantReadWriteLock使得多个读线程同时持有读锁（只要写锁未被占用），而写锁是独占的。

但是，读写锁如果使用不当，很容易产生“饥饿”问题：

比如在读线程非常多，写线程很少的情况下，很容易导致写线程“饥饿”，虽然使用“公平”策略可以一定程度上缓解这个问题，但是“公平”策略是以牺牲系统吞吐量为代价的。（在[ReentrantLock类](https://segmentfault.com/a/1190000015562293)的介绍章节中，介绍过这种情况）

1.2 StampedLock的特点

链接：https://segmentfault.com/a/1190000015808032?utm_source=tag-newest

StampedLock的主要特点概括一下，有以下几点：

1. 所有获取锁的方法，都返回一个邮戳（Stamp），Stamp为0表示获取失败，其余都表示成功；
2. 所有释放锁的方法，都需要一个邮戳（Stamp），这个Stamp必须是和成功获取锁时得到的Stamp一致；
3. StampedLock是不可重入的；（如果一个线程已经持有了写锁，再去获取写锁的话就会造成死锁）
4. StampedLock有三种访问模式：
   ①Reading（读模式）：功能和ReentrantReadWriteLock的读锁类似
   ②Writing（写模式）：功能和ReentrantReadWriteLock的写锁类似
   ③Optimistic reading（乐观读模式）：这是一种优化的读模式。
5. StampedLock支持读锁和写锁的相互转换
   我们知道RRW中，当线程获取到写锁后，可以降级为读锁，但是读锁是不能直接升级为写锁的。
   StampedLock提供了读锁和写锁相互转换的功能，使得该类支持更多的应用场景。
6. 无论写锁还是读锁，都不支持Conditon等待

> 我们知道，在ReentrantReadWriteLock中，当读锁被使用时，如果有线程尝试获取写锁，该写线程会阻塞。
> 但是，在Optimistic reading中，即使读线程获取到了读锁，写线程尝试获取写锁也不会阻塞，这相当于对读模式的优化，但是可能会导致数据不一致的问题。所以，当使用Optimistic reading获取到读锁时，必须对获取结果进行校验。

##### [5] Semaphore

Semaphore 类似于操作系统中的信号量，可以控制对互斥资源的访问线程数，以此**限制能同时访问共享资源的线程上限**。

~~~java
public static void main(String[] args) {
 // 1. 创建 semaphore 对象
 Semaphore semaphore = new Semaphore(3);
 // 2. 10个线程同时运行
 for (int i = 0; i < 10; i++) {
 new Thread(() -> {
 // 3. 获取许可
 try {
 semaphore.acquire();
 } catch (InterruptedException e) {
 e.printStackTrace();
 }
 try {
 log.debug("running...");
 sleep(1);
 log.debug("end...");
 } finally {
 // 4. 释放许可
 semaphore.release();
 }
 }).start();
 }
 }
~~~

~~~java
static final class NonfairSync extends Sync {
 private static final long serialVersionUID = -2694183684443567898L;
 NonfairSync(int permits) {
 // permits 即 state
 super(permits);
 }
 
 // Semaphore 方法, 方便阅读, 放在此处
 public void acquire() throws InterruptedException {
 sync.acquireSharedInterruptibly(1);
 }
 // AQS 继承过来的方法, 方便阅读, 放在此处
 public final void acquireSharedInterruptibly(int arg)
 throws InterruptedException {
 if (Thread.interrupted())
 throw new InterruptedException();
 if (tryAcquireShared(arg) < 0)
 doAcquireSharedInterruptibly(arg);
 }
 
 // 尝试获得共享锁
 protected int tryAcquireShared(int acquires) {
 return nonfairTryAcquireShared(acquires);
 }
 
 // Sync 继承过来的方法, 方便阅读, 放在此处
 final int nonfairTryAcquireShared(int acquires) {
 for (;;) {
 int available = getState();
 int remaining = available - acquires; 
 if (
 // 如果许可已经用完, 返回负数, 表示获取失败, 进入 doAcquireSharedInterruptibly
 remaining < 0 ||
 // 如果 cas 重试成功, 返回正数, 表示获取成功
 compareAndSetState(available, remaining)
北京市昌平区建材城西路金燕龙办公楼一层 电话：400-618-9090
 ) {
 return remaining;
 }
 }
 }
 
 // AQS 继承过来的方法, 方便阅读, 放在此处
 private void doAcquireSharedInterruptibly(int arg) throws InterruptedException {
 final Node node = addWaiter(Node.SHARED);
 boolean failed = true;
 try {
 for (;;) {
 final Node p = node.predecessor();
 if (p == head) {
 // 再次尝试获取许可
 int r = tryAcquireShared(arg);
 if (r >= 0) {
 // 成功后本线程出队（AQS）, 所在 Node设置为 head
 // 如果 head.waitStatus == Node.SIGNAL ==> 0 成功, 下一个节点 unpark
 // 如果 head.waitStatus == 0 ==> Node.PROPAGATE 
 // r 表示可用资源数, 为 0 则不会继续传播
 setHeadAndPropagate(node, r);
 p.next = null; // help GC
 failed = false;
 return;
 }
 }
 // 不成功, 设置上一个节点 waitStatus = Node.SIGNAL, 下轮进入 park 阻塞
 if (shouldParkAfterFailedAcquire(p, node) &&
 parkAndCheckInterrupt())
 throw new InterruptedException();
 }
 } finally {
 if (failed)
 cancelAcquire(node);
 }
 }
 
 // Semaphore 方法, 方便阅读, 放在此处
 public void release() {
 sync.releaseShared(1);
 }
 
 // AQS 继承过来的方法, 方便阅读, 放在此处
 public final boolean releaseShared(int arg) {
 if (tryReleaseShared(arg)) {
 doReleaseShared();
 return true;
 }
 return false;
 }
 
 // Sync 继承过来的方法, 方便阅读, 放在此处
北京市昌平区建材城西路金燕龙办公楼一层 电话：400-618-9090
3. 为什么要有 PROPAGATE
早期有 bug
releaseShared 方法
doAcquireShared 方法
 protected final boolean tryReleaseShared(int releases) {
 for (;;) {
 int current = getState();
 int next = current + releases;
 if (next < current) // overflow
 throw new Error("Maximum permit count exceeded");
 if (compareAndSetState(current, next))
 return true;
 }
 }
}
~~~

##### **[8] threadlocal**

https://www.bilibili.com/video/BV1SJ41157oF

使用ThreadLocal维护变量时，其为每个使用该变量的线程提供独立的变量副本，所以**每一个线程都可以独立的改变自己的副本，而不会影响其他线程对应的副本**。

**ThreadLocal内部实现机制：**

- **每个线程内部都会维护一个Map对象**，称为**ThreadLocalMap**，里边会包含若干了**Entry（K-V键值对）**，相应的线程被称为这些Entry的属主线程。
- **Entry的Key是一个ThreadLocal实例，Value是一个线程特有对象**。Entry的作用是为其属主线程建立起一个ThreadLocal实例与一个线程特有对象之间的对应关系
- **Entry**对Key的引用是弱引用；**Entry**对Value的引用是强引用（key时弱引用便于垃圾回收）。

可以用于**日期处理**，**随机数**，**上下文信息**。

**当某些数据是以线程为作用域并且不同线程有不同数据副本时，考虑ThreadLocal。**https://www.jianshu.com/p/3a09dd40f8a4

##### [9] CountDownLatch

**答：** 两个关键字经常放在一起比较和考察，下边我们分别介绍。

**CountDownLatch**是一个**倒计时协调器**，它可以实现一个或者多个线程等待其余线程完成一组特定的操作之后，继续运行。

**CountDownLatch的内部实现如下：**

- **CountDownLatch**内部维护一个计数器，CountDownLatch.countDown（）每被执行一次都会使计数器值减少1。

- **当计数器不为0时**，CountDownLatch.await（）方法的调用将会导致执行线程被暂停，这些线程就叫做该CountDownLatch上的等待线程。

- CountDownLatch.countDown（）相当于一个通知方法，**当计数器值达到0时**，唤醒所有等待线程。当然对应还有指定等待时间长度的CountDownLatch.await( long , TimeUnit)方法。

##### [10] CyclicBarrier？

**CyclicBarrier**是**一个栅栏**，可以实现多个线程相互等待执行到指定的地点，这时候这些线程会再接着执行，在实际工作中可以用来**模拟高并发请求测试**。

**可以认为是这样的**，当我们爬山的时候，到了一个平坦处，前面队伍会稍作休息，等待后边队伍跟上来，当最后一个爬山伙伴也达到该休息地点时，所有人同时开始从该地点出发，继续爬山。

**CyclicBarrier的内部实现如下：**

- 使用CyclicBarrier实现等待的线程被称为**参与方（Party）**，参与方只需要执行CyclicBarrier.await（）就可以实现等待，**该栅栏维护了一个显示锁**，可以识别出最后一个参与方，**当最后一个参与方调用await（）方法时**，前面等待的参与方都会被唤醒，并且该最后一个参与方也不会被暂停。
- **CyclicBarrier内部维护了一个计数器变量count = 参与方的个数**，调用await方法可以使得count -1。**当判断到是最后一个参与方时**，调用singalAll唤醒所有线程。

##### [10] Atmoic

**答：**介绍Atomic之前先来看一个问题吧，**i++操作是线程安全的吗**？

i++操作并不是线程安全的，它是一个复合操作，包含三个步骤：

- **拷贝i的值到临时变量**
- **临时变量++操作**
- **拷贝回原始变量i**

这是一个**复合操作，不能保证原子性**，所以这不是线程安全的操作。**那么如何实现原子自增等操作呢？**

这里就用到了JDK在java.util.concurrent.atomic包下的AtomicInteger等原子类了。**AtomicInteger类提供了getAndIncrement和incrementAndGet等原子性的自增自减等操作**。**Atomic等原子类内部使用了CAS来保证原子性。**

##### **[11] [FutureTask](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=futuretask)**

在介绍 Callable 时我们知道它可以有返回值，返回值通过 Future 进行封装。FutureTask 实现了 RunnableFuture 接口，该接口继承自 Runnable 和 Future 接口，这使得 FutureTask 既可以当做一个任务执行，也可以有返回值。

FutureTask 可用于异步获取执行结果或取消执行任务的场景。当一个计算任务需要执行很长时间，那么就可以用 FutureTask 来封装这个任务，主线程在完成自己的任务之后再去获取结果。

##### **[12] [ForkJoin](https://cyc2018.github.io/CS-Notes/#/notes/Java 并发?id=forkjoin)**

主要用于并行计算中，和 MapReduce 原理类似，都是把大的计算任务拆分成多个小任务并行计算。

ForkJoinPool 实现了工作窃取算法来提高 CPU 的利用率。每个线程都维护了一个双端队列，用来存储需要执行的任务。工作窃取算法允许空闲的线程从其它线程的双端队列中窃取一个任务来执行。窃取的任务必须是最晚的任务，避免和队列所属线程发生竞争。例如下图中，Thread2 从 Thread1 的队列中拿出最晚的 Task1 任务，Thread1 会拿出 Task2 来执行，这样就避免发生竞争。但是如果队列中只有一个任务时还是会发生竞争。

### 【<Java中的线程池>】

##### [1] 使用线程池的好处

为了降低资源消耗，提高响应速度，提高线程的可管理性，所以出现了线程池。

1. **降低资源消耗**：通过重复利用已创建的线程降低线程创建和销毁造成的消耗;
2. **提高响应速度**：当任务到达时，任务可以不需要的等到线程创建就能立即执行;
3. **提高线程的可管理性**：线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。

##### **[2] [Executor框架](https://www.cnblogs.com/zxrxzw/p/12116209.html)**

**1. 什么是Executor框架？**

我们知道线程池就是线程的集合，线程池集中管理线程，以实现线程的重用，降低资源消耗，提高响应速度等。线程用于执行异步任务，单个的线程既是工作单元也是执行机制。从JDK1.5开始，为了把工作单元与执行机制分离开，**Executor框架是一个统一创建与运行的接口。Executor框架实现的就是线程池的功能。**

**2. Executor框架结构图解**

Executor框架包括3大部分：

（1）**任务**：也就是工作单元，包括被执行任务需要实现的接口：Runnable接口或者Callable接口；

（2）**任务的执行**：也就是把任务分派给多个线程的执行机制，包括Executor接口及继承自Executor接口的ExecutorService接口。

（3）**异步计算的结果**：包括Future接口及实现了Future接口的[FutureTask](https://www.cnblogs.com/zhumiao/p/9492360.html)类。

**3. Executor框架成员：**

ThreadPoolExecutor实现类、ScheduledThreadPoolExecutor实现类、Future接口、Runnable和Callable接口、Executors工厂类

<img src="https://img2018.cnblogs.com/i-beta/1598528/201912/1598528-20191229194601187-1917151311.png" alt="img" style="zoom:50%;" />

##### [3] ThreadPoolExecutor类的七大参数字段

~~~java
    public ThreadPoolExecutor(int corePoolSize,
                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue<Runnable> workQueue,
                              ThreadFactory threadFactory,
                              RejectedExecutionHandler handler)
~~~

- **corePoolSize：核心线程数**：线程池中会维护一个最小的线程数量，即使这些线程处于空闲状态，他们也不会被销毁（除非设置了allowCoreThreadTimeOut），而且线程数小于此值的话，仍然会创建新的线程。
- **maximumPoolSize：最大线程数**：线程池所能容的最多线程数量。一个任务被提交到线程池后，首先会缓存到工作队列中，如果工作队列满了，则会创建一个新线程，然后从工作队列中的取出一个任务交由新线程来处理，而将刚提交的任务放入工作队列。线程池不会无限制的去创建新线程，它会有一个最大线程数量的限制，这个数量即由maximunPoolSize来指定。
- **keepAliveTime ：线程空闲的保活时间**：一个线程如果处于空闲状态，并且当前的线程数量大于corePoolSize，那么在指定时间后，这个空闲线程会被销毁，这里的指定时间由keepAliveTime来设定。
- **unit：时间单位**：keepAliveTime的计量单位。
- **workQueue：存储线程的队列**：新任务被提交后，会先进入到此工作队列中，任务调度时再从队列中取出任务。jdk中提供了四种工作队列。
- **threadFactory：创建线程的工厂**：创建一个新线程时使用的工厂，可以用来设定线程名、是否为daemon线程等等
- **handler：拒绝策略**：当工作队列中的任务已到达最大限制，并且线程池中的线程数量也达到最大限制，这时如果有新任务提交进来，该如何处理呢。这里的拒绝策略，就是解决这个问题的，jdk中提供了**4种**拒绝策略。

##### [4]  **线程池的排队策略**

1. 当线程数达到 小于**corePoolSize** ，即使有空闲队列，线程池也会优先创建一个新线程来执行任务。
2. 当线程数达到 corePoolSize 且并没有线程空闲时，加入任务，这时候会有两种情况：
   * 如果队列选择了**无界队列**，新加的任务会被加入workQueue 队列排队，直到有空闲的线程。
   * 如果队列选择了**有界队列**，任务会优先入队，那么任务超过了队列大小时，会创建 maximumPoolSize - corePoolSize 数目的线程来救急，若此范围线程空闲，则有keepAliveTime决定存活时间。
3. **针对有界队列**，如果线程到达 maximumPoolSize 仍然有新任务这时会执行拒绝策略。拒绝策略 jdk 提供了 4 种实现，其它著名框架也提供了实现。
4. **针对有界队列**，当高峰过去后，超过corePoolSize 的救急线程如果一段时间没有任务做，需要结束节省资源，这个时间由keepAliveTime 和 unit 来控制。

##### [6] 四种拒绝策略

**四种线程池拒绝策略**

当线程池的任务缓存队列已满并且线程池中的线程数目达到maximumPoolSize时，如果还有任务到来就会采取任务拒绝策略，可能是由于：第一，线程池异常关闭。第二，任务数量超过线程池的最大限制。线程池共包括4种拒绝策略，它们分别是：**AbortPolicy**, **CallerRunsPolicy**, **DiscardOldestPolicy**和**DiscardPolicy**。通常有以下四种策略：

* ThreadPoolExecutor.AbortPolicy:丢弃任务并抛出RejectedExecutionException异常。 
* ThreadPoolExecutor.DiscardPolicy：丢弃任务，但是不抛出异常。 
* ThreadPoolExecutor.DiscardOldestPolicy：丢弃队列最前面的任务，然后重新提交被拒绝的任务
* ThreadPoolExecutor.CallerRunsPolicy：由调用线程（提交任务的线程）处理该任务

**框架实现：**

+ Dubbo 的实现，在抛出 RejectedExecutionException 异常之前会记录日志，并 dump 线程栈信息，方
  便定位问题
+ Netty 的实现，是创建一个新线程来执行任务
+ ActiveMQ 的实现，带超时等待（60s）尝试放入队列，类似我们之前自定义的拒绝策略
+ PinPoint 的实现，它使用了一个拒绝策略链，会逐一尝试策略链中每种拒绝策略

##### [5] 常见的阻塞队列

https://blog.csdn.net/xiewenfeng520/article/details/107142566

前面我们介绍了线程池内部有一个排队策略，任务可能需要在队列中进行排队等候。常见的阻塞队列包括如下的四种，接下来我们一起来看看吧。

* **ArrayBlockingQueue（有界）**：**基于数组的有界阻塞队列，按FIFO排序**。新任务进来后，会放到该队列的队尾，有界的数组可以防止资源耗尽问题。当线程池中线程数量达到corePoolSize后，再有新任务进来，则会将任务放入该队列的队尾，等待被调度。如果队列已经是满的，则创建一个新线程，如果线程数量已经达到maxPoolSize，则会执行拒绝策略。
* **LinkedBlockingQuene（无界）**：**基于链表的无界阻塞队列（其实最大容量为Interger.MAX），按照FIFO排序**。由于该队列的近似无界性，当线程池中线程数量达到corePoolSize后，再有新任务进来，会一直存入该队列，而不会去创建新线程直到maxPoolSize，因此使用该工作队列时，参数maxPoolSize其实是不起作用的。

* **SynchronousQuene（有界）**：**同步队列，一个不缓存任务的阻塞队列**，生产者放入一个任务必须等到消费者取出这个任务。也就是说新任务进来时，不会缓存，而是直接被调度执行该任务，如果没有可用线程，则创建新线程，如果线程数量达到maxPoolSize，则执行拒绝策略。

* **PriorityBlockingQueue（无界）**：**具有优先级的无界阻塞队列**，优先级通过参数Comparator实现。

> **阻塞队列特点及其使用场景：**
>
> **ArrayBlockingQueue（有界）:**
>
> - 内部使用一个**数组**作为其存储空间，数组的存储空间是**预先分配**的
> - **优点是** put 和 take操作不会增加GC的负担（因为空间是预先分配的）
> - **缺点是** put 和 take操作使用同一个锁，可能导致锁争用，导致较多的上下文切换。
> - 会执行拒绝策略，有救急线程
> - ArrayBlockingQueue适合在生产者线程和消费者线程之间的**并发程度较低**的情况下使用。
>
> **LinkedBlockingQueue：**
>
> - 是一个无界队列（其实队列长度是Integer.MAX_VALUE）
> - 内部存储空间是一个**链表**，并且链表节点所需的**存储空间是动态分配**的
> - **优点是** put 和 take 操作使用两个显式锁（putLock和takeLock）
> - **缺点是**增加了GC的负担，因为空间是动态分配的。
> - 不会执行拒绝策略，无救急线程
> - LinkedBlockingQueue适合在生产者线程和消费者线程之间的**并发程度较高**的情况下使用。
>
> **SynchronousQueue：**
>
> * SynchronousQueue可以被看做一种特殊的**有界**队列。
> * 生产者线程生产一个产品之后，会等待消费者线程来取走这个产品，才会接着生产下一个产品。
> * 适合在生产者线程和消费者线程之间的处理**能力相差不大**的情况下使用。

##### [6] Java提供的四种线程池

Executors只是对线程池一些特定情况的简洁使用，直接用ThreadPoolExecutor构造线程池会获得更为强大的功能。java自带的四种线程池通过 ThreadPoolExecutor 的构造方法实现：

1. **newCachedThreadPool**：是一个**高速缓存**线程池，根据需要来创建线程的线程池，它的corePoolSize为0，maximumPoolSize设置为Integer.MAX_VALUE，所以maximumPool是**无界**的，可创建临时线程数是**无限**的。keepAliveTime设置为60L，代表所有空闲线程等待新任务的最长时间为60L。

> 这意味着，如果主线程提交任务的速度高于maxiunmPool中线程处理任务的速度时，将会不断CachedThreadPool创建新线程。极端情况下会耗尽CPU资源。所以它适用于**负载较轻**的场景，执行短期异步任务如果线程池长度超过处理需要，**可灵活回收空闲线程**，若无可回收，则新建线程。（可以**使得任务快速得到执行**，因为任务时间执行短，可以很快结束，也不会造成cpu过度切换）

~~~java
public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }
~~~

2. **newFixedThreadPool**：创建一个**可重用固定线程数**的线程池，可控制线程最大并发数，超出的线程会无限在队列中等待。因为采用**无界**的阻塞队列LinkedBlockingQueue，所以maximumPoolSize和keepAliveTime为无效函数，实际线程数量永远不会变化，只会小于等于corePoolSize。

> 适用于**负载较重**的场景，对当前线程数量进行限制。（保证线程数可控，不会造成线程过多，导致系统负载更为严重）

~~~java
public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>());
}
~~~

3. **newSingleThreadExecutor**：创建一个**单线程**的线程池，适用于需要保证顺序执行各个任务。它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。它的corePoolSize和keepAliveTime设置为1，由于采用无界堵塞队列LinkedBlockingQueue，可以保证无限缓存任务，并且线程固定。

~~~java
public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
}
~~~

4. **newScheduledThreadPool**：它继承于ThreadPoolExecutor。创建一个**定长任务**线程池，适用于执行延时或者周期性任务。

~~~java
public class OneMoreStudy {
    public static void main(String[] args) {
        final SimpleDateFormat sdf = new SimpleDateFormat("HH:mm:ss");
        ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(3);
        System.out.println("提交时间: " + sdf.format(new Date()));
        scheduledThreadPool.schedule(new Runnable() {
                @Override
                public void run() {
                    System.out.println("运行时间: " + sdf.format(new Date()));
                }
            }, 3, TimeUnit.SECONDS);
        scheduledThreadPool.shutdown();
    }
}
~~~

##### [7] 手写一个线程池

![image-20200709145932351](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200709145932351.png)

~~~java
package cn.itcast.n8;

import lombok.extern.slf4j.Slf4j;
import org.springframework.core.log.LogDelegateFactory;

import java.util.ArrayDeque;
import java.util.Deque;
import java.util.HashSet;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

@Slf4j(topic = "c.TestPool")
public class TestPool {
    public static void main(String[] args) {
        ThreadPool threadPool = new ThreadPool(1,
                1000, TimeUnit.MILLISECONDS, 1, (queue, task)->{
            // 1. 死等
//            queue.put(task);
            // 2) 带超时等待
//            queue.offer(task, 1500, TimeUnit.MILLISECONDS);
            // 3) 让调用者放弃任务执行
//            log.debug("放弃{}", task);
            // 4) 让调用者抛出异常
//            throw new RuntimeException("任务执行失败 " + task);
            // 5) 让调用者自己执行任务
            task.run();
        });
        for (int i = 0; i < 4; i++) {
            int j = i;
            threadPool.execute(() -> {
                try {
                    Thread.sleep(1000L);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                log.debug("{}", j);
            });
        }
    }
}

@FunctionalInterface // 拒绝策略
interface RejectPolicy<T> {
    void reject(BlockingQueue<T> queue, T task);
}

@Slf4j(topic = "c.ThreadPool")
class ThreadPool {
    // 任务队列
    private BlockingQueue<Runnable> taskQueue;

    // 线程集合
    private HashSet<Worker> workers = new HashSet<>();

    // 核心线程数
    private int coreSize;

    // 获取任务时的超时时间
    private long timeout;

    private TimeUnit timeUnit;

    private RejectPolicy<Runnable> rejectPolicy;

    // 执行任务
    public void execute(Runnable task) {
        // 当任务数没有超过 coreSize 时，直接交给 worker 对象执行
        // 如果任务数超过 coreSize 时，加入任务队列暂存
        synchronized (workers) {
            if(workers.size() < coreSize) {
                Worker worker = new Worker(task);
                log.debug("新增 worker{}, {}", worker, task);
                workers.add(worker);
                worker.start();
            } else {
//                taskQueue.put(task);
                // 1) 死等
                // 2) 带超时等待
                // 3) 让调用者放弃任务执行
                // 4) 让调用者抛出异常
                // 5) 让调用者自己执行任务
                taskQueue.tryPut(rejectPolicy, task);
            }
        }
    }

    public ThreadPool(int coreSize, long timeout, TimeUnit timeUnit, int queueCapcity, RejectPolicy<Runnable> rejectPolicy) {
        this.coreSize = coreSize;
        this.timeout = timeout;
        this.timeUnit = timeUnit;
        this.taskQueue = new BlockingQueue<>(queueCapcity);
        this.rejectPolicy = rejectPolicy;
    }

    class Worker extends Thread{
        private Runnable task;

        public Worker(Runnable task) {
            this.task = task;
        }

        @Override
        public void run() {
            // 执行任务
            // 1) 当 task 不为空，执行任务
            // 2) 当 task 执行完毕，再接着从任务队列获取任务并执行
//            while(task != null || (task = taskQueue.take()) != null) {
            while(task != null || (task = taskQueue.poll(timeout, timeUnit)) != null) {
                try {
                    log.debug("正在执行...{}", task);
                    task.run();
                } catch (Exception e) {
                    e.printStackTrace();
                } finally {
                    task = null;
                }
            }
            synchronized (workers) {
                log.debug("worker 被移除{}", this);
                workers.remove(this);
            }
        }
    }
}
@Slf4j(topic = "c.BlockingQueue")
class BlockingQueue<T> {
    // 1. 任务队列
    private Deque<T> queue = new ArrayDeque<>();

    // 2. 锁
    private ReentrantLock lock = new ReentrantLock();

    // 3. 生产者条件变量
    private Condition fullWaitSet = lock.newCondition();

    // 4. 消费者条件变量
    private Condition emptyWaitSet = lock.newCondition();

    // 5. 容量
    private int capcity;

    public BlockingQueue(int capcity) {
        this.capcity = capcity;
    }

    // 带超时阻塞获取
    public T poll(long timeout, TimeUnit unit) {
        lock.lock();
        try {
            // 将 timeout 统一转换为 纳秒
            long nanos = unit.toNanos(timeout);
            while (queue.isEmpty()) {
                try {
                    // 返回值是剩余时间
                    if (nanos <= 0) {
                        return null;
                    }
                    nanos = emptyWaitSet.awaitNanos(nanos);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            T t = queue.removeFirst();
            fullWaitSet.signal();
            return t;
        } finally {
            lock.unlock();
        }
    }

    // 阻塞获取
    public T take() {
        lock.lock();
        try {
            while (queue.isEmpty()) {
                try {
                    emptyWaitSet.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            T t = queue.removeFirst();
            fullWaitSet.signal();
            return t;
        } finally {
            lock.unlock();
        }
    }

    // 阻塞添加
    public void put(T task) {
        lock.lock();
        try {
            while (queue.size() == capcity) {
                try {
                    log.debug("等待加入任务队列 {} ...", task);
                    fullWaitSet.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            log.debug("加入任务队列 {}", task);
            queue.addLast(task);
            emptyWaitSet.signal();
        } finally {
            lock.unlock();
        }
    }

    // 带超时时间阻塞添加
    public boolean offer(T task, long timeout, TimeUnit timeUnit) {
        lock.lock();
        try {
            long nanos = timeUnit.toNanos(timeout);
            while (queue.size() == capcity) {
                try {
                    if(nanos <= 0) {
                        return false;
                    }
                    log.debug("等待加入任务队列 {} ...", task);
                    nanos = fullWaitSet.awaitNanos(nanos);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            log.debug("加入任务队列 {}", task);
            queue.addLast(task);
            emptyWaitSet.signal();
            return true;
        } finally {
            lock.unlock();
        }
    }

    public int size() {
        lock.lock();
        try {
            return queue.size();
        } finally {
            lock.unlock();
        }
    }

    public void tryPut(RejectPolicy<T> rejectPolicy, T task) {
        lock.lock();
        try {
            // 判断队列是否满
            if(queue.size() == capcity) {
                rejectPolicy.reject(this, task);
            } else {  // 有空闲
                log.debug("加入任务队列 {}", task);
                queue.addLast(task);
                emptyWaitSet.signal();
            }
        } finally {
            lock.unlock();
        }
    }
}
~~~



# JVM

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408201336136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzUxODAzOA==,size_16,color_FFFFFF,t_70)

#### 1. 说一下 JVM 的主要组成部分？

1. 类加载器（ClassLoader）
2. 运行时数据区（Runtime Data Area）
3. 执行引擎（Execution Engine）
4. 本地库接口（Native Interface）

>1. **各组件的作用**？
>
>>首先通过类加载器会把 Java 代码转换成字节码，运行时数据区再把字节码加载到内存中，执行引擎负责将字节码翻译成底层系统指令，交由 CPU 去执行，而这个过程中需要调用其他语言的本地库接口来实现整个程序的功能。
>
>2. **Java中的类加载机制有了解吗？**
>
>> Java中的类加载机制指虚拟机把描述类的数据从 Class 文件加载到内存，并对数据进行校验、转换、解析和初始化，最终形成可以被虚拟机直接使用的 Java 类型。
>> 类从被加载到虚拟机内存中开始，到卸载出内存为止，它的整个生命周期包括了：加载、验证、准备、解析、初始化、使用、卸载七个阶段。类加载机制的保持则包括前面五个阶段。

#### 2. 谈谈对运行时数据区的理解？

![1](http://images.cnitblog.com/blog/587773/201409/061921034534396.png)

VM中的内存主要划分为5个区域，即**方法区**，**堆内存**，**虚拟机栈**，**本地方法栈**以及**程序计数器**。

1. **方法区**：它用于存储已被虚拟机加载的类型信息、常量、静态变量、即时编译器编译后的代码等（存储的数据一般持久性比较强）数据。
2. **堆内存**：在虚拟机启动时创建，存放**对象实例**。Java 堆是垃圾收集器管理的主要区域，因此很多时候也被称做“GC”堆（Garbage  Collected  Heap）。从内存回收的角度看，由于现在收集器基本都采用分代收集算法，所以 Java 堆中还可以细分为：新生代和老年代。
3. **虚拟机栈**：为虚拟机执行**Java方法**（也就是字节码）服务。
4. **本地方法栈**：为虚拟机使用到的 **Native**（调用非java代码的接口）方法服务。
5. **程序计数器**：是当前**线程所执行的字节码的行号指示器**。

>1. **哪些属于线程独占，哪些属于线程共享？**
>
>>线程共享：方法区，堆内存
>>线程独占：程序计数器，虚拟机栈以及本地方法栈
>
>2. **解释下运行时常量池？**
>
>>运行时常量池（Runtime  Constant  Pool）是方法区的一部分。Class 文件中除了有类的版本、字段、方法、接口等描述信息外，还有一些信息是常量池，**用于存放编译期生成的各种字面量和符号引用**，这部分内容将在类加载后进入方法区的运行时常量池中存放。
>
>3. **堆和栈的区别是什么？**
>
>> 从软件设计的角度看，栈代表了处理**逻辑**，而堆代表了**数据**。

#### 3. 谈谈对内存泄漏的理解？

在 Java 中，内存泄漏就是**存在一些不会再被使用确没有被回收的对象**，这些对象有下面两个特点：

1. 这些对象是**可达**的，即在有向图中，存在通路可以与其相连；
2. 这些对象是**无用**的，即程序以后不会再使用这些对象。

如果对象满足这两个条件，这些对象就可以判定为 Java 中的内存泄漏，这些对象不会被 GC 所回收，然而它却占用内存。

**哪些操作会造成内存泄漏？**

内存泄漏，就是不再需要的对象仍然存在内存中，内存泄漏不断堆积的后果就是内存溢出，即内存不够用。

垃圾回收机制会定期扫描对象，如果一个对象没有被其他对象引用，或两个对象互相引用但没有被第三个对象引用，则它们的内存会被回收。

\1. setTimeout 的第一个参数使用字符串而非函数的话,会引发内存泄露

\2. 全局变量

\3. 闭包

\4. dom清空或删除时，事件未清除导致的内存泄漏

\5. 控制台日志

\6. 循环

#### 4. JMM是什么？

`JMM`：Java内存模型，是java虚拟机规范中所定义的一种内存模型，Java内存模型是标准化的，屏蔽掉了底层不同计算机的区别（`注意这个跟JVM完全不是一个东西，现在还有小伙伴搞错的`）。

其实早期计算机中cpu和内存的速度是差不多的，但在现代计算机中，`cpu的指令速度远超内存的存取速度`，由于计算机的存储设备与处理器的运算速度有几个数量级的差距，所以现代计算机系统都不得不加入一层读写速度尽可能接近处理器运算速度的`高速缓存（Cache）`来作为内存与处理器之间的缓冲。

将运算需要使用到的数据复制到缓存中，让运算能快速进行，当运算结束后再从缓存同步回内存之中，这样处理器就无须等待缓慢的内存读写了。

基于高速缓存的存储交互很好地解决了处理器与内存的速度矛盾，但是也为计算机系统带来更高的复杂度，因为它引入了一个新的问题：`缓存一致性（CacheCoherence）`。

在多处理器系统中，每个处理器都有自己的高速缓存，而它们又共享同一主内存（MainMemory)

![image-20200518151220348](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200518151220348.png)

#### 5. 为什么要学习Jvm？

1. 为了更好的理解java语言
2. 为了再内存泄漏和溢出时候进行补救

#### 6.  什么是栈帧？

**每个方法再虚拟机栈被执行的时候，都会同步创建一个栈帧**，用于存储局部变量表，操作数栈，动态链接，方法出口等信息。每个方法被调用直至执行完毕的过程，就对应着一个栈帧在虚拟机中从入栈到出栈的过程。

#### 7.  Stop-The-World

一.概述：

java对象内存申请过程：

1.JVM会试图为相关Java对象在Eden中初始化一块内存区域；当Eden空间足够时，内存申请结束。否则到下一步；
 2.JVM试图释放在Eden中所有不活跃的对象（minor collection），释放后若Eden空间仍然不足以放入新对象，则试图将部分Eden中活跃对象放入Survivor区；
 3.Survivor区被用来作为Eden及old的中间交换区域，当old区空间足够时，Survivor区的对象会被移到Old区，否则会被保留在Survivor区；
 4.当old区空间不够时，JVM会在old区进行major collection；
 5.垃圾收集后，若Survivor及old区仍然无法存放从Eden复制过来的部分对象，导致JVM无法在Eden区为新对象创建内存区域，则出现"Out of memory错误"；

**Stop-The-World:**

在新生代进行的GC叫做minor GC，在老年代进行的GC都叫major GC，Full GC同时作用于新生代和老年代。在垃圾回收过程中经常涉及到对对象的挪动（比如上文提到的对象在Survivor 0和Survivor 1之间的复制），进而导致需要对对象引用进行更新。为了保证引用更新的正确性，Java将暂停所有其他的线程，这种情况被称为“Stop-The-World”，导致系统全局停顿。Stop-The-World对系统性能存在影响，因此垃圾回收的一个原则是尽量减少“Stop-The-World”的时间。

不同垃圾收集器的Stop-The-World情况，Serial、Parallel和CMS收集器均存在不同程度的Stop-The-Word情况；而即便是最新的G1收集器也不例外。

- Java中一种全局暂停的现象,jvm挂起状态
- 全局停顿，所有Java代码停止，native代码可以执行，但不能和JVM交互
- 多半由于jvm的GC引起，如：
  1.老年代空间不足。
  2.永生代（jkd7）或者元数据空间（jkd8）不足。
  3.System.gc()方法调用。
  4.CMS GC时出现promotion failed和concurrent mode failure
  5.YoungGC时晋升老年代的内存平均值大于老年代剩余空间
  6.有连续的大对象需要分配
- 除了GC还有以下原因：
  1.Dump线程--人为因素。
  2.死锁检查。
  3.堆Dump--人为因素。
  Full GC 是清理整个堆空间—包括年轻代和老年代。

**GC时为什么会有全局停顿？**

类比在聚会时打扫房间，聚会时很乱，又有新的垃圾产生，房间永远打扫不干净，只有让大家停止活动了，才能将房间打扫干净。当gc线程在处理垃圾的时候，其它java线程要停止才能彻底清除干净，否则会影响gc线程的处理效率增加gc线程负担，特别是在垃圾标记的时候。

**危害**

- **长时间服务停止，没有响应**
- **遇到HA系统，可能引起主备切换，严重危害生产环境。**
- 新生代的gc时间比较短（），危害小。
- 老年代的gc有时候时间短，但是有时候比较长几秒甚至100秒--几十分钟都有。
- 堆越大花的时间越长。
  链接：https://www.jianshu.com/p/d686e108d15f

#### 8. 元空间（Metaspace）

java8中移除了永久代，新增了元空间的概念。原来的方法区是逻辑划分中的一个区域，对应hotspot jdk6中的永久代，可以说永久代是方法区在hotspot的一个具体实现，但是从jdk7以后方法区就“四分五裂了”，不再是在单一的一个去区域内进行存储。

java8中继承了一些jdk7中的改变：符号引用存储在native heap中，字符串常量和静态类型变量存储在普通的堆区中，这个影响了String的intern()方法的行为，这里不做intern的详述。

而在java8中移除了永久代，新增了元空间，其实在这两者之间存储的内容几乎没怎么变化，而是在内存限制、垃圾回收等机制上改变较大。元空间的出现就是为了解决突出的类和类加载器元数据过多导致的OOM问题，而从jdk7中开始永久代经过对方法区的分裂后已经几乎只存储类和类加载器的元数据信息了，到了jdk8，元空间中也是存储这些信息，而符号引用、字符串常量等存储位置与jdk7一致，还是“分裂”的方法区。

符号引用没有存在元空间中，而是存在native heap中，这是两个方式和位置，不过都可以算作是本地内存，在虚拟机之外进行划分，没有设置限制参数时只受物理内存大小限制，即只有占满了操作系统可用内存后才OOM。
**链接**：https://www.jianshu.com/p/474d98fc4776

#### 9. 守护线程的作用

Daemon的作用是为其他线程的运行提供便利服务，守护线程最典型的应用就是 GC (垃圾回收器)，它就是一个很称职的守护者。

#### 10. JVM之方法区和永久代（现叫元空间）关系

方法区只是一种逻辑上的概念，**永久代**指物理上的堆内存的一块空间，这块实际的空间完成了方法区存储字节码、静态变量、常量的功能等等。既然如此，现在元空间也可以认为是新的方法区的实现了。

元空间与永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。因此，默认情况下，元空间的大小仅受本地内存限制，但可以通过以下参数来指定元空间的大小：

元空间不在jvm中啊，你的图怎么感觉在jvm中？

#### 11 方法区、永久代、元空间的区别

https://blog.csdn.net/qq_38262266/article/details/107208357?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~top_click~default-1-107208357.nonecase&utm_term=%E5%85%83%E7%A9%BA%E9%97%B4%E5%92%8C%E6%96%B9%E6%B3%95%E5%8C%BA%E7%9A%84%E5%8C%BA%E5%88%AB

#### 12 OOM

**1）什么是OOM？**

 OOM，全称“Out Of Memory”，翻译成中文就是“内存用完了”，来源于java.lang.OutOfMemoryError。看下关于的官方说明： Thrown when the Java Virtual Machine cannot allocate an object because it is out of memory, and no more memory could be made available by the garbage collector. 意思就是说，当JVM因为没有足够的内存来为对象分配空间并且垃圾回收器也已经没有空间可回收时，就会抛出这个error（注：非exception，因为这个问题已经严重到不足以被应用处理）。

 

**2）为什么会OOM？**

为什么会没有内存了呢？原因不外乎有两点：

1）分配的少了：比如虚拟机本身可使用的内存（一般通过启动时的VM参数指定）太少。

2）应用用的太多，并且用完没释放，浪费了。此时就会造成内存泄露或者内存溢出。

**内存泄露**：申请使用完的内存没有释放，导致虚拟机不能再次使用该内存，此时这段内存就泄露了，因为申请者不用了，而又不能被虚拟机分配给别人用。

**内存溢出**：申请的内存超出了JVM能提供的内存大小，此时称之为溢出。



在之前没有垃圾自动回收的日子里，比如C语言和C++语言，我们必须亲自负责内存的申请与释放操作，如果申请了内存，用完后又忘记了释放，比如C++中的new了但是没有delete，那么就可能造成内存泄露。偶尔的内存泄露可能不会造成问题，而大量的内存泄露可能会导致内存溢出。

 

而在Java语言中，由于存在了垃圾自动回收机制，所以，我们一般不用去主动释放不用的对象所占的内存，也就是理论上来说，是不会存在“内存泄露”的。但是，如果编码不当，比如，将某个对象的引用放到了全局的Map中，虽然方法结束了，但是由于垃圾回收器会根据对象的引用情况来回收内存，导致该对象不能被及时的回收。如果该种情况出现次数多了，就会导致内存溢出，比如系统中经常使用的缓存机制。Java中的内存泄露，不同于C++中的忘了delete，往往是逻辑上的原因泄露。

 

**3）OOM的类型**



JVM内存模型：

按照JVM规范，JAVA虚拟机在运行时会管理以下的内存区域：

- 程序计数器：当前线程执行的字节码的行号指示器，线程私有
- JAVA虚拟机栈：Java方法执行的内存模型，每个Java方法的执行对应着一个栈帧的进栈和出栈的操作。
- 本地方法栈：类似“ JAVA虚拟机栈 ”，但是为native方法的运行提供内存环境。
- JAVA堆：对象内存分配的地方，内存垃圾回收的主要区域，所有线程共享。可分为新生代，老生代。
- 方法区：用于存储已经被JVM加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。Hotspot中的“永久代”。
- 运行时常量池：方法区的一部分，存储常量信息，如各种字面量、符号引用等。
- 直接内存：并不是JVM运行时数据区的一部分， 可直接访问的内存， 比如NIO会用到这部分。

按照JVM规范，除了程序计数器不会抛出OOM外，其他各个内存区域都可能会抛出OOM。

 

最常见的OOM情况有以下三种：

- java.lang.OutOfMemoryError: Java heap space ------>java堆内存溢出，此种情况最常见，一般由于内存泄露或者堆的大小设置不当引起。对于内存泄露，需要通过内存监控软件查找程序中的泄露代码，而堆大小可以通过虚拟机参数-Xms,-Xmx等修改。
- java.lang.OutOfMemoryError: PermGen space ------>java永久代溢出，即方法区溢出了，一般出现于大量Class或者jsp页面，或者采用cglib等反射机制的情况，因为上述情况会产生大量的Class信息存储于方法区。此种情况可以通过更改方法区的大小来解决，使用类似-XX:PermSize=64m -XX:MaxPermSize=256m的形式修改。另外，过多的常量尤其是字符串也会导致方法区溢出。
- java.lang.StackOverflowError ------> 不会抛OOM error，但也是比较常见的Java内存溢出。JAVA虚拟机栈溢出，一般是由于程序中存在死循环或者深度递归调用造成的，栈大小设置太小也会出现此种溢出。可以通过虚拟机参数-Xss来设置栈的大小。



4）**OOM分析--heapdump**

要dump堆的内存镜像，可以采用如下两种方式：

- 设置JVM参数-XX:+HeapDumpOnOutOfMemoryError，设定当发生OOM时自动dump出堆信息。不过该方法需要JDK5以上版本。
- 使用JDK自带的jmap命令。"jmap -dump:format=b,file=heap.bin <pid>"  其中pid可以通过jps获取。

dump堆内存信息后，需要对dump出的文件进行分析，从而找到OOM的原因。常用的工具有：

- mat: eclipse memory analyzer, 基于eclipse RCP的内存分析工具。详细信息参见：http://www.eclipse.org/mat/，推荐使用。  
- jhat：JDK自带的java heap analyze tool，可以将堆中的对象以html的形式显示出来，包括对象的数量，大小等等，并支持对象查询语言OQL，分析相关的应用后，可以通过http://localhost:7000来访问分析结果。不推荐使用，因为在实际的排查过程中，一般是先在生产环境 dump出文件来，然后拉到自己的开发机器上分析，所以，不如采用高级的分析工具比如前面的mat来的高效。

这个链接：http://www.ibm.com/developerworks/cn/opensource/os-cn-ecl-ma/index.html中提供了一个采用mat分析的例子 。

 

注意：因为JVM规范没有对dump出的文件的格式进行定义，所以不同的虚拟机产生的dump文件并不是一样的。在分析时，需要针对不同的虚拟机的输出采用不同的分析工具（当然，有的工具可以兼容多个虚拟机的格式）。IBM HeapAnalyzer也是分析heap的一个常用的工具。

#### 【<类加载器专题>】

##### [1]  什么是类加载器？

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/335fe19c-4a76-45ab-9320-88c90d6a0d7e.png)

类是在运行期间第一次使用时动态加载的，而不是一次性加载所有类。因为如果一次性加载，那么会占用很多的内存。包括以下 7 个阶段（加点盐，准备解出时写）：

- **加载（Loading）**
- **验证（Verification）**
- **准备（Preparation）**
- **解析（Resolution）**
- **初始化（Initialization）**
- 使用（Using）
- 卸载（Unloading）

> **加点盐，准备解析初始化**

**[类加载过程：](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=类加载过程)**包含了加载、验证、准备、解析和初始化这 5 个阶段。

* **加载：加载是指将类的.class文件中的二进制数据读入到内存中，将其放在运行时数据区的方法区内，最后在堆区创建一个java.lang.Class对象，用来封装类在方法区内的数据结构**。

  > **加载过程完成以下三件事**：
  >
  > - 通过类的完全限定名称获取定义该类的二进制字节流。
  > - 将该字节流表示的静态存储结构转换为方法区的运行时存储结构。
  > - 在内存中生成一个代表该类的 Class 对象，作为方法区中该类各种数据的访问入口。
  >
  > 其中二进制字节流可以从以下方式中获取：
  >
  > - 从 ZIP 包读取，成为 JAR、EAR、WAR 格式的基础。
  > - 从网络中获取，最典型的应用是 Applet。
  > - 运行时计算生成，例如动态代理技术，在 java.lang.reflect.Proxy 使用 ProxyGenerator.generateProxyClass 的代理类的二进制字节流。
  > - 由其他文件生成，例如由 JSP 文件生成对应的 Class 类。


* **验证**：**验证的作用是确保被加载的类的正确性**，包括文件格式验证，元数据验证，字节码验证以及符号引用验证。


* **准备：准备阶段为类的静态(static)变量分配内存，并将其初始化为默认值**。

  >实例变量不会在这阶段分配内存，它会在对象实例化时随着对象一起被分配在堆中。应该注意到，实例化不是类加载的一个过程，类加载发生在所有实例化操作之前，并且类加载只进行一次，实例化可以进行多次。
  >
  >由于方法区是一个逻辑区域，所以在JDK8之后，类变量则会随着Class对象一起存放在Java堆中。假设一个类变量的定义为public static int val = 3;那么变量val在准备阶段过后的初始值不是3而是0。这是因为尚未执行任何java方法，而把value复制为12的putstatic指令是被编译后，存放再类构造器的<clinit>()方法中，所以把value复制为123的操作需等到类的初始化阶段才会被执行。


* **解析：解析阶段时java虚拟机将常量池内的符号引用转换为直接引用的过程**。解析包括：类或接口的解析，字段解析，方法解析，接口方法解析。

  >其中解析过程在某些情况下可以在初始化阶段之后再开始，这是为了支持 Java 的动态绑定。符号引用以一组符号来描述所引用的目标，符号可以是任何形式的字面量，只要使用时能够无歧义的定位到目标即可。

  > 1. 符号引用（Symbolic References）：
  >
  > 　　符号引用以一组符号来描述所引用的目标，符号可以是任何形式的字面量，只要使用时能够无歧义的定位到目标即可。例如，在Class文件中它以CONSTANT_Class_info、CONSTANT_Fieldref_info、CONSTANT_Methodref_info等类型的常量出现。符号引用与虚拟机的内存布局无关，引用的目标并不一定加载到内存中。在[Java](http://lib.csdn.net/base/javaee)中，一个java类将会编译成一个class文件。在编译时，java类并不知道所引用的类的实际地址，因此只能使用符号引用来代替。比如org.simple.People类引用了org.simple.Language类，在编译时People类并不知道Language类的实际内存地址，因此只能使用符号org.simple.Language（假设是这个，当然实际中是由类似于CONSTANT_Class_info的常量来表示的）来表示Language类的地址。各种虚拟机实现的内存布局可能有所不同，但是它们能接受的符号引用都是一致的，因为符号引用的字面量形式明确定义在Java虚拟机规范的Class文件格式中。
  >
  > 2. 直接引用
  >
  >  直接引用可以是
  >
  > （1）直接指向目标的指针（比如，指向“类型”【Class对象】、类变量、类方法的直接引用可能是指向方法区的指针）
  >
  > （2）相对偏移量（比如，指向实例变量、实例方法的直接引用都是偏移量）
  >
  > （3）一个能间接定位到目标的句柄
  >
  > 直接引用是和虚拟机的布局相关的，同一个符号引用在不同的虚拟机实例上翻译出来的直接引用一般不会相同。如果有了直接引用，那引用的目标必定已经被加载入内存中了。
  >
  > 


* **初始化**：**初始化阶段才真正开始执行类中定义的 Java 程序代码**。初始化阶段是虚拟机执行类构造器 <clinit>() 方法的过程。

  > 在准备阶段，类变量已经赋过一次系统要求的初始值，而在初始化阶段，根据程序员通过程序制定的主观计划去初始化类变量和其它资源。
  >
  > **<clinit>方法** 的内容: **所有的类变量初始化语句和类型的静态初始化器**



![å¨è¿éæå¥å¾çæè¿°](https://img-blog.csdnimg.cn/20190311124819452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ozMzMyMDU=,size_16,color_FFFFFF,t_70)

##### [2] 类加载器的分类有？

**启动类加载器（Bootstrap ClassLoader）**：启动类加载器负责加载存放在JDK\jre\lib(JDK代表JDK的安装目录，下同)下，或被-Xbootclasspath参数指定的路径中的类。

**扩展类加载器（ExtClassLoader）**：扩展类加载器负责加载JDK\jre\lib\ext目录中，或者由java.ext.dirs系统变量指定的路径中的所有类库（如javax.*开头的类）。

**应用类加载器（AppClassLoader）**：应用类加载器负责加载用户类路径（ClassPath）所指定的类，开发者可以直接使用该类加载器。

##### [3] 类加载器的职责有？

**全盘负责**：当一个类加载器负责加载某个Class时，该Class所依赖的和引用的其他Class也将由该类加载器负责载入，除非显式使用另外一个类加载器来载入。

**父类委托**（防止重复）：类加载机制会先让父类加载器试图加载该类，只有在父类加载器无法加载该类时才尝试从自己的类路径中加载该类。父类委托机制是为了防止内存中出现多份同样的字节码，保证java程序安全稳定运行。

**缓存机制**：缓存机制将会保证所有加载过的Class都会被缓存，当程序中需要使用某个Class时，先从缓存区寻找该Class，只有缓存区不存在，系统才会读取该类对应的二进制数据，并将其转换成Class对象，存入缓存区。这就是为什么修改了Class后，必须重启JVM，程序的修改才会生效。

##### [4] 什么是双亲委派机制？

   双亲委派模式的工作原理的是**;如果一个类加载器收到了类加载请求，它并不会自己先去加载，而是把这个请求委托给父类的加载器去执行**，如果父类加载器还存在其父类加载器，则进一步向上委托，依次递归，请求最终将到达顶层的启动类加载器，如果父类加载器可以完成类加载任务，就成功返回，倘若父类加载器无法完成此加载任务，子加载器才会尝试自己去加载，这就是双亲委派模式，**即每个儿子都不愿意干活，每次有活就丢给父亲去干**，直到父亲说这件事我也干不了时，儿子自己想办法去完成，这不就是传说中的双亲委派模式.那么这种模式有什么作用?

   采用双亲委派模式的是好处是Java类随着它的类加载器一起具备了一种带有优先级的层次关系，**通过这种层级关可以避免类的重复加载**，当父亲已经加载了该类时，就没有必要子ClassLoader再加载一次。其次是考虑到安全因素，java核心api中定义类型不会被随意替换，假设通过网络传递一个名为java.lang.Integer的类，通过双亲委托模式传递到启动类加载器，而启动类加载器在核心Java API发现这个名字的类，发现该类已被加载，并不会重新加载网络传递的过来的java.lang.Integer，而直接返回已加载过的Integer.class，这样便可以防止核心API库被随意篡改。

> 当一个Hello.class这样的文件要被加载时。不考虑我们自定义类加载器，首先会在AppClassLoader中检查是否加载过，如果有那就无需再加载了。如果没有，那么会拿到父加载器，然后调用父加载器的loadClass方法。父类中同理会先检查自己是否已经加载过，如果没有再往上。注意这个过程，直到到达Bootstrap classLoader之前，都是没有哪个加载器自己选择加载的。如果父加载器无法加载，会下沉到子加载器去加载，一直到最底层，如果没有任何加载器能加载，就会抛出ClassNotFoundException。

---

#### 【<JVM垃圾回收专题>】

1. 我们首先需要**判断垃圾**，其中中心思想为判断其是否还有引用。可以使用**引用计数法**和**可达性分析**；
2. 我们对垃圾进行回收时，需要一些**垃圾回收算法**进行理论支持。包括：**标记-清除**，**复制**，**标记-整理**，**分代收集算法**。
3. 如果说垃圾回收算法是内存回收的方法论，那么**垃圾收集器**就是内存回收的具体实现。见下图，其中**CMS和G1**重点了解。
4. 最后我们划分了堆内存（年轻代<一个生成区和两个幸存区>和老年代）和非堆内存（永久代），进行垃圾分类。还有两种针对不同区域实施**垃圾回收策略**，追求高效率的回收。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408224418677.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzUxODAzOA==,size_16,color_FFFFFF,t_70)

##### [1] 垃圾回收的场所及原因？

**垃圾回收的主要场所是堆内存，主要对象是实例对象和变量**。随着程序的运行它们占据的内存越来越多，如果不及时进行垃圾回收，必然会带来程序性能的下降，甚至会因为可用内存不足造成一些不必要的系统异常。

##### [2] 为什么学习GC和如何学习GC？

当需要排查各种内存溢出、内存泄漏问题时，当垃圾收集器成为系统达到更高并发量的瓶颈时，我们就需要对这些自动化的技术实施必要的监控和调节。

* 哪些内存需要回收？-> 
* 什么时候回收？
* 如何回收？

##### [3]  JVM如何判定一个对象是否应该被回收？

 判断一个对象是否应该被回收，主要是看其**是否还有引用**。判断对象是否存在引用关系的方法包括引用计数法以及root根搜索方法。

1. **引用计数法**：是一种比较古老的回收算法。原理是**此对象有一个引用，即增加一个计数，删除一个引用则减少一个计数**。垃圾回收时，只需要收集计数为0的对象。此算法最致命的是无法处理对象间**循环引用**的问题。

2. **可达性分析**：root搜索方法的基本思路就是通过一系列可以做为root的对象作为起始点，从这些节点开始向下搜索。当一个对象到root节点没有任何引用链接时，则证明此对象是可以被回收的。

 >1. **什么对象会被认为是root对象?**
 >
 >>* jvm运行时方法区类静态变量(static)引用的对象
 >>* jvm运行时方法区常量引用的对象
 >>* jvm当前运行线程中的虚拟机栈变量表引用的对象
 >>* 本地方法栈中(jni)引用的对象
 >>* 被同步锁（synchronized）持有的对象
 >>* 虚拟机内部的引用
 >>
 >>**总之一句话，GC Root 对象一定是影响程序运行的对象。**
 >
 >2. **何为循环引用**?
 >
 >>[link](https://blog.csdn.net/fengzhiqi1993/article/details/81191949)
 >
 >3. **“引用”是什么意思？**
 >
 >>如果reference类型的数据中存储的数值代表的是另外一块内存的起始地址，就称为这块内存代表一个引用。JDK1.2以后将引用分为强引用，软引用，弱引用和虚引用四种。
 >
 >4. **非死不可?**
 >
 >>真正宣告一个对象死亡，至少要经历两次被标记的过程，如果没有引用链，就会进行第一次标记，随后进行一次筛选，筛选的条件时对象是对象是否覆盖过finalize方法，或者finalize方法已经被虚拟机调用过，则执行finalize方法。

##### [4] 在java中为什么不推荐使用finalize

**一般来说，finalze方法都是在Java虚拟机发现去除那些已经被执行了finalize的对象之外，没有任何活动的线程能够引用到该对象的时候调用。在finalze方法里，可以做任何事情，甚至让该对象重新可被其他线程引用；但是一般来说，finalize方法的通常目的是在该对象真正被回收之前做一些清理的工作。比如，一个代表输入/输出连接的对象，它的finalize方法可能会在自己被回收之前中断对应的I/O连接。**

https://baijiahao.baidu.com/s?id=1655232869611610920&wfr=spider&for=pc

我们都知道一个对象如果没有了任何引用，java虚拟机就认为这个对象没什么用了，就会对其进行垃圾回收，但是如果这个对象包含了finalize函数，性质就不一样了。怎么不一样了呢？

java虚拟机在进行垃圾回收的时候，一看到这个对象类含有finalize函数，就把这个函数交给FinalizerThread处理，而包含了这个finalize的对象就会被添加到FinalizerThread的执行队列，并使用一个链表，把这些包含了finalize的对象串起来。

![img](https://pics5.baidu.com/feed/1e30e924b899a9010d34c78331bb0d7d0208f532.jpeg?token=cc6b19d8b9ecf5e0697042b70da81e1d&s=0D40EC12E18768EA584DA0CE0200D0A1)

他的影响在于**只要finalize没有执行，那么这些对象就会一直存在堆区**，不过这里只是4个包含了finalize的对象，影响不是那么大，如果有一万个或者是十万个呢？这就影响大了。

finalize的原理其实很简单，在这里简要的梳理一下：

（1）对象在初始化的过程中会判断是否重写了finalize，方法是判断两个字段标志has_finalizer_flag和RegisterFinalizersAtInit。

（2）如果重写了finalize，那就把当前对象注册到FinalizerThread的ReferenceQueue队列中。注册之后的对象就叫做Finalizer。方法是调用register_finalizer函数。此时java虚拟机一看当前有这个对象的引用，于是就不进行垃圾回收了。

（3）对象开始被调用，FinalizerThread线程负责从ReferenceQueue队列中获取Finalizer对象。开始执行finalize方法，在执行之前，这个对象一直在堆中。

（4）对象执行完毕之后，将这个Finalizer对象从队列中移除，java虚拟机一看对象没有引用了，就进行垃圾回收了。

这就是整个过程。不过在这里我们主要看的是finalize方法对垃圾回收的影响，其实就是在第三步，也就是这个对象含有finalize，进入了队列但一直没有被调用的这段时间，会一直占用内存。



**为什么要舍弃finalize**

**第一：调用时机的不确定性**

虽然finalize()方法早晚会被调用到，但这种调用时机的不可控性可能会导致资源迟迟不被释放而出现系统级异常。因为计算机的资源有是限的，当明确要释放某些资源时（比如上面例子中reader所掌控的一系列资源），应该使用其它的办法让这些资源立即释放（后面给出例子）！

**第二：影响代码的可移植性**

因为每种JVM内置的垃圾回收算法都是不同的，所以可能在你的JVM里，你辛辛苦苦编写的使用finalize方法的案例运行的很好，但移植到不同的JVM中时，很有可能会崩溃的一塌糊涂！

**第三：成本较高**

如果某个类重载了finalize方法且在方法内部实现了一些逻辑，那么JVM在构造或销毁这个类的对象之前，会做很多额外的工作。很明显，如果一个类没有重载finalize方法，那么销毁时只要将堆中的内存处理一下就可以了，而如果重载了finalize方法的话，就要执行finalize方法，万一执行过程中再出现点异常或错误，那消耗的成本就更高了。

**第四：异常丢失**

第三点中也说过了，万一fianlize方法中抛出了异常，那么finalize会终止运行，而抛出的这个异常也会被舍弃，最终会让对象实例处于一种半销毁半存活的僵尸状态，导致意想不到的后果！

##### [4]  详细说下四种引用？

**强引用**：普通存在， P p = new P()，只要强引用存在，垃圾收集器**永远不会**回收掉被引用的对象。默认情况下，对象采用的均为强引用。

> 使用场景：例如数组

**软引用**：通过SoftReference类来实现软引用，在**内存不足**的时候会将这些软引用回收掉。软引用是Java中提供的一种比较适合于缓存场景的应用.

> 使用场景：创建缓存

**弱引用**：通过WeakReference类来实现弱引用，**每次垃圾回收**的时候肯定会回收掉弱引用。

> 使用场景：WeakHashMap类中的key

**虚引用**：也称为幽灵引用或者幻影引用，通过PhantomReference类实现。设置虚引用只是为了对象被回收时候收到一个**系统通知**。

> 使用场景：用于对象销毁前的一些操作，比如说资源释放等

##### [5]  常用的垃圾收集算法有哪些？

参考网站：https://www.cnblogs.com/ghoster/p/7580729.html

1. **标记-清除算法**（Mark-Sweep）：算法分为“标记”和“清除”两个阶段：**首先标记出所有需要回收的对象，在标记完成后统一回收所有被标记的对象**，之所以说它是最基本的收集算法，是因为后续的收集算法都是基于这种思路并对其不足进行改进而得到的。它的主要不足有两个：一是效率问题，标记和清除效率都不高；二是空间问题，标记清除后会产生大量不连续的内存碎片，空间碎片太多可能会导致以后程序在运行过程中需要分配较大对象时，无法找到足够的连续内存而不得不提前触发另一次垃圾收集动作。

   ![img](https://images2017.cnblogs.com/blog/938012/201709/938012-20170923172144353-1171383005.png)

2. **复制算法**(Copying)：为了解决效率问题，一种称为“复制”（Copying）的收集算法出现了，他**将可用内存按容量划分为大小相等的两块，每次只使用其中的一块。当这块的内存用完了，就将还存活这的对象复制到另外一块上面，然后再把已使用过的内存空间一次清理掉**。这样使得每次都是对整个半区进行内存回收，内存分配时也就不用考虑内存碎片等复杂情况，只要移动堆顶指针，按顺序分配内存即可，实现简单，运行高效。只是这种算法的代价是将内存缩小为了原来的一半，代价未免太高了一点。

   ![img](https://images2017.cnblogs.com/blog/938012/201709/938012-20170923180335196-1109227426.png)

3. **标记-整理算法**(Mark-compact)：复制收集算法在对象存活率较高时就要进行较多的复制操作，效率将会变低。更关键的是如果不想浪费50%的空间就要使用额外的空间进行分配担保（Handle Promotion当空间不够时，需要依赖其他内存），以应对被使用的内存中所有对象都100%存活的极端情况，对于“标记-整理”算法，标记过程仍与“标记-清除”算法一样，但是后续步骤不是直接对可回收对象进行清理，而是**让所有的存活对象都向一端移动，然后直接清理掉端边界以外的内存**。

   ![img](https://images2017.cnblogs.com/blog/938012/201709/938012-20170923180351353-1569305712.png)

4. **分代收集算法**：当前的商业虚拟机的垃圾收集都是采用“分代收集”（Generational Collection）算法，这种算法并没有什么新的思想，只是根据对象存活周期的不同将内存划分为几块。**一般是把堆划分为新生代和老年代，这样就可以根据各个年代的特点采用最适合的收集算法**。

   **为什么在新生代使用使用复制算法，在老年代使用标记整理算法？**

   在新生代中，每次垃圾收集时都发现有大批对象死去，只有少量存活，那就采用复制算法，只需要付出少量存活对象的复制成本就可以完成收集。而老年代中因为对象存活率高、没有额外空间对它进行分配担保，就必须使用“标记-清理”或者“标记-整理”算法来进行回收。

> **什么是内存碎片？如何解决？**
>
> 由于不同 Java 对象存活时间是不一定的，因此，在程序运行一段时间以后，如果不进行内存整理，就会出现零散的内存碎片。碎片最直接的问题就是会导致无法分配大块的内存空间，以及程序运行效率降低。所以，在上面提到的基本垃圾回收算法中，“复制”方式和“标记-整理”方式，都可以解决碎片的问题。

##### [4]  分代收集的理论支撑？

**弱分代假说**：绝大数对象都是朝生夕灭的；

**强分代假说**：熬过多次垃圾收集过程的对象越难以消亡。

**跨代引用假说**：跨代引用相对于同代引用只占少数。

>**1. 弱分代假说和强分代假说证明了什么？**
>
>**弱分代假说和强分代假说**鉴定了垃圾收集器一致的原则，收集器应该讲java划分为不同区域，然后将回收对象依据年龄（年龄即对象熬过垃圾收集的过程）分配到不同的存储之中存储，使用不同垃圾回收策略。
>
>**2. 跨代引用假说解释了什么？**
>
>由于对象之间不是孤立的，对象之间会存在跨代引用。所以可以用**跨代引用假说证明**，存在互相引用关系的两个对象，应该是倾向于同时生存和消亡的。举个例子，如果某新生代的对象存在于老年代难以消亡，那么引用会使新生代的对象存活很久，进而晋升到老年代中，这种跨代引用随即被消除了。
>
>**3. 记忆集？**
>
>https://segmentfault.com/q/1010000023017473/
>
>依据这条假说，我们不应该为了少量的跨代引用去扫描整个老年代。我们我们可以在新生代中建立一个全局数据结构--**记忆集**。这个结构把老年代划分为很多小块，并且标记出那一块存在跨代引用。当发生minor GC时，只有包含了跨代引用的小块内存里的对象才会被加入GC roots进行扫描。

##### [6] 常用的垃圾收集器有哪些？

垃圾回收算法是垃圾回收的方法论，垃圾收集器，是内存回收的实践论。[link](https://cyc2018.github.io/CS-Notes/#/notes/Java%20%E8%99%9A%E6%8B%9F%E6%9C%BA?id=%e5%9e%83%e5%9c%be%e6%94%b6%e9%9b%86%e5%99%a8)，记忆方法：**单线程：serial与serial old，多线程：ParNew与CMS，高吞吐：Parallel Scavenge与Parallel Old，G1**

1. **Serial 收集器** (标记-清理)：新生代与老年代的单线程收集器，标记和清理都是单线程，在垃圾回收时会暂停其他工作线程，直到它收集完，即stop the world。优点是简单粗暴适合单核及少核处理器。
2. **Serial Old 收集器**（标记-整理算法）老年代单线程收集器，Serial 收集器的老年代版本。服务端使用时：可以与Parallel Scavenge 收集器配合使用，也可以成为CMS收集器失败后的备选预案。
3. **ParNew 收集器**（标记-复制算法）新生代收集器，可以认为是 Serial 收集器的多线程版本，在多核 CPU 环境下有着比 Serial 更好的表现。它是激活CMS后默认的新生代收集器。
4. **Parallel Scavenge 收集器**（标记-复制算法）并行多线程收集器，追求高吞吐量，高效利用 CPU。吞吐量一般为 99%， 适合后台应用等对交互相应要求不高的场景。**吞吐量= 用户线程时间 / (用户线程时间+GC线程时间)**，吞吐量适合保证高效率的执行有效工作。
5. **Parallel Old 收集器**（标记-整理算法）Parallel Old 收集器的老年代版本，并行收集器，吞吐量优先。
6. **CMS(Concurrent Mark Sweep)**收集器（标记-清除算法）高并发、低停顿，追求最短 GC 回收停顿时间，cpu 占用比较高，响应时间快，停顿时间短，多核 cpu 追求高响应时间的选择。CMS 是英文 Concurrent Mark-Sweep 的简称，**是以牺牲吞吐量为代价来获得最短回收停顿时间的垃圾回收器**。对于要求服务器响应速度的应用上，这种垃圾回收器非常适合。
7. **G1** 收集器**在后台维护了一个优先列表，每次根据允许的收集时间，优先选择回收价值最大的 Region**(这也就是它的名字 Garbage-First的由来。

##### [7] 垃圾收集器如何互相配合使用

<img src="X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715164625585.png" alt="image-20200715164625585" style="zoom: 80%;" />

![image-20200715164735100](X:\Users\xu\AppData\Roaming\Typora\typora-user-images\image-20200715164735100.png)

##### [8] CMS说一下?

* **CMS垃圾清除的步骤**？

[link](https://blog.csdn.net/mc90716/article/details/80158138)：**首先停止线程，标记root根遍历直接对象，然后根据其扫瞄，之后停止线程重新扫描，最后删除**

1. **初始标记（stop the world）**：使用可达性分析记录下**直接**与 root 相连的对象，暂停所有的其他线程，速度很快；
2. **并发标记**：同时开启 GC 和用户线程，用 **CG root 直接关联**对象一个去记录可达对象。但在这个阶段结束，这并不能保证包含当前所有的可达对象。因为用户线程可能会不断的更新引用域，所以 GC 线程无法保证可达性分析的实时性。所以这个算法里会跟踪记录这些发生引用更新的地方。
3. **重新标记（stop the world）**：重新标记阶段就是为了修正并发标记期间因为用户程序继续运行而导致标记产生变动的那一部分对象的标记记录【这个阶段的停顿时间一般会比初始标记阶段的时间稍长，远远比并发标记阶段时间短】；
4. **并发清除**：开启用户线程，同时 GC 线程开始对为标记的区域做清扫。

* **CMS 的优缺点**？

**优点**：CMS(concurrent low pause collector)并发收集、低停顿；

 **缺点**：对 CPU 资源敏感、无法处理浮动垃圾、它使用的回收算法“标记-清除”算法会导致收集结束时会有大量空间碎片产生。 

>**并发消耗CPU资源** 其中的并发标记和并发清理是工作线程和垃圾回收线程并发工作，这样在需要STW的时间内不会让整个系统不可用。但是在并发标记阶段，需要根据GC Roots标记出大量的存活对象，而在并发清理阶段，则需要将垃圾对象从各种随机内存位置删掉，这两个阶段都非常消耗性能，所以垃圾回收线程会占用一部分的CPU资源，导致系统的执行效率降低。
>
>CMS默认的回收线程数是 (CPU个数+3)/4，当在CPU核数较多的时候，对系统性能的影响并不是特别大。但是如果是CPU核数较少，例如双核的时候，就会占用一个CPU去处理垃圾回收，系统的CPU资源直接降低50%，这就严重影响了效率。
>
>因为现在CPU的核数越来越多，所以这种场景基本不会对系统造成很大的影响，可以忽略不计。
>
>**Concurrent Mode Failure问题** 并发清理阶段，工作线程和垃圾回收线程并发工作的时候，此时工作线程会不断产生新的垃圾，但是垃圾回收线程并不会去处理这些新生成的垃圾对象，需要等到下次垃圾回收的时候才会去处理，这些垃圾对象称之为：浮动垃圾 。因为有这些浮动垃圾的存在，所以老年代不能在100%使用的时候才去进行垃圾回收，否则就放不下这些浮动垃圾了。有一个参数是“-XX:CMSInitiatingOccupancyFraction”，这个参数在jdk1.6里面默认是92%，意思是老年代使用了92%的空间就会执行垃圾回收了。但是即使预留了8%的内存去存放浮动垃圾，但是还是有可能放不下，这样就会产生Concurrent Mode Failure问题。一旦产生了Concurrent Mode Failure问题，系统会直接使用Serial Old垃圾回收器取代CMS垃圾回收器，从头开始进行GC Roots追踪对象，并清理垃圾，这样会导致整个垃圾回收的时间变得更长。
>
>解决办法就是根据系统的需求，合理设置“-XX:CMSInitiatingOccupancyFraction”的值，如果过大，则会产生Concurrent Mode Failure问题，如果设置的过小，则会导致老年代更加频繁的垃圾回收。
>
>**空间碎片问题** CMS的标记-清理算法会在并发清理的阶段产生大量的内存碎片，如果不整理的话，则会有大量不连续的内存空间存在，无法放入一些进入老年代的大对象，导致老年代频繁垃圾回收。所以CMS存在一个默认的参数 “-XX:+UseCMSCompactAtFullCollection”，意思是在Full GC之后再次STW，停止工作线程，整理内存空间，将存活的对象移到一边。还要一个参数是“-XX:+CMSFullGCsBeforeCompaction”,表示在进行多少次Full GC之后进行内存碎片整理，默认为0，即每次Full GC之后都进行内存碎片整理。
>
>CMS虽然使用并发的方式降低了STW的时间，但是还需要配合一些CMS的参数才能完全发挥出CMS的优势，否则甚至会降低垃圾回收的效率。因此只有掌握了CMS的原理和参数的调试，才能让系统运行的更加流畅。

##### [9] **G1 说一下**？

G1（Garbage-First），它是一款面向服务端应用的垃圾收集器，在多 CPU 和大内存的场景下有很好的性能。HotSpot 开发团队赋予它的使命是未来可以替换掉 CMS 收集器。G1（Garbage-First）开创了**面向局部收集**的设计思路和**基于region的内存布局**形式。JAVA9时取代Parallel Scavenge与Parallel Old组合。G1 在扫描了 region 以后，**对其中的活跃对象的大小进行排序，首先会收集那些活跃对象小的 region，以便快速回收空间**（要复制的活跃对象少了），因为活跃对象小，里面可以认为多数都是垃圾，所以这种方式被称为 Garbage First（G1）的垃圾回收算法，即：**垃圾优先的回收**。



堆被分为新生代和老年代，其它收集器进行收集的范围都是整个新生代或者老年代，而 G1 可以直接对新生代和老年代一起回收。

<img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/4cf711a8-7ab2-4152-b85c-d5c226733807.png" alt="img" style="zoom:50%;" />

G1 把堆划分成多个大小相等的独立区域（Region），新生代和老年代不再物理隔离。

<img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/9bbddeeb-e939-41f0-8e8e-2b1a0aa7e0a7.png" alt="img" style="zoom:50%;" />

通过引入 Region 的概念，从而将原来的一整块内存空间划分成多个的小空间，使得每个小空间可以单独进行垃圾回收。这种划分方法带来了很大的灵活性，使得可预测的停顿时间模型成为可能。通过记录每个 Region 垃圾回收时间以及回收所获得的空间（这两个值是通过过去回收的经验获得），并维护一个优先列表，每次根据允许的收集时间，优先回收价值最大的 Region。

每个 Region 都有一个 Remembered Set，用来记录该 Region 对象的引用对象所在的 Region。通过使用 Remembered Set，在做可达性分析的时候就可以避免全堆扫描。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/f99ee771-c56f-47fb-9148-c0036695b5fe.jpg)



如果不计算维护 Remembered Set 的操作，G1 收集器的运作大致可划分为以下几个步骤：

- **初始标记**：仅仅标记一下GCroot可以关联到的对象，并且修改TAMS指针的值，让下一个阶段用户线程并发运行时，可以正确在可用的region中分配新对象。这个阶段需要停顿线程但是耗时极短。而且是借用minor GC时候同步完成，所以G1收集器在这个接丢单没有额外的停顿。
- **并发标记**：从已经标记的堆中的对象进行可达性分析，递归扫描整个堆里的对象图，找出要回收的对象，这个过程耗时比较长，
- **最终标记**：为了修正在并发标记期间因用户程序继续运作而导致标记产生变动的那一部分标记记录，虚拟机将这段时间对象变化记录在线程的 Remembered Set Logs 里面，最终标记阶段需要把 Remembered Set Logs 的数据合并到 Remembered Set 中。这阶段需要停顿线程，但是可并行执行。
- **筛选回收**（暂停用户线程）：首先对各个 Region 中的回收价值和成本进行排序，根据用户所期望的 GC 停顿时间来制定回收计划。此阶段其实也可以做到与用户程序一起并发执行，但是因为只回收一部分 Region，时间是用户可控制的，而且停顿用户线程将大幅度提高收集效率。可以自由选择多个region构成回收集，然后把决定回收的那一部分region的存活对象复制到空的regions中，再清理掉整个旧的region的全部空间。

具备如下特点：

- 空间整合：整体来看是基于“标记 - 整理”算法实现的收集器，从局部（两个 Region 之间）上来看是基于“复制”算法实现的，这意味着运行期间不会产生内存空间碎片。
- 可预测的停顿：能让使用者明确指定在一个长度为 M 毫秒的时间片段内，消耗在 GC 上的时间不得超过 N 毫秒。
- **G1的另一个显著特点他能够让用户设置应用的暂停时间，为什么G1能做到这一点呢？也许你已经注意到了，G1回收的第4步，它是“选择一些内存块”，而不是整代内存来回收，这是G1跟其它GC非常不同的一点，其它GC每次回收都会回收整个Generation的内存(Eden, Old), 而回收内存所需的时间就取决于内存的大小，以及实际垃圾的多少，所以垃圾回收时间是不可控的；而G1每次并不会回收整代内存，到底回收多少内存就看用户配置的暂停时间，配置的时间短就少回收点，配置的时间长就多回收点，伸缩自如。 (阿里面试)**

##### [10] G1和CMS?

总体来说，G1跟CMS一样，是一块**低延时**的收集器，同样牺牲了吞吐量，不过二者之间得到了很好的权衡。 

G1与CMS对比有一下不同： 

1. 分代： CMS中，堆被分为PermGen，YoungGen，OldGen；而YoungGen又分了两个survivo区域。在G1中，堆被平均分成几个区域(region)，在每个区域中，虽然也保留了新老代的概念，但是收集器是以整个区域为单位收集的。 

2. 算法： 相对于CMS的“标记—清理”算法，G1会使用压缩算法，保证不产生多余的碎片。收集阶段，G1会将某个区域存活的对象拷贝的其他区域，然后将整个区域整个回收。 

3. 停顿时间可控： 为了缩短停顿时间，G1建立可预存停顿模型，这样在用户设置的停顿时间范围内，G1会选择适当的区域进行收集，确保停顿时间不超过用户指定时间。 

##### [10]  说下你对垃圾回收策略的理解/垃圾回收时机？

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408210708100.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzUxODAzOA==,size_16,color_FFFFFF,t_70)
答：JVM的内存可以分为**堆内存和非堆内存**。堆内存分为**年轻代（复制算法）和老年代（标记-整理算法）**。年轻代又可以进一步划分为**一个Eden（伊甸）区和两个Survivor（幸存）区**组成。

1. **Minor / Scavenge GC**：**所有对象创建在新生代的 Eden 区，当 Eden 区满后触发新生代的 Minor GC，将 Eden 区和非空闲 Survivor 区存活的对象复制到另外一个空闲的 Survivor 区中，在这个过程中保证一个 Survivor 区是空的，新生代 Minor GC 就是在两个 Survivor 区之间相互复制存活对象，直到 Survivor 区满为止**。我们创建的对象会优先在Eden分配，如果是大对象（很长的字符串数组）则可以直接进入老年代。另外，长期存活的对象将进入老年代，每一次MinorGC（年轻代GC），对象年龄就大一岁，默认15岁晋升到老年代。
2. **Full GC**：**Full GC是指发生在老年代的GC，当老年代没有足够的空间时即发生Full GC，发生Full GC一般都会有一次Minor GC。对整个堆进行整理，包括 Young、Tenured 和 Perm。**Full GC 因为需要对整个堆进行回收，而且会"**STOP THR WORLD"**所以比 Minor GC 要慢，因此应该尽可能减少 Full GC 的次数。在对 JVM 调优的过程中，很大一部分工作就是对于 Full GC 的调节。

> **如果生成区存活对象太多，导致幸存者区放不小怎么办？**
>
> 可以使用逃生门，将对象转移到其他内存区域，如：老年代。 

##### [11] 分区大小比值及其理论依据

![1](http://images.cnitblog.com/blog/587773/201409/061921034534396.png)

**生成区：s0：s1=8：1：1  老年代：新生代=2: 1**

* **为什么年轻代新增servivor区域？**

* 在年轻代新增Surviver区，有利于减轻老年代的负担，尽可能的让大部分对象在年轻代通过较高效的Yong GC回收掉，不至于老年代里存放的对象过多导致内存不足而进行频繁的Full GC操作。而且这种分区有利于减少内存碎片的产生。

* **为什么使用 8:1:1，而不使用5:5，或者8:2？**
* 由于IBM的研究表示，新生代中有98%的对象活不过第一轮收集。使用5:5会造成空间的极大浪费。哪为什么使用8:2？因为这样会导致比例为2的空间向空间为8的区域内复制时，发生minor gc速度过快。
* **老年代：新生代=2: 1?**

* 老年代不宜过小，如果老年代小，会导致转为老年代的时候，老年代撑不下，导致full gc，回收停顿时间过长。

##### [12] [内存分配策略](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=内存分配策略)

[1. 对象优先在 Eden 分配](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_1-对象优先在-eden-分配)

大多数情况下，对象在新生代 Eden 上分配，当 Eden 空间不够时，发起 Minor GC。

[2. 大对象直接进入老年代](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_2-大对象直接进入老年代)

大对象是指需要连续内存空间的对象，最典型的大对象是那种很长的字符串以及数组。

经常出现大对象会提前触发垃圾收集以获取足够的连续空间分配给大对象。

-XX:PretenureSizeThreshold，大于此值的对象直接在老年代分配，避免在 Eden 和 Survivor 之间的大量内存复制。

[3. 长期存活的对象进入老年代](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_3-长期存活的对象进入老年代)

为对象定义年龄计数器，对象在 Eden 出生并经过 Minor GC 依然存活，将移动到 Survivor 中，年龄就增加 1 岁，增加到一定年龄则移动到老年代中。

-XX:MaxTenuringThreshold 用来定义年龄的阈值。

[4. 动态对象年龄判定](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_4-动态对象年龄判定)

虚拟机并不是永远要求对象的年龄必须达到 MaxTenuringThreshold 才能晋升老年代，如果在 Survivor 中相同年龄所有对象大小的总和大于 Survivor 空间的一半，则年龄大于或等于该年龄的对象可以直接进入老年代，无需等到 MaxTenuringThreshold 中要求的年龄。

[5. 空间分配担保](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_5-空间分配担保)

在发生 Minor GC 之前，虚拟机先检查老年代最大可用的连续空间是否大于新生代所有对象总空间，如果条件成立的话，那么 Minor GC 可以确认是安全的。

如果不成立的话虚拟机会查看 HandlePromotionFailure 的值是否允许担保失败，如果允许那么就会继续检查老年代最大可用的连续空间是否大于历次晋升到老年代对象的平均大小，如果大于，将尝试着进行一次 Minor GC；如果小于，或者 HandlePromotionFailure 的值不允许冒险，那么就要进行一次 Full GC。

##### [13] [ Minor GC 和 Full GC触发条件](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=minor-gc-和-full-gc)

- Minor GC：回收新生代，因为新生代对象存活时间很短，因此 Minor GC 会频繁执行，执行的速度一般也会比较快。
- Full GC：回收老年代和新生代，老年代对象其存活时间长，因此 Full GC 很少执行，执行速度会比 Minor GC 慢很多。

[Full GC 的触发条件](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=full-gc-的触发条件)

对于 Minor GC，其触发条件非常简单，当 Eden 空间满时，就将触发一次 Minor GC。而 Full GC 则相对复杂，有以下条件：

[1. 调用 System.gc()](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_1-调用-systemgc)

只是建议虚拟机执行 Full GC，但是虚拟机不一定真正去执行。不建议使用这种方式，而是让虚拟机管理内存。

[2. 老年代空间不足](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_2-老年代空间不足)

老年代空间不足的常见场景为前文所讲的大对象直接进入老年代、长期存活的对象进入老年代等。

为了避免以上原因引起的 Full GC，应当尽量不要创建过大的对象以及数组。除此之外，可以通过 -Xmn 虚拟机参数调大新生代的大小，让对象尽量在新生代被回收掉，不进入老年代。还可以通过 -XX:MaxTenuringThreshold 调大对象进入老年代的年龄，让对象在新生代多存活一段时间。

[3. 空间分配担保失败](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_3-空间分配担保失败)

使用复制算法的 Minor GC 需要老年代的内存空间作担保，如果担保失败会执行一次 Full GC。具体内容请参考上面的第 5 小节。

[4. JDK 1.7 及以前的永久代空间不足](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_4-jdk-17-及以前的永久代空间不足)

在 JDK 1.7 及以前，HotSpot 虚拟机中的方法区是用永久代实现的，永久代中存放的为一些 Class 的信息、常量、静态变量等数据。

当系统中要加载的类、反射的类和调用的方法较多时，永久代可能会被占满，在未配置为采用 CMS GC 的情况下也会执行 Full GC。如果经过 Full GC 仍然回收不了，那么虚拟机会抛出 java.lang.OutOfMemoryError。

为避免以上原因引起的 Full GC，可采用的方法为增大永久代空间或转为使用 CMS GC。

[5. Concurrent Mode Failure](https://cyc2018.github.io/CS-Notes/#/notes/Java 虚拟机?id=_5-concurrent-mode-failure)

执行 CMS GC 的过程中同时有对象要放入老年代，而此时老年代空间不足（可能是 GC 过程中浮动垃圾过多导致暂时性的空间不足），便会报 Concurrent Mode Failure 错误，并触发 Full GC。

#### 【JVM调优】

**对JVM内存的系统级的调优主要的目的是减少GC的频率和Full GC的次数。**

##### **[1] 说下你用过的 JVM 监控工具？**

1. jvisualvm：虚拟机监视和故障处理平台

2. jps ：查看当前 Java 进程

3. jstat：显示虚拟机运行数据

4. jmap：内存监控

5. jhat：分析 heapdump 文件

6. jstack：线程快照

7. jinfo：虚拟机配置信息

##### [2]  如何利用监控工具调优？

- **1. 堆信息查看**

1. 可查看堆空间大小分配（年轻代、年老代、持久代分配）

2. 提供即时的垃圾回收功能

3. 垃圾监控（长时间监控回收情况）

4. 查看堆内类、对象信息查看：数量、类型等

5. 对象引用情况查看

- 有了堆信息查看方面的功能，我们一般可以顺利解决以下问题：

1. 年老代年轻代大小划分是否合理

2. 内存泄漏垃圾

3. 圾回收算法设置是否合理

- **2. 线程监控**

线程信息监控：系统线程数量

线程状态监控：各个线程都处在什么样的状态下

Dump 线程详细信息：查看线程内部运行情况 

死锁检查

- **3. 热点分析**

1. CPU 热点：检查系统哪些方法占用的大量 CPU 时间；

2. 内存热点：检查哪些对象在系统中数量最大（一定时间内存活对象和销毁对象一起统计）这两个东西对于系统优化很有帮助。我们可以根据找到的热点，有针对性的进行系统的瓶颈查找和进行系统优化，而不是漫无目的的进行所有代码的优化。

- **4. 快照**

快照是系统运行到某一时刻的一个定格。在我们进行调优的时候，不可能用眼睛去跟踪所有系统变化，依赖快照功能，我们就可以进行系统两个不同运行时刻，对象（或类、线程等）的不同，以便快速找到问题。

举例说，我要检查系统进行垃圾回收以后，是否还有该收回的对象被遗漏下来的了。那么，我可以在进行垃圾回收前后，分别进行一次堆情况的快照，然后对比两次快照的对象情况。

- **5. 内存泄露检查**

内存泄漏是比较常见的问题，而且解决方法也比较通用，这里可以重点说一下，而线程、热点方面的问题则是具体问题具体分析了。

内存泄漏一般可以理解为系统资源（各方面的资源，堆、栈、线程等）在错误使用的情况下，导致使用完毕的资源无法回收（或没有回收），从而导致新的资源分配请求无法完成，引起系统错误。内存泄漏对系统危害比较大，因为它可以直接导致系统的崩溃。

##### [3] JVM 的一些参数？

- **1. 堆设置**

-Xms：初始堆大小

-Xmx：最大堆大小

-XX:New**Size**=n：设置年轻代大小

-XX:New**Ratio**=n：设置年轻代和年老代的比值。如:为3，表示年轻代与年老代比值为 1：3，年轻代占整个年轻代年老代和的 1/4

-XX:Survivor**Ratio**=n：年轻代中 **Eden** 区与两个 **Survivor** 区的比值。注意 Survivor 区有两个。如：3，表示 Eden：Survivor=3：2，一个Survivor区占整个年轻代的 1/5

-XX:MaxPermSize=n：设置持久代大小

- **2. 收集器设置**

-XX:+UseSerialGC：设置串行收集器

-XX:+UseParallelGC：设置并行收集器

-XX:+UseParalledlOldGC：设置并行年老代收集器

-XX:+UseConcMarkSweepGC：设置并发收集器

- **3. 垃圾回收统计信息**

-XX:+PrintGC：开启打印 gc 信息

-XX:+PrintGCDetails：打印 gc 详细信息

-XX:+PrintGCTimeStamps

-Xloggc:filename

- **4. 并行收集器设置**

-XX:ParallelGCThreads=n：设置并行收集器收集时使用的 CPU 数

-XX:MaxGCPauseMillis=n：设置并行收集最大暂停时间

-XX:GCTimeRatio=n：设置垃圾回收时间占程序运行时间的百分比

- **5. 并发收集器设置**

-XX:+CMSIncrementalMode：设置为增量模式。适用于单 CPU 情况

-XX:ParallelGCThreads=n：设置并发收集器年轻代收集方式为并行收集时，使用的 CPU 数。并行收集线程数

##### [4] JVM在内存调优方面

JVM在内存调优方面，提供了几个常用的命令，分别为jps，jinfo，jstack，jmap以及jstat命令。分别介绍如下：

1. jps：主要用来输出JVM中运行的进程状态信息，一般使用jps命令来查看进程的状态信息，包括JVM启动参数等。

2. jinfo：主要用来观察进程运行环境参数等信息。

3. jstack：主要用来查看某个Java进程内的线程堆栈信息。jstack pid 可以看到当前进程中各个线程的状态信息，包括其持有的锁和等待的锁。

4. jmap：用来查看堆内存使用状况。jmap -heap pid可以看到当前进程的堆信息和使用的GC收集器，包括年轻代和老年代的大小分配等

5. jstat：进行实时命令行的监控，包括堆信息以及实时GC信息等。可以使用jstat -gcutil pid1000来每隔一秒来查看当前的GC信息。

##### [5]  怎么做JDK8的内存调优？

**1. JDK8内存结构**

JDK8的内存结构主要包括**程序计数器**（Program Counter Register）、**虚拟机栈**（Java Virtual Machine Stacks）、**本地方法栈**（Native Method Stacks）、**堆**（Java Heap）、**元空间**（Metaspace）。

其中**堆**又被划分为**老年代**（Old Generation）、**年轻代**（Young Generation），其中**年轻代**又被划分为一个**Eden区**和两个**Survivor区**。

一边说着，一边拿起笔在纸上画了起来：

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pbWcyMDIwLmNuYmxvZ3MuY29tL290aGVyLzE0NTY4Ny8yMDIwMDgvMTQ1Njg3LTIwMjAwODAyMDcwOTE0MzAyLTg3NjU4MjYxOS5wbmc?x-oss-process=image/format,png)

画完以后，我又说：**JDK8的内存调优主要针对的是堆和元空间**。内存调优时常用到JVM参数有这些：

**-server**

JVM的server模式, 在多CPU服务器中性能可以得到更好地发挥。JDK的64位版本只支持server模式，因此在这种情况下，选项是隐式的。

**-Xmx**

指定堆所分配内存的最大值，等同于-XX:MaxHeapSize。不附加字母时，单位为byte，必须是1024的倍数，并且大于2MB；附加字母k或K时，表示单位为KB；附加字母m或M时，表示单位为MB；附加字母g或G时，表示单位为G。

下面的例子是使用不同的单位把堆所分配内存的最大值设置为1GB：

```
-Xmx1G
-Xmx1024M
-Xmx1048576K
-Xmx1073741824
1234
```

**-Xms**

指定堆所分配内存的初始值，不附加字母时，单位为byte，必须是1024的倍数，并且大于1MB；附加字母k或K时，表示单位为KB；附加字母m或M时，表示单位为MB；附加字母g或G时，表示单位为G。如果不设置这个初始值，那么初始值将被设置为老年代和年轻代分配内存的大小的总和。

下面的例子是使用不同的单位把堆所分配的初始值设置为4GB：

```
-Xms4G
-Xms4096M
-Xms4194304K
-Xms4294967296
1234
```

**对于生产环境的部署，-Xms和-Xmx通常设置为相同的值。**

**-Xmn**

指定堆的年轻代分配内存的初始值和最大值，不附加字母时，单位为byte；附加字母k或K时，表示单位为KB；附加字母m或M时，表示单位为MB；附加字母g或G时，表示单位为G。

堆的年轻代区域用于存放新生对象。与其他区域相比，在这个区域执行垃圾回收的频率更高。如果年轻代的内存太小，那么将执行许多次垃圾回收。如果年轻代的内存太大，那么执行完整的垃圾回收可能需要很长时间才能完成。**一般建议把年轻代的大小保持在整个堆大小的1/2到1/4之间。**

下面的例子是使用不同的单位把年轻代所分配内存的初始值和最大值设置为2GB：

```
-Xmn2G
-Xmn2048M
-Xmn2097152K
-Xmn2147483648
1234
```

除了使用-Xmn选项设置年轻代的初始值和最大值，还可以使用-XX:NewSize设置年轻代的初始值，使用-XX:MaxNewSize设置年轻代的最大值。

**-XX:NewRatio**

指定老年代和年轻代空间大小的比率。默认为2，即老年代和年轻代空间大小的比率为2:1，年轻代占整个堆内存空间大小的1/3。下面的例子是把老年代和年轻代空间大小的比率设置为1：

```
-XX:NewRatio=1
1
```

另外，年轻代分配内存设置的优先级如下：

1. 高优先级: -XX:NewSize/-XX:MaxNewSize
2. 中优先级: -Xmn
3. 低优先级: -XX:NewRatio

**-XX:SurvivorRatio**

指定Eden区和一个Survivor区的空间大小的比率。默认为8，即Eden区和一个Survivor区的空间大小为8:1，因为一共有两个Survivor区，所以Eden区占年轻代内存大小的80%。下面的例子是把Eden区和一个Survivor区的空间大小的比率设置为4：

```
-XX:SurvivorRatio=4
1
```

**-XX:MetaspaceSize**

指定元空间第一次触发垃圾回收的内存大小的阈值。当元空间内存占用不断增大，直到达到这个阈值时，就会触发一次垃圾回收。所以，适当的增大这个阈值，会减少垃圾回收的次数。默认值根据平台而定，一般情况下大约20.8MB。下面的例子是把元空间第一次触发垃圾回收的内存大小设置为256MB：

```
-XX:MetaspaceSize=256M
1
```

有一些小伙伴对这个参数有误解，造成不必要的麻烦。重申一下：-XX:MetaspaceSize不是元空间内存大小的初始值，不是元空间内存大小的初始值，不是元空间内存大小的初始值，重要的事情说三遍。

**-XX:MaxMetaspaceSize**

指定元空间所分配内存的最大值，默认是没有限制，取决于系统的可用内存量，理论上可以占满整个系统的内存。为了避免这种惨剧，影响系统上的其他应用，需要适当设置它的大小。下面的例子是把元空间所分配内存的最大值设置为512MB：

```
-XX:MaxMetaspaceSize=512M
1
```

面试官微笑地说：这些常用的内存调优参数总结的不错，可以结合这些参数写一个内存调优实例吗？

被面试官夸奖一下，我按捺住心中的喜悦说：当然可以。

**内存调优实例**

**如果把堆内存的空间设置大一些，以减少垃圾回收的次数。但是由于堆内存过大，在垃圾回收时会导致长时间的停顿。假设服务器上的可用内存还有12GB，那么先指定堆所分配内存的最大值和初始值为8GB。一般情况下，年轻代内存大小需在整个堆大小的1/2到1/4之间，那么就指定年轻代内存大小为3GB,老年代内存大小为5GB。再把Eden区和一个Survivor区的空间大小的比率设置为4。**元空间第一次触发垃圾回收的内存大小的阈值设置为256MB，一般情况下足够用。元空间所分配内存的最大值设置为512MB，为了避免极端情况下占用大量内存。另外，还需要明确指定JVM以server模式启动。

内存调优的参数基本敲定，用它启动一个名为one-more-study-0.0.1-SNAPSHOT.jar的jar文件：

```
java -server -Xmx8G -Xms8G -Xmn3G -XX:SurvivorRatio=4 -XX:MetaspaceSize=256M -XX:MaxMetaspaceSize=512M -jar one-more-study-0.0.1-SNAPSHOT.jar
1
```

如果执行`jmap -heap`命令查看对应Java进程的内存配置和使用情况，应该是这样的：

```
Attaching to process ID 31828, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.251-b08

using thread-local object allocation.
Parallel GC with 8 thread(s)

Heap Configuration:   #堆的内存配置
   MinHeapFreeRatio         = 0
   MaxHeapFreeRatio         = 100
   # 堆内存的最大值
   MaxHeapSize       = 8589934592 (8192.0MB) 
   # 年轻代内存的大小
   NewSize           = 3221225472 (3072.0MB) 
   # 年轻代内存的最大值
   MaxNewSize        = 3221225472 (3072.0MB) 
   # 老年代内存的大小
   OldSize           = 5368709120 (5120.0MB) 
    # 老年代和年轻代空间大小的比率
    # 因为设置Xmn参数，该设置未生效
   NewRatio                 = 2
   #Eden区和一个Survivor区的空间大小的比率
   SurvivorRatio            = 4 
    # 元空间第一次触发垃圾回收的内存大小
   MetaspaceSize       = 268435456 (256.0MB)
    # 元空间内存的最大值
   MaxMetaspaceSize    = 536870912 (512.0MB)
   G1HeapRegionSize    = 0 (0.0MB)

Heap Usage: # 堆的使用情况
PS Young Generation
Eden Space: # Eden区内存的使用情况
   capacity = 2147483648 (2048.0MB)
   used     = 901945720 (860.16MB)
   free     = 1245537928 (1187.83MB)
   42.000120505690575% used
From Space: # Survivor的From区内存的使用情况
   capacity = 536870912 (512.0MB)
   used     = 0 (0.0MB)
   free     = 536870912 (512.0MB)
   0.0% used
To Space: # Survivor的To区内存的使用情况
   capacity = 536870912 (512.0MB)
   used     = 0 (0.0MB)
   free     = 536870912 (512.0MB)
   0.0% used
PS Old Generation # 老年代内存的使用情况
   capacity = 5368709120 (5120.0MB)
   used     = 0 (0.0MB)
   free     = 5368709120 (5120.0MB)
   0.0% used

12047 interned Strings occupying 1045744 bytes.
123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354
```

听了我的回答后，面试官对我会心一笑，我仿佛还在她的眼神中看到了一丝敬仰。正所谓：万两黄金容易得，知心一个也难求，欲知后事如何，且听下回分解。

##### [6] 调优实战

JVM调优工具

**Jconsole，jProfile，VisualVM**

**Jconsole :** jdk自带，功能简单，但是可以在系统有一定负荷的情况下使用。对垃圾回收算法有很详细的跟踪。详细说明参考[这里](http://pengjiaheng.spaces.live.com/blog/cns!2DAA368B386E6AEA!687.entry)

**JProfiler**：商业软件，需要付费。功能强大。详细说明参考[这里](http://pengjiaheng.spaces.live.com/blog/cns!2DAA368B386E6AEA!685.entry)

**VisualVM**：JDK自带，功能强大，与JProfiler类似。推荐。

如何调优

观察内存释放情况、集合类检查、对象树

上面这些调优工具都提供了强大的功能，但是总的来说一般分为以下几类功能

**堆信息查看**

![img](http://dl.iteye.com/upload/picture/pic/51401/7b7ece1a-1596-3240-a37d-c3a7d06e2c01.png) 

> 可查看堆空间大小分配（年轻代、年老代、持久代分配）
>
> 提供即时的垃圾回收功能
>
> 垃圾监控（长时间监控回收情况）

![img](http://dl.iteye.com/upload/picture/pic/51403/48059c43-43ff-3d91-8699-78e6ea8af8a6.png) 

> 查看堆内类、对象信息查看：数量、类型

![img](http://dl.iteye.com/upload/picture/pic/51405/dc26b52b-62d5-320d-a627-6a88e6b57d8f.png) 

> 对象引用情况查看 

有了堆信息查看方面的功能，我们一般可以顺利解决以下问题：

 --年老代年轻代大小划分是否合理

 --内存泄漏

 --垃圾回收算法设置是否合理

线程监控

![img](http://dl.iteye.com/upload/picture/pic/51407/4e7705f6-75f6-3549-8976-dce68396bbc8.png) 

> 线程信息监控：系统线程数量。
>
> 线程状态监控：各个线程都处在什么样的状态下

![img](http://dl.iteye.com/upload/picture/pic/51409/c9486ed8-90b4-3a46-96f3-7aaa97ace11f.png) 

> Dump线程详细信息：查看线程内部运行情况
>
> 死锁检查

**热点分析**

![img](http://dl.iteye.com/upload/picture/pic/51413/ece5e1f6-d7a6-3aa6-96d0-5f9d43f69808.png) 

  **CPU热点**：检查系统哪些方法占用的大量CPU时间

  **内存热点**：检查哪些对象在系统中数量最大（一定时间内存活对象和销毁对象一起统计）

  这两个东西对于系统优化很有帮助。我们可以根据找到的热点，有针对性的进行系统的瓶颈查找和进行系统优化，而不是漫无目的的进行所有代码的优化。

**快照**

  快照是系统运行到某一时刻的一个定格。在我们进行调优的时候，不可能用眼睛去跟踪所有系统变化，依赖快照功能，我们就可以进行系统两个不同运行时刻，对象（或类、线程等）的不同，以便快速找到问题

  举例说，我要检查系统进行垃圾回收以后，是否还有该收回的对象被遗漏下来的了。那么，我可以在进行垃圾回收前后，分别进行一次堆情况的快照，然后对比两次快照的对象情况。

**内存泄漏检查**

  内存泄漏是比较常见的问题，而且解决方法也比较通用，这里可以重点说一下，而线程、热点方面的问题则是具体问题具体分析了。

  **内存泄漏一般可以理解为系统资源（各方面的资源，堆、栈、线程等）在错误使用的情况下，导致使用完毕的资源无法回收（或没有回收），从而导致新的资源分配请求无法完成，引起系统错误。**

  内存泄漏对系统危害比较大，因为他可以直接导致系统的崩溃。

  需要区别一下，内存泄漏和系统超负荷两者是有区别的，虽然可能导致的最终结果是一样的。内存泄漏是用完的资源没有回收引起错误，而系统超负荷则是系统确实没有那么多资源可以分配了（其他的资源都在使用）。

**年老代堆空间被占满**

**异常：** java.lang.OutOfMemoryError: Java heap space

**说明：**



![img](http://dl.iteye.com/upload/picture/pic/51415/49464252-97ea-3ce2-b433-d9088bafb70a.png)

 

  这是最典型的内存泄漏方式，简单说就是所有堆空间都被无法回收的垃圾对象占满，虚拟机无法再在分配新空间。

  如上图所示，这是非常典型的内存泄漏的垃圾回收情况图。所有峰值部分都是一次垃圾回收点，所有谷底部分表示是一次垃圾回收后剩余的内存。连接所有谷底的点，可以发现一条由底到高的线，这说明，随时间的推移，系统的堆空间被不断占满，最终会占满整个堆空间。因此可以初步认为系统内部可能有内存泄漏。（上面的图仅供示例，在实际情况下收集数据的时间需要更长，比如几个小时或者几天）

**解决：**

  这种方式解决起来也比较容易，一般就是根据垃圾回收前后情况对比，同时根据对象引用情况（常见的集合对象引用）分析，基本都可以找到泄漏点。

**持久代被占满**

**异常：**java.lang.OutOfMemoryError: PermGen space

**说明：**

  Perm空间被占满。无法为新的class分配存储空间而引发的异常。这个异常以前是没有的，但是在Java反射大量使用的今天这个异常比较常见了。主要原因就是大量动态反射生成的类不断被加载，最终导致Perm区被占满。

  更可怕的是，不同的classLoader即便使用了相同的类，但是都会对其进行加载，相当于同一个东西，如果有N个classLoader那么他将会被加载N次。因此，某些情况下，这个问题基本视为无解。当然，存在大量classLoader和大量反射类的情况其实也不多。

**解决：**

  \1. -XX:MaxPermSize=16m

  \2. 换用JDK。比如JRocket。

**堆栈溢出**

**异常：**java.lang.StackOverflowError

**说明：**这个就不多说了，一般就是递归没返回，或者循环调用造成

**线程堆栈满**

**异常**：Fatal: Stack size too small

**说明**：java中一个线程的空间大小是有限制的。JDK5.0以后这个值是1M。与这个线程相关的数据将会保存在其中。但是当线程空间满了以后，将会出现上面异常。

**解决**：增加线程栈大小。-Xss2m。但这个配置无法解决根本问题，还要看代码部分是否有造成泄漏的部分。

**系统内存被占满**

**异常**：java.lang.OutOfMemoryError: unable to create new native thread

**说明**：

  这个异常是由于操作系统没有足够的资源来产生这个线程造成的。系统创建线程时，除了要在Java堆中分配内存外，操作系统本身也需要分配资源来创建线程。因此，当线程数量大到一定程度以后，堆中或许还有空间，但是操作系统分配不出资源来了，就出现这个异常了。

分配给Java虚拟机的内存愈多，系统剩余的资源就越少，因此，当系统内存固定时，分配给Java虚拟机的内存越多，那么，系统总共能够产生的线程也就越少，两者成反比的关系。同时，可以通过修改-Xss来减少分配给单个线程的空间，也可以增加系统总共内生产的线程数。

**解决：**

  \1. 重新设计系统减少线程数量。

  \2. 线程数量不能减少的情况下，通过-Xss减小单个线程大小。以便能生产更多的线程。

https://www.iteye.com/blog/pengjiaheng-552456yua

