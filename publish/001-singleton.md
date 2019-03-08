# Flutter 中的单例模式

单例模式是日常开发中最常用的设计模式之一，在工作中各种 Manager 和 SharedInstance 层出不穷。本文就分享一下单例在 Flutter 中的使用。

## 实现方法

首先我们先看一下，在 Flutter 中如何实现一个单例。

```dart
class SomeSharedInstance {
  // 单例公开访问点
  factory SomeSharedInstance() =>_sharedInstance()
  
  // 静态私有成员，没有初始化
  static SomeSharedInstance _instance;
  
  // 私有构造函数
  SomeSharedInstance._() {
    // 具体初始化代码
  }

  // 静态、同步、私有访问点
  static SomeSharedInstance _sharedInstance() {
    if (_instance == null) {
      _instance = SomeSharedInstance._();
    }
    return _instance;
  }
}
```

如上所示，我们首先定义了一个类 `SomeSharedInstance`，在业务中我们通过定义 `SomeSharedInstance()` 方法返回一个对单例的懒加载：如果不存在则初始化，如果存在则返回。因为 `Dart` 是一个单线程的语言，所以其调用是线程安全的，这意味着我们全局有且仅有一个 `_instance`。

## 知识点

### 懒汉模式 vs 饿汉模式

**懒汉模式**
在类加载时，不创建实例。加载时速度较快，运行时获取实例速度较慢。
上面的例子就是懒汉模式，它适用于绝大多数的场景。

**饿汉模式**
在类加载时，直接进行实例的创建。加载时获取实例速度较慢，运行时速度较快。对上面的代码做一个小的改动即可。

```dart
class SomeSharedInstance {
  // 单例公开访问点
  factory SomeSharedInstance() =>_sharedInstance()
  
  // 静态私有成员，没有初始化
  static SomeSharedInstance _instance = SomeSharedInstance._();
  
  // 私有构造函数
  SomeSharedInstance._() {
    // 具体初始化代码
  }

  // 静态、同步、私有访问点
  static SomeSharedInstance _sharedInstance() {
    return _instance;
  }
}
```

### 单例使用场景

- 需要频繁实例化然后销毁的对象。
- 创建对象时耗时过多或者耗资源过多，但又经常用到的对象。
- 有状态的工具类对象。
- 频繁访问数据库或文件的对象。

### 单例的风险

- 由于单例模式中没有抽象的层，因此扩展单例类是一件非常困难的事情。
- 滥用会带来很多负面问题：比如占用运行时资源，导致内存过限引发回收机制；长时间不使用可能会被错误的回收，导致状态丢失等。