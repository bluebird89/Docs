## [设计模式之美](https://time.geekbang.org/column/intro/250) 王争

- 看书效果
  - 比较偏重理论讲解，脱离真实开发
- 代码质量维度评判
  - 可维护性 maintainability
    - 代码易维护 在不破坏原有代码设计、不引入新 bug 的情况下，能够快速地修改或者添加代码
      - 代码分层清晰、模块化好、高内聚低耦合、遵从基于接口而非实现编程的设计原则
    - 代码不易维护 修改或者添加代码需要冒着极大的引入新 bug 的风险，并且需要花费很长的时间才能完成
  - 可读性 readability
    - 代码是否符合编码规范、命名是否达意、注释是否详尽、函数是否长短合适、模块划分是否清晰、是否符合高内聚低耦合等等
  - 可扩展性 extensibility
    - 在不修改或少量修改原有代码的情况下，通过扩展方式添加新功能代码
  - 灵活性 flexibility
    - 添加新功能代码的时候，原有代码已经预留好扩展点，不需要修改原有代码，只要在扩展点上添加新代码即可
    - 实现一个功能的时候，发现原有代码中，已经抽象出了很多底层可以复用模块、类等代码，可以拿来直接使用
    - 使用某组接口的时候，如果这组接口可以应对各种使用场景，满足各种不同的需求
  - 可复用性 reusability
    - 尽量减少重复代码的编写，复用已有的代码
  - 可测试性 testability

## 面向对象 Object Oriented Programming

- 面向对象编程 一种编程范式或编程风格。以类或对象作为组织代码的基本单元，并将封装、抽象、继承、多态四个特性，作为代码设计和实现的基石
  - 从字面上，按照最简单、最原始的方式来理解，就是将对象或类作为代码组织的基本单元，来进行编程的一种编程范式或者编程风格，并不一定需要封装、抽象、继承、多态这四大特性的支持。
  - 在进行面向对象编程的过程中，人们不停地总结发现，有了这四大特性，能更容易地实现各种面向对象的代码设计思路
- 面向对象编程语言 支持类或对象的语法机制，并有现成的语法机制，能方便地实现面向对象编程四大特性（封装、抽象、继承、多态）的编程语言
  - 只要某种编程语言支持类或对象的语法概念，并且以此作为组织代码的基本单元，那就可以被粗略地认为它就是面向对象编程语言了。至于是否有现成的语法机制，完全地支持了面向对象编程的四大特性、是否对四大特性有所取舍和优化，可以不作为判定的标准
- 一般来讲， 面向对象编程都是通过使用面向对象编程语言来进行的，但是，不用面向对象编程语言， 照样可以进行面向对象编程
- 面向对象分析（OOA） 面向对象设计（OOD）
- 分析和设计两个阶段最终产出是类的设计，包括程序被拆解为哪些类，每个类有哪些属性方法，类与类之间如何交互等等。比其他的分析和设计更加具体、更加落地、更加贴近编码，更能够顺利地过渡到面向对象编程环节。这也是面向对象分析和设计，与其他分析和设计最大不同点
- UML Unified Model Language
  - 《Java Modeling In Color With UML》
  - <https://app.zenuml.com>

### 特性

- 封装 Encapsulation 属性与操作隔离 隐藏信息、保护数据
  - 也叫作信息隐藏|数据访问保护
  - 类通过暴露有限访问接口，授权外部仅能通过类提供方式（或者叫函数）来访问内部信息或者数据
  - 属性作为数据自身属性，对调用方没有实际意义
  - 操作是对象的本质，对象的外部呈现
  - 需要编程语言本身提供一定的语法机制访问权限控制来支持
  - 意义
    - 任何代码都可以访问、修改类中的属性，影响代码可读性、可维护性
    - 类通过有限方法暴露必要操作，也能提高类的易用性
    - 把类属性都暴露给类的调用者
      - 调用者想要正确地操作这些属性，就势必要对业务细节有足够的了解。而这对于调用者来说也是一种负担。
      - 如果将属性封装起来，暴露少许的几个必要的方法给调用者使用，调用者就不需要了解太多背后的业务细节，用错的概率就减少很多
- 抽象 Abstraction 隐藏方法的具体实现
  - 让调用者只需要关心方法提供哪些功能，并不需要知道这些功能如何实现
  - 借助编程语言提供的接口类（比如 Java 中的 interface 关键字语法）或者抽象类（比如 Java 中的 abstract 关键字语法）语法机制来实现
  - 并不是一定要为实现类（PictureStorage）抽象出接口类（IPictureStorage），才叫作抽象。即便不编写 IPictureStorage 接口类，单纯的 PictureStorage 类本身就满足抽象特性
    - 类的方法是通过编程语言中的“函数”这一语法机制来实现的。
    - 通过函数包裹具体的实现逻辑，这本身就是一种抽象
    - 调用者在使用函数的时候，并不需要去研究函数内部的实现逻辑，只需要通过函数的命名、注释或者文档，了解其提供了什么功能，就可以直接使用了。比如，在使用 C 语言的 malloc() 函数时，并不需要了解它的底层代码是怎么实现的
    - 抽象概念是一个非常通用的设计思想，并不单单用在面向对象编程中，也可以用来指导架构设计等。而且这个特性也并不需要编程语言提供特殊的语法机制来支持，只需要提供“函数”这一非常基础的语法机制，就可以实现抽象特性、所以，没有很强的“特异性”，有时候并不被看作面向对象编程的特性之一。
  - 意义
    - 作为一种只关注功能点不关注实现的设计思路，帮大脑过滤掉许多非必要信息
    - 作为一个非常宽泛的设计思想，在代码设计中，起到非常重要的指导作用。很多设计原则都体现了抽象这种设计思想
  - 作为概念、理论的存在，不需要具体实践
- 继承 Inheritance
  - 单继承和多继承。单继承表示一个子类只继承一个父类，多继承表示一个子类可以继承多个父类
  - 意义
    - 代码复用
      - 并不是继承所独有的，可以通过其他方式来解决这个代码复用的问题，比如利用组合关系而不是继承关系
    - 通过继承来关联两个类，反应真实世界中的关系，非常符合人类认知，而且，从设计角度来说，也有一种结构美感
  - 过度使用继承
    - 继承层次过深过复杂，就会导致代码可读性、可维护性变差
    - 子类和父类高度耦合，修改父类的代码，会直接影响到子类
- 多态 Polymorphism
  - 子类可以替换父类，在实际代码运行过程中，调用子类方法实现
  - 继承加方法重写
    - 编程语言要支持继承  SortedDynamicArray 继承 DynamicArray，才能将 SortedDyamicArray 传递给 DynamicArray
    - 编程语言要支持子类可以重写（override）父类中方法  SortedDyamicArray 重写 DynamicArray 中 add() 方法
    - 支持父类对象可以引用子类对象，将 SortedDynamicArray 传递给 DynamicArray
  - 利用接口类语法
  - duck-typing 语法,只有一些动态语言才支持
    - Logger 和 DB 两个类没有任何关系，既不是继承关系，也不是接口和实现的关系，但是只要都有定义 record() 方法，就可以被传递到 test() 方法中，在实际运行的时候，执行对应的 record() 方法
    - 一些动态语言所特有的语法机制
  - 意义
    - 提高代码可扩展性和复用性 将不同集合类型（Array、LinkedList）传递给相同函数,只需要实现一个 print() 函数逻辑，就能应对各种集合数据打印操作

### 类间关系

- 泛化（Generalization） 继承关系
- 实现（Realization）接口和实现类之间关系
- 依赖（Dependency）一种比关联关系更加弱关系，包含关联关系
  - 不管是 B 类对象是 A 类对象的成员变量(聚合)
  - 还是 A 类方法使用 B 类对象作为参数或者返回值、局部变量(组合)
  - 只要 B 类对象和 A 类对象有任何使用关系
- 关联（Association）一种非常弱关系，包含聚合、组合两种关系
- 聚合（Aggregation）一种包含关系
  - A 类对象包含 B 类对象，B 类对象生命周期可以不依赖 A 类对象生命周期
  - 可以单独销毁 A 类对象而不影响 B 对象
- 组合（Composition）一种包含关系
  - A 类对象包含 B 类对象，B 类对象生命周期依赖 A 类对象生命周期，B 类对象不可单独存在
  - 被依赖类是否独立 被依赖类生成在依赖类内部还是外部，决定被依赖类生存周期

```java
public class A {
  private B b;
  public A(B b) {
    this.b = b;
  }
}


public class A {
  private B b;
  public A() {
    this.b = new B();
  }
}

public class A { 
	public void func(B b) { 
		... 
		}
}
```

### 面向对象编程 vs 面向过程编程

- 面向过程编程也是一种编程范式或编程风格。以过程（可以理解为方法、函数、操作）作为组织代码的基本单元，以数据（可以理解为成员变量、属性）与方法相分离为最主要的特点。
  - 面向过程风格是一种流程化的编程风格，通过拼接一组顺序执行的方法来操作数据完成一项功能。
- 面向过程编程语言首先是一种编程语言。最大特点是不支持类和对象两个语法概念，不支持丰富的面向对象编程特性（比如继承、多态、封装），仅支持面向过程编程。
- 最基本区别 代码组织方式不同
  - 面向过程风格代码被组织成了一组方法集合及其数据结构（struct User），方法和数据结构的定义是分开的。
  - 面向对象风格的代码被组织成一组类，方法和数据结构被绑定一起，定义在类中。
- 面向对象编程跟面向过程编程比起来优势
  - OOP 更加能够应对大规模复杂程序的开发
    - 需求足够简单，整个程序的处理流程只有一条主线，很容易被划分成顺序执行的几个步骤，然后逐句翻译成代码，这就非常适合采用面向过程这种面条式的编程风格来实现。
    - 进行面向对象编程的时候,先去思考如何给业务建模，如何将需求翻译为类，如何给类之间建立交互关系，而完成这些工作完全不需要考虑错综复杂的处理流程。当有了类的设计之后，然后再像搭积木一样，按照处理流程，将类组装起来形成整个程序。这种开发模式、思考问题的方式，在应对复杂程序开发的时候，思路更加清晰。
    - 面向对象编程还提供了一种更加清晰的、更加模块化的代码组织方式,类就是一种非常好的组织这些函数和数据结构的方式，是一种将代码模块化的有效手段。
    - 利用面向过程的编程语言照样可以写出面向对象风格的代码，只不过可能会比用面向对象编程语言来写面向对象风格的代码，付出的代价要高一些。而且，面向过程编程和面向对象编程并非完全对立的。很多软件开发中，尽管利用的是面向过程的编程语言，也都有借鉴面向对象编程的一些优点。
  - OOP 风格的代码更易复用、易扩展、易维护
    - 面向过程编程是一种非常简单的编程风格，并没有像面向对象编程那样提供丰富的特性。而面向对象编程提供的封装、抽象、继承、多态这些特性，能极大地满足复杂的编程需求，能方便我们写出更易复用、易扩展、易维护的代码。
    - 面向对象编程通过类这种组织代码的方式，将数据和方法绑定在一起，通过访问权限控制，只允许外部调用者通过类暴露的有限方法访问数据，而不会像面向过程编程那样，数据可以被任意方法随意修改。因此，面向对象编程提供的封装特性更有利于提高代码的易维护性。
    - 函数本身就是一种抽象，隐藏了具体的实现。在使用函数的时候，只需要了解函数具有什么功能，而不需要了解它是怎么实现的。从这一点上，不管面向过程编程还是是面向对象编程，都支持抽象特性。不过，面向对象编程还提供了其他抽象特性的实现方式。这些实现方式是面向过程编程所不具备的，比如基于接口实现的抽象。基于接口的抽象，可以在不改变原有实现的情况下，轻松替换新的实现逻辑，提高了代码的可扩展性。
    - 继承特性是面向对象编程相比于面向过程编程所特有的两个特性之一（另一个是多态）。如果两个类有一些相同的属性和方法，可以将这些相同的代码，抽取到父类中，让两个子类继承父类。这样两个子类也就可以重用父类中的代码，避免了代码重复写多遍，提高了代码的复用性。
    - 在需要修改一个功能实现的时候，可以通过实现一个新的子类的方式，在子类中重写原来的功能逻辑，用子类替换父类。在实际的代码运行过程中，调用子类新的功能逻辑，而不是在原有代码上做修改。这就遵从了“对修改关闭、对扩展开放”的设计原则，提高代码的扩展性。除此之外，利用多态特性，不同的类对象可以传递给相同的方法，执行不同的代码逻辑，提高了代码的复用性。
  - OOP 语言更加人性化、更加高级、更加智能
    - 跟二进制指令、汇编语言、面向过程编程语言相比，面向对象编程语言的编程套路、思考问题的方式，是完全不一样的。
    - 前三者是一种计算机思维方式，而面向对象是一种人类的思维方式。用前面三种语言编程的时候，在思考，如何设计一组指令，告诉机器去执行这组指令，操作某些数据，完成某个任务。
    - 在进行面向对象编程时候，在思考，如何给业务建模，如何将真实的世界映射为类或者对象，更加能聚焦到业务本身，而不是思考如何跟机器打交道。
    - 越高级编程语言离机器越“远”，离人类越“近”，越“智能”
