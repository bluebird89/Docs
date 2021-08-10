## [重学前端](https://time.geekbang.org/column/intro/154) 程劭非（winter）

- 知识体系和底层原理没有真正系统地理解。
- 做了管理，技术没跟上，并且还错过了最佳的学习时间，这个境遇可想而知，他们在工作中大概率只能是被动地接受需求解决问题，然后也同时焦虑着自己的未来，焦虑着自己的竞争力。
- 前端工程师成长需要两个视角
  - 一是立足标准，系统性总结和整理前端知识，建立自己的认知和方法论；
  - 二是放眼团队，从业务和工程角度思考前端团队的价值和发展需要。
- 除了前端自身的领域知识和工程特点外，你还需要了解程序员通用的编程能力和架构能力。
- 需要通过系统地学习和总结获取知识，通过练习获取编程能力，通过工作经验来获取架构和工程能力。
- 建立自己的知识体系，根据你自己的理解把前端的领域知识链接起来，形成结构，这样做，不但能帮助你记忆知识，还能在其中发现自己知识的缺失，甚至可以凭借知识体系来判断知识的重要性，来决定是否要深入学习。
- 问题
  - 前端的基础知识欠缺
  - 技术上存在短板，就会导致前端开发者的上升通道不甚顺畅。特别是一些小公司的程序员，只能靠自己摸索，这样就很容易陷入重复性劳动的陷阱，最终耽误自己的职业发展。
  - 面临技术发展问题带来的挑战。
- 缺少系统教育 + 技术快速革新，在这样的大环境下，前端工程师保持自学能力就显得尤其重要了。
- 目标
  - 摸索出适合自己的前端学习方法；
  - 帮助建立起前端技术的知识架构；
  - 理解前端技术背后的核心思想。
- 建立知识架构
  - 能够帮助把零散的知识组织起来，也能够帮助发现一些知识上的盲区。
  - 对于任何计算机语言来说，必定是“用规定的文法，去表达特定语义，最终操作运行时的”一个过程。在顶层和大结构上，逐层向下细分，知识框架就初见端倪，通过逻辑来保持完备性。
  - 学习过程，实际上就是知识架构不断进化的过程，通过知识架构的自然延伸，可以更轻松地记忆一些原本难以记住的点，还可以发现被忽视的知识盲点。
- 追本溯源
  - 有一些知识，背后有一个很大的体系
  - 些知识，涉及的概念本身经历了各种变迁，变得非常复杂和有争议性
  - 追本溯源，其实就是关注技术提出的背景，关注原始的论文或者文章，关注作者说的话。

![[../_static/frontend_knowledge_struct.png]]

## JavaScript

