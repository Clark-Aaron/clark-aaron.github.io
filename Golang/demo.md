# Golang的数据结构

[//]: # (__author__ = "Wenger Binning")
[//]: # (__version__ = "v0.0")

<!--http://www.topgoer.com/-->

## 数据类型

Golang的数据类型分为值类型与引用类型，值类型即直接存储数据值的类型，而引用类型是存储指向真实变量的首地址的类型；其中值类型有数值类型、字符类型、布尔类型与数组，引用类型有指针、结构体、函数、切片、接口、映射、通道。

### 数值类型

* `int`与`uint`：根据计算机平台不同，等同于int32与uint32或int64与uint64。
* `int8`与`uint8`：
* `int16`与`uint16`：
* `int32`与`uint32`：
* `int64`与`uint64`：
* `float32`与`float64`：
* `complex64`与`complex128`：
* `uintptr`：

#### 进制

* 进制标识
* 进制转换

### 字符类型

* `byte`：byte类型是用于存储ASCII编码的字符。
* `rune`：rune类型是用于存储UTF-8编码的字符。
* `string`：在Golang中，使用UTF-8作为字符串的默认编码方式，并以`"`标识字符串，并可以在字符串中嵌入转义字符；若想定义字符段，则需使用`\``来标识，不能使用转义字符，字符串底层是由byte类型的数组实现。

#### 转义字符

* `\r`：回车符
* `\n`：换行符
* `\t`：制表符
* `\'`：单引号
* `\"`：双引号
* `\`: 反斜杠

#### 字符串的应用

* 修改：将string转化为byte或rune类型数组，修改后转换位string，但是这并不是在原有的内容中修改，而是重新分配内存。

### 布尔类型

布尔类型只有`true`与`flase`两个值，且在Golang中，不允许将整型转化为buer类型。

### 指针

在Golang中，指针不能进行偏移和运算，属于安全指针。

* 指针地址
* 指针类型
* 指针取值

#### 指针的声明

* 一般声明

  ```go
  var <ptrName> *<type>
  ```

#### 内存分配

在指针声明之后，需要为指针分配地址。

* `new()`分配内存。
  
  ```go
  <ptrName> = new(<type>)
  ```

* `make()`只用于切片、映射、通道的内存创建,返回为本省。
  
  ```go
  <varName> = make（<type>,<size>）
  ```

#### 特殊指针

* 空指针：`nil`
* 数组指针


### 数组


数组即一种具有固定长度的序列。


* 数组的声明


  ```go
  // 一维数组
  var <arrayName> [<elementCount>]<type>
  // 多维数组
  var <arrayName> [<elementCount_1>][<elementCount_2>]<type>
  ```

* 数组的初始化

  
  ```go
  var <arrayName> = [<elementCount>]<type>{<elementValue_1>,<elementName_2>,...}
  var <arrayName> [<elementCount>]<type> = [<elementCount>]<type>{<elementValue_1>,<elementName_2>,...}
  var arr2 = [...]int{1, 2, 3, 4, 5, 6}
  var str = [5]string{3: "hello world", 4: "tom"}
  ```

#### 特殊的数组

* 指针数组：其元素为指针的数组。

### 切片

切片是通过内部指针和相关属性引用数组片段来实现变长方案,操作的实际上是底层数组；内部实现的数据结构是通过指针引用底层数组，本身只是一个只读对象，类似于数组指针的议长封装。

* 切片的定义：
  
  ```go 
  var <sliceName> []<type>
  ```

* `make()`动态创建切片

  ```go
  var <sliceName> []<type> = make([]<type>,<elementCount>,<Cap>)
  ```

  > Note：当切片的元素超出底层数组容量时，会自动分配一个底层数组，与原数组无任何关系。


### 结构体

结构体是为我们自定义数据类型的类型，使用`struct`标识。

* 结构体的定义：

  ```go
  type <typeName> struct {
  	<elementName_1> <elementType_1>
	<elementName_2> <elementType_2>
  }
  ```

  > Note: type <newType> <type> 是用来定义一个新的类型，newType的特性于type的特性相同，以上写法属于type于struct语法的结合。

* 结构体的实例化：

  ```go
  var <varName> <type>
  ```

### 接口

### 映射

map是一种无序的基于键值对的数据结构，必须初始化才能使用,底层仍为数组，将键经过hash后，对长度取余的值作为存储该键值的索引。

> Note: 对于hash冲突时，采用开放地址法解决。

* map的声明

  ```go
  map[<keyType>]<valueType>
  ```

### 通道

## 变量

变量是用于存储数据的内存空间，由变量名与变量值组成，变量值的类型必须是Golang中合法的数据类型。

### 变量的声明

在Golang中声明的变量必须使用，否在会抛出变量未使用的错误；而且在同一作用域内不允许重复声明。

* 变量的标准声明：

  ```go
  var <varName> <type>
  // 多个同类型变量的声明
  var <varName_1>, <varName_2> <type>
  // 多个不同类型变量的声明，一般用于全局变量的声明
  var (
	<varName_1> <type_1>
	<varName_2> <type_2>
  )
  ```

  > Note: 在Golang中，一般varName通常以小驼峰命名规则，type为数据类型；一般数值类型默认初始化为0，字符串默认初始化为空字符串，布尔类型默认初始化为flase，引用类型默认初始化为nil。

### 变量的初始化

* 变量的标准初始化：在函数声明时，会使用默认的值来初始化变量，如果则需要指定初始化值。
  
  ```go
  var <varName> <type> = <initialValue>
  ```

* 类型推导初始化：

  ```go
  var <varName> = <value>
  // 多个类型自动推断的声明
  var <varName_1>, <varName_2> = <value_1>, <value_2>
  ```

* `:=`声明变量并初始化

  ```go
  <varName> := <value>
  // 多个变量自动声明
  <varName_1>, <varName_2> := <value_1>, <value_2>
  ```

  > Note: 在Golang中，使用:=赋值符号可以声明变量并为之赋值，但是该符号的左侧必须存在至少一个未声明的变量,且一般只在函数内部使用。

### 变量的使用

* 变量的交换：

  ```go
  var varA, VarB int = 1, 2
  // 交换varA与varB的值
  varA, varB = varB, varA
  ```

  > Note: 该方法必须是同一类型时才能操作。


### 特殊变量

在编程中需要使用一些特殊变量来实现某些功能，这些变量有`_`、常量。


#### 空白标识符`_`

`_`是一个只写变量，常用于抛弃函数的返回值。

##### 空白标识符的应用

* `_`在import中的使用：只执行导入包的init（），，不做其他操作。

  
  ```go
  import _ <packageName>
  ```

* `_`在返回值中的使用：弃用多返回值的函数中的某一返回值。

#### 常量

常量是一种变量值恒定的变量，必须在声明时初始化，且常量的数据类型必须是值类型。

##### 常量的定义

常量的定义使用`const`来修饰。

* 常量的显式定义：

  
  ```go
  const <constName> <type>
  ```

* 常量的隐式定义：

  ```go
  const <constName> = <value>
  // 多个常量的定义
  const <constName_1>, <constName_2> = <value_1>,<value_2>
  ```

##### 常量的使用

* 枚举：

  ```go
  const (
 	MONDAY = 1
	TUESDAY = 2
	WEDNESDAY = 3
	THURSDAY = 4
	FRIDAY = 5
	SATURDAY = 6
	SUNDAY = 7
  )
  ```

  > Note: 可以使用`len()`获取变量的长度，`unsafe.Sizeof()`获取变量的内存大小。

#### iota

 `iota`：iota在const使用时初始化为0，之后没增加一行常量的定义，其值自动加一


## 类型转换

在Golang中只有强制类型转换。

```go
<type>(<value>)
```


## 运算符

在Golang中存在算数运算符、关系运算符、逻辑运算符、位运算符、赋值运算符等其他运算符。

### 算数运算符

* `*`：乘法运算,
* `/`：除法运算，
* `%`：取余运算，
* `+`：加法运算，
* `-`：减法运算，
* `++`：自增运算，
* `--`：自减运算，

### 关系运算符

* `==`与`!=`：等于与不等于
* `>`与`<=`：大于与不大于
* `<`与`>=`：小于与不小于


### 逻辑运算符

* `&&`：逻辑与
* `||`：逻辑或
* `!`：逻辑非

### 位运算符

* `&`：按位与
* `|`：按位或
* `^`：按位异或
* `<<`：左移
* `>>`：右移

### 赋值运算符

* `=`：赋值
* `*=`：先乘法再赋值
* `/=`：先除法再赋值
* `%=`：先取余再赋值
* `+=`：先加法再赋值
* `-=`：先减法再赋值
* `&=`：先位与再赋值
* `|=`：先位或再赋值
* `^=`：先异或再赋值
* `<<=`：先左移再赋值
* `>>=`：先右移再赋值

### 地址运算符

* `*`：取地址内容
* `&`：取变量地址