- 看似面向对象，实际是面向过程编程风格代码
  - 滥用 getter、setter 方法
    - 违反面向对象编程的封装特性，相当于将面向对象编程风格退化成了面向过程编程风格
    - 属性不一致
    - 在设计实现类的时候，除非真的需要，否则，尽量不要给属性定义 setter 方法。除此之外，尽管 getter 方法相对 setter 方法要安全些，但是如果返回的是集合容器（比如例子中的 List 容器），也要防范集合内部数据被修改的危险
  - 滥用全局变量和全局方法
    - 常见全局变量
      - 单例类对象在全局代码中只有一份，所以，相当于一个全局变量
      - 静态成员变量归属于类上的数据，被所有的实例化对象所共享，也相当于一定程度上的全局变量
      - 常量是一种非常常见的全局变量，比如一些代码中的配置参数，一般都设置为常量，放到一个 Constants 类中
        - 定义一个如此大而全的 Constants 类,把程序中所有用到常量，都集中地放到这个 Constants 类中
          - 影响代码可维护性
          - 增加代码编译时间
          - 影响代码的复用性
        - 改进
          - 将 Constants 类拆解为功能更加单一多个类
          - 并不单独地设计 Constants 常量类，而是哪个类用到某个常量，就把这个常量定义到这个类中
    - 常见全局方法
      - 静态方法一般用来操作静态变量或者外部数据
      - 联想一下常用各种 Utils 类，里面方法一般都会定义成静态方法，可以在不用创建对象情况下，直接拿来使用
        - 仅仅为了代码复用，生硬地抽象出一个父类出来（并不具有继承关系），会影响到代码的可读性
        - 只包含静态方法不包含任何属性的 Utils 类，是彻彻底底的面向过程的编程风格
        - 在软件开发中还是挺有用的，能解决代码复用问题。所以，并不是说完全不能用 Utils 类，而是要尽量避免滥用，不要不加思考地随意去定义 Utils 类
        - 不要设计一个过于大而全的 Utils 类，针对不同的功能，设计不同的 Utils 类
      - 静态方法将方法与数据分离，破坏了封装特性，是典型面向过程风格
    - 定义数据和方法分离的类
      - 数据定义在一个类中，方法定义在另一个类中
      - 基于 MVC 三层结构做 Web 方面后端开发中天天都在写
        - Controller 层负责暴露接口给前端调用
        - Service 层负责核心业务逻辑
        - Repository 层负责数据读写
        - 在每一层会定义相应 VO（View Object）、BO（Business Object）、Entity
        - 一般情况下，VO、BO、Entity 中只会定义数据，不会定义方法，所有操作这些数据业务逻辑都定义在对应的 Controller 类、Service 类、Repository 类中
        - 是典型面向过程的编程风格。这种开发模式叫作基于贫血模型开发模式，也是现在非常常用的一种 Web 项目的开发模式
- 面向对象编程中，为什么容易写出面向过程风格的代码
  - 面向过程编程风格恰恰符合人流程化思维方式，应该先做什么、后做什么，如何一步一步地顺序执行一系列操作，最后完成整个任务
  - 面向对象编程风格是一种自底向上的思考方式，不是先去按照执行流程来分解任务，而是将任务翻译成一个一个小的模块（也就是类），设计类之间的交互，最后按照流程将类组装起来，完成整个任务
  - 在面向对象编程中，类的设计需要技巧，一定设计经验的。要去思考如何封装合适的数据和方法到一个类里，如何设计类之间的关系，如何设计类之间的交互等等诸多设计问题
- 面向过程编程是面向对象编程的基础，面向对象编程离不开基础的面向过程编程
- 最终目的是写出易维护、易读、易复用、易扩展高质量代码
  - 只要能避免面向过程编程风格的一些弊端，控制好它的副作用，在掌控范围内为我们所用，就大可不用避讳在面向对象编程中写面向过程风格的代码

### 接口和抽象类

- 接口
  - 不能包含属性（也就是成员变量）
  - 只能声明方法，方法不能包含代码实现
  - 类实现接口，必须实现接口中声明所有方法
  - 实现面向对象的抽象特性、多态特性和基于接口而非实现设计原则
  - 侧重于解耦
    - 接口是对行为的一种抽象，相当于一组协议或者契约
    - 调用者只需要关注抽象接口，不需要了解具体实现，具体实现代码对调用者透明
    - 实现了约定和实现相分离，可以降低代码间的耦合性，提高代码的可扩展性
- 抽象类
  - 不允许被实例化，只能被继承
  - 可以包含属性和方法。方法既可以包含代码实现，也可以不包含代码实现（抽象方法）
  - 子类继承抽象类，必须实现抽象类中所有抽象方法
  - 实现面向对象的继承特性和模板设计模式等等
  - 继承+多态
    - 可以用继承加重写方法实现，没有通过抽象类的实现思路优雅
      - 可读性
      - 抽象类继承中，编译器会强制要求子类重写
- 抽象类实际上就是类，只不过是一种特殊类，不能被实例化为对象，只能被子类继承。表示一种 is-a 的继承关系
- 接口表示一种 has-a 关系，表示具有某些功能。对于接口，有一个更加形象的叫法，那就是协议（contract）
- C++ 只支持抽象类，不支持接口；Python 既不支持抽象类，也不支持接口，可以通过一些手段来模拟实现这两个语法概念
  - 用普通类来模拟接口
    - 让类中方法抛出 MethodUnSupportedException 异常，来模拟不包含实现的接口，并且能强迫子类在继承这个父类的时候，都去主动实现父类的方法，否则就会在运行时抛出异常
    - 将构造函数设置成 protected 属性的，这样就能避免非同包下的类去实例化 MockInterface。不过，这样还是无法避免同包中的类去实例化 MockInterface。为了解决这个问题，我们可以学习 Google Guava 中 @VisibleForTesting 注解的做法，自定义一个注解，人为表明不可实例化。
- 决定该用抽象类还是接口
  - 标准
    - 如果要表示一种 is-a 的关系，并且是为了解决代码复用问题，用抽象类
    - 如果要表示一种 has-a 关系，并且是为了解决抽象而非代码复用问题，用接口
  - 抽象类是一种自下而上设计思路，先有子类代码重复，然后再抽象成上层的父类（也就是抽象类）
  - 接口是一种自上而下的设计思路。一般都是先设计接口，再去考虑具体实现

```c++
class Strategy { // 用抽象类模拟接口
  public:
    ~Strategy();
    virtual void algorithm()=0;
  protected:
    Strategy();
};
```

```java
// 用普通类来模拟接口
public class MockInteface {
  protected MockInteface() {}
  public void funcA() {
    throw new MethodUnSupportedException();
  }
}
```

### 基于接口而非实现编程

- 另一个表述方式 基于抽象而非实现编程
- 将接口和实现相分离，封装不稳定实现，暴露稳定接口
  - 上游系统面向接口而非实现编程，不依赖不稳定实现细节，当实现发生变化的时候，上游系统的代码基本上不需要做改动，以此来降低耦合性，提高扩展性
- 越抽象、越顶层、越脱离具体某一实现的设计，越能提高代码的灵活性，越能应对未来的需求变化。好的代码设计，不仅能应对当下的需求，而且在将来需求发生变化的时候，仍然能够在不破坏原有代码设计的情况下灵活应对
- 基于实现编程问题
  - 暴露实现细节->函数命名不能暴露任何实现细节
  - 流程的固化->封装具体实现细节
- 基于接口
  - 为实现类定义抽象接口
  - 具体实现类依赖统一接口定义，遵从一致功能协议。使用者依赖接口，而不是具体实现类来编程
  - 通过实现类来反推接口定义 导致接口定义不够抽象，依赖具体实现
- 过度应用 为每一个实现类都定义对应的接口
  - 需要不需要定义接口 回归到设计原则初衷
  - 某个功能只有一种实现方式，未来也不可能被其他实现方式替换，就没有必要为其设计接口，也没有必要基于接口编程，直接使用实现类就可以
- 越是不稳定系统，越是要在代码的扩展性、维护性上下功夫。相反，如果某个系统特别稳定，在开发完之后，基本上不需要做维护，那我们就没有必要为其扩展性，投入不必要的开发时间。
- 不同实现如何切换
  - 配置文件+工厂模式
  - 反射
  - 依赖注入，从外部构建具体类的对象，传入使用的地方

### 多用组合少用继承

- 继承缺点
  - 继承层次过深、过复杂，也会影响到代码的可读性和可维护性
  - 继承类不具有父类定义的某个方法
    - 子类中重写（override）方法，抛出 UnSupportedMethodException 异常
      - 违背最小知识原则（Least Knowledge Principle 最少知识原则|者迪米特法则），暴露不该暴露的接口给外部，增加了类使用过程中被误用概率
    - 加一层抽象接口进行区分，每一个特性的区分都加一层，复杂度比较高了
- 组合优势
  - 通过组合（composition）、接口、委托（delegation）替换掉继承
  - is-a 关系 通过组合和接口 has-a 关系来替代
  - 多态 利用接口来实现
  - 代码复用 通过组合和委托来实现
  - 组合 打掉复杂继承关系，细颗粒度的拆分，灵活使用，注入其他依赖
- 判断
  - 继承改写成组合意味着要做更细粒度的类的拆分
  - 继类之间的继承结构稳定（不会轻易改变），继承层次比较浅（比如，最多有两层继承关系），继承关系不复杂，就可以大胆地使用继承
  - 系统越不稳定，继承层次很深，继承关系复杂，就尽量使用组合来替代继承

```java
public interface Flyable {
  void fly()；
}

public class FlyAbility implements Flyable {
  @Override
  public void fly() { //... }
}
	
//省略Tweetable/TweetAbility/EggLayable/EggLayAbility

public class Ostrich implements Tweetable, EggLayable {//鸵鸟
  private TweetAbility tweetAbility = new TweetAbility(); //组合
  private EggLayAbility eggLayAbility = new EggLayAbility(); //组合
  //... 省略其他属性和方法...
  @Override
  public void tweet() {
    tweetAbility.tweet(); // 委托
  }
  @Override
  public void layEgg() {
    eggLayAbility.layEgg(); // 委托
  }
}
```

### 面向过程的贫血模型和面向对象的充血模型

- 贫血模型 Anemic Domain Model
  - 像 UserBo 这样，只包含数据，不包含业务逻辑的类
  - 将数据与操作分离，破坏了面向对象封装特性，一种典型面向过程编程风格
  - 数据结构给框死了，改动难度成本高
- 充血模型 Rich Domain Model
  - 数据和对应的业务逻辑被封装到同一个类中
- 基于贫血模型
  - 数据访问层  Repository+Entity
  - 业务逻辑层 Service+BO(Business Object)
    - Service 层的数据和业务逻辑，被分割为 BO 和 Service 两个类中
  - 暴露接口层 Controller+VO(View Object)
  - 实际上是一种面向过程的编程风格
  - 受欢迎
    - 开发的系统业务可能都比较简单，简单到就是基于 SQL 的 CRUD 操作，根本不需要动脑子精心设计充血模型，贫血模型就足以应付这种简单业务的开发工作
    - 充血模型设计要比贫血模型更加有难度。充血模型是一种面向对象编程风格。从一开始就要设计好针对数据要暴露哪些操作，定义哪些业务逻辑。而不是像贫血模型那样，只需要定义数据，之后有什么功能开发需求，在 Service 层定义什么操作，不需要事先做太多设计。
    - 思维已固化，转型有成本
