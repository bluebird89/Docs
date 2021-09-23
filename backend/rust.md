## [rust](https://www.rust-lang.org)

Empowering everyone to build reliable and efficient software.

- 由 Mozilla 主导开发的通用、编译型编程语言
	- 原本是 Mozilla 员工 Graydon Hoare 的私人项目
	- Mozilla 于 2009 年开始赞助这个项目，并且在 2010 年首次揭露它的存在.全新的开源系统编程语言
- 设计准则为“安全、并发、实用”，支持函数式、并发式、过程式以及面向对象的编程风格。帮助开发者创造高速与安全的应用，同时能享受到现代多核处理器的强大特性
- 现有系统软件语言（如 C 和 C++）的一种安全替代语言。 与 C 和 C++ 一样，Rust 没有大型运行时或垃圾回收器，这几乎与所有其他现代语言形成了鲜明对比

## 特点

- 没有历史包袱，采百家之长。从语言内核看， Rust 重塑对基本概念的理解。比如它清晰地定义了变量的生命周期，不仅摒弃GC这样的内存和性能杀手，还不用关心手动内存管理，让内存安全和高性能兼得。
- 从语言外观，用起来很像 Python/TypeScript 高级语言，表达能力一流，但性能丝毫不输于 C/C++，表达力和高性能二者兼得
- 易懂语法避免段错误 (segmentation faults) 并保证线程安全
- 提供零成本抽象，更多语义，内存安全保证，不会发生竞争的线程，基于特性 (trait) 的泛型，模式匹配，类型推导，高效的 C 绑定，和最小运行时大小
- 优点
  - 优秀的 Macro 宏定义机制
  - 可 OO。基于 Traits 的简洁而强大的范型系统
  - 错误处理。基于 Option & Result 的空值和错误处理
  - 防 OOM。基于 Ownership、Borrowing、Lifetime 的内存管理机制
  - 新的范式（paramdigm）。子曾经曰过：如果一门编程语言没有带给你新的 paradigm，就不一定值得学，就好像学了 .net 再去学 java，或者学了 python 再学 ruby，从拓宽边界的角度，意义不大
  - 可以编译成 webassembly —— 未来的也许会真正实现「一次编译到处运行」的可执行体：浏览器内，IoT 设备，各种服务器，手机等。
  - 接近于 C/C++ 性能，不输于 ruby / elixir 表现力
  - 类型安全：编译器可确保不会将任何操作应用于错误类型的变量。
  - 内存安全：Rust 指针（称为“引用”）始终引用有效的内存。
  - 无数据争用：Rust 的 borrow 检查器通过确保程序的多个部分不能同时更改同一值来保证线程安全。
  - 零成本抽象：Rust 允许使用高级别概念，例如迭代、接口和函数编程，将性能成本控制在最低，甚至不会产生成本。 这些抽象的性能与手工编写的底层代码一样出色。
  - 最小运行时：Rust 具有非常小的可选运行时。 为了有效地管理内存，此语言也不具有垃圾回收器。 在这一点上，Rust 非常类似于 C 和 C++ 之类的语言
  - 面向裸机：Rust 可以用于嵌入式和“裸机”编程，因此适合用于编写操作系统内核或设备驱动程序
  -  允许控制用该语言编写的程序和库的性能和资源消耗（与 C 和 C++ 相似），同时在默认情况下仍保持内存安全，消除了所有常见的 bug 类。
  -  具有丰富的抽象功能，使开发人员能够将程序的许多不变量编码成代码，然后由编译器检查，而不是依赖于约定或文档。 此功能通常会导致产生“如果编译，它就有效”的感觉
  -  提供用于生成、测试、记录和共享代码的内置工具，以及丰富的第三方工具和库生态系统。 这些工具可以使在某些语言中难以执行的任务（例如生成依赖项）在 Rust 中变得容易且高效。
