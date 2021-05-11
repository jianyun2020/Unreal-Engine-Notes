# 简介

UBT(Unreal Build Tool)

UHT(Unreal Header Tool)

UE4代码不是标准的C++代码，是基于UE4源码层层封装了的，所以UHT将UE4代码转化成标准的C++代码，UBT负责调用UHT来实现这个转化工作，转化完成后，UBT调用标准C++代码的编译器来将UHT转化后的标准C++代码完全编译成二进制文件。从整体上看，UHT是UBT编译流程的一部分。

# UBT

## 目标(Targets)

虚幻编译工具支持数个目标类型的编译：

- 游戏(Game)：需要烘培数据才能运行的standalone游戏。
- 客户端(Client)：和游戏一样，但不包含任何服务器代码；适用于联网游戏。
- 服务器(Server)：和游戏一样，但不包含任何客户端代码。适用于联网游戏中的专用服务器(Dedicated Servers)。
- 编辑器(Editor)：扩展虚幻编辑器的目标。
- 程序(Program)：基于虚幻引擎的独立实用程序。

目标是通过C#源文件声明的，扩展名为`.target.cs`，并存储在项目的 *Source* 目录下。每个`.target.cs`文件都声明一个类，从`TargetRules`基类衍生而来，并设置属性来控制如何从其构造函数进行编译。当要求编译目标时，虚幻编译工具将编译`target.cs`文件，并在其中构造类来确定其设置。

类的名称必须与在其中声明这个类的文件的名称相匹配，后跟"Target"（例如，MyProject.target.cs定义类"MyProjectTarget"）。

目标文件的典型结构如下：

```c++
using UnrealBuildTool;
using System.Collections.Generic;
public class MyProjectTarget :TargetRules
{
  public MyProjectTarget(TargetInfo Target) : base(Target)
  {
    Type = TargetType.Game;
    // 此处为其他属性
  }
}
```

[官方详细文档](https://docs.unrealengine.com/zh-CN/ProductionPipelines/BuildTools/UnrealBuildTool/TargetFiles/index.html)

## 模块(Modules)

模块是UE4的构建块。引擎是以大量模块的集合形式实现的，游戏提供自己的模块来扩充自己。每个模块都封装了一组功能，并且可以提供公共接口和编译环境（包括宏、路径等）供其他模块使用。

模块是通过C#源文件声明的，扩展名为`.build.cs`，存储在项目的 *源（Source）* 目录下。属于一个模块的C++源代码与`.build.cs`文件并列存储，或者存储在它的子目录中。每个`.build.cs`文件都声明一个类，从`ModuleRules`基类衍生而来，并设置属性来控制如何从其构造函数进行构建。这些`.build.cs`文件都由UnrealBuildTool编译，并被构造来确定整个编译环境。

`.build.cs`文件的典型结构如下。

```c++
using UnrealBuildTool;
using System.Collections.Generic;
public class MyModule : ModuleRules
{
  public MyModule(ReadOnlyTargetRules Target) : base(Target)
  {
    // Settings go here
  }
}
```

[官方详细文档](https://docs.unrealengine.com/zh-CN/ProductionPipelines/BuildTools/UnrealBuildTool/ModuleFiles/index.html)

## 编译配置(BuildConfiguration)

## IWYU