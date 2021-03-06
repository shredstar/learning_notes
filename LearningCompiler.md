# 自己动手构建编译系统：编译汇编与链接

## 2 编译系统设计

### 2.1 编译程序的设计
编译器的结构：

源文件 => 词法分析（词法记号） => 语法分析（语法模块） => 语义分析(语义动作） => 代码生成（汇编代码） => 汇编文件

#### 2.1.1 词法分析
源代码 => **词法分析（词法记号）** => 语法分析

为了能识别出不同形式的词法记号，引入有限自动机的概念。有多种有限自动机：识别常量的有限自动机；识别标识符的有限自动机。

> 有限自动机从开始状态启动，读入一个字符作为输入，并根据该字符选择进入下一个状态。 继续读入新的字符，直到遇到结束状态为止，读入的所有字符序列便是有限自动机识别的词法记号。

词法分析器的输入是文本字符串，输出是线性词法记号序列。

#### 2.1.2 语法分析
语法分析器的输入是词法记号序列，输出是一种树形结构，通常称之为抽象语法树。
在抽象语法树中：
- 终结符 = 词法记号 = 叶子节点
- 非终结符 = 语法模块 = 抽象语法子树

在语法分析器工作前，首先要有文法（高级语言的形式化表示）。文法定义了源代码的书写规则，同时也是语法分析器构建抽象语法树的规则。
- 文法分析算法：
	- 自顶向下：LL(1)分析，递归下降子程序是其便捷实现方式。
	- 自底向上：算符优先分析、LR分析
- 递归下降子程序的基本原则：
	- > 将产生式左侧的非终结符转化为函数定义，将产生式右侧的非终结符转化为函数调用，将终结符转化为词法记号匹配。
	- 例子：
		```var2 = var1 + 100;```
		对应的递归下降子程序是：
		```
		void 赋值语句()
		{
			match(标识符);
			match(等号);
			表达式();
			match(分号);
		}
		```
	- 在实际语法分析器实现中，不一定要显示的构造抽象语法树。利用递归下降子程序实现的语法分析器，将语法分析合入了子程序的构造和执行，实现了在语法分析子程序中直接进行后续的工作，如语法分析和代码生成。

#### 2.1.3 符号表管理





## Resource
[source code](https://github.com/fanzhidongyzby/cit)