- 缺点
  - 处理更多细节
  - 复杂的所有权机制:在没有垃圾回收机制的前提下保障内存安全。这是一个相当复杂的概念

### 与 webassembly 结合

  - 未来几年软件开发，protable binary（平台无关的受控可执行代码）会越来越重要，而 webassembly 似乎是目前唯一受到几大厂商全力支持的方向
  - webassembly 应用场景不仅仅是 web（比如大型游戏的 web 化），更是服务端虚拟化的一个新的，也许是更优的解决方案
  - 随着 5G 时代到来，高带宽会带来网络边界的模糊：数据变得灵动起来，从而带动计算会时而发生在客户端，时而发生在服务端。当越来越多的计算可以直接发生在客户端时，一个平台无关的，安全的代码运行环境就变得至关重要，这也是 webassembly 的机会
  - webassebmly 目前支持最好的语言是什么？Rust

### 方向

- 高性能 Web。Rust + WASM
- 跨平台应用。Rust + Electron + Node.js，结合 Neon Binding，可以编译为 Node.js 的模块，并在 Electron 应用中调用，开发跨平台桌面应用

## 安装

- Rust 有一个为期六周的快速发布过程，并且支持大量的平台
- [rustup.rs](https://github.com/rust-lang/rustup.rs):The Rust toolchain installer 设置开发环境
- rustc 命令编写和编译 Rust 程序
- [Playground](https://play.rust-lang.org/) 设置一些限制可以保护站点不被恶意使用
	- 将代码保存到 GitHub Gist 中，便于用户分享

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
brew install rustup

rustup update # 更新
rustup self uninstall

rustc --version
cargo --version

rustup doc # 本地阅读核心文档

rustc  main.rs

./main
```

### 配置

- `$HOME/.cargo/env` 或者 `export PATH="$HOME/.cargo/bin:$PATH"`
- 所有工具安装 ~/.cargo/bin 目录， 并且能够找到 Rust 工具链，包括 rustc、cargo 及 rustup

```sh
echo 'export RUSTUP_DIST_SERVER=https://mirrors.tuna.tsinghua.edu.cn/rustup' >> ~/.bash_profile

# $HOME/.cargo/config
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'

[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

[source.tuna]
registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"

[source.sjtu]
registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index"

[source.rustcc]
registry = "git://crates.rustcc.cn/crates.io-index"

[source.aliyun]
registry = "https://code.aliyun.com/rustcc/crates.io-index"
```

## Dependency

- [cargo](https://github.com/rust-lang/cargo)Rust’s build system and package manager. <https://doc.rust-lang.org/cargo>

```sh
# Cargo.toml
cargo --verison
cargo new project
cargo build --realse
cargo run|check|update

rustup component add rls --toolchain stable-x86_64-apple-darwin
```

### Project Setup

- 基本结构
	- 
-  Cargo 依赖项管理器
	- cargo new 命令创建新项目模板
	- cargo build 编译项目
	- cargo run 命令编译并运行项目
	- cargo test 命令测试项目
	- cargo check 命令检查项目类型
	- cargo doc 命令编译项目的文档
	- cargo publish 命令将库发布到 crates.io
	- 将箱的名称添加到 Cargo.toml 文件来将依赖箱添加到项目
- 工具
	- lint
		- Rustfmt
		- Clippy
	- Linter and Formatter cargo-husky
	- cargo-make Task Runner
    - [cargo-watch](https://github.com/passcod/cargo-watch):Watches over your Cargo project's source <https://crates.io/crates/cargo-watch>  Live Reload
	- cargo-audit Dependency Vulnerability Checker 
- 结构
	- Cargo.toml  Rust 清单文件，可用于保存项目及依赖项的元数据
	- Cargo.lock  Dependency Lockfile
	- Src 子目录中 main.rs 文件可用于编写应用程序代码

```sh
cargo new hello_rust

cargo install wasm-pack          # Compile Rust to Wasm and generate JS interop code
cargo install cargo-make         # Task runner
cargo install simple-http-server # Simple server to serve assets
cargo new --lib rustmart && cd rustmart
```

### 模块系统

- 模块 
	- 一个编译单元。 它是 Rust 编译器可以运行的最小代码段。 
	- 箱中代码一起编译以创建二进制可执行文件或库
	- 箱包含具有隐式未命名顶级模块的 Rust 模块的层次结构。
- 箱 Rust 
	- 模块通过管理箱内单个代码项范围来帮助组织程序
	- 仅将箱编译为可重复使用的单元。
	- 结合使用相关代码项或项可以分组到相同模块中
	- 递归代码定义可以跨越其他模块
- 路径
	- 可以使用路径来命名代码中的项。 例如，路径可以是一个数据定义（例如，矢量、代码函数，甚至是模块）
	- 模块功能还可帮助控制路径的隐私。可以指定可公开访问代码部分和私有部分。 通过该功能可以隐藏实现详细信息
- 使用 Rust 编译器 (rustc) 来生成箱
- 使用 use 关键字 访问箱或库中可重复使用代码,箱或库中代码就会“进入范围”，可以访问程序中的定义和功能
	- 标准库在路径 std 的 use 语句中访问，如 use std::fmt
	- 其他箱或库是通过名称访问，例如 use regex::Regex
- 标准库 std 包含 Rust 程序中的基本定义和操作的可重复使用代码
	- 该库拥有核心数据类型（例如 String 和 `Vec<T>`）定义、Rust 基元的操作、常用宏函数的代码、对输入和输出操作的支持以及许多其他功能区域
	- std::collections - 集合类型的定义，如 HashMap。
	- std::env - 用于处理环境的函数
	- std::fmt - 控制输出格式的功能
	- std::fs - 用于处理文件系统的功能
	- std::io - 用于处理输入/输出的定义和功能
	- std::path - 支持处理文件系统路径数据的定义和功能
- 第三方箱存储库 [crates.io](https://crates.io/) The Rust community’s crate registry 
	- [structopt](https://crates.io/crates/structopt) - 用于轻松分析命令行参数的第三方 crate。
	- [chrono](https://crates.io/crates/chrono) - 用于处理日期和时间数据的第三方箱。
	- [regex](https://crates.io/crates/regex) - 用于处理正则表达式的第三方箱。
	- [serde](https://crates.io/crates/serde) - 适用于 Rust 数据结构的序列化和反序列化操作的第三方箱

## Syntax

- 函数体的左大括号紧跟在参数列表的括号后面
- 语句以分号 ; 结尾
- 缩进四个空格

### Variables

- 用关键字 let 声明。 每个变量都有一个唯一名称
- 变量后，可将其绑定到某个值，也可稍后在程序中绑定该值
- let immutable
	- 变量绑定默认不可变
	- 变量不可变，将值绑定到名称后，将无法更改此值
	- explicitly mention it using the mut keyword `let mut a = 123;`
- 隐藏
	- 可以声明与现有变量同名新变量。 新的声明会创建新的绑定
	- 新变量会隐藏上一个变量。 旧变量仍存在，但无法再于此范围内引用它。
- const:think of Rust’s const as a “label” to a constant value. During compile time they get replaced by their actual values in all the places they are used. It’s usually used for constants like port numbers, timeout values, error codes etc
- Destructuring:extracting the inner fields of an array or struct into separate variables

### Data Types

- Rust 是一种静态类型化的语言。编译器必须知道代码中所有变量的确切数据类型，以便程序编译和运行
- 编译器通常可以根据绑定值推断变量的数据类型。并非总是需要在代码中显式说明类型
	-  值推断数据类型不匹配为变量指定数据类型，因此编译器会发出错误
- 如果有多种类型，则必须通过使用类型注释，让编译器得知特定类型
- 内置基元数据类型。称为标量，因为它们表示单个值
	- 整数数字
	- 浮点数
	- 布尔型
	- 字符
- 集合类型
	- array|vector
	- Hashmap

#### Boolean

- 具有两个可能的值：true 或 false
- 广泛用于条件表达式

#### Number

- integers (numbers without decimal point) 
	- isize 和 usize 类型取决于运行程序的计算机的类型
		- 应在 64 位体系结构上使用 64 位类型，在 32 位体系结构上使用 32 位类型
		- 如果未指定整数类型，并且系统无法推断类型，则默认情况下，系统会分配 i32 类型（带符号的 32 位整数）
- floats (numbers with decimal point). 用于十进制值的浮点数据类型
	- f32（32 位）和 f64（64 位）
	- 默认浮点类型为 f64
	- 在新式 CPU 上，f64 类型速度与 f32 类型大致相同，但精度更高
- 用双引号将变量值括起来，编译器会将值解释为文本而不是数字

| 长度    | 有符号 | 无符号 |
| ------- | ------ | ------ |
| 8 bit   | i8     | u8     |
| 16 bit  |  i16      |    u16    |
| 32 bit  |  i32      |    u32    |
| 64 bit  |  i64      |    u64    |
| 128 bit |  i128   |      u128  |
| 与体系结构相关|   isize     |      usize  |

```rust
// Addition, Subtraction, and Multiplication
println!("1 + 2 = {} and 8 - 5 = {} and 15 * 3 = {}", 1u32 + 2, 8i32 - 5, 15 * 3);

// Integer and Floating point division
println!("9 / 2 = {} but 9.0 / 2.0 = {}", 9u32 / 2, 9.0 / 2.0);
```

#### String

- 所有文本类型都是有效 UTF-8 表示形式
- char 
	-  一种字符类型文本值
	- 最基元的文本类型。通过将项括在单引号中来指定值
	- 包含 unicode 码位，但不会使用 utf-8 编码
	- 一个 21 位整数，系统会将其宽度填充为 32 位
	- char 直接包含纯码位值
- Rust 作为一种系统语言，公开了字符串的一些内在复杂性。 随着复杂性的增加，对程序中内存使用方式的控制变得非常精细
	- 字符串是一种十分复杂的数据类型。 大多数语言使用其垃圾回收器来掩盖这种复杂性
- str 类型
	- 也称为“字符串切片”，是字符串数据的一种视图
	- 大多数情况下，使用在类型前面添加 & 符号 &str 引用样式语法来引用这些类型,指向不可变字符串数据的指针.字符串字面量的类型都是 &str
- String:growable whereas &str is immutable and fixed size
	- 在堆上分配。 使用 String 类型时，无需在编译代码之前知晓字符串的长度（字符数）
- 字符是单个项，而字符串是一系列字符

#### 元组

- 集中到一个复合值中的不同类型值的分组
- 元组中的各个值称为元素。些值指定为括在括号中的逗号分隔列表 `(<value>, <value>, ...)`
- 元组索引 
	- 元素通过从零开始索引位置进行访问 `<tuple>.<index>`
 
 #### 结构
 
- 多个其他类型组合体。结构中元素称为字段
- 与元组一样，结构中字段可以具有不同数据类型。 
- 显著好处 可以命名每个字段，以便清楚展示相应值含义
- 类型
	- 经典结构
		 - 定义 每个字段都具有名称和数据类型，主体在大括号 {} 中定义，字段指定为逗号分隔列表
		 - 使用语法 `<struct>.<field> `访问结构中字段
	- 元组结构
		- 类似于经典结构，字段没有名称，主体在括号 () 内定义。括号紧跟在结构名称后面。 结构名称和左括号之间不含空格
		- 访问元组结构中字段，使用语法`<tuple>.<index>`
		- 索引值从 0 开始
	 - 单元结构
		- 常用作标记
- 定义结构，请输入关键字 struct，后跟结构名称，
	- 名称为描述分组数据重要特征的结构类型，采用首字母大写形式

```rust
// Classic struct with named fields
struct Student { name: String, level: u8, remote: bool }

// Tuple struct with data types only
struct Grades(char, char, char, char, f32);

// Unit struct
struct Unit;

// Instantiate classic struct, specify fields in random order, or in specified order
let user_1 = Student { name: String::from("Constance Sharma"), remote: true, level: 2 };
let user_2 = Student { name: String::from("Dyson Tan"), level: 5, remote: false };

// Instantiate tuple structs, pass values in same order as types defined
let mark_1 = Grades('A', 'A', 'B', 'A', 3.75);
let mark_2 = Grades('B', 'A', 'A', 'C', 3.25);

println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}", 
         user_1.name, user_1.level, user_1.remote, mark_1.0, mark_1.1, mark_1.2, mark_1.3, mark_1.4);
println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}", 
         user_2.name, user_2.level, user_2.remote, mark_2.0, mark_2.1, mark_2.2, mark_2.3, mark_2.4);