- 从文法和运行时的角度去讨论 JavaScript 语言。它们是互相关联的，而语义就是文法到运行时之间的桥梁；它们分别又是完备的，任何语言特性都离不开两者，所以从语法和运行时的角度，都可以了解完整的 JavaScript。
- 编译原理基础 [[../computer/compiler#四则运算实例]]

### 文法

- 编译原理中对语言的写法的一种规定

#### 词法

- 规定了语言的最小语义单元：token，可以翻译成“标记”或者“词”
- 从字符到词的整个过程是没有结构的，只要符合词的规则，就构成词，一般来说，词法设计不会包含冲突。词法分析技术上可以使用状态机或者正则表达式来进行
- 源代码中的输入 分类
	- WhiteSpace 空白字符,JavaScript 可以支持更多空白符号
		- `<HT>`(或称`<TAB>`) 是 U+0009，是缩进 TAB 符，也就是字符串中写的 \t 
		- `<VT>`是 U+000B，也就是垂直方向的 TAB 符 \v，这个字符在键盘上很难打出来，所以很少用到。
		- `<FF>`是 U+000C，Form Feed，分页符，字符串直接量中写作 \f ，现代已经很少有打印源程序的事情发生了，所以这个字符在 JavaScript 源代码中很少用到
		- `<SP>`是 U+0020，就是最普通的空格了
		- `<NBSP>`是 U+00A0，非断行空格，它是 SP 的一个变体，在文字排版中，可以避免因为空格在此处发生断行，其它方面和普通空格完全一样。多数的 JavaScript 编辑环境都会把它当做普通空格（因为一般源代码编辑环境根本就不会自动折行……）。HTML 中，很多人喜欢用的 &nbsp; 最后生成的就是它了
		- `<ZWNBSP>`(旧称`<BOM>`) 是 U+FEFF，这是 ES5 新加入的空白符，是 Unicode 中的零宽非断行空格，在以 UTF 格式编码的文件中，常常在文件首插入一个额外的 U+FEFF，解析 UTF 文件的程序可以根据 U+FEFF 的表示方法猜测文件采用哪种 UTF 编码方式。这个字符也叫做“bit order mark”。
	- LineTerminator 换行符
		- `<LF>`是 U+000A，就是最正常换行符，在字符串中的\n。
		- `<CR>`是 U+000D，这个字符真正意义上的“回车”，在字符串中是\r，在一部分 Windows 风格文本编辑器中，换行是两个字符\r\n。
		- `<LS>`是 U+2028，是 Unicode 中的行分隔符。
		- `<PS>`是 U+2029，是 Unicode 中的段落分隔符。
		- 被词法分析器扫描出之后，会被语法分析器丢弃，但是换行符会影响 JavaScript 的两个重要语法特性：自动插入分号和“no line terminator”规则
	- Comment 注释
		- 分为单行注释和多行注释两种
		- 多行注释中允许自由地出现MultiLineNotAsteriskChar，也就是除了`*`之外的所有字符。而每一个`*`之后，不能出现正斜杠符/。
		- 除了四种 LineTerminator 之外，所有字符都可以作为单行注释。
		- 注意 多行注释中是否包含换行符号，会对 JavaScript 语法产生影响，对于“no line terminator”规则来说，带换行的多行注释与换行符是等效的。
	- Token 词
		- IdentifierName 标识符名称，典型案例是使用的变量名
			- 可以以美元符`$`、下划线 `_`或者 Unicode 字母开始，除了开始字符以外，IdentifierName中还可以使用 Unicode 中的连接标记、数字、以及连接符号
			- IdentifierName的任意字符可以使用 JavaScript 的 Unicode 转义写法，使用 Unicode 转义写法时，没有任何字符限制
			- IdentifierName可以是Identifier、NullLiteral、BooleanLiteral或者keyword，在ObjectLiteral中，IdentifierName还可以被直接当做属性名称使用
			- 仅当不是保留字的时候，IdentifierName会被解析为Identifier
			- 注意`<ZWNJ>`和`<ZWJ>`是 ES5 新加入的两个格式控制字符，它们都是 0 宽的。
			- 关键字也包含在内
			- 1 个为了未来使用而保留的关键字 enum
			- 在严格模式下, 有一些额外的为未来使用而保留的关键字 `implements package protected interface private public`
			- NullLiteral（null）和BooleanLiteral（true false）也是保留字，不能用于Identifier
		- Punctuator 符号，使用的运算符和大括号等符号
			- 除法和正则问题, / 和 /= 两个运算符被拆分为 DivPunctuator
			- 字符串模板问题，}也被独立拆分
			- `{ ( ) [ ] . ... ; , < > <= >= == != === !== + - * % ** ++ -- << >> >>> & | ^ ! ~ && || ? : = += -= *= %= **= <<= >>= >>>= &= |= ^= => / /= }`
		- NumericLiteral 数字直接量，就是我们写的数字
			- 十进制 Number 可以带小数，小数点前后部分都可以省略，但是不能同时省略
				- `12.toString()` `12. `被当作省略小数点后面部分的数字，而单独看成一个整体，要想让点单独成为一个 token，就要加入空格
				- 支持科学计数法 e 后面的部分，只允许使用整数
			- 以0x 0b 或者0o 开头时，表示特定进制的整数,不支持小数，也不支持科学计数法
		- StringLiteral 字符串直接量，用单引号或者双引号引起来的直接量
			- 双引号区别仅仅在于写法，在双引号字符串直接量中，双引号必须转义，在单引号字符串直接量中，单引号必须转义。字符串中其他必须转义的字符是\和所有换行符
			- 转义形式
				- 单字符转义  即一个反斜杠\后面跟一个字符这种形式
					- 有特别意义的字符包括有SingleEscapeCharacter所定义的 9 种
					- 除了这 9 种字符、数字、x 和 u 以及所有的换行符之外，其它字符经过\转义后都是自身
		- 正则表达式直接量 RegularExpressionLiteral
			- 由 Body 和 Flags 组成
			-  Body 部分至少有一个字符，第一个字符不能是 `*`（因为 /* 跟多行注释有词法冲突）
			-  并非机械地见到/就停止，在正则表达式[ ]中的/就会被认为是普通字符 `/[/]/.test("/");`
			-  除了\、/ 和`[`三个字符之外，JavaScript 正则表达式中的字符都是普通字符
		- Template 字符串模板，用反引号\` 括起来的直接量
			- 在 JavaScript 词法中，包含 ${ } 的 Template，是被拆开分析的 ``
			- 支持添加处理函数的写法，模板各段会被拆开，传递给函数当参数
			- 不需要关心大多数字符的转义，但是至少 ${ 和 \` 还是需要处理的
- 特别之处
	- 除法和正则表达式冲突问题 
		- JavaScript 不但支持除法运算符“ / ”和“ /= ”，还支持用斜杠括起来的正则表达式“ /abc/ ”
		- 对词法分析来说，其实是没有办法处理的，JavaScript 解决方案是定义两组词法，然后靠语法分析传一个标志给词法分析器，让它来决定使用哪一套词法
	- 字符串模板
		-  ${ }  内部可以放任何 JavaScript 表达式代码，这些代码是以“ } ” 结尾的，也就是说，这部分词法不允许出现“ } ”运算符
	-  是否允许“ } ”的两种情况，与除法和正则表达式的两种情况相乘就是四种词法定义，所以在 JavaScript 标准中，可以看到四种定义
		-  InputElementDiv
		-  InputElementRegExp
		-  InputElementRegExpOrTemplateTail
		-  InputElementTemplateTail
	-  为了解决这两个问题，标准中还不得不把除法、正则表达式直接量和“ } ”从 token 中单独抽出来，用词上，也把原本的 Token 改为 CommonToken。
-  对一般的语言的词法分析过程来说，都会丢弃除了 token 之外的输入，但是对 JavaScript 来说，不太一样，换行符和注释还会影响语法分析过程(将会在语法部分给详细讲解).所以要实现 JavaScript 的解释器，词法分析和语法分析非常麻烦，需要来回传递信息
-  零宽空格和零宽连接符、零宽非连接符
	-  零宽空格（zero-width space, ZWSP）用于可能需要换行处。 Unicode: U+200B HTML: &#8203;
	-  零宽不连字 (zero-width non-joiner，ZWNJ)放在电子文本的两个字符之间，抑制本来会发生的连字，而是以这两个字符原本的字形来绘制 Unicode: U+200C HTML: &#8204;
	-  零宽连字（zero-width joiner，ZWJ）是一个控制字符，放在某些需要复杂排版语言（如阿拉伯语、印地语）的两个字符之间，使得这两个本不会发生连字的字符产生了连字效果。 Unicode: U+200D HTML: &#8205;
	-  左至右符号（Left-to-right mark，LRM）是一种控制字符，用于计算机的双向文稿排版中。Unicode: U+200E HTML: &lrm; &#x200E; 或&#8206;
	-  右至左符号（Right-to-left mark，RLM）是一种控制字符，用于计算机的双向文稿排版中。Unicode: U+200F HTML: &rlm; &#x200F; 或&#8207;
	-  字节顺序标记（byte-order mark，BOM）常被用来当做标示文件是以UTF-8、UTF-16或UTF-32编码的标记  Unicode: U+FEFF

![[../_static/WhiteSpace_code.png]]
![[../_static/SingleEscapeCharacter.png|特别意义的字符]]

```js
`a${b}c${d}e`

`a${ // 模板头
b 
}c${ // 被称为模板中段
d
}e` // 模板尾

function f(){    
	console.log(arguments);
}
var a = "world"
f`Hello ${a}!`; // [["Hello", "!"], world]
```

#### 语法

##### 到底要不要写分号呢？

- 行尾使用分号的风格来自于 Java，也来自于 C 语言和 C++，这一设计最初是为了降低编译器的工作负担。
- 从今天的角度来看，行尾使用分号其实是一种语法噪音，恰好 JavaScript 语言又提供了相对可用的分号自动补全规则，所以，很多 JavaScript 的程序员都是倾向于不写分号。
- 自动插入分号规则 独立于所有的语法产生式定义
	- 有换行符，且下一个符号是不符合语法的，那么就尝试插入分号
	- 有换行符，且语法中规定此处不能有换行符，那么就自动插入分号
		-  JavaScript 标准定义中有`[no LineTerminator here]`字样，这是一个语法定义中的规则
		- a 的后面就要插入一个分号了。所以这段代码最终的结果，b 和 c 都变成了 2，而 a 还是 1
	- 源代码结束处，不能形成完整的脚本或者模块结构，那么就自动插入分号
		- 两个 IIFE,第三行结束的位置，JavaScript 引擎会认为函数返回的可能是个函数，那么，在后面再跟括号形成函数调用就是合理的，因此这里不会自动插入分号。
		- 一些鼓励不写分号的编码风格会要求大家写 IIFE 时必须在行首加分号的原因
		- 带换行符的注释也被认为是有换行符，而恰好的是，return 也有[no LineTerminator here]规则的要求

```js
var a = 1, b = 1, c = 1;
a
++
b
++
c

;(function(a){    
	console.log(a);
})()
;(function(a){    
	console.log(a);
})()

function f(){    
	return/*        
		This is a return value.    
	*/1;
}
f(); //undefined
```

### 语义

### 运行时

#### 类型

- 代码实际执行过程中用到的类型。所有的类型数据都会属于 7 个类型之一。
- 从变量、参数、返回值到表达式中间结果，任何 JavaScript 代码运行过程中产生的数据，都具有运行时类型。
- 除了这七种语言类型，还有一些语言的实现者更关心的规范类型
  - List 和 Record： 用于描述函数传参过程
  - Set：主要用于解释字符集等
  - Completion Record：用于描述异常、跳出等语句执行过程
  - Reference：用于描述对象属性访问、delete 等
  - Property Descriptor：用于描述对象的属性
  - Lexical Environment 和 Environment Record：用于描述变量和作用域
  - Data Block：用于描述二进制数据
- typeof 的运算结果，与运行时类型的规定有很多不一致的地方
  - typeof 的设计是有缺陷的

![[../_static/js_typeof_rs.png]]

##### Undefined

- Undefined 类型表示未定义，只有一个值，就是 undefined。
- 为什么有的编程规范要求用 void 0 代替 undefined？
  - 任何变量在赋值前是 Undefined 类型、值为 undefined，一般可以用全局变量 undefined（就是名为 undefined 的这个变量）来表达这个值，或者 void 运算来把任意一个表达式变成 undefined 值。
  - 因为 JavaScript 的代码 undefined 是一个变量，而并非是一个关键字，这是 JavaScript 语言公认的设计失误之一，所以，为了避免无意中被篡改，我建议使用 void 0 来获取 undefined 值。
- 跟 Null 有一定的表意差别，Null 表示的是：“定义了但是为空”。所以，在实际编程时，一般不会把变量赋值为 undefined，这样可以保证所有值为 undefined 的变量，都是从未赋值的自然状态

##### Null

- 只有一个值，就是 null，它的语义表示空值，与 undefined 不同，null 是 JavaScript 关键字，所以在任何代码中，都可以放心用 null 关键字来获取 null 值。

##### Boolean

- 有两个值， true 和 false，用于表示逻辑意义上的真和假，同样有关键字 true 和 false 来表示两个值。

##### String

- 用于表示文本数据。有最大长度是 2^53 - 1
- 有趣的是，这个所谓最大长度，并不完全是理解中的字符数。
- String 的意义并非“字符串”，而是字符串的 UTF16 编码，字符串的操作 charAt、charCodeAt、length 等方法针对的都是 UTF16 编码。所以，字符串的最大长度，实际上是受字符串的编码长度影响的。
- 字符串是永远无法变更的，一旦字符串构造出来，无法用任何方式改变字符串的内容，所以字符串具有值类型的特征。
- JavaScript 字符串把每个 UTF16 单元当作一个字符来处理，所以处理非 BMP（超出 U+0000 - U+FFFF 范围）的字符时，应该格外小心。
- 这个设计继承自 Java，最新标准中是这样解释的，这样设计是为了“性能和尽可能实现起来简单”。因为现实中很少用到 BMP 之外的字符。

##### Number

- 表示通常意义上的“数字”。这个数字大致对应数学中的有理数，在计算机中有一定的精度限制。
- 有 18437736874454810627(即 2^64-2^53+3) 个值
- 基本符合 IEEE 754-2008 规定的双精度浮点数规则，但是 JavaScript 为了表达几个额外的语言场景
  - NaN，占用了 9007199254740990，这原本是符合 IEEE 规则的数字
  - Infinity，无穷大
  - -Infinity，负无穷大。
- 有 +0 和 -0，在加法类运算中没有区别，
  - 除法的场合则需要特别留意区分，“忘记检测除以 -0，而得到负无穷大”的情况经常会导致错误
  - 区分 +0 和 -0 的方式，正是检测 1/x 是 Infinity 还是 -Infinity。
- 根据双精度浮点数的定义，Number 类型中有效的整数范围是 -0x1fffffffffffff 至 0x1fffffffffffff，所以 Number 无法精确表示此范围外的整数。
- 根据浮点数定义，非整数 Number 类型无法用 `==（===` 也不行） 来比较
  - `console.log( 0.1 + 0.2 == 0.3);` 输出结果 false，说明两边不相等的，这是浮点运算的特点，也是很多同学疑惑的来源，浮点数运算的精度问题导致等式左右的结果并不是严格相等，而是相差了个微小的值。
  - 这里错误的不是结论，而是比较的方法，正确的比较方法是使用 JavaScript 提供的最小精度值 `console.log( Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON);`

##### Symbol

- ES6 中引入的新类型，是一切非字符串对象 key 的集合，在 ES6 规范中，整个对象系统被用 Symbol 重塑。
- 具有字符串类型的描述，但是即使描述相同，Symbol 也不相等。
- 用 Symbol.iterator 来自定义 for…of 在对象上的行为
- 全局的 Symbol 函数无法使用 new 来调用

```js
var mySymbol = Symbol("my symbol");

