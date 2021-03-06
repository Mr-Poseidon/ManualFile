# C++ Primer Plus 电子笔记

[TOC]



## 第13章、类继承

1. 类继承：比修改代码更好的扩展类和修改类的方法。

2. 继承的作用：

   - 可以在已有类的基础上添加新的功能
   - 可以给类添加数据
   - 可以修改类的方法行为

3. 原始类称为基类，继承类称为派生类。

4. 创建和回收派生类对象的过程：

   - 调用基类构造函数（初始化继承的数据成员）
   - 调用派生类构造函数（初始化新增的数据成员）
   - 调用派生类析构函数
   - 调用基类析构函数

   注意：派生类的构造函数总是调用一个基类的构造函数。可以使用初始化   器列表语法指明要使用的基类构造函数，否则使用默认的基类构造函数。

   

5. 派生类不能直接访问基类的私有成员，必须通过基类的公有方法或保护方法访问基类的私有成员。

6. 一般将基类和派生类的类声明放在同一个头文件中，然后具体实现则放在各自的文件中。

7. 派生类和基类的**特殊关系**：

   - 派生类对象可以使用基类的**非**私有成员

   - 基类指针可以隐式转换指向派生类对象

   - 基类引用可以隐式转换引用派生类对象

     注：基类指针只能调用基类方法，不能调用派生类方法，因为派生类方法中可能存在新增的数据成员。

   基类能够引用派生类对象的原因：

   ​		基类中拥有的数据成员，派生类都通过继承拥有。

   派生类不能够引用基类对象的原因：

   ​		派生类中可能存在新增的数据成员，而基类中都没有。

8. 引用兼容性属性能够将基类对象通过构造函数，初始化为派生类对象。

9. C++的三种继承方式：

   - 公有继承
   - 保护继承
   - 私有继承

10. 多态的概念：

    同一个方法，在基类和派生类中的行为是不同的，具有多种形态。

11. 多态公有继承的实现机制：

    - 在派生类中重新定义基类的方法
    - 使用虚方法

12. 使用与不使用virtual关键字的区别：

    - 使用virtual关键字，则根据实际的**对象类型**来选择调用的方法
    - 不使用virtual关键字，则根据**指针类型**来选择调用的方法。哪怕是基类指针指向派生类对象，不使用virtual关键字也是调用的基类方法。

13. 应该将派生类中可能会重新声明的方法，在基类中声明为虚方法。在基类中声明为虚的方法，通过继承，在派生类中自动称为虚方法。

14. 为了确保在释放派生类对象时，正确调用析构函数，应该将基类的析构函数声明为虚析构函数。

    **为基类声明一个虚析构函数是一种惯例。**

    虚函数能够根据实际的对象类型选择对应的方法。

15. 派生类构造函数初始化基类私有数据时，采用**成员初始化列表语法**。

16. 在派生类中，必须使用域解析运算符来调用基类方法。

    若派生类中没有重新定义基类方法，则可以不使用域解析运算符。

17. 多态特性的体现：

    ​		可以使用一个基类数组来表示多种类型的派生类对象。

18. 设置虚析构函数的必要性：

    ​		虚析构函数可以确保正确的析构函数序列被调用。

    ​		可以正确释放派生类对象的所有内存。

19. 联编（自己的理解：联系编译）的概念：

    ​		将源代码中的函数调用，解释为执行特定的函数代码块，称为函数名联编。

20. 联编类型：

    - 编译过程中联编，静态联编，早期联编
    - 程序运行时选择正确的代码，动态联编，晚期联编。

21. 派生类转换为基类，称作“向上强制转换”；基类转换为派生类，称作“向下强制转换”。向下强制转换必须使用显式类型转换。向上转换是安全操作，向下转换可能带来不安全的操作。

22. 编译器对非虚方法采用静态联编；隐式向上转换导致基类指针可以指向派生类对象，所以采用动态联编。

23. 静态联编的优点：

    ​		效率更高。（所以设置为C++的默认选择）。

24. 构造函数不能是虚函数。因为派生类不能继承基类的构造函数，所以将类构造函数声明为虚函数没有意义。

25. 友元不能是虚函数，友元函数不是类成员，只有类成员才可以是虚函数。

26. 重新定义不会生成函数的两个重载版本，而是隐藏了基类的方法。重新定义将隐藏所有的同名基类方法。

27. 如果基类声明被重载了，应该在派生类中重新定义所有的基类重载方法。

    若只重新定义其中的一个方法，则其他方法将被隐藏。

28. 在类外，使用公有方法访问保护成员。

    派生类成员可以直接访问基类的保护成员。

29. 为了保证数据的封装性，必须对数据成员采用私有访问控制。若对数据成员采用保护访问控制，派生类成员可直接访问基类数据成员，基类数据成员就失去了数据的安全性。

30. 保护访问控制的体现：

    ​		保护成员函数可以使派生类访问基类中外部无法访问的内部函数。

31. 包含纯虚函数的类称为抽象类（abstract base class,ABC），不能实例化对象，只能作为基类。

32. 在原型中使用=0，表示该函数是一个纯虚函数，该类是一个抽象类。

    例如：void Move(int x,int y) = 0;

33. 抽象类描述的是至少使用一个纯虚函数的接口，使用常规虚函数来实现这种接口。

34. 在基类中行为不同的方法应该被声明为虚函数。

35. 保护访问权限保护的数据和方法对基类和派生类可见，同时对外隐藏。

36. 若定义了构造函数，则编译器不会定义默认的构造函数，最好提供一个显式的默认构造函数。

37. 构造函数不能够被继承的原因：

    ​		构造函数用于创建新的对象，而不是被现有对象引用。

38. 必须定义显式的析构函数来释放构造函数使用new分配的所有内存，并完成对象所需的清理工作。

39. 对于基类，必须提供一个虚的析构函数。

40. 使用explicit关键字将禁止进行隐式转换。但仍然允许显式转换。

41. 返回引用和返回对象的区别：

    ​		返回引用可节省时间和内存，不需要调用构造函数和拷贝数据。

    ​		直接返回对象与值传递对象相似，他们都生成临时副本。

42. 不能返回在函数中创建的临时对象的引用，因为对象在函数结束时被回收，该引用对象也将不存在。

43. 若函数通过引用或者指针传递对象，则按引用返回对象。

44. 可用const关键字传递参数，来保证参数不被修改。

45. 声明为const 的引用或指针，只能将参数传递给声明为const的引用或指针

46. 不能被继承的三大部分：

    - 构造函数不能被继承
    - 析构函数不能被继承
    - 赋值运算符不能被继承

47. 若类构造函数通过new来初始化指针，则需要提供一个显式的赋值运算符

48. 将派生类对象赋值给基类对象，会调用基类对象的赋值运算符，并且只处理基类的成员。

49. 若想把基类对象赋值给派生类对象，需要在构造函数中，对基类对象转换为派生类对象进行定义，或者，派生类定义了用于将基类对象赋值给派生类对象的赋值运算符。

50. 设计基类时，必须确定能否将类方法声明为虚方法。

51. 纯虚方法用于定义派生类的通用接口。











## 面向对象三大特性解决的问题

1. 封装解决了数据的安全问题。
2. 继承解决了类的功能扩展和功能修改问题。
3. 多态解决了一个接口多个实现的问题。