- 基于充血模型领域驱动设计 Domain Driven Design DDD
  - 用来指导如何解耦业务系统，划分业务模块，定义业务领域模型及其交互
  - 被大众熟知，基于微服务念的兴起，用来指导划分服务
  - 有点儿类似敏捷开发、SOA、PAAS 等概念，听起来很高大上，但实际上只值“五分钱”
  - 关键 对所做业务熟悉程度，而并不是对领域驱动设计这个概念本身掌握程度。即便对领域驱动搞得再清楚，但是对业务不熟悉，也并不一定能做出合理的领域设计。所以，不要把领域驱动设计当银弹，不要花太多的时间去过度地研究它
  - 也是按照 MVC 三层架构分层的，跟基于贫血模型的传统开发模式的区别主要在 Service 层
  - Service 层包含 Service 类和 Domain 类两部分。Domain 相当于贫血模型中 BO。Domain 与 BO 区别在于基于充血模型开发，既包含数据，也包含业务逻辑。而 Service 类变得非常单薄
  - 场景
    - 非常重要区别 两种不同的开发模式会导致不同的开发流程
      - 基于充血模型的 DDD 开发模式开发流程，在应对复杂业务系统的开发的时候更加有优势
      - 平时开发大部分都是 SQL 驱动（SQL-Driven）开发模式
        - 接到后端接口开发需求，去看接口需要数据对应到数据库中，需要哪张表或者哪几张表
        - 思考如何编写 SQL 语句来获取数据。之后就是定义 Entity、BO、VO
        - 模板式地往对应 Repository、Service、Controller 类中添加代码
        - 业务逻辑包裹在一个大的 SQL 语句中，而 Service 层可以做的事情很少。SQL 都是针对特定的业务功能编写的，复用性差
    - 基于充血模型的 DDD 开发模式
      - 需要事先理清楚所有的业务，定义领域模型所包含的属性和方法。
      - 领域模型相当于可复用业务中间层。新功能需求开发都基于之前定义好的领域模型来完成
  - 需要支持更复杂业务逻辑时，充血模型优势就显现出来
  - 将业务逻辑移动到 Domain 中，Service 类变得很薄，并没有完全将 Service 类去掉
    - 让 Service 类负责与 Repository 交流，不是让领域模型 与 Repository 打交道，保持领域模型的独立性，不与任何其他层代码（Repository 层的代码）或开发框架（比如 Spring、MyBatis）耦合，将流程性代码逻辑（比如从 DB 中取数据、映射数据）与领域模型的业务逻辑解耦，让领域模型更加可复用
    - Service 类负责跨领域模型的业务聚合功能
    - Service 类负责一些非功能性及与三方系统交互的工作。比如幂等、事务、发邮件、发消息、记录日志、调用其他系统的 RPC 接口等，都可以放到 Service 类中
- 基于贫血模型的传统开发模式，重 Service 轻 BO；基于充血模型的 DDD 开发模式，轻 Service 重 Domain
  - Service 层被改造成充血模型，Controller 层和 Repository 层还是贫血模型，是否有必要也进行充血领域建模
    - Controller 层主要负责接口暴露，Repository 层主要负责与数据库打交道，这两层包含的业务逻辑并不多，如果业务逻辑比较简单，就没必要做充血建模，即便设计成充血模型，类也非常单薄
    - 面向过程编程风格的副作用
      - Repository 的 Entity 即便被设计成贫血模型，违反面向对象编程的封装特性，有被任意代码修改数据的风险，但 Entity 的生命周期是有限的。传递到 Service 层之后，就会转化成 BO 或者 Domain 来继续后面的业务逻辑。Entity 的生命周期到此就结束了，所以也并不会被到处任意修改
      - Controller 层的 VO 实际上是一种 DTO（Data Transfer Object，数据传输对象）。主要作为接口的数据传输承载体，将数据发送给其他系统。从功能上来讲，理应不包含业务逻辑、只包含数据

```java
public class VirtualWallet { // Domain领域模型(充血模型)
  private Long id;
  private Long createTime = System.currentTimeMillis();;
  private BigDecimal balance = BigDecimal.ZERO;
  
  public VirtualWallet(Long preAllocatedId) {
    this.id = preAllocatedId;
  }
  
  public BigDecimal balance() {
    return this.balance;
  }
  
  public void debit(BigDecimal amount) {
    if (this.balance.compareTo(amount) < 0) {
      throw new InsufficientBalanceException(...);
    }
    this.balance = this.balance.subtract(amount);
  }
  
  public void credit(BigDecimal amount) {
    if (amount.compareTo(BigDecimal.ZERO) < 0) {
      throw new InvalidAmountException(...);
    }
    this.balance = this.balance.add(amount);
  }
}


public class VirtualWalletService {
  // 通过构造函数或者IOC框架注入
  private VirtualWalletRepository walletRepo;
  private VirtualWalletTransactionRepository transactionRepo;
  
  public VirtualWallet getVirtualWallet(Long walletId) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet = convert(walletEntity);
    return wallet;
  }
  
  public BigDecimal getBalance(Long walletId) {
    return walletRepo.getBalance(walletId);
  }
  
  @Transactional
  public void debit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet = convert(walletEntity);
    wallet.debit(amount);
    VirtualWalletTransactionEntity transactionEntity = new VirtualWalletTransactionEntity();
    transactionEntity.setAmount(amount);
    transactionEntity.setCreateTime(System.currentTimeMillis());
    transactionEntity.setType(TransactionType.DEBIT);
    transactionEntity.setFromWalletId(walletId);
    transactionRepo.saveTransaction(transactionEntity);
    walletRepo.updateBalance(walletId, wallet.balance());
  }
  
  @Transactional
  public void credit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet = convert(walletEntity);
    wallet.credit(amount);
    VirtualWalletTransactionEntity transactionEntity = new VirtualWalletTransactionEntity();
    transactionEntity.setAmount(amount);
    transactionEntity.setCreateTime(System.currentTimeMillis());
    transactionEntity.setType(TransactionType.CREDIT);
    transactionEntity.setFromWalletId(walletId);
    transactionRepo.saveTransaction(transactionEntity);
    walletRepo.updateBalance(walletId, wallet.balance());
  }

  @Transactional
  public void transfer(Long fromWalletId, Long toWalletId, BigDecimal amount) {
    //...跟基于贫血模型的传统开发模式的代码一样...
  }
}
```

### 实例 接口调用鉴权功能

- 明确需求
  - 面向对象分析主要分析对象是“需求”，可以粗略地看成“需求分析”
  - 首先要做的都是将笼统需求细化到足够清晰、可执行
  - 通过沟通、挖掘、分析、假设、梳理，搞清楚具体的需求有哪些，哪些是现在要做的，哪些是未来可能要做的，哪些是不用考虑做的
  - 从最简单方案想起，然后再优化
  - 通过应用名+密码做认证
    - 给每个允许访问服务调用方，派发一个应用名（或者叫应用 ID、AppID）和一个对应密码（或者叫秘钥）
    - 调用方每次进行接口请求时携带自己 AppID 和密码
    - 微服务在接收到接口调用请求后解析出 AppID 和密码，跟存储在微服务端 AppID 和密码进行比对。如果一致，说明认证成功，则允许接口调用请求；否则拒绝接口调用请求
  - 应对重放攻击 提出问题再解决问题，是一个非常好的迭代优化方法
    - 借助 OAuth 验证思路 隐藏密码、不可逆加密与比对
    - 调用方将请求接口 URL 跟 AppID、密码拼接在一起，然后进行加密，生成一个 token。进行接口请求时，将这个 token 及 AppID，随 URL 一块传递给微服务端
    - 微服务端接收到数据后，根据 AppID 从数据库中取出对应密码，并通过同样生成算法，生成 token
    - 用新生 token 跟调用方传递 token 对比，一致允许接口调用请求。否则拒绝接口调用请求
  - URL 拼接上 AppID、密码生成 token 是固定，还是可以通过重放攻击方式，伪装成认证系统，调用这个 URL 对应接口
    - 进一步优化 token 生成算法，引入一个随机变量，让每次接口请求生成的 token 都不一样
    - 将 URL、AppID、密码、时间戳四者进行加密来生成 token。调用方接口请求时将 token、AppID、时间戳，随 URL 一并传递给微服务端
    - 微服务端收到数据后，验证当前时间戳跟传递过来时间戳，是否在一定时间窗口内（比如一分钟）。如果超过一分钟，则判定 token 过期，拒绝接口请求。如果没有超过一分钟，执行上轮逻辑
    - 未认证系统还是可以在一分钟 token 失效窗口内，通过截获请求、重放请求调用接口
      - 攻与防之间本来就没有绝对的安全。能做的就是尽量提高攻击的成本
      - 这个方案虽然有漏洞，但实现起来足够简单，而且不会过度影响接口本身的性能（比如响应时间）
      - @TODO 微服务端存储每个授权调用方的 AppID 和密码 开发像鉴权这样的非业务功能，最好不要与具体的第三方系统有过度的耦合
  - 确定需求 用什么描述不是重点，描述清楚才是最重要的。基于文字版本需求描述，来进行类、属性、方法、交互等的设计
    - 调用方进行接口请求时，将 URL、AppID、密码、时间戳拼接在一起，通过加密算法生成 token，并且将 token、AppID、时间戳拼接在 URL 中，一并发送到微服务端
    - 微服务端接收到调用方接口请求后，从请求中拆解出 token、AppID、时间戳。首先检查传递过来时间戳跟当前时间，是否在 token 失效时间窗口内
    - 如果已经超过失效时间，那就算接口调用鉴权失败，拒绝接口调用请求。如果 token 验证没有过期失效，微服务端从自己存储中，取出 AppID 对应密码，通过同样 token 生成算法，生成另外一个 token，与调用方传递过来 token 进行匹配；如果一致，则鉴权成功，允许接口调用，否则就拒绝接口调用
- 面向对象设计（OOD） 设计产出是类
  - 划分职责进而识别出有哪些类
    - 类是现实世界中事物一个建模。但并不是每个需求都能映射到现实世界，也并不是每个类都与现实世界中事物一一对应，对于一些抽象的概念是无法通过映射现实世界中的事物的方式来定义类的
    - 一种识别类方法 把需求描述中名词罗列出来，作为可能候选类，然后再进行筛选
    - 另外一种方根据需求描述，把其中涉及功能点一个一个罗列出来，再去看哪些功能点职责相近，操作同样属性，是否应该归为同一个类
    - 功能点列表
      1. 把 URL、AppID、密码、时间戳拼接为一个字符串
      2. 对字符串通过加密算法加密生成 token
      3. 将 token、AppID、时间戳拼接到 URL 中，形成新的 URL
      4. 解析 URL，得到 token、AppID、时间戳等信息
      5. 从存储中取出 AppID 和对应的密码
      6. 根据时间戳判断 token 是否过期失效
      7. 验证两个 token 是否匹配
    - 根据功能点可以粗略得到三个核心类
      - 1、2、6、7 都跟 token 有关，负责 token 的生成、验证
      - 3、4 都在处理 URL，负责 URL 拼接、解析
      - 5 操作 AppID 和密码，负责从存储中读取 AppID 和密码
      - AuthToken 负责实现 1、2、6、7 操作
      - Url=> ApiReques 负责 3、4 操作
      - CredentialStorage 负责 5 操作
    - 针对复杂需求开发，首先进行模块划分，将需求简单划分成几个小的、独立功能模块，然后再在模块内部，应用刚讲方法，进行面向对象设计。而模块划分和识别，跟类划分和识别，是类似的套路
  - 定义类及其属性和方法
    - 方法识别  将功能点=>方法，识别出需求描述中动词作为候选方法，再进一步过滤筛选
    - 并不是所有出现名词都被定义为类的属性（业务模型是否归属），可能是参数
    - 需要挖掘一些没有出现在功能点描述中属性
    - 从业务模型上理应具有哪些属性和方法。一方面保证类定义完整性，另一方面不仅为当下需求，还为未来需求做准备
  - 定义类与类之间交互关系
    - 实现关系  CredentialStorage 和 MysqlCredentialStorage 之间关系
  - 将类组装并提供执行入口
    - 接口鉴权并不是一个独立运行系统，而是一个集成在系统上运行的组件，所以，封装所有实现细节，设计一个最顶层 ApiAuthenticator 接口类，暴露一组给外部调用者使用的 API 接口，作为触发执行鉴权逻辑的入口
- 在写代码之前，花很多时间做分析和设计，绘制出完美类图、UML 图，也不可能把每个细节、交互都想得很清楚。落实代码时候，还是要反复迭代、重构、打破重写

## 设计原则

