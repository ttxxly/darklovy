Python 是一种解释型、面向对象、动态数据类型的高级程序设计语言。

Python 由 Guido Van Rossum 于1989年底发明，第一个公开发行版本发行于1991年。

Python是纯粹的自由软件， 源代码和解释器CPython遵循 GPL(GNU General Public License)协议。Python语法简洁清晰，特色之一是强制用空白符(white space)作为语句缩进。

Python具有丰富和强大的库。它常被昵称为胶水语言，能够把用其他语言制作的各种模块（尤其是C/C++）很轻松地联结在一起。常见的一种应用情形是，使用Python快速生成程序的原型（有时甚至是程序的最终界面），然后对其中有特别要求的部分，用更合适的语言改写，比如3D游戏中的图形渲染模块，性能要求特别高，就可以用C/C++重写，而后封装为Python可以调用的扩展类库。需要注意的是在您使用扩展类库时可能需要考虑平台问题，某些可能不提供跨平台的实现。

### 优点

**简单**：Python是一种代表简单主义思想的语言。阅读一个良好的Python程序就感觉像是在读英语一样。它使你能够专注于解决问题而不是去搞明白语言本身。

**易学**：Python极其容易上手，因为Python有极其简单的说明文档 [7]  。

**速度快：**Python 的底层是用 C 语言写的，很多标准库和第三方库也都是用 C 写的，运行速度非常快。 [5]  

**免费、开源**：Python是[FLOSS](https://baike.baidu.com/item/FLOSS)（自由/[开放源码](https://baike.baidu.com/item/%E5%BC%80%E6%94%BE%E6%BA%90%E7%A0%81)软件）之一。使用者可以自由地发布这个软件的拷贝、阅读它的[源代码](https://baike.baidu.com/item/%E6%BA%90%E4%BB%A3%E7%A0%81)、对它做改动、把它的一部分用于新的自由软件中。FLOSS是基于一个团体分享知识的概念。

**高层语言**：用Python语言编写程序的时候无需考虑诸如如何管理你的程序使用的内存一类的底层细节。

**可移植性**：由于它的开源本质，Python已经被移植在许多平台上（经过改动使它能够工作在不同平台上）。这些平台包括Linux、Windows、FreeBSD、Macintosh、Solaris、OS/2、Amiga、AROS、AS/400、BeOS、OS/390、z/OS、Palm  OS、QNX、VMS、Psion、Acom RISC OS、VxWorks、PlayStation、Sharp Zaurus、Windows  CE、PocketPC、Symbian以及Google基于linux开发的android平台。

**解释性**：一个用编译性语言比如C或C++写的程序可以从[源文件](https://baike.baidu.com/item/%E6%BA%90%E6%96%87%E4%BB%B6)（即C或C++语言）转换到一个你的计算机使用的语言（[二进制代码](https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6%E4%BB%A3%E7%A0%81)，即0和1）。这个过程通过[编译器](https://baike.baidu.com/item/%E7%BC%96%E8%AF%91%E5%99%A8)和不同的标记、选项完成。

运行程序的时候，连接/转载器软件把你的程序从硬盘复制到内存中并且运行。而Python语言写的程序不需要编译成二进制代码。你可以直接从[源代码](https://baike.baidu.com/item/%E6%BA%90%E4%BB%A3%E7%A0%81)运行 程序。

在计算机内部，Python[解释器](https://baike.baidu.com/item/%E8%A7%A3%E9%87%8A%E5%99%A8)把源代码转换成称为[字节码](https://baike.baidu.com/item/%E5%AD%97%E8%8A%82%E7%A0%81)的中间形式，然后再把它翻译成计算机使用的[机器语言](https://baike.baidu.com/item/%E6%9C%BA%E5%99%A8%E8%AF%AD%E8%A8%80)并运行。这使得使用Python更加简单。也使得Python程序更加易于移植。

[**面向对象**](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)：Python既支持[面向过程](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E8%BF%87%E7%A8%8B)的编程也支持面向对象的编程。在“面向过程”的语言中，程序是由过程或仅仅是可重用代码的函数构建起来的。在“[面向对象](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)”的语言中，程序是由数据和功能组合而成的对象构建起来的。

**可扩展性**：如果需要一段关键代码运行得更快或者希望某些算法不公开，可以部分程序用C或C++编写，然后在Python程序中使用它们。

**可嵌入性**：可以把Python嵌入C/C++程序，从而向程序用户提供脚本功能。

**丰富的库**：Python标准库确实很庞大。它可以帮助处理各种工作，包括[正则表达式](https://baike.baidu.com/item/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)、文档生成、[单元测试](https://baike.baidu.com/item/%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)、[线程](https://baike.baidu.com/item/%E7%BA%BF%E7%A8%8B)、数据库、网页浏览器、CGI、FTP、电子邮件、XML、XML-RPC、HTML、WAV文件、密码系统、GUI（[图形用户界面](https://baike.baidu.com/item/%E5%9B%BE%E5%BD%A2%E7%94%A8%E6%88%B7%E7%95%8C%E9%9D%A2)）、Tk和其他与系统有关的操作。这被称作Python的“功能齐全”理念。除了标准库以外，还有许多其他高质量的库，如wxPython、Twisted和Python图像库等等。

规范的代码：Python采用强制缩进的方式使得代码具有较好可读性。而Python语言写的程序不需要编译成二进制代码。

​     

### 缺点

**单行语句和命令行输出问题**：很多时候不能将程序连写成一行，如import sys;for i in sys.path:print i。而perl和awk就无此限制，可以较为方便的在shell下完成简单程序，不需要如Python一样，必须将程序写入一个.py文件。

**独特的语法**

这也许不应该被称为局限，但是它用缩进来区分语句关系的方式还是给很多初学者带来了困惑。即便是很有经验的Python程序员，也可能陷入陷阱当中。

**运行速度慢**：这里是指与C和C++相比。