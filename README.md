# BeijingUniversityOfPostsAndTelecommunicationsMaster-PhdThesisTemplate

**警告：本项目非官方实现，出现问题概不负责。**

本项目转载自[Overleaf模板](https://www.overleaf.com/latex/templates/beijing-university-of-posts-and-telecommunications-master-slash-phd-thesis-template/dkpkvpsvvhpg)

[Overleaf实现链接](https://www.overleaf.com/read/ftxnytqpspvq)

## 关于

在本项目之前有多个为北邮研究生学位设计的LaTeX文档类，经过张煜博士（Dazzle Zhang）和王贤凌博士（rioxwang）的努力，[BUPTGraduateThesis](https://github.com/rioxwang/BUPTGraduateThesis)的功能已经相当完善。
但是，之前的项目也存在很多问题。
首先，由于之前的项目启动时间较早，原文档类使用了很多较为古老的方式来实现功能，而这些方法已经逐渐被新的方案所代替。
其次，原文档类使用了很多LaTeX的底层命令，再加上注释的缺乏，其代码的可读性较差。这使得项目后期维护困难，也使得让更多人参与进来的的门槛较高。
针对这些问题，本项目采用了一些新的方法来重新实现北邮研究生学位论文。
其中最主要的就是本项目不再直接调用xeCJK，而是通过ctex的定制化功能来实现。由于字体选择、中文格式设定等功能大多直接由ctex完成。在代码量大幅减少的同时，本项目几乎可以实现在Windows、MacOS上的开箱即用。Linux系统上也只需按照ctex的常规方式配置字体即可。
除此之外，对于页眉页脚、目录、引文等部分的调整也都采用相应的包来实现，从而尽可能的避免使用底层命令，提高代码的可读性。

## 使用说明

### 编译

由于本项目采用一些较新的工具来实现功能，对于老版本的LaTeX系统可能存在兼容性问题，建议使用最新的TexLive或者MikTex来进行编译。

虽然ctex可以自行适应编译引擎，但还是推荐使用XeLaTeX引擎来进行编译。为了实现引用、编号等功能，可使用以下命令进行编译。（在MikTex下使用`latexmk`可能需要单独安装一个[Perl](http://strawberryperl.com/)）
```
latexmk -pdfxe -synctex=1 %DOC%
```

### 选项

- `txmath` 默认采用cm数学字体，可使用该选项启用Times字体的数学部分。
- `review` 用以自动在扉页上隐藏个人信息。
- `chapterbib` 默认将引文列在正文的末尾，可使用该选项将采用文献列在各章的末尾。

## 已知问题

### 扉页 

研究生院给的扉页样例上却采用了粗宋体（伪粗体），但本文档类绘制的扉页并没有采用粗体字。这是因为Windows上其实并没有粗宋体字形，ctex使用黑体来代替粗宋体。不过《关于研究生学位论文格式的统一要求》上并没有明确指出对粗宋体的使用，我想应该问题不大。实在不放心的话可以自行用Word绘制中英文扉页和声明，然后导出成`cover.pdf`放在本项目的根目录。本文档类在发现`cover.pdf`之后便不会自行绘制相应的内容而是直接将`cover.pdf`贴在文档的最前面。
另外，如果`cover.pdf`和`cover.tex`都没有找到，文档类会直接放弃绘制扉页。

### 数学字体

~~不知是我系统的问题还是`newtx`包存在问题，我这里调用`newtxmath`之后就有部分数学符号无法使用。现在暂时采用LaTeX默认的cm数学字体。不过不管用什么数学字体，LaTeX的数学排版肯定比Word强。另外本文档类提供一个`txmath`选项来开启`newtxmath`的调用。~~

发现问题我的系统里少一个叫`boondox`的字体包，手动安装之后便可以正常编译`newtxmath`了。
如果有遇到相似问题的可以尝试一下。

### 引文格式

虽然《关于研究生学位论文格式的统一要求》里面没有明确说明，但是格式要求是基本符合[国家标准](https://zh.wikipedia.org/wiki/%E6%96%87%E5%90%8E%E5%8F%82%E8%80%83%E6%96%87%E7%8C%AE%E8%91%97%E5%BD%95%E8%A7%84%E5%88%99)的。
所以本项目采用[biblatex-gb7714-2015](https://www.ctan.org/pkg/biblatex-gb7714-2015)来处理引文格式。
但由于该包没有在以前的文档类中使用过，并不清楚学校对该包的接受度如何。

### 注脚

`BUPTGraduateThesis`文档类使用了给很大的篇幅来实现带圈数字的注脚，但我在《关于研究生学位论文格式的统一要求》并没有看到相应的要求。另外我觉得注脚并不是什么很有必要的功能，本项目放弃对带圈数字的实现。


### 自动缩略语

`BUPTGraduateThesis`中实现了非常强大的自动缩略语功能，但是我在移植过程中发现自动缩略语所依赖`glossaries`包似乎跟`biblatex`冲突。由于时间紧迫，未能查明具体原因。暂时放弃实现相应的功能，现在只能手动管理缩略语了。

### 功能缺乏

由于本项目几乎完全重写，功能实现其实远没有`BUPTGraduateThesis`项目那么完整。暂时需要大家自行修改代码来实现硕士、博士后论文，涉密论文所需的调整。如果日后有时间我会尽量完善相关的功能。

## 致谢

感谢张煜博士和王贤凌博士的贡献。虽然本文档类几乎完全重写，但很多地方还是参考了`BUPTGraduateThesis`项目。

另外一些实现细节也参考了[SJTUThesis](https://github.com/sjtug/SJTUThesis)的实现，在此也对[相关人员](https://github.com/sjtug/SJTUThesis/graphs/contributors)表示感谢。