var o = new Object
o[Symbol.iterator] = function() {
	var v = 0
	return {
		next: function() {
			return { value: v++, done: v > 10 }
		}
	}        
};
for(var v of o) 
	console.log(v); // 0 1 2 3 ... 9
```

##### Object

- 在 JavaScript 中，对象定义 “属性的集合”。
- 属性分为数据属性和访问器属性，二者都是 key-value 结构，key 可以是字符串或者 Symbol 类型。
- JavaScript 中的“类”仅仅是运行时对象的一个私有属性，而 JavaScript 中是无法自定义类型的
- 为什么给对象添加的方法能用在基本类型上？
  - 几个基本类型，在对象类型中有一个“亲戚 Number String Boolean Symbol
  - 3 与 new Number(3) 是完全不同的值，一个是 Number 类型， 一个是对象类型。
  - Number、String 和 Boolean，三个构造器是两用的，当跟 new 搭配时，产生对象，当直接调用时，它们表示强制类型转换
  - Symbol 函数比较特殊，直接用 new 调用它会抛出错误，但它仍然是 Symbol 对象的构造器。
  - JavaScript 语言设计上试图模糊对象和基本类型之间的关系，日常代码可以把对象方法在基本类型上使用
  - 甚至在原型上添加方法，应用于基本类型
  - 运算符提供了装箱操作，会根据基础类型构造一个临时对象，使得能在基础类型上调用对应对象的方法。

##### 类型转换

- StringToNumber
  - 存在语法结构，支持十进制、二进制、八进制和十六进制
  - 还包括正负号科学计数法，可以使用大写或者小写的 e 来表示
  - parseInt 和 parseFloat 并不使用这个转换，所以支持的语法跟这里不尽相同。
    - 在不传入第二个参数的情况下，parseInt 只支持 16 进制前缀“0x”，而且会忽略非数字字符，也不支持科学计数法。
    - 在一些古老浏览器环境中，parseInt 还支持 0 开头的数字作为 8 进制前缀，这是很多错误的来源。
    - 在任何环境下，建议传入 parseInt 第二个参数，而 parseFloat 则直接把原字符串作为十进制来解析，它不会引入任何的其他进制。
  - 多数情况下，Number 是比 parseInt 和 parseFloat 更好的选择。
- NumberToString
  - 在较小的范围内，数字到字符串的转换是完全符合你直觉的十进制表示。
  - 当 Number 绝对值较大或者较小时，字符串表示则是使用科学计数法表示的。
- 装箱转换
  - 把基本类型转换为对应对象
  - 全局 Symbol 函数无法使用 new 来调用，可以利用装箱机制来得到一个 Symbol 对象，利用函数 call 方法来强迫产生装箱。
  - 会频繁产生临时对象，在一些对性能要求较高的场景下，应该尽量避免对基本类型做装箱转换。
  - 每一类装箱对象皆有私有的 Class 属性，这些属性可以用 Object.prototype.toString 获取
  - 在 JavaScript 中，没有任何方法可以更改私有的 Class 属性，因此 Object.prototype.toString 是可以准确识别对象对应的基本类型的方法，它比 instanceof 更加准确。
  - call 本身会产生装箱操作，所以需要配合 typeof 来区分基本类型还是对象类型。
- 拆箱转换
  - 在 JavaScript 标准中，规定了 ToPrimitive 函数，它是对象类型到基本类型的转换（即，拆箱转换）
  - 对象到 String 和 Number 的转换都遵循“先拆箱再转换”的规则。通过拆箱转换，把对象变成基本类型，再从基本类型转换为对应的 String 或者 Number。
  - 会尝试调用 valueOf 和 toString 来获得拆箱后的基本类型。如果 valueOf 和 toString 都不存在，或者没有返回基本类型，则会产生类型错误 TypeError。
  - 到 String 的拆箱转换会优先调用 toString
  - 在 ES6 之后，允许对象通过显式指定 @@toPrimitive Symbol 来覆盖原有的行为

![[../_static/js_type_transmit.png]]

```js
var symbolObject = (function(){ return this; }).call(Symbol("a"));
console.log(typeof symbolObject); //object
console.log(symbolObject instanceof Symbol); //true
console.log(symbolObject.constructor == Symbol); //true

var symbolObject = Object(Symbol("a"));    
console.log(typeof symbolObject); //object    
console.log(symbolObject instanceof Symbol); //true    
console.log(symbolObject.constructor == Symbol); //true

console.log(Object.prototype.toString.call(symbolObject)); //[object Symbol]

var o = {        
	 valueOf : () => {console.log("valueOf"); return {}},        
	 toString : () => {console.log("toString"); return {}}    
}    
o * 2    // valueOf    // toString    // TypeError
String(o)    // toString    // valueOf    // TypeError

