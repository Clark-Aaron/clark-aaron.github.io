# C++流程结构

[//]: # (__author__ = "Clark Aaron")

在C++的流程结构中，默认使用顺序结构；除此之外，还有有分支结构、循环结构，以及在流程机构中所需要的控制语句。顺序结构是按照从上至下、从左至右的顺序依次执行。

## 分支结构

分支结构有if语句、switch语句。

### if

if语句用于根据布尔值执行不同的程序。

* 单分支结构：

  ```c++
  if <bool> {
    <true code>;
  }
  ```

* 二分支结构：

  ```c++
  if <bool> {
    <true code>;
  } else {
    <false code>;
  }
  ```

* 多分支结构：

  ```c++
  if <bool> {
    <true code>;
  }
  else if <bool> {
    <true code>;
  } else {
    <false code>;
  }
  ```

### switch

switch语句根据对象的不同值来执行不同程序。

* switch选择：

  ```c++
  switch <object> {
    case <value_1>:
      <case code>;
      break;
    case <value_2>:
      <case code>
      break;
    default:
      <default code>;
  }
  ```

* 多重选择语句：

  ```c++
  switch <object> {
    case <value_1>:
      <case code>;
    case <value_2>:
      <case code>
    default:
      <default code>;
  }
  ```

## 循环结构

循环结构中有for语句、while语句。

### for

* 有限循环：

  ```c++
  for(<initialization expression>;<condition expression>;<step expression>) {
    <loop code>;
  }
  ```

* 无限循环：

  ```c++
  for(;;) {
    <loop code>;
  }
  ```

* 序列遍历：

  ```c++
  for (<statement>:<squence>) {
      <loop code>;
  }
  ```

### while

while用于条件循环语句，

* 当型循环：

  ```c++
  while (<condition expression>) {
    <loop code>;
  }
  ```

* 直到型循环：

  ```c++
  do {
    <loop code>;
  } while (<condition expression>)
  ```

## 控制语句

### break

### continue

### return