```

#### 枚举

- 可为任意一种变体类型
- 每个枚举变体都能有对应数据
- 用 enum 关键字创建枚举类型，具有枚举变体的任意组合
	- 可以具有命名字段、没有名称的字段或根本没有字段
	- 采用首字母大写形式
	- 枚举中的每个变体都是独立的，可存储不同数量和类型的值
-  任何使用 WebEvent 枚举变体的函数都必须接受枚举中的所有变体。不存在只接受 WEClick 变体而不接受其他变体的函数
	- 解决枚举变体要求的一种方法
		- 为枚举每个变体定义单独结构
		- 枚举中的每个变体都使用相应的结构
		- 结构容纳的数据与相应枚举变体所容纳的数据相同。 用户可借此定义样式单独引用每个逻辑变体

```rust
enum WebEvent {
    // An enum variant can be like a unit struct without fields or data types
    WELoad,
    // An enum variant can be like a tuple struct with data types but no named fields
    WEKeys(String, char),
    // An enum variant can be like a classic struct with named fields and their data types
    WEClick { x: i64, y: i64 }
}

// Define a tuple struct
struct KeyPress(String, char);

// Define a classic struct
struct MouseClick { x: i64, y: i64 }

// Redefine the enum variants to use the data from the new structs
// Update the page Load variant to have the boolean type
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }

let we_load = WebEvent::WELoad(true);
// Instantiate a MouseClick struct and bind the coordinate values
let click = MouseClick { x: 100, y: 250 };

// Set the WEClick variant to use the data in the click struct
let we_click = WebEvent::WEClick(click);

// Instantiate a KeyPress tuple and bind the key values
let keys = KeyPress(String::from("Ctrl+"), 'N');
    
// Set the WEKeys variant to use the data in the keys tuple
let we_key = WebEvent::WEKeys(keys);
```

#### Array

- 按顺序存储在内存中相同类型对象的集合
- 长度 数组中元素数
	- 可在代码中指定，也可由编译器计算
	- fixed size 大小是固定的,永远不会更改
- 签名定义 `[T; size]`
	- T  数组中所有元素数据类型
	- size 表示数组长度的非负整数
-  索引 
	-  元素从 0 开始隐式编号,`<array>[<index>]` 使用索引访问数组中元素
	- 越界 使用不在允许范围内的索引访问数组中的元素，编译器将返回错误
		- 任何值为负的索引也为越界索引

 ```rust
// Declare array, initialize all values, compiler infers length = 7
let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
  
// Declare array, first value = "0", length = 5
let bytes = [0; 5];
```
 
 #### Vector
 
 - can grow/shrink in size
 - 与数组一样，可以使用向量存储具有相同数据类型的多个值。
 - 与数组不同之处在于，向量长度可以随时增大或缩小
	 - 在编译时，大小随时间更改的功能是隐式的。 因此，Rust 无法像在数组中阻止越界访问一样在向量中阻止访问无效位置
- 使用 Vec::new() 方法创建向量
	- 可在向量末尾添加和删除值。若要支持这种行为，请使用 mut 关键字将向量变量声明为可变变量
	- `push(<value>)` 将值添加到向量末尾
	- `pop()` 删除向量末尾的值
- 使用索引访问向量中元素值
	- 无法使用不在允许范围内的索引访问向量中的元素,编译通过，但程序在表达式位置进入不可恢复的死机状态并停止程序执行。

```rust
// Create empty vector, declare vector mutable so it can grow and shrink
let mut fruit = Vec::new();
// Push values onto end of vector, type changes from generic `T` to String
fruit.push("Apple");
fruit.push("Banana");
fruit.push("Cherry");
println!("Fruits: {:?}", fruit);
println!("Pop off: {:?}", fruit.pop());
println!("Fruits: {:?}", fruit); 
```
 
 ##### 泛型
 
 - 泛型类型 T `<T>`
 - 不知道真实数据类型，请使用泛型类型声明
 - 用于声明向量
	 -  `<vector><T> `声明由泛型（未知）数据类型 T 组成的向量
	 - 实际创建向量，请使用具体类型，如 `<vector>u32`（类型为 u32 的向量）或者 `<vector>String`（类型为字符串的向量）
- 声明和初始化向量常用方法 用 vec! 宏, 该宏还接受与数组构造函数相同语法
 
```rust
// Declare vector, initialize with three values
let three_nums = vec![15, 3, 46];
println!("Initial vector: {:?}", three_nums);  
  