o[Symbol.toPrimitive] = () => {console.log("toPrimitive"); return "hello"}    
console.log(o + "")    // toPrimitive    // hello
```

#### 面向对象还是基于对象？

- 基于对象定义 语言和宿主基础设施由对象来提供，并且 JavaScript 程序即是一系列互相通讯的对象集合
- 对象并不是计算机领域凭空造出来的概念，它是顺着人类思维模式产生的一种抽象（于是面向对象编程也被认为是：更接近人类思维模式的一种编程范式）。
- 在《面向对象分析与设计》Grady Booch 替我们做了总结，从人类的认知角度来说，对象应该是下列事物之一
  - 一个可以触摸或者可以看见的东西
  - 人的智力可以理解的东西
  - 可以指导思考或行动（进行想象或施加动作）的东西。
- 在不同的编程语言中，设计者也利用各种不同的语言特性来抽象描述对象，最为成功的流派是使用“类”的方式来描述对象，这诞生了诸如 C++、Java 等流行的编程语言。提供了完全运行时的对象系统，这使得它可以模仿多数面向对象编程范式，所以它也是正统的面向对象语言。
- JavaScript 的对象设计跟目前主流基于类的面向对象差异非常大。 JavaScript 对象的具体设计：具有高度动态性的属性集合。
- JavaScript 早年却选择了一个更为冷门的方式：原型
  - 因为一些公司政治原因，JavaScript 推出之时受管理层之命被要求模仿 Java，所以，JavaScript 创始人 Brendan Eich 在“原型运行时”的基础上引入了 new、this 等语言特性，使之“看起来更像 Java”。
  - 在 ES6 出现之前，大量的 JavaScript 程序员试图在原型体系的基础上，把 JavaScript 变得更像是基于类的编程，进而产生了很多所谓的“框架”，比如 PrototypeJS、Dojo。事实上，它们成为了某种 JavaScript 的古怪方言，甚至产生了一系列互不相容的社群，显然这样做的收益是远远小于损失的。
  - 从运行时角度看，可以不必受到这些“基于类的设施”的困扰，这是因为任何语言运行时类的概念都是被弱化的。
- JavaScript 对象特征
  - 对象具有唯一标识性：即使完全相同的两个对象，也并非同一个对象。用内存地址来体现的， 对象具有唯一标识的内存地址，所以具有唯一的标识。
  - 对象有状态：对象具有状态，同一对象可能处于不同状态之下。
  - 对象具有行为：即对象的状态，可能因为它的行为产生变迁。
- 在 JavaScript 中，将状态和行为统一抽象为“属性”，考虑到 JavaScript 中将函数设计成一种特殊对象，所以 JavaScript 中的行为和状态都能用属性来抽象。
- JavaScript 中对象独有的特色是：对象具有高度的动态性，这是因为 JavaScript 赋予了使用者在运行时为对象添改状态和行为的能力。
- 为了提高抽象能力，JavaScript 属性被设计成比别的语言更加复杂的形式，提供数据属性和访问器属性（getter/setter）两类。用一组特征（attribute）来描述属性（property）。
- 数据属性
  - 特征
    - value 属性值
    - writable 决定属性能否被赋值
    - enumerable 决定 for in 能否枚举该属性
    - configurable 决定该属性能否被删除或者改变特征值
  - 通常用于定义属性的代码会产生数据属性，其中的 writable、enumerable、configurable 都默认为 true。可以使用内置函数 getOwnPropertyDescriptor 来查看
- 访问器（getter/setter）属性
  - 特征
    - getter 函数或 undefined，在取属性值时被调用
    - setter 函数或 undefined，在设置属性值时被调用
    - enumerable 决定 for in 能否枚举该属性
    - configurable 决定该属性能否被删除或者改变特征值
  - 允许使用者在写和读属性时，得到完全不同的值，可以视为一种函数的语法糖
  - 使用 Object.defineProperty 改变属性的特征，或者定义访问器属性
  - 在创建对象时，可以使用 get 和 set 关键字来创建访问器属性
  - 跟数据属性不同，每次访问属性都会执行 getter 或者 setter 函数
- JavaScript 对象的运行时是一个“属性的集合”，属性以字符串或者 Symbol 为 key，以数据属性特征值或者访问器属性特征值为 value
  - 对象是一个属性的索引结构（索引结构是一类常见的数据结构，可以把它理解为一个能够以比较快的速度用 key 来查找 value 的字典）
- 应该在理解其设计思想的基础上充分挖掘它的能力，而不是机械地模仿其它语言。
- 要想理解 JavaScript 对象，必须清空脑子里“基于类的面向对象”相关的知识，回到人类对对象的朴素认知和面向对象的语言无关基础理论，就能够理解 JavaScript 面向对象设计的思路。

```js
var o = {         
	a: 1,        
	f() {            
		console.log(this.a);        
	}        
};
o.b = 2;    
console.log(o.a, o.b); //1 2

//a和b皆为数据属性
Object.getOwnPropertyDescriptor(o,"a") // {value: 1, writable: true, enumerable: true, configurable: true}
Object.getOwnPropertyDescriptor(o,"b") // {value: 2, writable: true, enumerable: true, configurable: true}

Object.defineProperty(o, "b", {value: 2, writable: false, enumerable: false, configurable: true});    //a和b都是数据属性，但特征值变化了 
Object.getOwnPropertyDescriptor(o,"a"); // {value: 1, writable: true, enumerable: true, configurable: true}    
Object.getOwnPropertyDescriptor(o,"b"); // {value: 2, writable: false, enumerable: false, configurable: true}    o.b = 3;    console.log(o.b); // 2

var o = { get a() { return 1 } };
```

#### JavaScript对象：真的需要模拟类吗？

- JavaScript 本身就是面向对象的，它并不需要模拟，只是它实现面向对象的方式和主流的流派不太一样，所以才让很多人产生了误会。
- “类”并非面向对象的全部，但不应该责备社区出现这样的方案，事实上，因为一些公司的政治原因，JavaScript 推出之时，管理层就要求它去模仿 Java。所以，JavaScript 创始人 Brendan Eich 在“原型运行时”的基础上引入了 new、this 等语言特性，使之“看起来语法更像 Java”，而 Java 正是基于类的面向对象的代表语言之一。
- 但是 JavaScript 这样的半吊子模拟，缺少了继承等关键特性，导致大家试图对它进行修补，进而产生了种种互不相容的解决方案。
- 从 ES6 开始，JavaScript 提供了 class 关键字来定义类，尽管，这样的方案仍然是基于原型运行时系统的模拟，但是它修正了之前的一些常见的“坑”，统一了社区的方案，这对语言的发展有着非常大的好处。
- 什么是原型？
  - 在不同的编程语言中，设计者也利用各种不同的语言特性来抽象描述对象。
  - 最为成功的流派是使用“类”的方式来描述对象，这诞生了诸如 C++、Java 等流行的编程语言。这个流派叫做基于类的编程语言。
    - 提倡使用一个关注分类和类之间关系开发模型。在这类语言中，总是先有类，再从类去实例化一个对象。
    - 类与类之间又可能会形成继承、组合等关系。类又往往与语言的类型系统整合，形成一定编译时的能力。
  - 还有一种就是基于原型的编程语言，利用原型来描述对象。JavaScript 就是其中代表。
    - 更为提倡程序员去关注一系列对象实例的行为，而后才去关心如何将这些对象，划分到最近的使用方式相似的原型对象，而不是将它们分成类。
    - 通过“复制”的方式来创建新对象。一些语言的实现中，还允许复制一个空对象。这实际上就是创建一个全新的对象。
    - JavaScript 并非第一个使用原型的语言，在它之前，self、kevo 等语言已经开始使用原型来描述对象了。
    - 在 JavaScript 之前，原型系统就更多与高动态性语言配合，并且多数基于原型的语言提倡运行时的原型修改，我想，这应该是 Brendan 选择原型系统很重要的理由。
- 原型系统的“复制操作”两种实现思路
  - 并不真的去复制一个原型对象，而是使得新对象持有一个原型的引用,JavasScript 采用的
  - 切实地复制对象，从此两个对象再无关联。
- JavaScript 的原型
  - 抛开 JavaScript 用于模拟 Java 类的复杂语法设施（如 new、Function Object、函数的 prototype 属性等），原型系统可以说相当简单，可以用两条概括
    - 如果所有对象都有私有字段`[[prototype]]`，就是对象的原型
    - 读一个属性，如果对象本身没有，则会继续访问对象的原型，直到原型为空或者找到为止。
  - 从 ES6 以来，JavaScript 提供了一系列内置函数，以便更为直接地访问操纵原型
    - Object.create 根据指定的原型创建新对象，原型可以是 null
    - Object.getPrototypeOf 获得一个对象的原型
    - Object.setPrototypeOf 设置一个对象的原型。
    - 利用这三个方法，可以完全抛开类的思维，利用原型来实现抽象和复用
- 在 ES3 和之前的版本，JS 中类的概念是相当弱的，它仅仅是运行时的一个字符串属性。“类”的定义是一个私有属性`[[class]]`，语言标准为内置类型诸如 Number、String、Date 等指定了`[[class]]`属性，以表示它们的类。语言使用者唯一可以访问`[[class]]`属性方式 Object.prototype.toString。
- 在 ES5 开始，` [[class]]  `私有属性被 Symbol.toStringTag 代替，Object.prototype.toString 的意义从命名上不再跟 class 相关。甚至可以自定义 Object.prototype.toString 的行为

```js
var cat = {    
	say(){        
		console.log("meow~");    
	},    
	jump(){        
		console.log("jump");    
	}
}
var tiger = Object.create(
	cat,  
	{    
		say:{       
			writable:true,        
			configurable:true,        
			enumerable:true,        
			value:function(){            
				console.log("roar!");        
			}    
		}
	}
)
var anotherCat = Object.create(cat);
anotherCat.say();
var anotherTiger = Object.create(tiger);
anotherTiger.say();