- “看懂”和“会用”是两回事，而“用好”更是难上加难
- 使用时候过于教条主义，拿原则当真理，生搬硬套，适得其反
  - 定义->设计的初衷->解决哪些问题->哪些应用场景

### SRP Single Responsibility Principle 单一职责原则

- A class or module should have a single responsibility
  - 把模块看作比类更加抽象概念，类也可以看作模块
  - 把模块看作比类更加粗粒度代码块，模块中包含多个类，多个类组成一个模块
  - 越抽象越模糊
- 一个类只负责完成一个职责或者功能 反向理解
  - 不要设计大而全的类，要设计粒度小、功能单一的类
  - 一个类包含两个或者两个以上业务不相干功能，就说职责不够单一，应该将它拆分成多个功能更加单一、粒度更细的类
- 不同应用场景、不同阶段需求背景下，对同一个类的职责是否单的判定，可能都是不一样的
  - 在某种应用场景或者当下需求背景下，一个类的设计可能已经满足单一职责原则
  - 但如果换个应用场景或着在未来的某个需求背景下，可能就不满足了，需要继续拆分成粒度更细的类脱离具体应用场景
- 从不同业务层面去看待同一个类的设计，对类是否职责单一，也会有不同认识
  - 从“用户”业务层面来看，UserInfo 包含信息都属于用户，满足职责单一原则
  - 从更加细分“用户展示信息”“地址信息”“登录认证信息”等等这些更细粒度业务层面来看，那 UserInfo 就应该继续拆分
- 真正软件开发中没必要过于未雨绸缪，过度设计
  - 可以先写一个粗粒度的类，满足业务需求
  - 持续重构  随着业务发展，如果粗粒度类越来越庞大，代码越来越多，可以将粗粒度类，拆分成几个更细粒度类
- 更有指导意义、更具有可执行性判断原则
  - 类中代码行数、函数或属性过多，会影响代码可读性和可维护性,一个类的代码行数最好不能超过 200 行，函数个数及属性个数都最好不要超过 10 个
  - 类依赖其他类过多，或者依赖类其他类过多，不符合高内聚、低耦合设计思想
  - 私有方法过多，就要考虑能否将私有方法独立到新的类中，设置为 public 方法，供更多的类使用，从而提高代码的复用性
  - 比较难给类起一个合适名字，很难用一个业务名词概括，或者只能用一些笼统 Manager、Context 之类词语来命名，说明类职责定义得可能不够清晰
  - 类中大量方法都是集中操作类中某几个属性，比如，在 UserInfo 例子中，如果一半方法都是在操作 address 信息，就可以考虑将这几个属性和对应的方法拆分出来
- 类职责是否设计得越单一越好
  - 内聚性丢失，可维护性变差

### OCP Open Closed Principle 开闭原则 对扩展开放、修改关闭

- software entities (modules, classes, functions, etc.) should be open for extension , but closed for modification
- 添加一个新功能应该在已有代码基础上扩展代码（新增模块、类、方法等），而非修改已有代码（修改模块、类、方法等）
- 设计初衷 只要没有破坏原有代码的正常运行，没有破坏原有的单元测试
- 添加功能 当每秒钟接口超时请求个数超过预先设置最大阈值时，也要触发告警发送通知
  - 将 check() 函数的多个入参封装成 ApiStatInfo 类
  - handler 概念，将 if 判断逻辑分散在各个 handler 中
  - 改动
    - 在 ApiStatInfo 类中添加新的属性 timeoutCount 给类中添加新属性和方法
      - 同样代码改动，在粗代码粒度下，被认定为“修改”，在细代码粒度下，又可以被认定为“扩展”
      - 添加属性和方法相当于修改类，在类这个层面，这个代码改动可以被认定为“修改”
      - 并没有修改已有属性和方法，在方法（及其属性）这一层面，又可以被认定为“扩展”
    - 添加新 TimeoutAlertHander 类
    - ApplicationContext 类 initializeBeans() 方法中，往 alert 对象中注册新的timeoutAlertHandler
      - 核心逻辑集中在 Alert 类及其各个 handler 中，添加新告警逻辑，Alert 类完全不需要修改，而只需要扩展一个新 handler 类
    - 使用 Alert 类时候，给 check() 函数入参 apiStatInfo 对象设置 timeoutCount 值
- How
  - 开闭原则讲的就是代码扩展性问题，是判断一段代码是否易扩展的“金标准”
  - 指导思想 为尽量写出扩展性好的代码，要时刻具备扩展意识、抽象意识、封装意识
    - 写代码时要多花点时间往前多思考一下，这段代码未来可能有哪些需求变更、如何设计代码结构，事先留好扩展点，以便在未来需求变更的时候，不需要改动代码整体结构、做到最小代码改动情况下，新代码能够很灵活地插入到扩展点上，做到“对扩展开放、对修改关闭”
    - 识别出代码可变部分和不可变部分之后，要将可变部分封装起来，隔离变化，提供抽象化不可变接口，给上层系统使用。当具体实现发生变化的时候，只需要基于相同抽象接口，扩展一个新实现，替换掉老实现即可，上游系统代码几乎不需要修改
  - 具体方法论
    - 最常用来提高代码扩展性方法：多态、依赖注入、基于接口而非实现编程以及抽象意识，以及大部分设计模式（比如，装饰、策略、模板、职责链、状态等）
- 项目中灵活应用
  - 关键 预留扩展点
  - 业务导向的系统 了解当下以及未来可能要支持的业务需求
  - 跟业务无关的、通用的、偏底层的系统 要了解“会被如何使用？今后打算添加哪些功能？使用者未来会有哪些更多的功能需求？
  - 对于比较确定的、短期内可能就会扩展，或者需求改动对代码结构影响比较大情况，或者实现成本不高扩展点，在编写代码时候就可以事先做些扩展性设计。
  - 对于一些不确定未来是否要支持需求，或者实现起来比较复杂扩展点，可以等到有需求驱动的时候，再通过重构代码的方式来支持扩展的需求
  - 代码扩展性会跟可读性相冲突

```java
public class Alert {
  private AlertRule rule;
  private Notification notification;

  public Alert(AlertRule rule, Notification notification) {
    this.rule = rule;
    this.notification = notification;
  }

  public void check(String api, long requestCount, long errorCount, long durationOfSeconds) {
    long tps = requestCount / durationOfSeconds;
    if (tps > rule.getMatchedRule(api).getMaxTps()) {
      notification.notify(NotificationEmergencyLevel.URGENCY, "...");
    }
    if (errorCount > rule.getMatchedRule(api).getMaxErrorCount()) {
      notification.notify(NotificationEmergencyLevel.SEVERE, "...");
    }
  }
}

// 重构
public class Alert {
  private List<AlertHandler> alertHandlers = new ArrayList<>();
  
  public void addAlertHandler(AlertHandler alertHandler) {
    this.alertHandlers.add(alertHandler);
  }

  public void check(ApiStatInfo apiStatInfo) {
    for (AlertHandler handler : alertHandlers) {
      handler.check(apiStatInfo);
    }
  }
}

public class ApiStatInfo {//省略constructor/getter/setter方法
  private String api;
  private long requestCount;
  private long errorCount;
  private long durationOfSeconds;
  private long timeoutCount; // 改动一：添加新字段
}

public abstract class AlertHandler {
  protected AlertRule rule;
  protected Notification notification;
  public AlertHandler(AlertRule rule, Notification notification) {
    this.rule = rule;
    this.notification = notification;
  }
  public abstract void check(ApiStatInfo apiStatInfo);
}

public class TpsAlertHandler extends AlertHandler {
  public TpsAlertHandler(AlertRule rule, Notification notification) {
    super(rule, notification);
  }

  @Override
  public void check(ApiStatInfo apiStatInfo) {
    long tps = apiStatInfo.getRequestCount()/ apiStatInfo.getDurationOfSeconds();
    if (tps > rule.getMatchedRule(apiStatInfo.getApi()).getMaxTps()) {
      notification.notify(NotificationEmergencyLevel.URGENCY, "...");
    }
  }
}

public class ErrorAlertHandler extends AlertHandler {
  public ErrorAlertHandler(AlertRule rule, Notification notification){
    super(rule, notification);
  }

  @Override
  public void check(ApiStatInfo apiStatInfo) {
    if (apiStatInfo.getErrorCount() > rule.getMatchedRule(apiStatInfo.getApi()).getMaxErrorCount()) {
      notification.notify(NotificationEmergencyLevel.SEVERE, "...");
    }
  }
}
public class TimeoutAlertHandler extends AlertHandler {//省略代码...}
	
// 应用
public class ApplicationContext {
  private AlertRule alertRule;
  private Notification notification;
  private Alert alert;
  
  public void initializeBeans() {
    alertRule = new AlertRule(/*.省略参数.*/); //省略一些初始化代码
    notification = new Notification(/*.省略参数.*/); //省略一些初始化代码
	  
    alert = new Alert();
    alert.addAlertHandler(new TpsAlertHandler(alertRule, notification));
	alert.addAlertHandler(new ErrorAlertHandler(alertRule, notification));
    alert.addAlertHandler(new ErrorAlertHandler(alertRule, notification));
  }
	
  public Alert getAlert() { return alert; }

  // 饿汉式单例
  private static final ApplicationContext instance = new ApplicationContext();
  private ApplicationContext() {
    initializeBeans();
  }
  public static ApplicationContext getInstance() {
    return instance;
  }
}

public class Demo {
  public static void main(String[] args) {
    ApiStatInfo apiStatInfo = new ApiStatInfo();
    apiStatInfo.setTimeoutCount(289);
    ApplicationContext.getInstance().getAlert().check(apiStatInfo);
  }
}
```

### LSP Liskov Substitution Principle 里式替换原则

- 1986 年由 Barbara Liskov 提出 If S is a subtype of T, then objects of type T may be replaced with objects of type S, without breaking the program
- 1996 年，Robert Martin 在他的 SOLID 原则中，重新描述  Functions that use pointers of references to base classes must be able to use objects of derived classes without knowing it。
- 关注的角度是不一样
  - 多态是面向对象编程的一大特性，也是面向对象编程语言的一种语法。是一种代码实现思路。
  - 里式替换是一种设计原则，用来指导继承关系中子类该如何设计，子类设计要保证在替换父类的时候，不改变原有程序逻辑以及不破坏原有程序正确性
- Design By Contract
  - 子类可以改变函数内部实现逻辑，但不能改变函数原有行为约定包括：函数声明要实现功能；对输入、输出、异常约定；甚至包括注释中所罗列任何特殊说明

### ISP Interface Segregation Principle 接口隔离原则

- Clients should not be forced to depend upon interfaces that they do not use。
- “客户端” 接口的调用者或者使用者
  - 确定客户端需不需要
- 功能以接口形式做不同实现，通用、复用性好

### DIP 依赖倒置原则

- 控制反转  Inversion Of Control IOC
  - 控制 指对程序执行流程控制
  - 反转 指在没有使用框架前，程序控制整个程序执行。使用后，整个程序执行流程可以通过框架来控制。
  - 流程控制权从程序员“反转”到框架
- 类似于模板设计模式 doTest() => JunitApplication::main()

```java
// original
public class UserServiceTest {
  public static boolean doTest() {
    // ... 
  }
  
  public static void main(String[] args) {//这部分逻辑可以放到框架中
    if (doTest()) {
      System.out.println("Test succeed.");
    } else {
      System.out.println("Test failed.");
    }
  }
}

// IOC
public abstract class TestCase {
  public void run() {
    if (doTest()) {
      System.out.println("Test succeed.");
    } else {
      System.out.println("Test failed.");
    }
  }
  
  public abstract boolean doTest();
}

public class JunitApplication {
  private static final List<TestCase> testCases = new ArrayList<>();
  
  public static void register(TestCase testCase) {
    testCases.add(testCase);
  }
  
  public static final void main(String[] args) {
    for (TestCase case: testCases) {
      case.run();
    }
  }

public class UserServiceTest extends TestCase {
  @Override
  public boolean doTest() {
    // ... 
  }
}

// 注册操作还可以通过配置的方式来实现，不需要程序员显示调用register()
JunitApplication.register(new UserServiceTest();
```

- 依赖注入 Dependency Injection DI
  - 依赖注入是一个标价 25 美元，实际上只值 5 美分的概念
  - 不通过 new() 方式在类内部创建依赖类对象，而是将依赖类对象在外部创建好之后，通过构造函数、函数参数等方式传递（或注入）给类使用
  - 将依赖类对象传递进来，提高代码扩展性，可以灵活地替换依赖类
  - 优化 把 MessageSender 定义成接口，基于接口而非实现编程