// Declare vector, first value = "0", length = 5
let zeroes = vec![0; 5];
println!("Zeroes: {:?}", zeroes);
```
 
 #### 哈希映射
 
 - `HashMap<K, V>` 通过映射每个键 K 及其值 V 来存储数据
 - 大小可以增加
 - 数据存储在堆中
 - `get(<key>)` 通过键访问数据,在运行时检查对哈希映射项的访问
	 - `get(&str)` 方法返回 Option<&Value> 类型，使用“Some()”表示法包装方法调用结果
	 - 对无效哈希映射键用 get 方法，返回“None”
 - `<hash_map_name>.insert()` 添加元素
	 - to_string() 将字符串字面量 (&str) 值转换为 String 类型,哈希映射包含实际值，而不是该值引用或指针
 -  .remove() 从哈希映射中删除条目

```rust
use std::collections::HashMap;
let mut reviews: HashMap<String, String> = HashMap::new();

reviews.insert("Ancient Roman History".to_string(), "Very accurate.".to_string());
reviews.insert("Cooking with Rhubarb".to_string(), "Sweet recipes.".to_string());
reviews.insert("Programming in Rust".to_string(), "Great examples.".to_string());

// Look for a specific review
let book: &str = "Programming in Rust";
println!("\nReview for \'{}\': {:?}", book, reviews.get(book));