var o = new Object;
var n = new Number;
var s = new String;
var b = new Boolean;
var d = new Date;
var arg = function(){ return arguments }();
var r = new RegExp;
var f = new Function;
var arr = new Array;
var e = new Error;
console.log([o, n, s, b, d, arg, r, f, arr, e].map(v => Object.prototype.toString.call(v))); 

// 用字符串加法触发了 Object.prototype.toString 的调用，发现这个属性最终对 Object.prototype.toString 的结果产生了影响。
var o = { [Symbol.toStringTag]: "MyObject" }    
console.log(o + "");
```

- new 操作具体做的事情
  - 以构造器 prototype 属性（注意与私有字段`[[prototype]]`区分）为原型，创建新对象
  - 将 this 和调用参数传给构造器，执行
  - 如果构造器返回的是对象，则返回，否则返回第一步创建对象
- new 这样的行为，试图让函数对象在语法上跟类变得相似，但是，客观上提供了两种方式
  - 在构造器中修改 this,添加属性
  - 在构造器 prototype 属性指向的对象(从这个构造器构造出来的所有对象的原型),上添加属性
- 通过 new 调用函数，跟直接调用 this 取值有明显区别 仅普通函数和类能够跟 new 搭配使用
- 没有 Object.create、Object.setPrototypeOf 的早期版本中，new 运算是唯一一个可以指定`[[prototype]]`的方法（ mozilla 提供了私有属性 **proto**，但是多数环境并不支持），所以，当时已经有人试图用它来代替后来的 Object.create，
  - 可以用 new 来实现一个 Object.create 的不完整的 polyfill. 无法做到与原生的 Object.create 一致，一个是不支持第二个参数，另一个是不支持 null 作为原型

```js
// 用构造器模拟类
function c1(){
    this.p1 = 1;
    this.p2 = function(){
        console.log(this.p1);
    }
} 
var o1 = new c1;
o1.p2();

function c2(){
}
c2.prototype.p1 = 1;
c2.prototype.p2 = function(){
    console.log(this.p1);
}
var o2 = new c2;
o2.p2();

Object.create = function(prototype){    
	var cls = function(){}    
	cls.prototype = prototype;    
	return new cls;
}
```

- ES6 中的类
  - 加入新特性 class，new 跟 function 搭配的怪异行为终于可以退休了（虽然运行时没有改变），在任何场景，都推荐使用 ES6 的语法来定义类，而令 function 回归原本的函数语义
  - 在标准中删除所有`[[class]]`相关私有属性描述，类的概念正式从属性升级成语言的基础设施
  - 通过 get/set 关键字来创建 getter
  - 通过括号和大括号来创建方法
  - 数据型成员最好写在构造器里面
  - 提供了继承能力
- 在新的 ES 版本中，不再需要模拟类了：有了光明正大的新语法。而原型体系同时作为一种编程范式和运行时机制存在。可以自由选择原型或者类作为代码的抽象风格，但是无论选择哪种，理解运行时的原型系统都是很有必要的一件事。

```js
class Rectangle {  
	constructor(height, width) {    
		this.height = height;    
		this.width = width;  
	}  
	// Getter  
	get area() {    
		return this.calcArea();  
	}  
	// Method  
	calcArea() {    
		return this.height * this.width;  
	}
}

class Animal {   
	constructor(name) {    
		this.name = name;  
	}    
	speak() {    
		console.log(this.name + ' makes a noise.');  
	}
}