```java

// 非依赖注入实现方式
public class Notification {
  private MessageSender messageSender;
  
  public Notification() {
    this.messageSender = new MessageSender(); //此处有点像hardcode
  }
  
  public void sendMessage(String cellphone, String message) {
    //...省略校验逻辑等...
    this.messageSender.send(cellphone, message);
  }
}

public class MessageSender {
  public void send(String cellphone, String message) {
    //....
  }
}
// 使用Notification
Notification notification = new Notification();

// 依赖注入的实现方式
public class Notification {
  private MessageSender messageSender;
  
  public Notification(MessageSender messageSender) {
    this.messageSender = messageSender;
  }
  
  public void sendMessage(String cellphone, String message) {
    this.messageSender.send(cellphone, message);
  }
}

public interface MessageSender {
  void send(String cellphone, String message);
}

// 短信发送类
public class SmsSender implements MessageSender {
  @Override
  public void send(String cellphone, String message) {
    //....
  }
}

// 站内信发送类
public class InboxSender implements MessageSender {
  @Override
  public void send(String cellphone, String message) {
    //....
  }
}

//使用Notification
public class Demo {
  public static final void main(String args[]) {
    MessageSender sender = new SmsSender(); //创建对象
    Notification notification = new Notification(sender);//依赖注入
    notification.sendMessage("13918942177", "短信验证码：2346");
  }
}
```

- 依赖注入框架（DI Framework） 自动注入
  - 创建对象、组装（或注入）对象工作仅仅是被移动到更上层代码而已，还是需要手动来实现
  - 依赖注入框架 只需要通过依赖注入框架提供的扩展点，简单配置一下所有需要创建的类对象、类与类之间的依赖关系，就可以实现由框架来自动创建对象、管理对象的生命周期、依赖注入等原本需要程序员来做的事情
  - 框架  Google Guice、Java Spring、Pico Container、Butterfly Container 等
- 依赖反转原则 Dependency Inversion Principle DIP
  - High-level modules shouldn’t depend on low-level modules. Both modules should depend on abstractions. In addition, abstractions shouldn’t depend on details. Details depend on abstractions.
  - 高层模块和低层模块划分
    - 在调用链上，调用者属于高层，被调用者属于低层
    - 在平时业务代码开发中，高层模块依赖底层模块是没有任何问题的。实际上，这条原则主要还是用来指导框架层面设计，跟前面讲到的控制反转类似
  - 拿 Tomcat 这个 Servlet 容器作为例
    - Tomcat 是运行 Java Web 应用程序容器。编写的 Web 应用程序代码只需要部署在 Tomcat 容器下，便可以被 Tomcat 容器调用执行。
    - 按照之前划分原则，Tomcat 就是高层模块，编写的 Web 应用程序代码是低层模块。Tomcat 和应用程序代码之间并没有直接的依赖关系，两者都依赖同一个“抽象”，也就是 Servlet 规范。
    - Servlet 规范不依赖具体 Tomcat 容器和应用程序的实现细节，而 Tomcat 容器和应用程序依赖 Servlet 规范

### KISS 原则 & YAGNI 原则

- KISS 原则讲 “如何做”问题（尽量保持简单），而 YAGNI 原则说“要不要做”问题（当前不需要就不要做）
- Keep It Simple and Stupid
  - 经常用来指导更加广泛的系统设计、产品设计
  - 代码足够简单，也就意味着很容易读懂，bug 比较难隐藏。即便出现 bug，修复起来也比较简单
  - 并不是代码行数越少就越“简单”，还要考虑逻辑复杂度、实现难度、代码的可读性等
  - KMP 算法本身具有逻辑复杂、实现难度大、可读性差的特点。本身就复杂的问题，用复杂的方法解决，并不违背 KISS 原则
  - How
    - 不要使用可能不懂技术来实现代码。比如前面例子中正则表达式，还有一些编程语言中过于高级语法等
    - 不要重复造轮子，要善于使用已有工具类库。经验证明，自己去实现这些类库，出 bug 概率会更高，维护成本也比较高
    - 不要过度优化。不要过度使用一些奇技淫巧（比如，位运算代替算术运算、复杂的条件语句代替 if-else、使用一些过于底层的函数等）来优化代码，牺牲代码可读性
- YAGNI You Ain’t Gonna Need It
  - 不要做过度设计 不要去设计当前用不到的功能；不要去编写当前用不到的代码
  - 往项目里引入大量常用的 library 包

### Don’t Repeat Yourself DRY 原则

- 实现逻辑重复,语义并不重复 不违反 DRY 原则
  - 对于包含重复代码问题，通过抽象成更细粒度函数方式来解决
- 实现逻辑不重复，语义重复|功能重复，违反 DRY 原则
- 代码执行重
- DRY 原则跟代码的可复用性讲的是两回事 “不重复”并不代表“可复用”
- “复用”和“可复用性”关注角度不同
  - 代码“可复用性”是从代码开发者角度来讲
  - “复用” 从代码使用者角度来讲
- How
  - 减少代码耦合
  - 满足单一职责原则
  - 模块化
  - 业务与非业务逻辑分离
  - 通用代码下沉
- Rule of Three”
  可以用在很多行业和场景中
  如果把这个原则用在这里，在第一次写代码的时候，如果当下没有复用需求，而未来复用需求也不是特别明确，并且开发可复用代码的成本比较高，就不需要考虑代码的复用性。在之后开发新功能时发现可以复用之前写这段代码，那就重构这段代码，让其变得更加可复用
  第一次编写代码时不考虑复用性；第二次遇到复用场景时再进行重构使其复用

### LOD Law of Demeter 迪米特法则

- “高内聚、松耦合”
  - 高内聚 用来指导类本身设计
    - 相近功能应该放到同一个类中，不相近功能不要放到同一个类中
  - 松耦合 用来指导类与类之间依赖关系设计
    - 在代码中类与类之间依赖关系简单清晰。即使两个类有依赖关系，一个类的代码改动不会或者很少导致依赖类的代码改动
  - 两者并非完全独立不相干。高内聚有助于松耦合，松耦合又需要高内聚支持
- 迪米特法则|最小知识原则 The Least Knowledge Principle
  - Each unit should have only limited knowledge about other units: only units “closely” related to the current unit. Or: Each unit should only talk to its friends; Don’t talk to strangers.
  - 没有直接依赖关系类之间，不要有依赖；有依赖关系类之间，尽量只依赖必要接口（也就是定义中的“有限知识”）
  - Document 类
    - 构造函数中的 downloader.downloadHtml() 逻辑复杂，耗时长，不应该放到构造函数中，影响代码可测试性
    - HtmlDownloader 对象在构造函数中通过 new 来创建，违反基于接口而非实现编程设计思想，也会影响到代码可测试性
    - 从业务含义上来讲，Document 网页文档没必要依赖 HtmlDownloader 类，违背了迪米特法则

```java
// 把 address 和 content 交给 NetworkTransporter，而非是直接把 HtmlRequest 交给 NetworkTransporter
public class NetworkTransporter {
    // 省略属性和其他方法...
    public Byte[] send(String address, Byte[] data) {
      //...
    }
}

public class HtmlDownloader {
  private NetworkTransporter transporter;//通过构造函数或IOC注入
  
  // HtmlDownloader这里也要有相应的修改
  public Html downloadHtml(String url) {
    HtmlRequest htmlRequest = new HtmlRequest(url);
    Byte[] rawHtml = transporter.send(
      htmlRequest.getAddress(), htmlRequest.getContent().getBytes());
    return new Html(rawHtml);
  }
}

// 重构 Document
public class Document {
  private Html html;
  private String url;
  
  public Document(String url) {
    this.url = url;
    HtmlDownloader downloader = new HtmlDownloader();
    this.html = downloader.downloadHtml(url);
  }
  //...
}

public class Document {
  private Html html;
  private String url;
  
  public Document(String url, Html html) {
    this.html = html;
    this.url = url;
  }
  //...
}


// 通过一个工厂方法来创建Document
public class DocumentFactory {
  private HtmlDownloader downloader;
  
  public DocumentFactory(HtmlDownloader downloader) {
    this.downloader = downloader;
  }
  
  public Document createDocument(String url) {
    Html html = downloader.downloadHtml(url);
    return new Document(url, html);
  }
}
```

### 实践 业务系统案例

- 公司依赖业务，业务开发需要技术，技术是更底层更通用的能力
- 通过一个积分兑换系统开发实战，展示业务系统整个开发套路
- 需求分析
  - 通过产品线框图、用户用例（user case ）或者叫用户故事（user story）来细化业务流程
  - 用户用例有点儿类似单元测试用例。侧重情景化，其实就是模拟用户如何使用产品，描述用户在一个特定的应用场景里的一个完整的业务操作流程。包含更多的细节，且更加容易被人理解，可以进行如下的设计
    - 用户获取积分时告知积分有效期
      - 赚取渠道 下订单、每日签到、评论
      - 有效期根据不同渠道，设置不同有效期
    - 用户使用积分时优先使用快过期积分
      - 消费渠道 抵扣订单金额、兑换优惠券、积分换购、参与活动扣积分
      - 根据不同的消费渠道，设置不同的积分兑换规则
    - 用户查询积分明细时显示积分有效期和状态（是否过期）
    - 用户查询总可用积分时排除掉过期积分
- 系统设计
  - 面向对象设计聚焦在代码层面（主要是针对类），那系统设计就是聚焦在架构层面（主要是针对模块），两者有很多相似之处
  - 将功能放到合适模块中
    - 第一种 积分赚取渠道及兑换规则、消费渠道及兑换规则的管理和维护（增删改查），不划分到积分系统中，而是放到更上层的营销系统中。这样积分系统就会变得非常简单，只需要负责增加积分、减少积分、查询积分、查询积分明细等这几个工作。
    - 第二种 积分赚取渠道及兑换规则、消费渠道及兑换规则的管理和维护，分散在各个相关业务系统中，比如订单系统、评论系统、签到系统、换购商城、优惠券系统等。
    - 一个功能的修改或添加，经常要跨团队、跨项目、跨系统才能完成，那说明模块划分的不够合理，职责不够清晰，耦合过于严重
    - 为避免业务知识耦合，让下层系统更加通用，一般来讲，不希望下层系统（被调用系统）包含太多上层系统（调用系统）业务信息，但是，可以接受上层系统包含下层系统业务信息
    - 积分系统所负责的工作是一样的，只包含积分的增、减、查询，以及积分明细的记录和查询
  - 设计模块与模块之间交互关系
    - 同步接口调用 简单直接
    - 利用消息中间件异步调用 解耦效果更好
    - 上下层系统之间调用倾向于通过同步接口，同层之间调用倾向于异步消息调用
- 业务开发
  - 数据库和接口的设计非常重要，一旦设计好并投入使用之后不能轻易改动
    - 改动数据库表结构，需要涉及数据迁移和适配
    - 改动接口，需要推动接口使用者修改相应代码
    - 这两种情况，即便是微小的改动，执行起来都会非常麻烦。因此在设计接口和数据库的时候，一定要多花点心思和时间，切不可过于随意
    - 业务逻辑代码侧重内部实现，不涉及被外部依赖接口，也不包含持久化数据，对改动容忍性更大
  - 数据库设计
  - 接口设计
    - 借鉴 facade（外观）设计模式，在职责单一细粒度接口之上，再封装一层粗粒度 接口给外部使用
  - 业务模型设计
