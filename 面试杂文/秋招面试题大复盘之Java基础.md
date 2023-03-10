### Java基础语法

- [ ] 面向对象的特征？谈谈你对他们的理解

  面向对象的三大特征有封装，继承和多态。先说封装把，常见的封装在我们写java项目里面就实体类来说把，他就是一个典型的封装，将属性进行私有化封装，然后使用get，set方法外接出去，这也就典型的说明了封装就是把内部结构不给使用者看，只是将使用者需要看的地方抛出去，供使用者使用，优点就是大大的提供了解耦，可以更好的去及进行代码的维护。再说继承，继承的话从总的来说就是子类可以继承父类的方法以及属性，继承是java的面象对象的一块基石。最后是多态，多态表示是同一个行为具有不同的表现或形态的能力，其实用在我们Java中就是指同一个方法调用，由于对象不同可能会有不同的行为，就比如说大人休息可能是一个人静静，小孩游戏就是玩游戏。重载与重写，引用类型的转换，接口回调这些都是多态的行为。

- [ ] 对equals和hashcode的理解

  先来单独说说equals和==的区别，==如果是基本数据类型的话，就用来比较数值，如果是引用类型的话，比较的是引用类型的物理地址，而equals是用来比较引用类型的，他的比较逻辑需要自己重写equals方法，比如String类型可以用来比较两个字符串是否相等，就是其类中重写了equals方法，hashcode呢是使用特定的算法对引用类型的物理地址进行计算，如果说他们两个的必要关系，我觉得是在重写equlas必须重写hashcode，他们需要hashcode来比较两个值对象是否相等。比如一些容器框架这样等等。

- [ ] final、finalize、finally的不同之处

  首先说说final，fianl是一个修饰符，用来修饰变量，方法和类。被修饰的变量意味该值在初始化后不可改变。被修饰的类表示不能再被继承了。修饰方法把方法锁定，以防止子类对其进行修改。再说说finalize，finalize是一个方法，在垃圾回收的时候被调用，一般情况下大部分对象都需要此方法去回收，我们也可以实现finalize方法，去修改一下垃圾回收的逻辑。最后说说finally，finally是捕捉异常try catch最后的操作，他不论是否有异常都会被执行，常常用来关闭一些流之类的。但是这个一定执行也是在与finally对应的try语句执行的情况下才会应验。

- [ ] String、StringBuffer、StringBuilder的区别

  他们三个都是Java为我们提供的一个字符串操作类，Stirng更多用来处理不改变的字符串，因为String是不能被直接改变的，他的每一次改变地址中都会有一个新的字符串，但是StringBuffer和StringBuilder不同，他们是可以改变，可以对字符串本身进行改变，他们两个的区别是StringBuilder是线程安全的，StringBuffer并不是线程安全的，他们两个StringBuilder是线程不安全，但是更快速，StringBuffer是线程安全的，当然String由于是final修饰的，他是更安全的。

- [ ] 接口与抽象类的区别

  先说说他们相同的点，接口和抽象类都不能被实例化，他们的子类只有在实现了他们的方法后才能实例化。他们的区别呢，一个类可以多实现几个接口，但是一个类只能继承一个抽象类。接口强调的是功能的实现，而抽象类更在乎关系的抽取。接口成员变量默认为public static final，必须赋初值，不能被修改；其所有的成员方法都是public、abstract的。抽象类中成员变量默认default，可在子类中被重新定义，也可被重新赋值；抽象方法被abstract修饰，不能被private、static、synchronized和native等修饰，必须以分号结尾，不带花括号。

- [ ] this & super在构造方法中的区别

  我先说说this吧，this在java中代表的是当前对象，他保存了当前对象的内存地址，指向自身。this只能使用在实例对象中，不能使用在静态方法中。super的话通俗来讲，是子类可以使用此关键字来调用父类的成员变量以及方法和构造方法。他们两共同点就是必须要在构造方法的首行声明，并且不能同时使用在构造方法中。

- [ ] Java的移位运算符

  有符号左移位运算：<<  比如说 将2 移位 1位，那么就是 2 << 1 ，将2划算成2进制 0000 0000 0000 0010 左移位就是 0000 0000 0100。 有符号右移位 ,那么就是 >>, 2>>1 就为 0000 0000 0000 0001 那就是1。还有无符号右移：>>>；总结就是

  - `<<` :左移运算符,`x << 1`,相当于x乘以2(不溢出的情况下),低位补0
  - `>>` :带符号右移,`x >> 1`,相当于x除以2,正数高位补0,负数高位补1
  - `>>>` :无符号右移,忽略符号位,空位都以0补齐

- [ ] 为什么需要泛型

  为了规范吧我的理解是这样，Java中的泛型是一种假泛型，他在代码编译时会进行类型擦除。而且他也能避免强制类型转换。

- [ ] 泛型类如何定义

  定义泛型这玩意好像谁都会把。具体的定义就三种，泛型类，泛型方法，泛型接口。

- [ ] 泛型接口如何定义

- [ ] 泛型方法如何定义