class Dog extends Animal {  
	constructor(name) {    
		super(name); // call the super class constructor and pass in the name parameter 
	}  
	speak() {    
		console.log(this.name + ' barks.'); 
	}
}
let d = new Dog('Mitzie');d.speak(); // Mitzie barks.
```

#### JavaScript对象：知道全部的对象分类吗？

- JavaScript 的对象机制并非简单的属性集合 + 原型
	- 不论怎样编写代码，都没法绕开 Array，实现一个跟原生的数组行为一模一样的对象，这是由于原生数组的底层实现了一个自动随着下标变化的 length 属性。
	- 在浏览器环境中，也无法单纯依靠 JavaScript 代码实现 div 对象，只能靠 document.createElement 来创建
- 对象分类
- 宿主对象（host Objects） 由 JavaScript 宿主环境提供的对象，行为完全由宿主环境决定。
	- 宿主对象也分为固有的和用户可创建两种
	- 在浏览器环境中全局对象是 window
		- window 上的属性，一部分来自 JavaScript 语言，一部分来自浏览器环境。
		- JavaScript 标准中规定了全局对象属性，W3C 的各种标准中规定了 Window 对象的其它属性。
	- 宿主会提供一些构造器
- 内置对象（Built-in Objects） 由 JavaScript 语言提供的对象
	- 固有对象（Intrinsic Objects ）由标准规定，随着 JavaScript 运行时创建而自动创建的对象实例。ECMA 标准提供了一份[固有对象表](https://262.ecma-international.org/9.0/#sec-well-known-intrinsic-objects)
	- 原生对象（Native Objects） 可以由用户通过 Array、RegExp 等内置构造器或者特殊语法创建的对象。
		- 能够通过语言本身的构造器创建的对象称作原生对象
		- 通过这些构造器，可以用 new 运算创建新的对象
		- 几乎所有这些构造器的能力都是无法用纯 JavaScript 代码实现的，也无法用 class/extend 语法来继承,这些构造器创建的对象多数使用了私有字段,这些字段使得原型继承方法无法正常工作，可以认为这些原生对象都是为了特定能力或者性能，而设计出来的“特权对象”。
			- Error: `[[ErrorData]]`
			- Boolean: `[[BooleanData]]`
			- Number: `[[NumberData]]`
			- Date: `[[DateValue]]`
			- RegExp: `[[RegExpMatcher]]`
			- Symbol: `[[SymbolData]]`
			- Map:` [[MapData]]`
	- 普通对象（Ordinary Objects） 由{}语法、Object 构造器或者 class 关键字定义类创建的对象，它能够被原型继承。
- 用对象来模拟函数与构造器：函数对象与构造器对象
	- JavaScript 为这类对象预留了私有字段机制，并规定了抽象的函数对象与构造器对象的概念。
	- 函数对象定义 具有`[[call]]`私有字段对象
	- 构造器对象定义 具有私有字段`[[construct]]`对象
	- 用对象模拟函数的设计代替了一般编程语言中的函数，可以像其它语言的函数一样被调用、传参。任何宿主只要提供了“具有`[[call]]`私有字段的对象”，就可以被 JavaScript 函数调用语法支持。
		- `[[call]]`私有字段必须是一个引擎中定义的函数，需要接受 this 值和调用参数，并且会产生域的切换
		- 任何对象只需要实现`[[call]]`，就是一个函数对象，可以去作为函数被调用。
		- 如果能实现`[[construct]]`，就是一个构造器对象，可以作为构造器被调用。
	- 只要字段符合，宿主对象和内置对象（如 Symbol 函数）可以模拟函数和构造器
		- 对于宿主和内置对象来说，实现`[[call]]`（作为函数被调用）和`[[construct]]`（作为构造器被调用）不总是一致的。比如内置对象 Date 在作为构造器调用时产生新的对象，作为函数时，则产生字符串
		- 浏览器宿主环境中，提供的 Image 构造器，则根本不允许被作为函数调用。
		- 基本类型（String、Number、Boolean），它们的构造器被当作函数调用，则产生类型转换的效果。
		- 在 ES6 之后 `=>` 语法创建的函数仅仅是函数，无法被当作构造器使用
	- 用户用 function 关键字创建的函数必定同时是函数和构造器。不过，表现出来的行为效果却并不相同。
		- `[[call]]`和`[[construct]]`行为总是相似的，它们执行同一段代码
	- `[[construct]]`执行过程
		- 以 Object.prototype 为原型创建一个新对象
		- 以新对象为 this，执行函数`[[call]]`
		- 如果`[[call]]`返回值是对象，那么，返回这个对象，否则返回第一步创建的新对象。
	- 这样的规则造成了有趣的现象，如果构造器返回一个新的对象，那么 new 创建的新对象就变成了一个构造函数之外完全无法访问的对象，这一定程度上可以实现“私有”。
- 在固有对象和原生对象中，有一些对象的行为跟正常对象有很大区别。常见的下标运算或者设置原型跟普通对象不同
	- Array：Array 的 length 属性根据最大的下标自动发生变化
	- Object.prototype：作为所有正常对象的默认原型，不能再给它设置原型了
	- String：为了支持下标运算，String 的正整数属性访问会去字符串里查找
	- Arguments：arguments 的非负整数型下标属性跟对应的变量联动
	- 模块 namespace 对象：特殊的地方非常多，跟一般对象完全不一样，尽量只用于 import 吧。类型数组和数组缓冲区：跟内存块相关联，下标运算比较特殊
	- bind 后的 function：跟原来的函数相关联

![[../_static/ecma_native_object.png]]

```js
console.log(new Date); // 1
console.log(Date())

new (a => 0) // error

function f(){    
	return 1;
}
var v = f(); //把f作为函数调用
var o = new f(); //把f作为构造器调用

function cls(){    
	this.a = 100;    
	return {        
		getValue:() => this.a    
	}
}
var o = new cls;
o.getValue(); //100
//a在外面永远无法访问到
```

### 执行过程

#### Promise 里代码为什么比setTimeout先执行？

- 一个 JavaScript 引擎会常驻于内存中，等待（宿主）把 JavaScript 代码或者函数传递给它执行
- ES3 和更早版本中，JavaScript 本身没有异步执行代码能力，意味着，宿主环境传递给 JavaScript 引擎一段代码，引擎就把代码直接顺次执行，这个任务也就是宿主发起的任务
- ES5 之后，JavaScript 引入 Promise，不需要浏览器安排，JavaScript 引擎本身可以发起任务
- 采纳 JSC 引擎术语
	- 宏观任务 宿主发起的任务
	- 微观任务  JavaScript 引擎发起任务
- JavaScript 引擎等待宿主环境分配宏观任务，在操作系统中，通常等待的行为都是一个事件循环，所以在 Node 术语中，也会把这个部分称为事件循环
- 事件循环原理
	- 宏观任务队列就相当于事件循环
	- 宏观任务中，JavaScript 的 Promise 还会产生异步代码，JavaScript 必须保证这些异步代码在一个宏观任务中完成，因此，每个宏观任务中又包含了一个微观任务队列
	- 有了宏观任务和微观任务机制，可以实现 JavaScript 引擎级和宿主级任务，例如：Promise 永远在队列尾部添加微观任务。setTimeout 等宿主 API，则会添加宏观任务
- Promise
	- JavaScript 语言提供的一种标准化的异步管理方式
	- 总体思想 需要进行 io、等待或者其它异步操作的函数，不返回真实结果，而返回一个“承诺”，函数调用方在合适时机，选择等待这个承诺兑现（通过 Promise 的 then 方法的回调）
	- then 回调是一个异步执行过程
		- 输出的顺序是 a b c
		- 进入 console.log(“b”) 之前，毫无疑问 r 已经得到了 resolve，但是 Promise 的 resolve 始终是异步操作，所以 c 无法出现在 b 之前。
- 微任务始终先于宏任务

```js
// 即使耗时一秒的 c1 执行完毕，再 enque 的 c2，仍然先于 d 执行
setTimeout(()=>console.log("d"), 0)
var r = new Promise(function(resolve, reject){
	resolve()
});
r.then(() => { 
	var begin = Date.now();
	// 强制 1 秒的执行耗时，可以确保任务 c2 是在 d 之后被添加到任务队列。
	while(Date.now() - begin < 1000);
	console.log("c1") 
	new Promise(function(resolve, reject){
		resolve()
	}).then(() => console.log("c2"))
});
```

- 异步执行顺序
	- 分析有多少个宏任务
	- 每个宏任务中，分析有多少个微任务
	- 根据调用次序，确定宏任务中的微任务执行次序
	- 根据宏任务的触发规则和调用次序，确定宏任务的执行次序
	- 确定整个顺序

![[../_static/js_microtask_queue.png]]

```js
function sleep(duration) {        
	return new Promise(function(resolve, reject) {   
		setTimeout(resolve,duration);       
	})    
}    
sleep(1000).then( ()=> console.log("finished"));

var r = new Promise(function(resolve, reject){
	console.log("a");
	resolve()
});
r.then(() => console.log("c"));
console.log("b")