- 为什么分 MVC 三层
  - 优点
    - 代码复用 越低层复用性越高
    - 隔离变化 越低层变化越小
    - 隔离关注点
      - Repository 层只关注数据的读写。Service 层只关注业务逻辑，不关注数据的来源。Controller 层只关注与外界打交道，数据校验、封装、格式转换，并不关心业务逻辑。三层之间的关注点不同，分层之后，职责分明，更加符合单一职责原则，代码的内聚性更好
    - 提高代码可测试性
    - 应对系统的复杂性
  - BO、VO、Entity 存在意义 推荐每层都定义各自的数据对象
    - VO、BO、Entity 并非完全一样。比如，可以在 UserEntity、UserBo 中定义 Password 字段，但显然不能在 UserVo 中定义 Password 字段，否则就会将用户的密码暴露出去。
    - VO、BO、Entity 三个类虽然代码重复，但功能语义不重复，从职责上讲是不一样的。所以，也并不能算违背 DRY 原则。在前面讲到 DRY 原则的时候，针对这种情况，如果合并为同一个类，那也会存在后期因为需求的变化而需要再拆分的问题。
    - 为了尽量减少每层之间耦合，把职责边界划分明确，每层都会维护自己的数据对象，层与层之间通过接口交互。数据从下一层传递到上一层的时候，将下一层的数据对象转化成上一层的数据对象，再继续处理。虽然这样的设计稍微有些繁琐，每层都需要定义各自的数据对象，需要做数据对象之间的转化，但是分层清晰。对于非常大的项目来说，结构清晰是第一位的！
    - 解决代码重复
      - 将公共的字段定义在父类中，让 VO、BO、Entity 都继承这个父类，各自只定义特有的字段。因为这里的继承层次很浅，也不复杂，所以使用继承并不会影响代码的可读性和可维护性。后期如果因为业务的需要，有些字段需要从父类移动到子类，或者从子类提取到父类，代码改起来也并不复杂
    - 不同分层之间数据对象互相转化
      - 最简单方式 手动复制
      - Java 中提供多种数据对象转化工具，比如 BeanUtils、Dozer 等，大大简化对象转化工作
      - VO、BO、Entity 都是基于贫血模型的，而且为兼容框架或开发库（比如 MyBatis、Dozer、BeanUtils），需要定义每个字段 set 方法。违背 OOP 的封装特性，会导致数据被随意修改
      - Entity 和 VO 生命周期是有限的，都仅限在本层范围内。而对应 Repository 层和 Controller 层也都不包含太多业务逻辑，不会有太多代码随意修改数据，即便设计成贫血、定义每个字段的 set 方法，相对来说也是安全的。
      - Service 层包含比较多的业务逻辑代码，所以 BO 就存在被任意修改的风险了。但是，设计的问题本身就没有最优解，只有权衡。为了使用方便，我们只能做一些妥协，放弃 BO 的封装特性，由程序员自己来负责这些数据对象的不被错误使用。

### 实践 非业务的通用框架

- 目标 设计开发一个小的框架
  - 能够获取接口调用各种统计信息，比如，响应时间的最大值（max）、最小值（min）、平均值（avg）、百分位值（percentile）、接口调用次数（count）、频率（tps） 等
  - 支持将统计结果以各种显示格式（比如：JSON 格式、网页格式、自定义显示格式等）输出到各种终端（Console 命令行、HTTP 网页、Email、日志文件、自定义输出终端等），以方便查看
- 需求分析 从线框图中挖掘出隐藏需求
  - 功能性需求分析
    - 接口统计信息 接口响应时间统计信息，以及接口调用次数统计信息等
    - 统计信息类型 max、min、avg、percentile、count、tps 等
    - 统计信息显示格式 Json、Html、自定义显示格式
    - 统计信息显示终端 Console、Email、HTTP 网页、日志、自定义显示终端
    - 统计触发方式
      - 主动 以一定的频率定时统计数据，并主动推送到显示终端，比如邮件推送
      - 被动 用户触发统计，比如用户在网页中选择要统计的时间区间，触发统计，并将结果显示给用户
    - 统计时间区间 框架需要支持自定义统计时间区间，比如统计最近 10 分钟的某接口的 tps、访问次数，或者统计 12 月 11 日 00 点到 12 月 12 日 00 点之间某接口响应时间的最大值、最小值、平均值等
    - 统计时间间隔 对于主动触发统计，还要支持指定统计时间间隔，也就是多久触发一次统计显示。比如，每间隔 10s 统计一次接口信息并显示到命令行中，每间隔 24 小时发送一封统计信息邮件
  - 非功能性需求分析（没有明确要求，不要过早介入）
    - 易用性 否易集成、易插拔、跟业务代码是否松耦合、提供的接口是否够灵活等等，有时文档写得好坏甚至都有可能决定一个框架是否受欢迎
    - 性能
      - 不影响或很少影响接口本身的响应时间
      - 对内存的消耗
    - 扩展性
      - 使用者可以在不修改框架源码甚至不拿到框架源码情况下，为框架扩展新功能
    - 容错性  对框架可能存在的各种异常情况都考虑全面，对外暴露的接口抛出的所有运行时、非运行时异常都进行捕获处理
    - 通用性
      - 除了接口统计这样一个需求，还可以适用到其他哪些场景中，比如是否还可以处理其他事件的统计信息，比如 SQL 请求时间的统计信息、业务统计信息（比如支付成功率）等
- 框架设计
  - 借鉴 TDD（测试驱动开发）和 Prototype（最小原型）思想，先聚焦于一个简单的应用场景，基于此设计实现一个简单的原型
    - 尽管这个最小原型系统在功能和非功能特性上都不完善，但能够看得见、摸得着，比较具体、不抽象，能够很有效地帮助缕清更复杂设计思路，是迭代设计的基础
    - 先聚焦于一个非常具体、简单应用场景
    - 走一遍流程
  - 模块
    - 数据采集：负责打点采集原始数据，包括记录每次接口请求响应时间和请求时间。数据采集
      - 过程要高度容错，不能影响到接口本身可用性
      - 因为这部分功能是暴露给框架的使用者的，在设计数据采集 API 时要尽量考虑其易用性
    - 存储：负责将采集原始数据保存下来，以便后面做聚合统计
      - 储方式有多种，比如：Redis、MySQL、HBase、日志、文件、内存等
      - 数据存储比较耗时，为尽量地减少对接口性能（比如响应时间）的影响，采集和存储过程异步完成
    - 聚合统计：负责将原始数据聚合为统计数据，比如：max、min、avg、pencentile、count、tps 等。为了支持更多聚合统计规则，代码希望尽可能灵活、可扩展
    - 显示：负责将统计数据以某种格式显示到终端，比如：输出到命令行、邮件、网页、自定义显示终端等
- 面向对象设计与实现
  - 划分职责进而识别出有哪些类
    - MetricsCollector 类负责 采集接口请求的原始数据。可以为 MetricsCollector 抽象出一个接口，但这并不是必须的，暂时只能想到一个 MetricsCollector 的实现方式
    - MetricsStorage 接口负责原始数据存储，RedisMetricsStorage 类实现 MetricsStorage 接口
    - Aggregator 类负责根据原始数据计算统计数据
    - ConsoleReporter 类、EmailReporter 类分别负责以一定频率统计并发送统计数据到命令行和邮件。是否可以抽象出可复用的抽象类，或者抽象出一个公共的接口，暂时还不确定
  - 定义类及类与类之间的关系
    - 先在 IDE 中创建好这几个类，然后开始试着定义属性和方法
    - 统计显示所要完成的功能逻辑细
      - 根据给定时间区间，从数据库中拉取数据
      - 根据原始数据，计算得到统计数据
      - 将统计数据显示到终端（命令行或邮件）
      - 定时触发以上 3 个过程的执行
    - 将类组装起来并提供执行入口,有两个执行入口
      - MetricsCollector 类，提供一组 API 来采集原始数据
      - ConsoleReporter 类和 EmailReporter 类，用来触发统计显示

```java

public class MetricsCollector {
  private MetricsStorage metricsStorage;

  // 兼顾代码的易用性，新增一个封装了默认依赖的构造函数
  public MetricsCollectorB() {
    this(new RedisMetricsStorage());
  }

  // 兼顾灵活性和代码的可测试性，这个构造函数继续保留
  public MetricsCollectorB(MetricsStorage metricsStorage) {
    this.metricsStorage = metricsStorage;
  }
  // 省略其他代码...
}

public class Aggregator {
  public Map<String, RequestStat> aggregate(
          Map<String, List<RequestInfo>> requestInfos, long durationInMillis) {
    Map<String, RequestStat> requestStats = new HashMap<>();
    for (Map.Entry<String, List<RequestInfo>> entry : requestInfos.entrySet()) {
      String apiName = entry.getKey();
      List<RequestInfo> requestInfosPerApi = entry.getValue();
      RequestStat requestStat = doAggregate(requestInfosPerApi, durationInMillis);
      requestStats.put(apiName, requestStat);
    }
    return requestStats;
  }

  private RequestStat doAggregate(List<RequestInfo> requestInfos, long durationInMillis) {
    List<Double> respTimes = new ArrayList<>();
    for (RequestInfo requestInfo : requestInfos) {
      double respTime = requestInfo.getResponseTime();
      respTimes.add(respTime);
    }

    RequestStat requestStat = new RequestStat();
    requestStat.setMaxResponseTime(max(respTimes));
    requestStat.setMinResponseTime(min(respTimes));
    requestStat.setAvgResponseTime(avg(respTimes));
    requestStat.setP999ResponseTime(percentile999(respTimes));
    requestStat.setP99ResponseTime(percentile99(respTimes));
    requestStat.setCount(respTimes.size());
    requestStat.setTps((long) tps(respTimes.size(), durationInMillis/1000));
    return requestStat;
  }

  // 以下的函数的代码实现均省略...
  private double max(List<Double> dataset) {}
  private double min(List<Double> dataset) {}
  private double avg(List<Double> dataset) {}
  private double tps(int count, double duration) {}
  private double percentile999(List<Double> dataset) {}
  private double percentile99(List<Double> dataset) {}
  private double percentile(List<Double> dataset, double ratio) {}
}


public interface StatViewer {
  void output(Map<String, RequestStat> requestStats, long startTimeInMillis, long endTimeInMills);
}

public class ConsoleViewer implements StatViewer {
  public void output(
          Map<String, RequestStat> requestStats, long startTimeInMillis, long endTimeInMills) {
    System.out.println("Time Span: [" + startTimeInMillis + ", " + endTimeInMills + "]");
    Gson gson = new Gson();
    System.out.println(gson.toJson(requestStats));
  }
}

public class EmailViewer implements StatViewer {
  private EmailSender emailSender;
  private List<String> toAddresses = new ArrayList<>();

  public EmailViewer() {
    this.emailSender = new EmailSender(/*省略参数*/);
  }

  public EmailViewer(EmailSender emailSender) {
    this.emailSender = emailSender;
  }

  public void addToAddress(String address) {
    toAddresses.add(address);
  }

  public void output(
          Map<String, RequestStat> requestStats, long startTimeInMillis, long endTimeInMills) {
    // format the requestStats to HTML style.
    // send it to email toAddresses.
  }
}


public class ConsoleReporter {
  private MetricsStorage metricsStorage;
  private Aggregator aggregator;
  private StatViewer viewer;
  private ScheduledExecutorService executor;

  public ConsoleReporter(MetricsStorage metricsStorage, Aggregator aggregator, StatViewer viewer) {
    this.metricsStorage = metricsStorage;
    this.aggregator = aggregator;
    this.viewer = viewer;
    this.executor = Executors.newSingleThreadScheduledExecutor();
  }

  public void startRepeatedReport(long periodInSeconds, long durationInSeconds) {
    executor.scheduleAtFixedRate(new Runnable() {
      @Override
      public void run() {
        long durationInMillis = durationInSeconds * 1000;
        long endTimeInMillis = System.currentTimeMillis();
        long startTimeInMillis = endTimeInMillis - durationInMillis;
        Map<String, List<RequestInfo>> requestInfos =
                metricsStorage.getRequestInfos(startTimeInMillis, endTimeInMillis);
        Map<String, RequestStat> requestStats = aggregator.aggregate(requestInfos, durationInMillis);
        viewer.output(requestStats, startTimeInMillis, endTimeInMillis);
      }
    }, 0L, periodInSeconds, TimeUnit.SECONDS);
  }

}

public class EmailReporter extends ScheduledReporter {
  // 省略其他代码...
  public void startDailyReport() {
    // new Date()可以获取当前时间
    Date firstTime = trimTimeFieldsToZeroOfNextDay(new Date());
    Timer timer = new Timer();
    timer.schedule(new TimerTask() {
      @Override
      public void run() {
        // 省略其他代码...
      }
    }, firstTime, DAY_HOURS_IN_SECONDS * 1000);
  }

  protected Date trimTimeFieldsToZeroOfNextDay(Date date) {
    Calendar calendar = Calendar.getInstance(); // 这里可以获取当前时间
    calendar.setTime(date); // 重新设置时间
    calendar.add(Calendar.DATE, 1);
    calendar.set(Calendar.HOUR_OF_DAY, 0);
    calendar.set(Calendar.MINUTE, 0);
    calendar.set(Calendar.SECOND, 0);
    calendar.set(Calendar.MILLISECOND, 0);
    return calendar.getTime();
  }
}}
}


public class PerfCounterTest {
  public static void main(String[] args) {
    MetricsStorage storage = new RedisMetricsStorage();
    Aggregator aggregator = new Aggregator();

    // 定时触发统计并将结果显示到终端
    ConsoleViewer consoleViewer = new ConsoleViewer();
    ConsoleReporter consoleReporter = new ConsoleReporter(storage, aggregator, consoleViewer);
    consoleReporter.startRepeatedReport(60, 60);

    // 定时触发统计并将结果输出到邮件
    EmailViewer emailViewer = new EmailViewer();
    emailViewer.addToAddress("wangzheng@xzg.com");
    EmailReporter emailReporter = new EmailReporter(storage, aggregator, emailViewer);
    emailReporter.startDailyReport();

    // 收集接口访问数据
    MetricsCollector collector = new MetricsCollector(storage);
    collector.recordRequest(new RequestInfo("register", 123, 10234));
    collector.recordRequest(new RequestInfo("register", 223, 11234));
    collector.recordRequest(new RequestInfo("register", 323, 12334));
    collector.recordRequest(new RequestInfo("login", 23, 12434));
    collector.recordRequest(new RequestInfo("login", 1223, 14234));

    try {
      Thread.sleep(100000);
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
  }
}

public abstract class ScheduledReporter {
  protected MetricsStorage metricsStorage;
  protected Aggregator aggregator;
  protected StatViewer viewer;

  public ScheduledReporter(MetricsStorage metricsStorage, Aggregator aggregator, StatViewer viewer) {
    this.metricsStorage = metricsStorage;
    this.aggregator = aggregator;
    this.viewer = viewer;
  }

  protected void doStatAndReport(long startTimeInMillis, long endTimeInMillis) {
    long durationInMillis = endTimeInMillis -  startTimeInMillis;
    Map<String, List<RequestInfo>> requestInfos =
            metricsStorage.getRequestInfos(startTimeInMillis, endTimeInMillis);
    Map<String, RequestStat> requestStats = aggregator.aggregate(requestInfos, durationInMillis);
    viewer.output(requestStats, startTimeInMillis, endTimeInMillis);
  }

}
```

