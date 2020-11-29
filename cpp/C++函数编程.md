# C++函数编程

[//]: # (__author__ = "Clark Aaron")

## 函数

C++是一门强类型检查语言，即每一个函数调用的实参在编译期间都要经过类型检查，并尝试类型转换，如果不行则报错；所以所有函数必须在调用前进行声明或
定义。

### 函数的定义

函数在调用前必须被定义，除了直接在调用前定义函数外，也可以在头文件中进行声明，而在源文件中实现该函数。

* 函数的一般定义：

  ```c++
  // 函数一般定义的格式：
  <return type> <function name>(<paramater list>) {
    <function code>
  }
  // 函数一般定义的举例：
  int min(int a, int b) {
    return (a<b)?a:b;
  }
  ```

* 函数的分离定义：函数原型（由函数返回类型 、名称、参数列表构成）的声明与实现。

  ```c++
  // 函数的声明格式：
  <return type> <function name>(<paramater list>);
  // 函数的声明举例：
  int min(int a,int b);
  // 函数的实现格式：
  <return type> <function name>(<paramater list>) {
    <function code>
  }
  // 函数的实现的举例：
  int min(int a,int b) {
    return (a<b)?a:b;
  }
  ```

  > Note：一般使用函数的分离定义的方式函数，并将函数原型的声明放在头文件中，并在同名的源文件中实现该函数原型，在实现中其他必须保持一致，但参数名称可以不同（推荐使用一致的参数名称）。

### 函数的参数

参数是函数与外界进行数据交互的接口。函数定义时的参数称为形参，函数调用时的参数称为实参；实参为外部数据，在函数执行时会将实参复制一份给函数的形参。C++不支持传统的函数参数声明，即将函数参数的类型说明放在函数头与函数体之间。

* 参数列表：参数列表中有多个参数时，使用`,`隔离开。

  ```c++
  // 一般参数：
  int min(<type> <paramater name>,<type> <paramater name>);
  // 带有默认值的参数：
  int compare(<type> <paramater name>,<type> <paramater name>,<type> <paramater name> = <default value>);
  // 

  ```

  > Note：带有默认值的参数必须放在一般参数的右边，

#### 参数的传递

C++的函数支持数据、指针、引用三种方式传递参数。

* 数据传递参数的方式：即按值传递的参数传递方式。在使用该方式传递参数时会将实参的值复制一份到对应的内存空间（在堆栈中分配的形参）。形参与实参是两个具有相同值的不同对象。

  ```c++
  // 数据传递的方式传递参数的格式：
  <return type> <function name>(<type> <paramater name>);
  ```

  > Note：按值传递参数是将数据对象复制一份到函数内部。

* 指针传递参数的方式：即参数为指针。事实上，在含有指针参数的函数在调用时，实参与形参具有指向同一数据的不同指针。函数内外可以根据该指针实现内外数据的交互。

  ```c++
  // 按指针参数传递的方式传递参数的格式：
  <return type> <function name>(<type>* <pointer name>);
  ```

  > Note：指针传递参数是将指针复制一份到函数内部，数组参数因为不允许拷贝数组，所以通常转化为指针使用。

* 引用传递参数的方式：引用参数传递参数事实上是将形参声明为实参的引用。这样等同于指针传递参数的方式。

  ```c++
  <returnType> <funcName>(<type>& <parName>);
  ```

  > Note：引用传递是对数据对象的引用。

#### 参数的缺省数据

C++支持参数的缺省值，必须位于参数列表的末尾。

### 函数的返回

C语言与经典C++均支持在无返回值类型时，返回一个int类型的返回值；在标准C++中不再支持这一功能，如果确定函数无返回值，只需将返回值类型指定为void即可。除void类型的返回之外，所有其他类型的返回必须调用return语句返回。

#### 函数的返回引用

返回引用是指函数的返回值为一个对象的引用。通常默认返回对象左引用，实际返回该变量的地址。

* 返回引用：

  ```c++
  <return type>& <function name>(<paramater list>);
  ```

### 函数的应用

#### 内联函数

内联函数即使用`inline`修饰函数，内联函数是在编译时使用函数的定义体替换调用语句，不会为内联函数建立运行时环境，适合于简单的函数；其中匿名函数不会指定为内联函数、递归函数、含有循环或switch的函数。

#### 匿名函数

* Lambda表达式：Lambda表达式实质上是一种基于模板的匿名内联函数拥有自己的参数列表、返回值与函数体，可以在函数内部定义。
  
  ```c++
  [capture](parameters) [mutable] -> <return> {statement}
  ```

  > Note：capture即捕获，将lambda使用的外部变量捕获，可以分为值捕获与引用捕获

#### 模板函数

模板函数即由函数模板生成的函数。

## 方法

方法是抽象类型的行为抽象，实现访问对象的接口。

### 方法的定义

方法必须是抽象数据类型的成员。可以在类内声明，类外实现。

* 方法的定义：

  ```c++
  class Human {
    private:
      string Name;
    public:
      void Print();
  }

  void Human::Print() {             // Print方法的定义。
    std::cout << this->Name <<endl;
  }
  ```

### 方法的参数

方法的参数基本与函数的参数一样；但是在参数列表中，有一个默认的参数this指针。

### 方法的返回

方法的参数一般与函数的返回一样（构造方法与析构方法例外）。

#### 方法的返回引用

返回引用在方法中一般类对象本身的引用，这样可以让方法的返回继续调用方法。

* 方法的返回引用：

  ```c++
  class Human {
    private：
      string name;
    public:
      Human& SetName(string name);        // SteName()返回是一个Human引用。
      Human&  Print();                    // Print()返回是一个Human引用。
  }

  Human& Human::SetName(string name) {
    this->name = name;
    return *this;                         // SetName()返回对象本身。
  }

  Human& Human::Print() {
    cout << this->name <<endl;
    return *this;                         // Print()返回对象本身。
  }

  int main() {
    Human people;
    people.SetName("Clark").Print();      // 连续调用方法。
  }
  ```

  但是当方法是一个常量方法时，this既是一个指针常量也是一个常量指针，返回对象本身只能指定为引用常量：

  ```c++
   class Human {
    private：
      string name;
    public:
      Human& SetName(string name);        // SteName()返回是一个Human引用。
      const Human&  Print() const;        // Print()返回是一个Human引用常量。
  }

  Human& Human::SetName(string name) {
    this->name = name;
    return *this;                         // SetName()返回对象本身的引用。
  }

  const Human& Human::Print() const {
    cout << this->name <<endl;
    return *this;                         // Print()返回对象本身的引用常量。
  }

  int main() {
    Human people;
    people.SetName("Clark").Print();      // 使用这样的连续调用方法时可行的。
    // people.Print().SetName("Clark");   // 使用这样的连续调用方式时不可行。
  }
  ```

  为了解决常量方法人仍可以连续调用的问题，我们可以通过方法重载与私有方法实现该功能。

  ```c++
  class Human {
    private:
      string name;
      void print() const;                 // 这是一个私有的显示方法。
    public:
      Human& Print();                     // 这是一个非常量方法。
      const Human& Print() const;         // 这是一个常量方法。
  }

  void Human::print() const {             // 实现数据成员显示的功能。
    cout << this->name;
  }


  Human& Human::Print() {                 // 实现返回对象的引用。
    print();
    return *this;
  }

  const Human& Human::Print() const {     // 实现返回对象的引用常量。
    print();
    return *this;
  }

  int main() {
    Human people;
    people.SetName("Clark").Print();      // 使用这样的连续调用方法时可行的。调用返回引用常量的Print().
    people.Print().SetName("Clark");      // 使用这样的连续调用方式时也可行。调用返回引用的Print().
  }
  ```

### 方法的应用

类型的方法成员是进行数据成员操作、对象间信息交互的接口。在这些接口中有一些特殊的接口是所有类型都有或者具有特殊功能的方法成员。例如构造方法、析构方法、常数方法、静态方法等。

#### 构造方法

构造方法是用于实例化对象时自动初始化对象的方法。其方法名称与类型名称相同、无返回值、可以被重载。编译器会为没有构造方法的类型自动构建默认的无参构造方法。

* 构造方法：构造方法除了方法名称、参数、返回，还具有一个初始化列表。常量数据与引用必须在初始化列表中初始化。

  ```c++
  class Human {
    private:
      string name;
      string gander；
    public:
      Human(string name,string gander);
  }

  Human::Human(string name,string gander):    // 这里使用了构造方法的列表初始化。
  name(name),
  gander(gander)
  {}
  ```

  > Note：对象的初始化方法有（按照初始化的优先级排列）：类内初始值、列表初始化、构造方法的函数体。构造方法必须是公开成员、禁止显式调用、不能声明为常数方法。

* 委托构造方法：委托构造方法即在构造方法初始化列表中调用其他构造方法，但在使用委托构造函数时需要注意，初始化列表中不能有其他初始化成员。

  ```c++
   class Human {
    private:
      string name;
    public:
      Human(string name);
      Human();
  }

  // Class Human.
  Human::Human(string name):
  name(name)
  {}

  Human::Human():             // 这里使用了委托构造方法。
  Human("Clark Aaron")
  {}
  ```

* 重载构造方法：多个构造方法间必须有不同的参数列表。

  ```c++
    class Human {
      private:
        string name;
      public:
        Human(string name);
        Human(const Human& human);
        Human()=default;           // 这里是让编译器生成默认构造方法。
    }

    // Class Human.
    Human::Human(string name):
    name(name)
    {}
    ```

* 复制构造方法：复制构造方法用于同类型对象初始化对象、函数调用与返回、初始化容器中元素、根据初始化列表初始化数组元素。如果需要定义复制构造方法，则同样也需要重载赋值构运算符。

  ```c++
  class Human {
    private:
      string name;
    public:
      Human(const Human& source);         // 复制方法的声明。
  }

  Human::Human(const Human& source) {     // 复制方法的实现。
  }
  ```

  > Note：如果未定义复制构造方法（即使定义了其他构造方法），编译器也会定义一个默认的复制构造方法。将复制构造放定义未私有成员将禁止对象间的复制。

#### 析构方法

析构方法（destructor）用于内存回收、关闭连接等工作，在对象销毁时自动调用。其方法名的格式是前缀`~`与类型名称、无返回、无参数表，不支持重载。如果没有定义析构方法，编译器会自动生成一个默认的析构方法。

* 析构方法的一般用法：用于对象销毁时的清理工作。一般如果需要自定义析构方法，则同时需要定义赋值构造方法与重载赋值运算符。

  ```c++
  class Human {
    private:
      string name;
    public:
      ~Human();
  }

  // Class Human.
  Human:: ~Human(){
    //在这里实现对象销毁的清理工作。
  }
  ```

  > Note：析构方法不能被显式调用且必须为公开成员。

* 虚拟析构方法的用法：虚拟构造方法是为解决继承关系中的内存泄漏问题。

  ```c++
  class Human {
    private:
      string name;
    public:
    virtual ~Human();
  }

  class Chinese: public Human {
    public:
    virtual ~Chinese();
  }

  // Class Human.
  Human:: ~Human(){
    //在这里实现对象销毁的清理工作。
  }
  ```

#### 移动方法

移动方法用于完成临时对象的复制问题，移动方法用于将对象的内存空间通过赋值的方式从右值转移到左值。移动方法可以分为移动赋值方法于移动拷贝方法。如果类型没有定义了赋值方法、拷贝方法、析构方法，并且所有成员都是可移动（定义移动方法的类型）的时候，编译器会自动生成移动赋值方法于移动拷贝方法。

* 移动赋值方法：
  
  ```c++
  class Human {
    private:
      string name;
    public:
      Human&  operator=(Human&& source) {
        //移动赋值方法定义。
      }
  }
  ```

* 移动拷贝方法：

  ```c++
  class Human {
    private:
      string name;
    public:
      Human(Human&& source);
  }
  Human::Human(Human&& source) {
    // 移动拷贝方法的定义。
  }
  ```


#### 常量方法

常量方法用来标识不修改数据成员的方法。使用const来标识。

* 常量方法的定义：

  ```c++
  class Human {
    private:
      string name;
    public:
      void Print() const;     // 声明Print()为常量方法，不能修改数据成员。
  }

  void Human::Print() const {
    std::cout << this.name;
  }
  ```

  > Note：必须在方法成员的声明与定义时都使用const来修饰。否则会编译错误。

#### 静态方法

静态方法

#### 虚拟方法

虚拟方法是实现动态多态性的基础，是通过动态联编实现的。虚方法采用前缀`virtual`来标识。除构造函数之外的所有非静态方法和非内联函数都可以声明为法。对于虚方法采用动态联编的方式实现。在继承中，当超类指针调用虚方法时，会动态绑定到实际指向的对象；简而言之，当超类指针指向子类对象时，超类对象的虚方法实际指向的子类的重写超类虚拟方法的方法。

* `override`用于标识该方法重写超类的虚拟方法，如果标识的方法未重写超类的虚拟方法会发生编译错误。

  ```c++
  class Human {
    public:
      virtual void speak();
  }
  class Chinese {
    public:
    void speak() override;
  }
  ```

* `final`用于标识子类不能重写超类的虚拟方法。

  ```c++
  class Human {
    public:
      void fly() final;
  }
  class chinese {
    public:
      void run();
  }
  ```

#### 纯虚方法

纯虚方法即没有具体实现的虚拟方法，在虚方法声明时将函数初始化为0即可。具有纯虚方法的类称为抽象类。抽象类不能用于实例化对象。

* 纯虚方法的声明：

  ```c++
  virtual <return type> <function name>(<paramater list>) = 0;
  ```

## 模板

模板是C++实现代码重用机制的重要工具，是泛型技术的基础。表示一种概念级的通用程序设计方法。STL是基于模板实现的C++标准库。模板的声明与实现一般都放在头文件中。

### 模板的定义

模板使用`template`来定义，并且使用typename来定义模板参数并使用尖括号包含模板参数。

* 类模板的定义：

  ```c++
  template <template T, int SIZE>
  class Stack {                     // 类模板的定义。
      private:
          T elems[SIZE];
          int top;
      public:
          Stack();
          void push(T value);
          T pop();
  }
  ```

* 方法模板的定义：方法模板是实现类模板的方法成员时使用的模板。方法模板不能是虚拟方法。

  ```c++
  template <template T, int SIZE>
  class Stack {
      private:
          T elems[SIZE];
          int top;
      public:
          Stack();
          void push(T value);
          T pop();
  }

  // 类模板的方法成员的实现。
  template <typename T, int SIZE>       // 方法模板的定义。
  Stack<T,SIZE>::Stack() {
    // 实现构造方法。
  }
  template <typename T, int SIZE>
  void Stack<T,SIZE>::push(T value) {
    // 实现入栈操作。
  }

  ```

* 函数模板的定义：使用`template`来定义模板，`typename`或`class`来标识模板的类型参数，由于class用于定义类，则一般使用typename。
  
  ```c++
  template <typename T>
  T min(T a,T b) {
    return (a<b)?a:b;
  }
  ```

### 模板的参数

模板是一种忽略具体数据类型，只考虑程序操作逻辑的通用程序设计方法。模板的参数一般是数据类型，称为类型参数，一般使用`typename`或者`class`来标识，但是由于class常用于定义类，所以一般使用typename；在定义类模板时可能使用非类型参数，即具体的数据类型。

#### 类型模板参数

类型模板参数的实参是实际的数据类型。

#### 常量模板参数

非类型模板参数的实参是常数，不能是变量。常数模板参数的类型是受限的，只能是整数类型、枚举类型、指针类型等，不能使用浮点类型、抽象类型以及void。

#### 缺省模板参数

指定缺省时默认的模板参数。

* 缺省模板参数：

  ```c++
  template <typename T1,typename T2 = int>    // T2指定默认缺省模板参数。
  T1 sum(T1 a, T2 b=0);
  ```

#### 可变模板参数

C++11标准支持阐述类型与个数都不确定的模板。

* 可变模板参数的模板：

  ```c++
  template <typename T1,typename ... T2>
  T1 sum(T1 p,T2 ... arg) {
    // 其中T2为可变模板参数，称为参数包，可以是零个以上不同类型的模板参数。
  }
  ```

### 模板的对象

由模板生成对象的过程称为模板的实例化。模板的对象有模板类、模板方法、模板方法。只有在模板使用时，函数模板根据实参的类型生成处理该类型的模板对象，然后再调用使用模板对象。当遇到同一类型的使用时，不会再次实例化，只会调用第一次实例化的模板对象。在模板参数匹配时也不会进行类型转换。可以通过强制类型转换、指定参数类型、多个模板参数来实现特定类型的实例化。

* 模板类：由类模板生成的类。在使用模板类定义对象时，不会生成类的模板方法成员。

  ```c++
  // 使用Stack模板生成一个对象。
  Stack<int,10> intStack;
  ```

* 模板方法：由方法模板生成的方法。在遇到方法模板调用时，根据实参的类型生成处理该类型的模板方法。

* 模板函数：由函数模板生成的函数。

  ```c++
  int minnum;
  minnum = min(2,3);            // 根据实参类型自动生成一个模板函数。
  ```

* 强制类型转换：使用强制类型转换实参为指定数据类型的模板实例化。

  ```c++
  int minnum;
  minnum = min(int(3.2),2);     // 生成int类型的模板函数。
  ```

* 指定参数类型：指定模板的参数类型实现指定数据类型的模板实例化。

  ```c++
  double minnum;
  minnum = min<double>(1,3.2);  // 生成double类型的模板函数。
  ```

* 多个模板参数：使用多个模板参数来实现多个不同类型的模板实例化。

  ```c++
  template <typename T1,typename T2>
  T1 min(T1 a,T2 b) {
    return (a<b)?a:b;
  }
  int minnum;
  nimnum = min(1,2.3);          // 生成min<int,float>的模板函数。  
  ```

### 模板的特化

C++允许为模板定义某种数据类型的替代版本，称为模板的特化。特化模板与原模板具有同样的结构，只是制定了数据类型。

* 模板的特化：

  ```c++
  template <typename T1,typename T2>
  T1 min(T1 a,T2 b) {
    return (a<b)?a:b;
  }
  template<>    // 函数模板min()的特化。
  char* min(char* a, int* a) {
    // code.
  }

  ```

### 模板的应用

STL是基于模板实现的C++标准库。
