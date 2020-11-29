# C++程序设计

[//]: # (__author__ = "Clark Aaron")

C++是兼容C程序设计的一门混合程序设计语言，同时支持面向过程程序设计与面向对象程序设计。面向过程程序设计适用于个人开发的程序设计思维，其中SP（Structure Programming，结构化程序设计）思想（自顶向下、分而治之、模块编程）是其主要特征；其中模块编程是使用顺序、分支、循环三种流程结构实现具体功能的函数。面向对象程序设计适用于团队开发的程序设计思维，抽象数据、类型封装是其主要特征。以对象表示客观事物，以继承描述客观事物间的关系，以消息传递来反映客观事物间的交互。

## 抽象类型

抽象类型即ADT（Abstract Data Type，抽象数据类型），是一种编程中的数据类型。抽象是指有意忽略问题的某些细节和与当前问题无关的方面，把事物的主要特征抽象出来。可以分为数据抽象与过程抽象。

* 数据抽象：数据抽象即提取客观事物主要的数据特征来描述对象，获取抽象数据类型的数据特征。

* 过程抽象：过程抽象即提取客观事物主要的行为特征来描述对象，获取抽象出具类型的行为特征，同时也作为访问ADT数据成员的接口。

## 类型封装

封装是将底层的元素组合起来，形成高层次实体的技术。类型封装通过类型的访问权限来进行封装。即通过private、protected与public三种权限。通过封装，隐藏类型的数据成员以及敏感的结构，只对外保留特定的接口来访问。C++提供struct与class两种封装结构，其中struct中成员默认的访问权限时公开权限，class中成员的默认结构是私有权限。

### 公开权限

公开权限即该成员对外部和子类都可见的接口，可以让外部直接访问。使用`public`来标识。

* 具有公开权限的结构：

  ```c++
  class <class name> {
    public:
      <member>;
  }
  ```

### 保护权限

保护权限即该成员对外部不可见但对子类可见的接口，可以让子类直接访问，使用`protected`来标识。

* 具有保护权限的结构：

  ```c++
  class <class name> {
    protected:
      <member>;
  }
  ```

### 私有权限

私有成员即该成员对外部以及子类都不可见的接口。外部只能通过拥有公开权限的接口来间接访问，使用`private`来标识。

* 具有私有权限的结构：

  ```c++
  class <class name> {
    private:
      <member>;
  }
  ```

## 类型继承

继承是实现代码重用机制的手段,即子类复制了超类的数据成员和成员函数。子类不仅能够继承超类的属性和行为（除析构函数、友元、静态成员，构造函数在C++11之前也不能被继承），而且能够修改或增加新的属性和行为。C++支持单继承也支持多继承。继承可以通过继承方式控制子类继承自超类的成员对外的访问权限，这不影响子类对超类成员的访问权限。同时子类可以扩展自己的成员，也可以对超类的方法成员进行重写、重载。当子类重写超类的方法成员时，超类的方法成员被隐藏，如果必须使用超类的方法成员需使用全名`<superClass>::<funcName>`；同时也可以使用using设定方法在该区块的可见性。

### 公开继承

公开继承的方式是不改变子类继承自超类的任何成员对外的访问权限。

* 公开继承：

  ```c++
  class <subClass>: public <superClass> {
    <member>;
  }
  ```

### 保护继承

保护继承的方式是将子类继承自超类的公开成员对外的访问权限更改为保护，继承的保护成员与私有成员对外的访问权限不变。

* 保护继承：

  ```c++
  class <subClass>: protected <superClass> {
    <member>;
  }
  ```

### 私有继承

私有继承的方式是将子类继承自超类的公有成员与保护成员对外的访问权限更改为私有，继承的私有成员对外的访问权限不变。

* 私有继承：

  ```c++
  class <subClass>: private <superClass> {
    <member>;
  }
  ```

#### 禁止继承

可以使用`final`来表明该类不能被继承。

* 禁止继承：

  ```c++
  class <className> final {
    <member>;
  }
  ```

* 使用`using`修改指定超类的非私有成员权限：

  ```c++
  class <subClass>: private <superClass> {
    public:
      using <superClass>::<protectedMember>;      // 将超类的保护成员指定为公开成员。
  }
  ```

* 使用`using`声明派生类要继承基类的构造函数；

  ```c++
  using <superClass>::<superClass>;
  ```

#### 虚拟继承

虚拟继承时解决多继承中的成员冲突问题，使用`virtual`

### 阻止继承

可以通过`final`来限定该类型不能被继承。

* 阻止继承：

  ```c++
  class <class name> final {
    <member>;
  }
  ```

### 单继承

单继承即子类只拥有一个超类的继承方式。

* 单继承方式：

  ```c++
  class <subclass name>: <inheritance type> <superclass name> {
    <member>;
  }
  ```

### 多继承

多继承即子类拥有多个超类的继承方式。

* 多继承方式：

  ```c++
  class <subclass name>:
    <inheritance type> <superclass name>

  ```

### 继承的应用

* 被子类重写的超类的方法成员调用：

  * 使用成员的全名来调用：

    ```c++
    // human is user-defined class.
    class human {
      private:
        string birth;
        string gander;
        float high;
        float weight;
      protected:
        void setBirth(string birth);
        void setGrander(string grander);
        void setHight(float hight);
        void setWeight(float weight);
      public:
        human(string birth,string grander,float hight,float weight);
        boolean print();
        boolean set();
    }

    // chinese is inheritting human class.
    class chinese: public human {
        private:
          string IDcard;
          string nationality;
        protected:
          void setIDcard(string IDcard);
          void setNationality(string naionality);
        public:
          chinese();
    }

    // chinese method member is defining.
    chinese::chinese():
      human(birth,grander,hight,weight)              // 这里使用
    {

    }
    ```

## 接口多态

多态（polymorphism）是指不同对象结构到同一消息时会产生的不同行为，是处理类的层次结构之间以及同一类内部同名函数的关系问题。这一机制是在抽象类型的接口上实现的。实现多态的方式有接口重载多态、对象继承多态、类型模板多态。多态实现的方式分为静态多态性与动态多态性。

### 重载多态

C++是一门强类型检查语言，在每一个函数、方法调用用时会经过类型检查。如果实参类型与对应的形参类型不匹配，C++就会尝试可能的类型转换。若是转换之后仍没有函数原型相匹配，则产生编译错误。

#### 函数重载

#### 方法重载

#### 模板重载

#### 运算符重载

运算符重载可以扩展C++运算符的功能。运算符是一种特殊的函数，operator是运算符函数的限定。同时也可以创建新的运算符。运算符可以重载方法或者函数都可以，当运算符重载为方法时，this指针默认为第一个参数。当运算符重载为函数时，通常将函数作为类的友元。

* 可以重载的运算符：

  | 运算符 | 说明 |
  |:---:|:--- |
  | + |
  | - |
  | * | 
  | / |
  | % |
  | & |
  | \| |
  | ~ |
  | ^ |
  | == |
  | != |
  | > |
  | <= |
  | < |
  | >= |

* 不可以重载的运算符：

  | 运算符 | 说明 |
  |:---:|:--- |
  | :: |
  | .* |
  | . |
  | ?: |

* 赋值运算符的重载：

  ```c++
  class Human {
    private:
      string name;
    public:
      Human& operator=(const Human& human);       // 重载赋值运算符。
  }

  Human& Human::operator=(const Human& human) {   // 重载复制运算符的实现。
      this->name = human->name;
      return *this;
  }
  ```

* 前自增运算符：

  ```c++
  x& operator++(){};
  ```

* 后自增运算符：

  ```c++
  x operator++(){};
  ```

* 类型转换运算符：将类成员转化为int类型。

  ```c++
  operator <type>(0) {
    <code>;
    return <typeValue>;
  }
  ```

* 函数调用运算符：

### 继承多态

实现对象继承多态需要满足继承的基础上，子类重写超类的接口并将超类的指针绑定到子类对象上。在超类使用接口时，实际是子类的重写接口。

#### 方法重写

#### 虚拟方法

虚拟方法时运行时多态的基础，通过动态联编实现的。允许函数调用与函数体之间的绑定在程序运行时确定。使用`virtual`修饰的方法。表达存在却无法表达的抽象概念。`virtual`指明该函数使用动态联编。

* override是限定子类的函数一定要覆盖超类的虚函数，如果未覆盖则编译出错。

 ```c++
 virtual void Print(int a) override {}
 ```

* final限定只让子类的子类继承虚函数的实现，不想让其覆盖，只能限定子类中虚函数的实现函数。

所有的虚函数在使用前必须被实现。且之后所有的继承均为虚函数。

* 虚拟析构方法：

#### 纯虚方法

纯虚函数是指在声明时被初始化为0的方法成员。

* 纯虚函数：

 ```c++
 virtual <returnType> <funcName>(<type> <parName>) = 0;
 ```

#### 抽象类

具有纯虚函数的类称为抽象类。抽象类不能实例化。

多态是面向对象编程的又一重要特征，是指不同对象接收到通一消息时会产生不同的行为。多态有三种表现形式：继承多态、重载多态、模板多态。

### 模板多态

即使用模板的方式实现多态。

* 类模板：

  ```c++
  template <typename T1>
  class <className> {
      <member>;
  }
  ```

  > Note：类成员中使用了T1参数。

### 运行时类型信息

RTTI（Run-Time Type Information）是解决多态问题引入的机制。提供了在程序运行时获取对象类型的方法。在C++中，支持RTTI的运算符有`dynamic_cast`、`typeid`有些编译环境默认关闭RTTI的，需要开启才能使用。

* 强制转换：dynamic_cast是一个强制类型转换的操作符，用于多态超类指针与子类指针之间的转换。是在运行时转换的。

  ```c++
  dynamic_cast<<type>*>(obj);
  dynamic_cast<<type>&>(obj);
  dynamic_cast<<type>&&>(obj);
  ```

  > Note：通常type中有虚函数；在以下情况转换成功：
  >
  > * obj为type的公开子类或公开超类；
  > * obj与type为同一类型；

* 类型判断：typeid用于在程序运行时判断对象的真实述据类型，定义在tyoeinfo中。
  
  ```c++
  typeid(obj);
  ```

  > Note：该对象返回一个type_info的引用，type_info定义在typeinfo中，拥有一个name()方法获取类型名称。

## 类型友元

友元即提供给一些函数或类直接访问类的私有与保护成员。友元不是类的成员，但是是类接口的一部分。友元不具有逆向性和传递性。

### 友元类

友元类是将其他类作为类的友元。

* 友元类的声明：

  ```c++
  class Human {
    private:
      string Name;
    public:
      Human();
      ~Human();
    friend class Developer;                             // 声明Developer为Human的友元类。
  }
  ```

  > Note：友元类中的所有方法成员可以直接访问对象的私有和保护成员。

### 友元函数

友元函数是将函数作为类的友元。

* 友元函数的声明：

  ```C++
  class Human {
      private：
        string Name;
      public:
        Human();
        ~Human();
      friend bool Set(int index, string value);   // 声明Set为Human的友元函数。
  }
  ```

  > Note：友元函数一般是将运算符函数声明为友元来直接访问类的私有与保护成员。