- [ ] 泛型的上限和下限

  泛型的上限定义由extends来定义，他指定的是此泛型，下限由super来定义。

- [ ] 如何理解Java中的泛型是伪泛型

  Java中的泛型是一种假泛型，他在代码编译时会进行类型擦除

- [ ] 注解的作用

  注解主要有四个方面的使用，生成文档，编译检查，编译时动态处理，运行时动态处理。

- [ ] 注解的常见分类

  Java有自带的注解，比如重写的时候。元注解，元注解就是用来定义注解的注解。还有用户自己定义的注解。

- [ ] Java异常类层次结构

  异常顶级父类是throwable，他下面分为两个大结构，一个是异常（Exception），一个是错误（error)，错误指的是非常严重的异常，是在靠程序不可解决的异常，另外一种，是Exception，他是Java中主要来处理的异常，他下面分为编译时异常和运行时异常，编译时异常指的是在编写代码的时候，我们的写法通不过编译监测这种，而运行时异常指的是在程序运行过程中，因为逻辑等产生的异常。常见的有NullPointException，IndexOutBound，ClassCast等

- [ ] throw和throws的区别

  throw是异常的抛出，我们在写代码时可能会因为逻辑等问题发出异常，这个时候，我们需要创建一个合适的异常类将他抛出，用的关键字就是throw。throws是异常的声明，就是我们在捕获异常的时候，不能解决这个异常就需要向上抛异，此时就要使用throw这个关键字来抛异常了。

- [ ] 异常的底层

  暂且不懂。

- [ ] 什么是反射

  通俗来讲，反射就是Java程序在运行过程中，我们可以动态的获取他的类中的一切，包括成员变量，成员方法以及构造方法。

- [ ] 反射的使用

  说道反射的使用，那我就说一说反射获取类的三种方法，通过全类名，Class.forName获取；通过对象.getClass获取，通过类名.Class获取。但是需要注意的是，如果需要创建实例对象，那么类一定要有一个空参构造器。

- [ ] getName、getCanonicalName、getSimpleName的区别?

  getName是获取类名的全限定名，Jvm中的Class表示。getSimpleName只获取类名。getCanonicalName只要用来输出toString，在内部类和数组类型的表示形式不是这样的。

- [ ] 什么是spi机制

  Spi是jdk内置的一种服务提供发现机制，可以用来启用框架扩展和替换组件。比如java.sql.Driver接口，其他不同的厂商可以针对同一接口做出不同的体现。

- [ ] spi机制的应用

  各种的jar包的使用就算是吧。

- [ ] 集合有哪些类，他的体系结构具体有哪些

  这个好说，Java集合从大方向来说,主要就Collection和Map，而Collection接口的主要存对象的，他的实现类分别为list和Set，List的主要实现类有ArrayList，LinkedList，vector；ArrayList底层为数组实现，当然也有数组的特点，容易查找，难增删。vector和ArrayList大体上是一致的，但是他是线程是安全的，对，ArrayList线程并不是安全的，LinkedList底层是双向链表，容易增删，难查找。Set的主要实现类TreeSet,HashSet,LinkedHashSet,Treeset的底层是二叉树，HashSet的底层是Hash表，LinkedHashSet存储数据的底层是Hash表，用双向链表记录插入顺序。Map主要是用来存键值对数据的，他的主要实现类有HashMap，HashTable和TreeMap。底层都是Hash表。

- [ ] ArrayList的底层

  ArrayList底层由数组组成，在jdk7时，他在创建的时候会先创建一个长度为10的数组，在每次调用add函数时，就会给数组进行赋值，直到长度到达10的时候，就会自动扩容为原来大小的1.5倍，在jdk8中，除了只有在第一次调用add函数时才会创建长度为10的数组，其他情况都一样。

- [ ] ArrayList自动扩容

  上面说了。

- [ ] Map有哪些类

  Map有HashMap，TreeMap和HashTable,LinkedHashMap

- [ ] JDK7中HashMap如何实现

  JDK7中的HashMap采用的是冲突链表方式存储数据的，先对比两个值的哈希表，如果不行就对比哈希值，如果还是不行就使用两个对象的equals方法对比。

- [ ] JDK8中HashMap如何实现

  JDK8中HashMap采用的是开放地址方式，当链表中的元素达到8个时，会将链表转换成红黑树。

- [ ] HashSet是如何实现的

  HashSet是对HashMap的一个简单的封装。

- [ ] HashMap的扩容机制

  当HashMap中的元素个数超过数组大小(数组总大小length,不是数组中个数size)*loadFactor时，就会_***\*调用resize方法\****进行数组扩容，loadFactor的默认值为***0.75***，这是一个折中的取值。也就是说，默认情况下，数组大小为***16**_，那么当HashMap中元素个数超过160.75=12（这个值就是代码中的threshold值，也叫做临界值）的时候，就把数组的大小扩展为 2*16=32，即扩大一倍，然后重新计算每个元素在数组中的位置。至于为什么是0.75？这是大量实验得出的结果。如果取0.5,超过一般就扩容,造成资源的浪费；如果取1,到临界值才扩容,会增加哈希碰撞的几率。