// d 必定发生在 c 之后，因为 Promise 产生的是 JavaScript 引擎内部的微任务，而 setTimeout 是浏览器 API，它产生宏任务。
var r = new Promise(function(resolve, reject){        
	console.log("a");        
	resolve()    
});    
setTimeout(()=>console.log("d"), 0)    
r.then(() => console.log("c"));    console.log("b")
```

- Example
	- setTimeout 把整个代码分割成 2 个宏观任务，这里不论是 5 秒还是 0 秒，都是一样的
	- 第一个宏观任务中，包含了先后同步执行的 console.log(“a”); 和 console.log(“b”);。setTimeout 后
	- 第二个宏观任务执行调用 resolve，然后 then 中的代码异步得到执行，调用 console.log(“c”)，最终输出的顺序才是： a b c。
- Promise 是 JavaScript 中的一个定义，实际编写代码时，可以发现，它似乎并不比回调的方式书写更简单，但是从 ES6 开始，有了 async/await，这个语法改进跟 Promise 配合，能够有效地改善代码结构。

```js
function sleep(duration) {        
	return new Promise(function(resolve, reject) {            
		console.log("b");            
		setTimeout(resolve,duration);        
	})    
}    
console.log("a");    
sleep(5000).then(()=>console.log("c"));
```

- async/await
	-  ES2016 新加入特性，提供了用 for、if 等代码结构来编写异步的方式。运行时基础是 Promise
	-  async 函数必定返回 Promise，把所有返回 Promise 的函数都可以认为是异步函数
	-  async 函数是一种特殊语法，特征是在 function 关键字之前加上 async 关键字，这样定义一个 async 函数
	-  可以在其中使用 await 来等待一个 Promise
	-  async 函数强大之处在于，可以嵌套。在定义了一批原子操作的情况下，可以利用 async 函数组合出新的 async 函数

```js
function sleep(duration) {    
	return new Promise(function(resolve, reject) {
		setTimeout(resolve,duration);    
	})
}
async function foo(){    
	console.log("a")    
	await sleep(2000)    
	console.log("b")
}
async function foo2(){    
	await foo("a");    
	await foo("b");
}
```
- generator/iterator 也常常被跟异步一起来讲，必须说明 generator/iterator 并非异步代码，只是在缺少 async/await 的时候，一些框架（最著名的要数 co）使用这样的特性来模拟 async/await。
	- 但是 generator 并非被设计成实现异步，所以有了 async/await 之后，generator/iterator 来模拟异步的方法应该被废弃。

#### 闭包和执行上下文到底是怎么回事？

- 闭包 closure
	- 绑定了执行环境的函数
	- 与普通函数的区别 携带了执行的环境
	- 环境部分
		- 环境：函数的词法环境（执行上下文的一部分）
		- 标识符列表：函数中用到的未声明的变量
	- 表达式部分：函数体
	- JavaScript 中跟闭包对应的概念是“函数”，可能是这个概念太过于普通，跟闭包看起来又没什么联系，所以大家不自觉地把这个概念对应到看起来更特别的“作用域”吧
- 执行上下文：执行的基础设施
	- 定义 一段代码（包括函数），执行所需的所有信息
	- ES3 中包含
		- scope：作用域|作用域链
		- variable object 变量对象，用于存储变量的对象
		- this value：this 值
	- ES5 中改进了命名方式
		- lexical environment：词法环境，当获取变量时使用
		- variable environment：变量环境，当声明变量时使用
		- this value：this 值
	- 在 ES2018 中
		- lexical environment：词法环境，当获取变量或者 this 值时使用
		- variable environment：变量环境，当声明变量时使用
		- code evaluation state：用于恢复代码执行位置
		- Function：执行的任务是函数时使用，表示正在被执行的函数
		- ScriptOrModule：执行的任务是脚本或者模块时使用，表示正在被执行的代码
		- Realm：使用的基础库和内置对象实例
		- Generator：仅生成器上下文有这个属性，表示当前生成器
- var 声明与赋值
	- var 声明作用域函数执行的作用域。var 会穿透 for 、if 等语句。
	- 在只有 var，没有 let 的旧 JavaScript 时代，诞生了一个技巧 立即执行的函数表达式（IIFE）
		- 通过创建一个函数，并且立即执行，来构造一个新的域，从而控制 var 的范围
		- 让函数变成函数表达式，最常见做法 加括号
			- 括号有个缺点 如果上一行代码不写分号，括号会被解释为上一行代码最末的函数调用，产生完全不符合预期，并且难以调试的行为，加号等运算符也有类似的问题。
			- 一些推荐不加分号的代码风格规范，会要求在括号前面加上分号
			- 推荐的写法是使用 void 关键字
	- var 的特性会导致声明的变量和被赋值的变量是两个 b，JavaScript 中有特例，就是使用 with 的时候
- let 是 ES6 开始引入的新的变量声明模式，比起 var 的诸多弊病，let 做了非常明确的梳理和规定。
	- 为了实现 let，JavaScript 在运行时引入了块级作用域。
	- 在 let 出现之前，JavaScript 的 if for 等语句皆不产生作用域。
	- for；if；switch；try/catch/finally语句会产生 let 使用的作用域

```js
(function(){    
	var a;    
	//code
}());

(function(){    
	var a;    
	//code
})();

;(function(){    
	var a;    
	//code
})();

void function(){    
	var a;    
	//code
}();

var b;
void function(){    
	var env = {b:1};    
	b = 2;    
	console.log("In function b:", b);    
	with(env) {        
		var b = 3;        
		console.log("In with b:", b);    
	}
}();
console.log("Global b:", b);
```

- Realm
	- 标准（9.0）中引入
	- 在 ES2016 之前的版本中，标准中甚少提及{} 原型问题。在实际的前端开发中，通过 iframe 等方式创建多 window 环境并非罕见的操作，所以，这才促成了新概念 Realm 的引入。
	- Realm 中包含一组完整的内置对象，而且是复制关系。
	- 对不同 Realm 中的对象操作，会有一些需要格外注意的问题，比如 instanceOf 几乎是失效的。

```js
var iframe = document.createElement('iframe')
document.documentElement.appendChild(iframe)
iframe.src="javascript:var b = {};"

var b1 = iframe.contentWindow.b;
var b2 = {};
//  b1、 b2 由同样的代码“ {} ”在不同的 Realm 中执行，所以表现出了不同的行为。
console.log(typeof b1, typeof b2); //object objectconsole.log(b1 instanceof Object, b2 instanceof Object); //false true
```

- 切换上下文最主要场景 函数调用
- 函数
	- 普通函数 用 function 关键字定义的函数
	- 箭头函数 用 => 运算符定义的函数
	- 生成器函数 用 function * 定义的函数
	- 异步函数：普通函数、箭头函数和生成器函数加上 async 关键字
	- 方法 在 class 中定义的函数
	- 类 用 class 定义的类，实际上也是函数
- 对普通变量而言，这些函数并没有本质区别，都是遵循了“继承定义时环境”的规则，它们的一个行为差异在于 this 关键字
	- this 是执行上下文中很重要的一个组成部分。同一个函数调用方式不同，得到的 this 值也不同
	- 普通函数的 this 值由“调用它所使用的引用”决定，其中奥秘就在于：获取函数的表达式，实际上返回的并非函数本身，而是一个 Reference 类型
	- Reference 类型由两部分组成：一个对象和一个属性值。
	- 做一些算术运算（或者其他运算时），Reference 类型会被解引用，即获取真正的值（被引用的内容）来参与运算，而类似函数调用、delete 等操作，都需要用到 Reference 类型中的对象。
	- 调用函数时使用的引用，决定了函数执行时刻的 this 值。
	- 从运行时的角度来看，this 跟面向对象毫无关联，与函数调用时使用的表达式相关。
	- 改为箭头函数后，不论用什么引用来调用它，都不影响它的 this 值。	
	- 在方法中，this 的行为也不太一样，得到了 undefined 的结果。
	- 生成器函数、异步生成器函数和异步普通函数跟普通函数行为是一致的，异步箭头函数与箭头函数行为是一致的。
	- 函数能够引用定义时的变量，能记住定义时的 this，因此，函数内部必定有一个机制来保存这些信息。在 JavaScript 标准中，为函数规定了用来保存定义时上下文的私有属性`[[Environment]]`
	- 当一个函数执行时，会创建一条新的执行环境记录，记录的外层词法环境（outer lexical environment）会被设置成函数的`[[Environment]]` 这个动作就是切换上下文了
- 用一个栈来管理执行上下文，栈中的每一项包含一个链表
	- 当函数调用时，会入栈一个新的执行上下文，函数调用结束时，执行上下文被出栈。
	- this 则是一个更为复杂的机制，JavaScript 标准定义了` [[thisMode]] `私有属性,取值
		- lexical：表示从上下文中找 this，对应箭头函数
		- global：表示当 this 为 undefined 时，取全局对象，对应普通函数
		- strict：当严格模式时使用，this 严格按照调用时传入的值，可能为 null 或者 undefined
	- 方法的行为跟普通函数有差异，恰恰是因为 class 设计成了默认按 strict 模式执行
	- 函数创建新的执行上下文中的词法环境记录时，会根据`[[thisMode]]`来标记新纪录的`[[ThisBindingStatus]]`私有属性
		- 代码执行遇到 this 时，会逐层检查当前词法环境记录中的`[[ThisBindingStatus]]`，当找到有 this 的环境记录时获取 this 的值
		- 规则的实际效果，嵌套的箭头函数中的代码都指向外层 this

```js
function showThis(){    
	console.log(this);
}
var o = {    
	showThis: showThis
}
showThis(); // global
o.showThis(); // o
```

```js
const showThis = () => {
    console.log(this);
}
var o = {
    showThis: showThis
}
showThis(); // global
o.showThis(); // global
```

```js
class C {    
	showThis() {        
		console.log(this);    
	}
}
var o = new C();
var showThis = o.showThis;
showThis(); // undefined
o.showThis(); // o
```

```js
"use strict"
function showThis(){    
	console.log(this);
}
var o = {    
	showThis: showThis
}
showThis(); // undefined
o.showThis(); // o
```

```js
// 切换上下文
var a = 1;
foo();

