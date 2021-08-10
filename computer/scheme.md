## [scheme](http://www.scheme-reports.org/)

- 一种函数式编程语言， Lisp 两种主要方言之一（另一种为Common Lisp）,诞生于1975年的MIT
- 不同于Common Lisp，Scheme 遵循极简主义哲学，以一个小型语言核心作为标准，加上各种强力语言工具（语法糖）来扩展语言本身
- 不同实现之间的差异成为了它的一个劣势
- 哲学：设计计算机语言不应该进行功能的堆砌，而应该尽可能减少弱点和限制，使剩下的功能显得必要。
- 第一个使用静态作用域的Lisp方言，也是第一个引入“干净宏”和第一类续延的编程语言。
- 特色
  - 词法定界（Lexical Scoping）
  - 动态类型（Dynamic Typing）
  - 良好的可扩展性
  - 尾递归（Tail Recursive）
  - 函数可以作为值返回
  - 支持一流的计算连续
  - 传值调用（passing-by-value）
  - 算术运算相对独立
- Scheme语言的语法规则的第5次修正稿，1998年制定，即Scheme语言的现行标准，目前大多数Scheme语言的实现都将达到或遵循此标准，并且几乎都加入了一些属于自己的扩展特色

## 实现

- [MIT/GNU Scheme](http://www.gnu.org/software/mit-scheme/) is available for Intel-architecture (x86) machines running GNU/Linux, FreeBSD, IBM OS/2 or Microsoft Windows 9x/ME/NT/2000/XP.
  - MIT为SICP（计算机程序的构造与解释）课程开发的Scheme环境。
  - 基本上就是一个精简的Emacs编辑器加上Scheme语言解释器，所以对Emacs不熟悉的人用起来比 较困难。
  - [Scheme](https://groups.csail.mit.edu/mac/projects/scheme/)
- [Guile](https://www.gnu.org/software/guile/):an implementation of the Scheme programming language, supporting the Revised5 and most of the Revised6 language reports, as well as many SRFIs. It also comes with a library of modules that offer additional features, like an HTTP server and client, XML parsing, and object-oriented programming.
  - [GNU Guile 3.0.7 Reference Manual](https://www.gnu.org/software/guile/manual/)
- [ChezScheme](https://github.com/cisco/ChezScheme)
  - `sudo apt install uuid-dev ncurses-dev`
- [racket](https://racket-lang.org/)
- [GNU CLisp](http://clisp.cons.org/) 一个Common Lisp的解释器，不带IDE。Common Lisp也是Lisp语系的一大方言，很多人认为Common Lisp才是Lisp的“正统”。

```sh
# Guile
sudo apt install guile-3.0

## mit-scheme
sudo apt install mit-scheme
# Open an interactive shell (REPL):
scheme
## 编译源码
(cf "add")
## 运行编译好的程序
(load "add")

# Run a scheme program (with no REPL output):
scheme --quiet < script.scm

# Load a scheme program into the REPL:
scheme --load script.scm

# Load scheme expressions into the REPL:
scheme --eval "(define foo 'x)"

# Open the REPL in quiet mode:
scheme --quiet

wget https://mirror.racket-lang.org/installers/7.3/racket-7.3-x86_64-linux.sh
bash racket-7.3-x86_64-linux.sh

racket
```

## 开发环境

- vscode
  - 安装 vscode-scheme  Code Runner
  - settings.json->code-runner.executorMapByFileExtension ->".scm": "scheme <"
- Emacs
	- [ParEdit mode](http://mumble.net/~campbell/emacs/paredit.el) 插件

## 语法

- 注释
  - 单行注释，以分号[;]开始一直到行尾结束
  - 多行注释：标准的Scheme语言定义中没有，Guile中 以符号组合"#!"开始，以相反的另一符号组合"!#"结束
- 块(form)是Scheme语言中的最小程序单元，一个Scheme语言程序是由一个或多个form构成。没有特殊说明的情况下 form 都由小括号括起来
  - 允许form的嵌套

### 结构

- 原子诸如数，字符串，布尔值，变量，空表这类简单数据。
	- 对非变量的原子求值，得到原子自身
	- 对变量求值，得到变量绑定的值
- 表达式形式只有一种：列表
	- 一对括号包含起来的就是列表
	- 表里元素用空格分开
	- 列表可以嵌套。这样的表达式在Lisp里叫做S-表达式，意思是符号表达式
- S-表达式的实质是用抽象句法树(AST)表达程序，直接省去了解析这道工序
	- 程序就是句法树
	- 程序即数据，数据即程序
	- 无论是编译时还是运行时，都可以修改，注入，加载，或者生成新的程序
- (car  ‘(1 2 3 4))
	- 函数car接收一个列表参数，并返回这个参数的第一个值，也就是1。注意例子里的参数(1 2 3 4)前有一单引号。这是因为Scheme总是把一个普通列表当作表达式计算。加上单引号相当于告诉Scheme，不要对(1 2 3 4)估值，把它当成数据对待。如果不加这个单引号，Scheme会执行(1 2 3 4)。执行的规则是把该列表的第一个元素当成函数来调用。而第一个元素是1，不是函数，Scheme会抛出错误。
- (cdr ‘(1 2 3 4)) 调用函数cdr（读作kuder）。函数cdr也是把一个列表作为参数，并返回这个列表除去第一个元素后的子表。所以对(cdr ‘(1 2 3 4))求值，就得到(2 3 4)。 

### 变量

- 定义 `(define 变量名 值)`
- `(set! 变量名 值)`
- 变量和过程绑定
  - 全局变量都用define来定义，并放在过程代码的外部
  - 局部变量则用let等绑定到过程内部使用 `(lcet ((…)…) …)`
  - letrec帮助局部过程实现递归的操作，这不仅在letrec绑定的过程内，而且还包括所有初始化的东西
- apply  为数据赋予某一操作过程，第一个参数必需是一个过程，随后的其它参数必需是列表
- map  第一个参数也必需是一个过程，随后的参数必需是多个列表，返回的结果是此过程来操作列表后的值
- eval，delay，for-each，force，call-with-current-continuation

```scheme
(letrec ((even?
        (lambda(x)
        (if (= x 0)
            (odd? (- x 1)))))
    (odd?
        (lambda(x)
        (if (= x 0) #f
                (even? (- x 1))))))
(even? 88))

(apply + (list 2 3 4))
(map car '((a . b)(c . d)(e . f)))
```

### 数据类型

#### 简单数据类型

- 逻辑型(boolean) `#t` `#f`
  - 只有一种操作：not 只要not后面的参数不是逻辑型，其返回值均为#f
- 数字型(number)
  - 二进制的 ` #b1010  `
  - 八进制的 `#o567`
  - 十进制的123或`  #d123 `
  - 十六进制的 `#x1afc`
  - 复数型(complex) 定义 (define c 3+2i)
  - 实数型（real）定义 (define f 22/7)
  - 有理数型（rational）定义 (define p 3.1415)
  - 整数型(integer)  定义 (define i 123)
- 字符型(char):以符号组合 "#" 开始，表示单个字符，可以是字母、数字或"`[ ! $ % & * + - . / : %lt; = > ? @ ^ _ ~ ]`"等等其它字符
- 符号型(symbol):可以是单词，用括号括起来的多个单词，也可以是无意义的字母组合或符号组合，它在某种意义上可以理解为C中的枚举类型
  - 单引号' 与quote是等价的
  - 不同的是符号类型不能象字符串那样可以取得长度或改变其中某一成员字符的值，但二者之间可以互相转换

#### 复合数据类型

###### 字符串 string

- 由多个字符组成的数据类型,由双引号括起的内容

###### 点对(pair)

- 由一个点和被它分隔开的两个所值组成的。形如： (1 . 2) 或 (a . b)，注意的是点的两边有空格 `(define p (cons 4 5))   => (4 . 5)`
  - 一个点对包含两个指针，每个指针指向一个值
  - 用函数cons构造点对。比如说(cons 1 2)就构造出点对(1 . 2)。因为点对总是由函数cons构造，点对又叫做cons cell
  - 点对左边的值用函数car取出来，右边的值可以由函数cdr取出来
  - 如果一个点对右边不是一个值，而是一个指针，指向另外一个列表，我们就得到了列表

###### 列表(list)

- 由多个相同或不同的数据连续组成的数据类型  `(define la (list 1 2 3 4 ))`
- list是pair的子类型，list一定是一个pair，而pair不是list
- cadr，cdddr等过程是专门对PAIR型数据再复合形成的数据操作的过程，最多可以支持在中间加四位a或d
- 矩阵表达
- 树也可以用列表直观表达：(A B C (D (F H) G) E)

###### 向量（vector）

一种元素按整数来索引的对象，异源的数据结构，在占用空间上比同样元素的列表要少 `(define v (vector 1 2 3 4 5))`

### 操作符

- 类型判断:`(boolean? #t)`
- 比较:(= 34 34)
  - equal?则是判断两个对象是否具有相同的结构并且结构中的内容是否相同
  - eq?是判断两个参数是否指向同一个对象
- 算术
  - `(- 4)`
  - `(max 8 89 90 213)`
- 转换:`(symbol->string 'better)`

### 控制

- 顺序结构:用begin来将多个form放在一对小括号内，最终形成一个form
- if结构: (if 测试 过程1 过程2)
- cond结构 (cond ((测试) 操作) … (else 操作))
- case结构 (case (表达式) ((值) 操作)) ... (else 操作)))
  - 值可以是复合类型数据
- and结构与逻辑与运算操作类似，and后可以有多个参数，只有它后面的参数的表达式的值都为#t时，它的返回值才为#t，否则为#f
- or结构与逻辑或运算操作类似，or后可以有多个参数，只要其中有一个参数的表达式值为#t，其结果就为#t，只有全为#f时其结果才为#f
- 循环:可以用递归来很轻松的实现
- 递归

```scheme
(define  factoral (lambda (x)
    (if (<= x 1) 1
        (* x (factoral (- x 1))))))

(define (factoral n)
    (define (iter product counter)
        (if (> counter n)
            product
            (iter (* counter product) (+ counter 1))))
    (iter 1 1))
(display (factoral 4))

(define loop
    (lambda(x y)
    (if (<= x y)
        (begin (display x) (display #\\space) (set! x (+ x 1))
            (loop x y)))))
```

### 输入输出

- 用到端口概念，相当于C中的文件指针，也就是Linux中的设备文件
- 查看：`(current-input-port)` `(current-output-port)`
- 判断是否为空：`input-port?` `output-port?`
- 打开：`open-input-file`，`open-output-file`  参数是文件名字符串
- 关闭：`close-input-port`，`close-output-port` 参数是打开的端口
- 输入
  - 打开一个输入文件后，返回的是输入端口，可以用read过程来输入文件的内容 `(define name (read))`
- 输出
  - display
  - `(write "hello\\nworld" port1)`

#### 过程 Procedure

- 相当于C语言中函数，不同的是Scheme语言过程是一种数据类型
- 操作符lambda后第一个子列表是参数列表，而第二个子列表是函数定义
- 定义匿名函数 `(lambda (x) (* 2 x))`
- 用define绑定函数名 `(define add5 (lambda (x) (+ x 5)))` `(add5 11)`
	- `(define 1+ (lambda (x) (+ 1 x)))` 定义递加函数，并把它绑定到函数名1+上
	- Scheme对函数名没有限制。对所有函数名一视同仁
	- 规范里定义的函数没有特殊地位，完全可以用自己的函数定义取代
- Scheme提供一条捷径，省去lambda
	- `(define (same? x y)`             
	- `(not (or (> x y) (< x y)))` 

## 函数编程

- 用一系列函数应用实现程序
- 每个函数接受参数，计算后返回结果。计算过程中没有副作用，不改变任何变量的状态
- 函数本身是一等公民，可以作为数据传入另外的函数，也可以作为结果被其它函数返回
- Scheme提供许多方便的工具把这些函数黏合起来。这种高度支持模块化编程的能力绝对让人惊叹

## 工具

## 图书

- [The Scheme Programming Language](https://www.scheme.com/tspl4/)
- The Little Schemer
- The Seasoned Schemer

## 参考

- [Schemers.org](http://www.schemers.org) is a collection of resources for the Scheme programming language.