reviews.insert("Ancient Roman History".to_string(), "Very accurate.".to_string());
```
 
#### Object

  - Bag of data:

### control loop

- if 块也可充当表达式。 条件分支中所有执行块都必须为要编译的代码返回相同的类型
- 循环
	- loop 创建无限循环 利用此关键字可连续重复表达式主体中操作，直到执行一些直接操作来停止
	- while：在条件为 true 时重复代码
	- for：对集合中所有值重复代码

```rust
let mut counter = 1;
// stop_loop is set when loop stops
let stop_loop = loop {
    counter *= 2;
    if counter > 100 {
        // Stop loop, return counter value
        break counter;
    }
};
// Loop should break when counter = 128
println!("Break the loop at counter = {}.", stop_loop);
```

### function

-  执行特定任务的代码块
	- 根据任务将程序中代码分割成块
	- 通过分割，代码变得更易于理解和维护
	- 为任务定义函数后，可以在需要执行相应任务时调用该函数
- 每个 Rust 程序必须有一个 main 函数
	- main 函数中代码始终是 Rust 程序中运行的第一个代码
	- main 函数不包含任何输入参数
- 函数签名 `fn is_divisible_by(dividend: u32, divisor: u32) -> bool`
- 声明 用 fn 关键字
	- 不在意文件中函数定义位置，只要在文件中某处定义函数即可
- 参数
	- 集列在括号 () 内
	- 命名每个参数并在函数声明的开头指定数据类型
- 函数体
	- 执行函数任务代码在大括号 {} 内定义
- return
	-  在函数参数列表后面和函数体的左大括号前面添加语法 `-> <type>`
	- without an explicit return 始终返回代码块中最后一个表达式的值。可以根据需要显式使用 return 关键字
	- 显式使用 return 关键字时，语句以分号结束
	- implicitly 不使用 return 关键字情况下创建和发送回返回值时，remove the semicolon from that line
- 调用 
	- 函数名称以及括号中输入参数
- closure
- Iterators
  - & is the reference operator
  - the * is the dereference operator

### 宏

- 类似于函数，采用可变数量输入参数
- 将文本字符串中的每个大括号 {} 实例替换为列表中下一个参数的值
- `println!()`

### Debug

-  `#[derive(Debug)]` 在代码执行期间查看某些在标准输出中无法查看的值
- 使用 println! 宏查看调试数据
- 使用 `{:#?}` 以可读方式格式化数据