在别处定义了foo：
// 这里的 foo 能够访问 b（定义时词法环境），却不能访问 a（执行时的词法环境），这就是执行上下文的切换机制了
var b = 2;
function foo(){    
	console.log(b); // 2    
	console.log(a); // error
}
```
```js
var o = {}
o.foo = function foo(){    
	console.log(this);    
	return () => {        
		console.log(this);        
		return () => console.log(this);    
	}
}
o.foo()()(); // o, o, o
```

- 操作 this 的内置函数
	- Function.prototype.call 和 Function.prototype.apply 可以指定函数调用时传入的 this 值
	- Function.prototype.bind 可以生成一个绑定过的函数，这个函数的 this 值固定了参数
	- call、bind 和 apply 用于不接受 this 的函数类型如箭头、class 都不会报错,这时候，它们无法实现改变 this 的能力，但是可以实现传参

```js
function foo(a, b, c){    
	console.log(this);    
	console.log(a, b, c);
}
// call 和 apply 作用是一样的，只是传参方式有区别
foo.call({}, 1, 2, 3);
foo.apply({}, [1, 2, 3]);

foo.bind({}, 1, 2, 3)();
```

#### 语句执行机制 try里面放return，finally还会执行吗？

- JavaScript 语句执行机制
- Completion 类型
	- 在 try 中有 return 语句，finally 中的内容会执行 
	- 在 finally 中加入 return 语句，finally 中的 return “覆盖”了 try 中的 return
	- 执行机制的基础是 JavaScript 语句执行的完成状态，用一个标准类型来表示：Completion Record（用于描述异常、跳出等语句执行过程）， 表示一个语句执行完之后的结果，有三个字段
		- `[[type]] `表示完成类型，有 break continue return throw 和 normal
		- `[[value]]` 表示语句返回值，如果语句没有，则是 empty
		- `[[target]] `表示语句目标，通常是一个 JavaScript 标签
- JavaScript 使用 Completion Record 类型控制语句执行过程
- 普通语句 不带控制能力的语句
	- 类型
		- 声明类语句
			- var 声明
			- const 声明
			- let 声明
			- 函数声明
			- 类声明
		- 表达式语句
		- 空语句
		- debugger 语句
	- 在执行时，从前到后顺次执行（这里先忽略 var 和函数声明的预处理机制），没有任何分支或者重复执行逻辑。
	- 执行后，得到 `[[type]]` 为 normal 的 Completion Record，JavaScript 引擎遇到会继续执行下一条语句
	- 使用 Chrome 自带的调试工具，输入一个表达式，在控制台可以得到结果，在前面加上 var，就变成 undefined.显示的正是语句的 Completion Record 的`[[value]]`
- 语句块 拿大括号括起来的一组语句，一种语句的复合结构，可以嵌套
	- 本身并不复杂，需要注意的是语句块内部的语句的 Completion Record 的`[[type]]` 如果不为 normal，会打断语句块后续的语句执行。
	- 如果每一个语句都是 normal 类型，那么会顺次执行
	- 插入一条 return 语句，产生了一个非 normal 记录，那么整个 block 会成为非 normal。这个结构就保证了非 normal 的完成类型可以穿透复杂的语句嵌套结构，产生控制效果。
- 控制型语句
	- 带有 if、switch 关键字，会对不同类型的 Completion Record 产生反应
	- 一类 对其内部造成影响，如 if、switch、while/for、try。
	- 另一类 对外部造成影响如 break、continue、return、throw，
	- break 、continue 、return 、throw 四种类型与控制语句两两组合产生的效果，产生控制代码执行顺序和执行逻辑的效果
- try 和 return 的组合
	- finally 中的内容必须保证执行，所以 try/catch 执行完毕，即使得到的结果是非 normal 型的完成记录，也必须要执行 finally。
	- 当 finally 执行也得到了非 normal 记录，则会使 finally 中的记录作为整个 try 结构的结果。

![[../_static/js_control_effort.png]]

```js
function foo(){
  try{
    return 0;
  } catch(err) {
  } finally {
    console.log("a")
  }
}
// finally 确实执行了，而且 return 语句也生效了，foo() 返回了结果 0
// 函数并没有立即返回
console.log(foo());
```

- 带标签语句 任何 JavaScript 语句是可以加标签的，在语句前加冒号即可
	- 大部分时候，这个东西类似于注释，没有任何用处。唯一有作用的时候是：与完成记录类型中的 target 相配合，用于跳出多层循环。
	- break/continue 语句如果后跟了关键字，会产生带 target 的完成记录。一旦完成记录带了 target，那么只有拥有对应 label 的循环语句会消费它。

```js
outer: while(true) {      
	inner: while(true) {          
		break outer;      
	}    
}    
console.log("finished")
```

## HTML

文档元信息 出现在 head 标签中的元素，包含了描述文档自身的一些信息
语义相关 扩展了纯文本，表达文章结构、不同语言要素的标签
链接 提供到文档内和文档外的链接
替换型标签 引入声音、图片、视频等外部元素替换自身的一类标签
表单 用于填写和提交信息的一类标签
表格：表头、表尾、单元格等表格的结构

## CSS

- 侧重从语言和设计思想的角度来讲解，我们同样可以对两者的全貌建立一些认知。

## 浏览器实践

- 包含了浏览器工作的原理和一些重要的 API，包括 BOM、DOM、CSSOM 和其他一些内容。了解了这些知识，你才能把 JavaScript 和 HTML、CSS 连接起来，用 JavaScript 来实现功能。

## 前端综合应用

### 性能

- 对任何一个前端团队而言，性能是它价值的核心指标，从早年“重构”的实践开始，前端有通过性能证明自己价值的传统。但是性能并非细节的堆砌，也不是默默做优化，所以，会从团队的角度来跟你一起探讨性能的方法论和技术体系。

### 工具链

- 会探讨企业中工具链的建设思路。对一个高效又合作良好的前端团队来说，一致性的工具链是不可或缺的保障，作为开发阶段的入口，工具链又可以和性能、发布、持续集成等系统链接到一起，成为团队技术管理的基础。

### 持续集成

- 并非一个新概念，但是过去持续集成概念和理论都主要针对软件开发，而对前端来说，持续集成是一个新的课题（当然对持续集成来说，前端也是一个新课题），比如 daily build 就完全不适用前端，前端代码必须是线上实时可用的。这一部分内容将会针对前端的持续集成提出一些建设的思路。

### 搭建系统

前端工作往往多而繁杂，针对高重复性、可模块化的业务需求，传统的人工开发不再适用，搭建系统是大部分大型前端团队的选择。
介绍什么是搭建系统，以及一些常见的搭建系统类型。架构与基础库最后一个部分，会给大家介绍前端架构和基础库的知识。软件架构师主要解决功能复杂性的问题，服务端架构师主要解决高流量问题，而前端是页面间天然解耦，分散在用户端运行的系统，但是前端架构也有自己要解决的问题。