## 代码重构

- 目的（why）
  - 重构是一种对软件内部结构的改善，目的是在不改变软件的可见行为的情况下，使其更易理解，修改成本更低
  - 时刻保证代码质量的一个极其有效手段，不至于让代码腐化到无可救药地步
  - 优秀代码或架构不是一开始就能完全设计好的,都是迭代出来的
  - 避免过度设计的有效手段 维护代码过程中，真正遇到问题时再对代码进行重构，能有效避免前期投入太多时间做过度设计
  - 将理论知识应用到实践的一个很好场景，能够锻炼熟练使用理论知识的能力
- 对象（what）
  - 大重构
    - 对顶层代码设计重构，包括：系统、模块、代码结构、类与类之间的关系等的重构
    - 手段：分层、模块化、解耦、抽象可复用组件等等
    - 涉及代码改动会比较多，影响面会比较大，难度也较大，耗时会比较长，引入 bug 风险也会相对比较大
  - 小重构
    - 对代码细节重构，主要针对类、函数、变量等代码级别的重构，比如规范命名、规范注释、消除超大类或函数、提取重复代码等等
    - 利用编码规范
    - 要修改的地方比较集中，比较简单，可操作性较强，耗时会比较短，引入 bug 风险相对来说也会比较小
    - 只需要熟练掌握各种编码规范，就可以做到得心应手
- 时机（when）
  - 寄希望于在代码烂到一定程度后，集中重构解决所有问题是不现实的，必须探索一条可持续、可演进方式
  - 把单元测试、Code Review 、持续重构作为开发一部分，成为一种开发习惯
- 方法（how）
  - 对于大规模高层次重构 一定是有组织、有计划且非常谨慎，需要有经验、熟悉业务资深同事来主导
    - 因为涉及模块、代码会比较多，如果项目代码质量又比较差，耦合比较严重，往往会牵一发而动全身，本来觉得一天就能完成重构会发现越改越多、越改越乱，没一两个礼拜都搞不定。而新业务开发又与重构相冲突，最后只能半途而废，revert 掉所有的改动，很失落地又去堆砌烂代码了
    - 在进行大型重构时要提前做好完善重构计划，有条不紊地分阶段来进行
    - 每个阶段完成一小部分代码重构，然后提交、测试、运行，发现没有问题之后，再继续进行下一阶段的重构，保证代码仓库中代码一直处于可运行、逻辑正确状态
    - 每个阶段都要控制好重构影响到的代码范围，考虑好如何兼容老的代码逻辑，必要时还需要写一些兼容过渡代码。
    - 只有这样，才能让每一阶段的重构都不至于耗时太长（最好一天就能完成），不至于与新的功能开发相冲突。
  - 小规模低层次重构
    - 因为影响范围小，改动耗时短，所以，只要愿意并且有时间，随时都可以去做。
    - 除了人工去发现低层次质量问题，还可以借助很多成熟静态代码分析工具（比如 CheckStyle、FindBugs、PMD），来自动发现代码中问题，然后针对性地进行重构优化。
  - 对于重构，资深工程师、项目 leader 要负起责任来，没事就重构一下代码，时刻保证代码质量处在一个良好的状态。否则会出现“破窗效应”，往项目里堆砌烂代码成本太低了
  - 保持代码质量最好方法 打造一种好技术氛围，驱动大家主动去关注代码质量，持续重构代码

### 保证重构不出错技术手段

- 单元测试 Unit Testing
  - 由研发工程师自己来编写，用来测试自己写的代码的正确性
  - 集成测试（Integration Testing）对象 整个系统或者某个功能模块，比如测试用户注册、登录功能是否正常，一种端到端（end to end）测试
  - 单元测试 对象 类或者函数，测试一个类和函数是否都按照预期逻辑执行，代码层级测试，相对于集成测试，粒度更小一些
  - Why
    - 为重构保驾护航
    - 有效帮助发现代码中 bug
    - 发现代码设计问题
    - 对集成测试补充
    - 阅读单元测试能帮助你快速熟悉代码
    - TDD 可落地执行的基础
  - How
    - 针对代码设计覆盖各种输入、异常、边界条件的测试用例
    - 测试代码实现起来比较简单,不同测试用例之间代码差别并不是很大
    - 将覆盖率作为衡量单元测试质量的唯一标准是不合理的,更重要的是要看测试用例是否覆盖了所有可能的情况
    - 单元测试不要依赖被测试函数具体实现逻辑，只关心被测函数实现什么功能。切不可为追求覆盖率，逐行阅读代码，然后针对实现逻辑编写单元测试
    - 步骤
      - 提高代码的可读性
      - 提高代码的可测试性
      - 编写完善的单元测试
      - 所有重构完成之后添加注释
    - 程序出错该返回
      - 函数出错
        - 错误码
          - 熟悉编程语言中有异常这种语法机制就尽量不要使用错误码
          - 异常相对于错误码有诸多方面优势，比如可以携带更多的错误信息（exception 中可以有 message、stack trace 等信息）等
        - NULL 值
          - 返回代表不存在语义的 NULL 值比返回异常更加合理
        - 空对象
        - 异常对象
          - 受检异常
          - 非受检异常
          - 处理方法
            - 直接吞掉
            - 往上抛出
            - 包裹成新 异常抛出
  - 为何难落地
    - 价值得不到正确认可
- 代码可测试性
  - What
    - mock  用一个“假”服务替换真正服务
      - 测试中依赖外部服务 依赖确定返回结果
      - 控制对象返回需要模拟的异常，来测试代码在异常情况表现
      - 网络中断、超时、Redis、RPC 服务的不可用，都会影响单元测试的执行
  - Anti-Patterns
    - 未决行为 代码输出是随机或者说不确定的
    - 滥用可变全局变量
    - 滥用静态方法
    - 复杂继承关
    - 高度耦合代码
- 解耦
  - why
    - 应对复杂性
      - “高内聚、松耦合”是一个比较通用的设计思想，不仅可以指导细粒度的类和类之间关系的设计，还能指导粗粒度的系统、架构、模块的设计。相对于编码规范，它能够在更高层次上提高代码的可读性和可维护性。
      - 聚焦在某一模块或类中，不需要了解太多其他模块或类的代码，焦点不至于过于发散，降低了阅读和修改代码的难度。
      - “高内聚、松耦合”的代码可测试性也更加好，容易 mock 或者很少需要 mock 外部依赖的模块或者类。
  - what
    - 能不能把模块与模块之间、类与类之间依赖关系画出来，根据依赖关系图的复杂性来判断是否需要解耦重构。
  - how
    - 封装与抽象
      - 可以有效地隐藏实现的复杂性，隔离实现的易变性，给依赖的模块提供稳定且易用的抽象接口
    - 中间层
      - 简化模块或类之间的依赖关系
      - 起到过渡的作用，能够让开发和重构同步进行，不互相干扰
        - 引入一个中间层，包裹老的接口，提供新的接口定义
        - 新开发的代码依赖中间层提供的新接口
        - 将依赖老接口的代码改为调用新接口
        - 确保所有的代码都调用新接口之后，删除掉老的接口
    - 模块化
      - 能搭建出如此复杂的系统，并且能维护得了，最主要原因就是将系统划分成各个独立模块，让不同人负责不同模块，即便在不了解全部细节情况下，管理者也能协调各个模块，让整个系统有效运转

```java
  public String generate() throws IdGenerationFailureException {
    String substrOfHostName = null;
    try {
      substrOfHostName = getLastFieldOfHostName();
    } catch (UnknownHostException e) {
      throw new IdGenerationFailureException("host name is empty.");
    }
    long currentTimeMillis = System.currentTimeMillis();
    String randomString = generateRandomAlphameric(8);
    String id = String.format("%s-%d-%s",
            substrOfHostName, currentTimeMillis, randomString);
    return id;
  }

 private String getLastFieldOfHostName() throws UnknownHostException{
    String substrOfHostName = null;
    String hostName = InetAddress.getLocalHost().getHostName();
    if (hostName == null || hostName.isEmpty()) { // 此处做判断
      throw new UnknownHostException("...");
    }
    substrOfHostName = getLastSubstrSplittedByDot(hostName);
    return substrOfHostName;
 }

  @VisibleForTesting
  protected String getLastSubstrSplittedByDot(String hostName) {
    if (hostName == null || hostName.isEmpty()) {
      throw IllegalArgumentException("..."); //运行时异常
    }
    String[] tokens = hostName.split("\\.");
    String substrOfHostName = tokens[tokens.length - 1];
    return substrOfHostName;
  }


public class RandomIdGenerator implements IdGenerator {
  private static final Logger logger = LoggerFactory.getLogger(RandomIdGenerator.class);

  @Override
  public String generate() throws IdGenerationFailureException {
    String substrOfHostName = null;
    try {
      substrOfHostName = getLastFieldOfHostName();
    } catch (UnknownHostException e) {
      throw new IdGenerationFailureException("...", e);
    }
    long currentTimeMillis = System.currentTimeMillis();
    String randomString = generateRandomAlphameric(8);
    String id = String.format("%s-%d-%s",
            substrOfHostName, currentTimeMillis, randomString);
    return id;
  }

  private String getLastFieldOfHostName() throws UnknownHostException{
    String substrOfHostName = null;
    String hostName = InetAddress.getLocalHost().getHostName();
    if (hostName == null || hostName.isEmpty()) {
      throw new UnknownHostException("...");
    }
    substrOfHostName = getLastSubstrSplittedByDot(hostName);
    return substrOfHostName;
  }

  @VisibleForTesting
  protected String getLastSubstrSplittedByDot(String hostName) {
    if (hostName == null || hostName.isEmpty()) {
      throw new IllegalArgumentException("...");
    }

    String[] tokens = hostName.split("\\.");
    String substrOfHostName = tokens[tokens.length - 1];
    return substrOfHostName;
  }

  @VisibleForTesting
  protected String generateRandomAlphameric(int length) {
    if (length <= 0) {
      throw new IllegalArgumentException("...");
    }

    char[] randomChars = new char[length];
    int count = 0;
    Random random = new Random();
    while (count < length) {
      int maxAscii = 'z';
      int randomAscii = random.nextInt(maxAscii);
      boolean isDigit= randomAscii >= '0' && randomAscii <= '9';
      boolean isUppercase= randomAscii >= 'A' && randomAscii <= 'Z';
      boolean isLowercase= randomAscii >= 'a' && randomAscii <= 'z';
      if (isDigit|| isUppercase || isLowercase) {
        randomChars[count] = (char) (randomAscii);
        ++count;
      }
    }
    return new String(randomChars);
  }
}
```

