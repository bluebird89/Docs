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

### 文法

- 词法
- 语法

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
