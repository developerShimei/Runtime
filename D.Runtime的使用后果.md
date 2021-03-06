# Runtime 开发的后果

[上一篇: Runtime的表现](https://github.com/Magic-Unique/Runtime/blob/master/C.Runtime的表现.md)

[下一篇: Runtime的实践(一)](https://github.com/Magic-Unique/Runtime/blob/master/E.1.Runtime的实践(一).md)

## Objective-C允许我们基于C语言的面向对象开发

在前面的篇幅介绍了类在C语言中的表现，我们写的类最终都会变成一个结构体，我们写的对象最终也是一个结构体。并且 Runtime 也允许我们去`读取`和`修改`这些结构体。

这一决定让很多问题变得很简单。

> 比如有两个人开发，你的小伙伴是主要开发者，而你就是帮他写工具类。后来你们发现，`UIAlertController`在低版本的iOS系统可能会出现闪退，但是你们的项目已经在各个地方都用到了`UIAlertController`，你们觉得一个一个找到他们再做版本适配是一个大工程。

> 此时，你就可以利用 Runtime 去写版本适配代码，把相关方法都做一下修改(这些方法都是苹果写好的，你要修改就只能继承，但是Runtime不需要你继承就可以直接修改)，然后导入到工程中，所有的代码均做了适配。

在你使用 Runtime 的时候，你必须要知道 Runtime 是处于什么位置。

Runtime的一边是面向过程的C语言，另一边是面向对象的Objective-C。你通过C语言去做面向对象开发。也就是说

**你绕过了OC，去做了面向对象开发**

OC是一个成熟的面向对象语言，它拥有一个面向对象语言应有的机制和保护，保证你写的代码在面向对象层是正确的(这里是指你写的方法绝对不会变成另一个类的方法，而不是你写的bug)。

一旦你**绕过了OC，利用Runtime做面向对象开发**，那么你写的代码就不受一个成熟的面向对象的语言所**保护**，很有可能出现面向对象层的运行错误。

## 乱用 Runtime 很有可能破坏面向对象机制

好吧，Runtime就是这么强大，Runtime就是这么可怕。

最终类的结构体是可以进行数据的读写的。也就是说允许你在程序运行的时候动态改变一个类的信息。

> 当程序运行到某一个点时，我们可以给一个类添加一个方法
> 比如这个点是 8:00，添加的方法名叫做`newMethod`，在 8:00 前调用`newMethod`会程序崩溃，但 8:00 后调用`newMethod`就不会崩溃。

比如你把一个类的实例方法换到了另一个类上，然后去调用它，编译时并不会报错。但运行时错误就会出现。

你在改造 OC，OC是一个成熟的语言，甚至比你还要老，你去改造它。

如果你技术成熟，改造可以让 OC 更能配合你开发。

如果你技术不成熟，改造的后果无法预测。

[上一篇: Runtime的表现](https://github.com/Magic-Unique/Runtime/blob/master/C.Runtime的表现.md)

[下一篇: Runtime的实践(一)](https://github.com/Magic-Unique/Runtime/blob/master/E.1.Runtime的实践(一).md)