## Pattern Matching

```sh
match VALUE {
  PATTERN1 => EXPRESSION1,
  PATTERN2 => EXPRESSION2,
  PATTERN3 => EXPRESSION3,
}
```

## 教程

- [rustlings](https://github.com/rust-lang/rustlings/):crab Small exercises to get you used to reading and writing Rust code!
- [rust-by-example](https://github.com/rust-lang/rust-by-example):Learn Rust with examples (Live code editor included) <https://doc.rust-lang.org/stable/rust-by-example/>
  - [rust-by-example-cn](https://github.com/rust-lang-cn/rust-by-example-cn):Rust By Example 中文版
- [The Rust Reference](https://doc.rust-lang.org/reference/index.html)
- [The Rustonomicon](https://doc.rust-lang.org/nomicon/index.html):The Dark Arts of Unsafe Rust
- [tour_of_rust](https://github.com/richardanaya/tour_of_rust):A tour of rust's language features <https://tourofrust.com/>
- [Command line apps in Rust](https://rust-cli.github.io/book/index.html)
- 《陈天 · Rust 编程第一课》

## 项目

- [bevy](https://github.com/bevyengine/bevy):A refreshingly simple data-driven game engine built in Rust <https://bevyengine.org/>

## 图书

- [Rust Programming Language](https://doc.rust-lang.org/book/) [book](https://github.com/rust-lang/book)
  - [Rust程序设计](https://kaisery.github.io/trpl-zh-cn/) [美]吉姆·布兰迪（Jim Blandy）[美]贾森·奥伦多夫（Jason Orendorff）李松峰 (译)
  - [trpl-zh-cn](https://github.com/KaiserY/trpl-zh-cn):Rust 程序设计语言（第二版） <https://kaisery.github.io/trpl-zh-cn/>
- Rust 编程之道
- 《深入浅出 Rust》
- 《Rust 权威指南》
- 《精通 Rust (第 2 版)》

## 工具

- 包管理
  - [rayon](https://github.com/rayon-rs/rayon):Rayon: A data parallelism library for Rust
  - [Docs.rs](https://docs.rs/)

### 框架

  - [tokio](https://github.com/tokio-rs/tokio):A runtime for writing reliable, asynchronous, and slim applications with the Rust programming language. <https://tokio.rs>
  - [yew](https://github.com/yewstack/yew):Rust / Wasm framework for building client web apps <https://yew.rs/docs/>
  - [actix-web](https://github.com/actix/actix-web):Actix web is a small, pragmatic, and extremely fast rust web framework. <https://actix.rs>
  - [nickel.rs](https://github.com/nickel-org/nickel.rs):An expressjs inspired web framework for Rust <http://nickel-org.github.io/>
  - [nannou](https://github.com/nannou-org/nannou) A Creative Coding Framework for Rust.https://nannou.cc/


- [wasm-pack](https://github.com/rustwasm/wasm-pack):📦✨ your favorite rust -> wasm workflow tool! <https://rustwasm.github.io/wasm-pack/>
- [clap](https://github.com/clap-rs/clap):A full featured, fast Command Line Argument Parser for Rust <https://clap.rs>
- [crossbeam](https://github.com/crossbeam-rs/crossbeam):Tools for concurrent programming in Rust
- 工具
  - [racer](https://github.com/racer-rust/racer):Rust Code Completion utility
  - [remacs](https://github.com/Wilfred/remacs):Rust heart Emacs
  - [cross](https://github.com/rust-embedded/cross):“Zero setup” cross compilation and “cross testing” of Rust crates
- search
  - [tantivy](https://github.com/tantivy-search/tantivy):Tantivy is a full-text search engine library inspired by Apache Lucene and written in Rust
  - [Toshi](https://github.com/toshi-search/Toshi):A full-text search engine in rust
- [pest](https://github.com/pest-parser/pest):The Elegant Parser <https://pest.rs>
- [hyper](https://github.com/hyperium/hyper):An HTTP library for Rust <https://hyper.rs/>
- [rust-analyzer](https://github.com/rust-analyzer/rust-analyzer)An experimental Rust compiler front-end for IDEs <https://rust-analyzer.github.io/>
- MQ
  - [flume](https://github.com/zesterer/flume):A safe and fast multi-producer, single-consumer channel. <https://crates.io/crates/flume>
- GUI
  - [iced](https://github.com/hecrj/iced):A cross-platform GUI library for Rust, inspired by Elm
- IDE
  - Clion + Rust 插件

## 参考

- [](https://doc.rust-lang.org/book/)
- [文档](https://kaisery.gitbooks.io/rust-book-chinese/content/)
- [rust-gentle-intro](https://stevedonovan.github.io/rust-gentle-intro/)
- [patterns](https://github.com/rust-unofficial/patterns):A catalogue of Rust design patterns
- [awesome-rust](https://github.com/rust-unofficial/awesome-rust):A curated list of Rust code and resources.
- [futures-rs](https://github.com/rust-lang-nursery/futures-rs):Zero-cost asynchronous programming in Rust <http://rust-lang-nursery.github.io/futures-rs>
- [rust-web-framework-comparison](https://github.com/flosse/rust-web-framework-comparison):A comparison of some web frameworks and libs written in Rust
- [How Rust Views Tradeoffs](https://www.infoq.com/presentations/rust-tradeoffs/)

- [RUST语言的编程范式](https://coolshell.cn/articles/20845.html)
- [并发篇](https://mp.weixin.qq.com/s/9g0wVT-5PpmXRoKJZo-skA)
- [安全篇](https://mp.weixin.qq.com/s/HCHYr5sWnEG_qOGE3hfNnQ)
- [网络篇](https://mp.weixin.qq.com/s/bOxEEK7Hh_tsua8HBahsjg)
- [并发原语](https://mp.weixin.qq.com/s/fJO-rCgL9N5fPvrqtHe9Ug)
- [编程语言](https://mp.weixin.qq.com/s/ZA-_BARVAWe0Q4eM0lYgwg)
- [RAII](https://mp.weixin.qq.com/s/jaKjzc_1rkDe67rfpnFTgg)
- [内存管理](https://mp.weixin.qq.com/s/1juaadR3AqHa8H19sHWHmQ)
- [泛型](https://mp.weixin.qq.com/s/SJsEurfZr4TG-I3rncid5A)
