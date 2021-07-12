当创建一个类时，您不需要重新编写新的数据成员和成员函数，只需指定新建的类继承了一个已有的类的成员即可。这个已有的类称为基类，新建的类称为派生类。

```c++
// 基类
class Animal {

}

// 派生类
class Dog: public Animal {

}
```

一个类可以派生自多个类，这意味着它可以从多个基类继承数据和函数。定义一个派生类，使用一个类派生列表来指定基类，类派生列表以一个或多个基类命名

```c++
class derived_class: public/protected/private base_class {
    
}
```

例：

```c++
#include <iostream>

using namespace std;

// 基类
class Shape 
{
  public:
    void setWidth(int w)
    {
      width = w;
    }
    void setHeight(int h)
    {
      height = h;
    }
  protected:
    int width;
    int height;
};

// 派生类
class Rectangle: public Shape
{
  public:
    int getArea()
    {
      return (width * height)
    }
};

int main(void)
{
  Rectangle Rect;
  Rect.setWidth(5);
  Rect.setHeight(7);

  // 输出对象的面积
  cout << "Total area: " << Rect.getArea() << endl;

  return 0;
}
```

# 访问控制和继承

派生类可以访问基类中所有非私有成员，因此基类成员如果不想被派生类的成员函数访问，则应在基类中声明为private。

|访问|public|protected|private|
|---|---|---|---|
|同一个类|yes|yes|yes|
|派生类|yes|yes|no|
|外部的类|yes|no|no|

一个派生类继承了所有的基类方法，但下列情况除外：
- 基类的构造函数、析构函数和拷贝构造函数
- 基类的重载运算符
- 基类的友元函数

