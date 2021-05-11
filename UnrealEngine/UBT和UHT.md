# 简介

UBT(Unreal Build Tool)

UHT(Unreal Header Tool)

UE4代码不是标准的C++代码，是基于UE4源码层层封装了的，所以UHT将UE4代码转化成标准的C++代码，UBT负责调用UHT来实现这个转化工作，转化完成后，UBT调用标准C++代码的编译器来将UHT转化后的标准C++代码完全编译成二进制文件。从整体上看，UHT是UBT编译流程的一部分。