## 编程规范

- 主要解决代码可读性问题，相对于设计原则、设计模式，更加具体、更加偏重代码细节
- 命名
  - 长命名可以包含更多信息，更能准确直观地表达意图，但是由它们组成的语句就会很长。在代码列长度有限制的情况下，会经常出现一条语句被分割成两行情况，影响代码可读性
  - 在足够表达含义情况下，命名当然是越短越好
  - 对于作用域比较小变量可以使用相对短的命名
  - 原则 以能准确达意为目标
  - 技巧
    - 利用上下文简化命名
    - 命名要可读、可搜索
  - 命名接口和抽象类 项目统一
    - 接口
      - 接口加前缀“I”
      - 实现加后缀“Impl”
    - 抽象类
      - 带上前缀“Abstract”
- 注释（Naming and Comments）
  - 让代码更容易看懂
  - 内容包含 做什么、为什么、怎么做
  - 比代码承载的信息更多
  - 起到总结性作用、文档的作用
  - 太多
    - 有可能意味着代码写得不够可读，需要写很多注释来补充
    - 对代码本身的阅读起到干扰
    - 后期维护成本也比较高
  - 类和函数一定要写注释，而且要写得尽可能全面、详细，函数内部注释要相对少一些，一般都是靠好的命名、提炼函数、解释性变量、总结性注释来提高代码的可读性
- 代码风格（Code Style）
  - 类、函数长度限制 当一个类代码读起来感觉头大，实现某个功能时不知道该用哪个函数，想用哪个函数翻半天都找不到
  - 一行代码长度 不能超过 IDE 显示宽度
  - 善用空行分割单元块
  - 推荐两格缩进，可以节省空间，不要用 tab 键缩进，显示宽度不同
  - 大括号是否要另起一行
  - 类成员排列顺序
    - 在 Google Java 编程规范中，依赖类按照字母序从小到大排列。类中先写成员变量后写函数。成员变量之间或函数之间，先写静态成员变量或函数，后写普通变量或函数，并且按照作用域大小依次排列
- 编程技巧（Coding Tips）
  - 把代码分割成更小的单元块 将大块复杂逻辑提炼成类或者函数，屏蔽掉细节，让阅读代码人不至于迷失在细节中，提高代码可读性
  - 避免函数参数过多 大于等于 5 个的时候
    - 考虑函数是否职责单一，是否能通过拆分成多个函数的方式来减少参数
    - 将函数的参数封装成对象
  - 勿用函数参数来控制逻辑
    - 布尔类型作为标识参数来控制逻辑
    - 根据参数是否为 null”来控制逻辑的情况
    - 应该将其拆分成多个函数。拆分之后函数职责更明确，不容易用错
  - 函数设计要职责单一
  - 移除过深的嵌套层次
    - 去掉多余的 if 或 else 语句
    - 使用 continue、break、return 关键字，提前退出嵌套
    - 调整执行顺序来减少嵌套
    - 将部分嵌套逻辑封装成函数调用
  - 使用解释性变量
    - 常量取代魔法数字
    - 使用解释性变量来解释复杂表达式

## 设计模式

- 创建型
  - 常用：单例模式、工厂模式（工厂方法和抽象工厂）、建造者模式
  - 不常用：原型模式
- 结构型
  - 常用：代理模式、桥接模式、装饰者模式、适配器模式
  - 不常用：门面模式、组合模式、享元模式
- 行为型
  - 常用：观察者模式、模板模式、策略模式、职责链模式、迭代器模式、状态模式
  - 不常用：访问者模式、备忘录模式、命令模式、解释器模式、中介模式。

### 单例模式 Singleton Design Pattern

- 一个类只允许创建一个对象（或者实例）
	- 对象唯一性的作用范围是进程内的（线程间都唯一），在进程间是不唯一的
- 场景
- 一个类的两个线程同时分别执行函数，并且同时写日志到文件中，有可能存在日志信息互相覆盖情况
	- 锁是一个对象级别锁，一个对象在不同线程下同时调用 log() 函数，会被强制要求顺序执行。不同对象之间并不共享同一把锁。在不同线程下，通过不同对象调用执行 log() 函数，锁并不会起作用，仍然有可能存在写入日志互相覆盖的问题
	- FileWriter 本身就是线程安全的，内部实现中本身就加了对象级别的锁
- 场景
	- 有些数据在系统中只应保存一份
- 实现
	- 构造函数需要是 private 访问权限的，这样才能避免外部通过 new 创建实例
	- 考虑对象创建时的线程安全问题
	- 考虑是否支持延迟加载
	- 考虑 getInstance() 性能是否高（是否加锁）
- 方式
	- 饿汉式  
		- 类加载时，instance 静态实例已经创建并初始化好了instance 实例创建过程是线程安全的
		- 不支持延迟加载（在真正用到 IdGenerator 的时候，再创建实例）
			- 如果初始化耗时长，最好不要等到真正要用时才去执行初始化过程，影响系统性能
	- 懒汉式
		- 给 getInstance() 方法加把锁（synchronzed），导致这个函数的并发度很低
		- 量化一下的话，并发度是 1，也就相当于串行操作了
		- 偶尔会被用到，还可以接受。如果频繁地用到，频繁加锁、释放锁及并发度低等问题，会导致性能瓶颈，这种实现方式就不可取了
	- 双重检测
		- 只要 instance 被创建之后，即便再调用 getInstance() 函数也不会再进入到加锁逻辑中
		- 有人说，这种实现方式有些问题。因为指令重排序，可能会导致 IdGenerator 对象被 new 出来，并且赋值给 instance 之后，还没来得及初始化（执行构造函数中的代码逻辑），就被另一个线程使用了。要解决这个问题，我们需要给 instance 成员变量加上 volatile 关键字，禁止指令重排序才行
		- 只有很低版本 Java 会有这个问题。现在用的高版本的 Java 已经在 JDK 内部实现中解决了（解决方法，把对象 new 操作和初始化操作设计为原子操作，就自然能禁止重排序）
	- 静态内部类
- 问题 有点类似硬编码
	- 对 OOP 特性支持不友好
	- 隐藏类之间依赖关系
	- 对代码的扩展性不友好
		- 例子 在系统中创建两个数据库连接池，慢 SQL 独享一个数据库连接池，其他 SQL 独享另外一个数据库连接池，这样就能避免慢 SQL 影响到其他 SQL 的执行
	- 对代码可测试性不友好
		- 无法实现 mock 替换
	- 不支持有参数的构造函数
- 替代方案
	- 将单例生成对象作为参数传递给函数（也可以通过构造函数传递给类的成员变量），可以解决单例隐藏类之间依赖关系的问题。不过，对于的其他问题，比如对 OOP 特性、扩展性、可测性不友好等问题，还是无法解决
- 线程唯一
	- Java 语言本身提供了 ThreadLocal 工具类，可以更加轻松地实现线程唯一单例，底层实现原理基于下面代码中所示的 HashMap
- 集群环境下单例
	- 进程内唯一、进程间也唯一，不同进程间共享同一个对象，不能创建同一个类的多个对象
	- 需要把这个单例对象序列化并存储到外部共享存储区（比如文件）。进程在使用这个单例对象的时候，需要先从外部共享存储区中将它读取到内存，并反序列化成对象，然后再使用，使用完成之后还需要再存储回外部共享存储区
	- 为了保证任何时刻，在进程间都只有一份对象存在，一个进程在获取到对象之后，需要对对象加锁，避免其他进程再将其获取。在进程使用完这个对象之后，还需要显式地将对象从内存中删除，并且释放对对象的加锁
- 多例模式
	- 跟工厂模式不同之处 多例模式创建的对象是同一个类对象，工厂模式创建是不同子类对象

```java
public void log(String message) { synchronized(this) { writer.write(mesasge); } }
public void log(String message) { synchronized(Logger.class) { // 类级别的锁 writer.write(mesasge); } }

public class IdGenerator { 
  private AtomicLong id = new AtomicLong(0);
  private static IdGenerator instance;
  private IdGenerator() {}
  public static synchronized IdGenerator getInstance() {
    if (instance == null) {
      instance = new IdGenerator();
    }
    return instance;
  }
  public long getId() { 
    return id.incrementAndGet();
  }
}

public class IdGenerator { 
  private AtomicLong id = new AtomicLong(0);
  private static IdGenerator instance;
  private IdGenerator() {}
	
  public static IdGenerator getInstance() {
    if (instance == null) {
      synchronized(IdGenerator.class) { // 此处为类级别的锁
        if (instance == null) {
          instance = new IdGenerator();
        }
      }
    }
    return instance;
  }
	
  public long getId() { 
    return id.incrementAndGet();
  }
}
// 静态内部类
public class IdGenerator { 
  private AtomicLong id = new AtomicLong(0);
  private IdGenerator() {}

  private static class SingletonHolder{
    private static final IdGenerator instance = new IdGenerator();
  }
  
  public static IdGenerator getInstance() {
    return SingletonHolder.instance;
  }
 
  public long getId() { 
    return id.incrementAndGet();
  }
}

// 1. 老使用方式
public demofunction() {
  //...
  long id = IdGenerator.getInstance().getId();
  //...
}

// 2. 新使用方式：依赖注入
public demofunction(IdGenerator idGenerator) {
  long id = idGenerator.getId();
}
// 外部调用demofunction()的时候，传入idGenerator
IdGenerator idGenerator = IdGenerator.getInsance();
demofunction(idGenerator);
	

public class IdGenerator {
  private AtomicLong id = new AtomicLong(0);

  private static final ConcurrentHashMap<Long, IdGenerator> instances
          = new ConcurrentHashMap<>();

  private IdGenerator() {}

  public static IdGenerator getInstance() {
    Long currentThreadId = Thread.currentThread().getId();
    instances.putIfAbsent(currentThreadId, new IdGenerator());
    return instances.get(currentThreadId);
  }

  public long getId() {
    return id.incrementAndGet();
  }
}
	

public class IdGenerator {
  private AtomicLong id = new AtomicLong(0);
  private static IdGenerator instance;
  private static SharedObjectStorage storage = FileSharedObjectStorage(/*入参省略，比如文件地址*/);
  private static DistributedLock lock = new DistributedLock();
  
  private IdGenerator() {}

  public synchronized static IdGenerator getInstance() 
    if (instance == null) {
      lock.lock();
      instance = storage.load(IdGenerator.class);
    }
    return instance;
  }
  
  public synchroinzed void freeInstance() {
    storage.save(this, IdGeneator.class);
    instance = null; //释放对象
    lock.unlock();
  }
  
  public long getId() { 
    return id.incrementAndGet();
  }
}

// IdGenerator使用举例
IdGenerator idGeneator = IdGenerator.getInstance();
long id = idGenerator.getId();
IdGenerator.freeInstance();
								 
// 多例模式
public class BackendServer {
  private long serverNo;
  private String serverAddress;

  private static final int SERVER_COUNT = 3;
  private static final Map<Long, BackendServer> serverInstances = new HashMap<>();

  static {
    serverInstances.put(1L, new BackendServer(1L, "192.134.22.138:8080"));
    serverInstances.put(2L, new BackendServer(2L, "192.134.22.139:8080"));
    serverInstances.put(3L, new BackendServer(3L, "192.134.22.140:8080"));
  }

  private BackendServer(long serverNo, String serverAddress) {
    this.serverNo = serverNo;
    this.serverAddress = serverAddress;
  }

  public BackendServer getInstance(long serverNo) {
    return serverInstances.get(serverNo);
  }

  public BackendServer getRandomInstance() {
    Random r = new Random();
    int no = r.nextInt(SERVER_COUNT)+1;
    return serverInstances.get(no);
  }
}							
```

### 工厂模式

- 简单工厂 Simple Factory
	- 看作是工厂方法模式一种特例
	- 大部分以“Factory”结尾
	- 创建对象方法一般是 create 开头
	- 尽管实现中有多处 if 分支判断逻辑，违背开闭原则，但权衡扩展性和可读性，在大多数情况下（比如，不需要频繁地添加 parser，也没有太多的 parser）是没有问题的
- 工厂方法
- 抽象工厂

## 参考

- 《设计模式：可复用面向对象软件的基础 Design Patterns: Elements of Reusable Object-Oriented Software》
