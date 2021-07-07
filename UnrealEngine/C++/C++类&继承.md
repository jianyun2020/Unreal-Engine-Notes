# C++类成员函数

成员函数定义在类内部：

```c++
class Box {
   public:
      double length;
      double breadth;
      double height;
      
      // 内联函数
      double getVolume(void)
      {
         return length * breadth * height;
      }
};
```

或者单独使用**范围解析运算符::**来定义。

```c++
double Box::getVloume(void)
{
   return length * breadth * height;
}
```