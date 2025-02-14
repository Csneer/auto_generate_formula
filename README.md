## Project：自动生成小学四则运算题目

> 简要介绍见下方

### **实现一个自动生成小学四则运算题目的命令行程序**

* 使用 -n 参数控制生成题目的个数，例如：
  `Myapp.exe -n 10` 将生成10个题目。
* 使用 -r 参数控制题目中数值（自然数、真分数和真分数分母）的范围，例如：
  `Myapp.exe -r 10` 将生成10以内（不包括10）的四则运算题目。

该参数可以设置为1或其他自然数。该参数必须给定，否则程序报错并给出帮助信息。

* 生成的题目中计算过程不能产生负数，也就是说算术表达式中如果存在形如$e_1 − e_2$的子表达式，那么 $e_1 ≥ e_2$ 。
* 生成的题目中如果存在形如$e_1 ÷ e_2$的子表达式，那么 ****其结果应是真分数**** 。
* ****每道题目中出现的运算符个数不超过3个。****
* 程序一次运行生成的题目不能重复， ****即任何两道题目不能通过有限次交换+和×左右的算术表达式变换为同一道题目**** 。例如，23 + 45 = 和45 + 23 = 是重复的题目，6 × 8 = 和8 × 6 = 也是重复的题目。****3+(2+1)和1+2+3这两个题目是重复的，由于+是左结合的，1+2+3等价于(1+2)+3，也就是3+(1+2)，也就是3+(2+1)。但是1+2+3和3+2+1是不重复的两道题，因为1+2+3等价于(1+2)+3，而3+2+1等价于(3+2)+1，它们之间不能通过有限次交换变成同一个题目。****

> 生成的题目存入执行程序的当前目录下的Exercises.txt文件，格式如下：
>
> 1. 四则运算题目1
> 2. 四则运算题目2
>    ……

其中真分数在输入输出时采用如下格式，真分数五分之三表示为3/5，真分数二又八分之三表示为2'3/8。

* 在生成题目的同时，计算出所有题目的答案，并存入执行程序的当前目录下的 `Answers.txt`文件，格式如下：
  1.答案1
  2.答案2

特别的，真分数的运算如下例所示：1/6 + 1/8 = 7/24。

* 程序应能支持一万道题目的生成。
* 程序支持对给定的题目文件和答案文件，判定答案中的对错并进行数量统计，输入参数如下：

  `Myapp.exe -e <exercisefile>.txt -a <answerfile>.txt`

  统计结果输出到文件Grade.txt，格式如下：

  Correct: 5 (1, 3, 5, 7, 9)

  Wrong: 5 (2, 4, 6, 8, 10)

其中“:”后面的数字5表示对/错的题目的数量，括号内的是对/错题目的编号。为简单起见，假设输入的题目都是按照顺序编号的符合规范的题目。

### 项目介绍

主程序文件  `main.py`，算式生成与答案文件 `generator.py `，判定题目与答案生成文件 ` validator.py`

命令行运行命令：

`python main.py -n 30 -r 100`

`python main.py -e Exercises.txt -a Answers.txt`
