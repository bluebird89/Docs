## xUnit

#computer #test

- 开发 在 编码阶段 以 函数方法 为粒度编写测试用例，检验 代码逻辑 的正确性。
- 单元测试可以尽早发现编码中的低级错误。越早发现问题，也越容易解决问题
  - 白盒测试一般只在单元测试中使用
  - 黑盒测试在单元测试、集成测试等各个阶段都可以使用。

## How

- 黑盒测试 只关注调用方法返回结果，不知道代码内部具体实现
- 设计 根据是否知道源代码写测试用例
  - 知道盒子用途 知道函数的具体用途、输入参数和返回结果含义
- 覆盖
  - 语句覆盖
  - 分支覆盖 最常使用考察指标
  - 条件覆盖
- 单元测试用例 经典模板 Given-When-Then(GWT)
  - 断言 Given 描述测试的前置条件或初始状态
  - 输入数据 When 描述测试过程中发生的行为
  - 预期输出 Then 描述测试结束后断言输出结果
- 原则：单元测试尽可能以函数方法等**较小粒度**进行组织。
  - 常见测试框架都支持通过测试套件（TestSuite）对测试用例（TestCase）在逻辑上进行组织，测试套件可以嵌套，整个单元测试可以组织为树状结构。
  - 轻量：不要有过多的前置条件或外部依赖.易于重复执行，方便重现和定位问题。
  - 独立：同一个测试套件的不同的用例相互独立,避免依赖，可乱序执行，结果稳定复现。
  - 隔离：使用测试套件隔离资源,使用测试套件与 Fixture 隔离测试用例的资源依赖，以方便管理。
- 用例设计
  - 正常流程通过输入合法的 典型数据、边界值 看基本功能是否正确实现
  - 异常流程通过输入非法数据看异常处理流程是否符合预期
  - 首先设计覆盖 正常流程 的用例，构造一些合法的输入：一个典型的 IP 报文，一个有扩展头部的 IP 报文，一个带有 TCP/UDP payload 的 IP 报文……
  - 其次设计覆盖 异常流程 的用例，构造一些非法的输入：空指针，不完整的 IP 头，非 IP 协议……
  - 最后再考虑一些边界情况：一个不带 payload 的 IP 报文，一个大小为 64K 上限的 IP 报文，一个头部完整但payload 不完整的 IP 报文……

```sh
SCENARIO( "vectors can be sized and resized", "[vector]" ) {
    GIVEN( "A vector with some items" ) {
        std::vector<int> v( 5 );

        REQUIRE( v.size() == 5 );  // REQUIRE() 即 assert()
        REQUIRE( v.capacity() >= 5 );

        WHEN( "the size is increased" ) {
            v.resize( 10 );

            THEN( "the size and capacity change" ) {
                REQUIRE( v.size() == 10 );
                REQUIRE( v.capacity() >= 10 );
            }
        }
        WHEN( "the size is reduced" ) {
            v.resize( 0 );

            THEN( "the size changes but not capacity" ) {
                REQUIRE( v.size() == 0 );
                REQUIRE( v.capacity() >= 5 );
            }
        }
    }
}
```

## [PHPUnit](https://github.com/sebastianbergmann/phpunit)

The PHP Unit Testing framework. <https://phpunit.de/>

### 安装

```sh
# global
wget https://phar.phpunit.de/phpunit.phar
chmod +x phpunit.phar
sudo mv phpunit.phar /usr/local/bin/phpunit
phpunit --version

sudo pear config-set auto_discover 1
sudo pear install pear.phpunit.de/PHPUnit

sudo pear channel-discover pear.phpunit.de
sudo pear install phpunit/PHPUnit

# project
composer require --dev phpunit/phpunit
```

### 配置

- PhpStrom
  - 创建代码文件
  - 右键 goto->test 创建测试文件->指定目录
  - 测试文件引入源文件
  - 配置文件
    - 设置：phpunit->user composer autoloader->vender/autoloader.php
    - 测试文件路径：run->edit configuration->directory
  - 执行单个文件
    - 当前测试类右键Run即可
    - `phpunit tests/ArraysTest.php`
- `--coverage-html $directory`
- `--configuration $file`
- `--bootstrap $phpScript`
- `--group=NakedPhp_Form`
- `--no-globals-backup and --no-static-backup`
- `--colors`
- `--stop-on-error and --stop-on-failure`
- `--debug`
- `--strict`
- `--filter`
- 默认配置文件 phpunit.xml

```sh
phpunit -c phpunit.xml

phpunit --[colors] MyTest.php
```

### 问题

```sh
could not find driver
sudo pecl install pdo_sqlite
```

## [Junit](https://github.com/junit-team/junit5)

- The next generation of JUnit. <https://junit.org>
- 测试方法使用@Test修饰
- 使用public void修饰，不带任何参数
- 新建源代码目录存放测试代码
- 测试类包与被测试类保持一致
- 测试单元中每个方法可以独立测试，方法间不能有任何依赖
- 测试类使用Test作为类名后缀
- 测试方法使用test作为方法名前缀

Failture:由断言方法引起，输出与预期不一样
Error:代码异常引起
测试用例不是用来证明你是对的，而是用来证明你没有错

### 版本

- JUnit5=Platform+Jupiter+Vintage

## 基础

- adopting descriptive test names and using a single assertion per test
- broken up the role of the class in tiny pieces which together give the full picture of the unit requirements.
- 结构
  - one test case per every class： Class -> `ClassTest`
  - Every test is a method，Every method will be run independently in an isolated environment
- 声明
  - method 命名 test*
  - 通过 @test 注解，函数名字不必以 test 开头
- `ClassTest`通常继承 `PHPUnit\Framework\TestCase`
- 全局单元测试:一次性执行所有的单元测试，可以编写 phpunit.xml 文件来实现
  - `<directory>test</directory>` 指定了测试代码都放在 test 目录下
- 组织测试
  - 文件系统来编排测试套件:所有测试用例源文件放在一个测试目录中
    - 通过对测试目录进行递归遍历，PHPUnit 能自动发现并运行测试 `phpunit --bootstrap src/autoload.php tests`,
    - `phpunit --bootstrap src/autoload.php tests/CurrencyTest` 单个文件
  - 用 XML 配置来编排测试套件
- 未完成的测试与跳过的测试
- 数据库测试:DbUnit 扩展大大简化了为测试设置数据库的操作，并且可以在对数据执行了一系列操作之后验证数据库的内容,支持 MySQL、PostgreSQL、Oracle 和 SQLite。通过集成 Zend Framework 或 Doctrine 2，也可以访问其他数据库系统，比如 IBM DB2 或者 Microsoft SQL Server。
  - 数据库交互建立和维护都很复杂。对数据库进行测试时，需要考虑以下这些变数：
    - 数据库和表
    - 向表中插入测试所需要的行
    - 测试运行完毕后验证数据库的状态
    - 每个新测试都要清理数据库
      -　保持每个测试所使用的数据量较小并且尽可能用非数据库测试来对代码进行测试，即使很大的测试套件也能轻松在一分钟内跑完。
  - todo

```sh
phpunit --colors -stop-on-error -stop-on-failure --denug --strict

phpunit -c phpunit.xml --testsuite=Unit  # 指定套件
 --coverage-html . # 在根目录下生成 HTML 格式的测试覆盖率报告文档
```

#### 组织

- 用文件系统来编排
- 用 XML 配置 `--testsuite`

### 数据验证

#### assert*()

- an if() construct inside a test used for enable checks on variables
- contain multiple assertions, beware that the first failure will prevent the subsequent assertions from being executed. Only the assert*() calls which strictly depends on the previous ones to make sense should be placed in the same method as them.
- support a supplemental string parameter named $message, which will be shown in the case of a failing test caused by the assertion
- `void assertTrue(boolean expected, boolean actual)`
- `void assertFalse(boolean condition)`
- `assertEquals($expected, $actual)`
- `void assertArrayEquals(expectedArray, resultArray):assertArrayEquals()`
- `assertSame($expected, $actual)`
- `void assertNotSame(boolean condition):assertNotSame()`
- `assertContains($needle, $haystack)`
- `assertArrayHasKey($key, $array) assertContainsOnly($type, $haystack)`
- `assertType($type, $variable)`
- `assertNotNull($variable)`
- `void assertNull(Object object)`
- `assertLessThan(),assertGreaterThan()`
- `assertGreatherThanOrEqual(), assertLessThanOrEquals()`
- `ssertStringsStartsWith($prefix, $string) assertStringsEndsWith($suffix, $string)`

#### fixture

- fixture 对开始执行某个测试时应用程序和数据库所处初始状态的描述
  - more than one fixture is requested, the common practice is to break down the test case, preparing more than one test case class for the system under test; these classes represents different scenarios and
- executed for every test,the test methods have the same state as a starting point
- `setUp()` 运行测试方法前，调用的模板方法,创建测试所用对象的地方
- `tearDown()` 测试方法运行结束后，不管是成功还是失败，调用的模板方法,清理测试所用对象的地方
  - - 只有在 `setUp()` 中分配了诸如文件或套接字之类的外部资源时才需要实现 `tearDown()`
  - - 如果 `setUp()` 中只创建纯 PHP 对象，通常可以略过 `tearDown()`。
  - 如果在 `setUp()` 中创建了大量对象，可能想要在`  tearDown() ` 中 `unset()` 指向这些对象的变量，这样可以被垃圾回收机制回收掉。对测试用例对象的垃圾回收动作则是不可预知的。
- `setUpBeforeClass(`) 与 `tearDownAfterClass()` 在测试用例类的第一个测试运行之前和测试用例类最后一个测试运行之后调用
- `assertPreConditions()` and`  assertPostConditions() ` executed before and after the a test method.
  - differ from setUp() and tearDown() since they are executed only if the test did not already fail and they can halt the execution with a failing assertion.
  - setUp() and tearDown() should never throw exceptions and they are executed anyway, unconcerned by the current test outcome.
- sharing a fixture between test cases can be a smell for a bad design
  - 在测试之间共享基境的需求源于某个未解决的设计问题
  - 一个有实际意义的例子是数据库连接：只登录数据库一次，然后重用此连接，而不是每个测试都建立一个新的数据库连接。这样能加快测试的运行。
  - 共享会降低测试价值。潜在设计问题是对象之间并非松散耦合。如果解决掉潜在设计问题并使用桩件(stub)来编写测试，就能达成更好的结果，而不是在测试之间产生运行时依赖并错过改进设计的机会。
  - 全局状态:使用 singleton 代码很难测试,使用全局变量代码也一样，类的静态属性也是
    - 通常情况下，欲测代码和全局变量之间会强烈耦合，并且其创建无法控制
    - 另外一个问题：一个测试对全局变量的改变可能会破坏另外一个测试
    - 全局变量 `$foo = 'bar';` 实际上是存储为 `$GLOBALS['foo'] = 'bar'` 超全局变量`$GLOBALS` 在任何变量作用域中都总是可用的内建变量
    - 在函数或者方法的变量作用域中，要访问全局变量 `$foo`，可以直接访问 `$GLOBALS['foo']` 来创建一个引用全局变量的局部变量

#### annotations

- a standard way to add metadata to code entities: add behavior to test case class without making write boilerplate code
- must be placed in docblock comments
  - the php engine there is no native support for them: phpunit extracts them from the comment block using reflection.
- `@Test`
- `@Before`
- `@After`
- `@BeforeClass`
- `@AfterClass`
- `@Ignore`
- `@dataProvider`
- `@depends` solve this common problem of logic and temporal precedence
  - 依赖关系并允许生产者（producer）返回一个测试基境（fixture）实例，并将此实例传递给依赖于它的消费者（consumer）们
    - 作为运行前置条件
  - 生成：返回数据
  - 依赖数据作为参数引入到测试中，可以修改
  - 多个参数按照声明顺序作为测试参数传入:第一个参数是第一个生产者提供的基境，第二个参数是第二个生产者提供的基境，以此类推
- `@depends clone` 来传递指向（深）拷贝对象的引用
- `@depends shallowClone` 来传递指向（正常浅）克隆对象（基于 PHP 关键字 `clone`）的引用
- `@group`

#### stub

- 不希望引入外部依赖，希望调用时立即返回一些提前准备好的“假数据”，需要“仿冒”这个依赖
- 将对象替换为（可选地）返回配置好的返回值的测试替身的实践方法称为打桩（stubbing）
- 可以用桩件（Stub）来“替换掉被测系统所依赖的实际组件，这样测试就有了对被测系统的间接输入的控制点。使得测试能强制安排被测系统的执行路径，否则被测系统可能无法执行”
- 包含了预定义好的数据并且在测试时返回给调用者的对象.比如很多组预定义好的输入、输出数据，比如数据库查询结果。
- 创建桩件
  - `createStub()` 会自动递归地基于方法的返回类型对返回值进行上桩。
  - `$this->getMockBuilder`
- 配置桩件
  - $stubmethod()
    - 当原始类中不包含名字为“method”的方法时，`$stub->method('doSomething')->willReturn('foo');`才能正常运行
    - 如果原始类包含名为“method”的方法，用 `$stub->expects($this->any())->method('doSomething')->willReturn('foo');`
  - 返回结果
    - willReturn()
    - will($this->returnArgument(0));
    - will($this->returnSelf());
    - `will($this->returnValueMap($map));`
    - `will($this->returnCallback('str_rot13'));`
    - 迭代 `will($this->onConsecutiveCalls(2, 3, 5, 7));`
- 验证
- TODO:构造参数如何配置

#### output

### 行为验证

#### Mock object

- 黑盒测试：关注调用方法的返回过程
- 仅记录它们调用信息的对象,比如模拟的文件保存接口、数据发送接口等。
- 将对象替换为能验证预期行为（例如断言某个方法必会被调用）的测试替身的实践方法
- 用仿件对象（mock object）“作为观察点来核实被测试系统在测试中的间接输出。
- 通常，仿件对象还需要包括桩件的功能，因为如果测试尚未失败则仿件对象需要向被测系统返回一些值，但是其重点还是在对间接输出的核实上。
- 因此，仿件对象远不止是桩件加断言，它是以一种从根本上完全不同的方式来使用的”
- PHPUnit 只会对在某个测试的作用域内生成的仿件对象进行自动校验。诸如在数据供给器内生成或用 `@depends` 标注注入测试的仿件对象，PHPUnit 并不会自动对其进行校验。
- lightweight implementations or extensions of interfaces and objects that implement the public interface in a controlled way.
- specify that any of that object's public or protected methods return a specific value
- 创建仿件
  - $this->createMock(Observer::class)
  - `$this->getMockBuilder()->setMethods(['set'])->getMock();`
    - 更灵活配置创建属性
- 期望 `expects($this->once())->method('update')->with($this->equalTo('something'));`
  - expects($this->once()) 返回一个匹配器:为 update() 方法建立预期：以字符串 'something' 为参数调用一次
    - any()
    - never()
    - once()
    - exectly(int $count)
    - at(int $index)
  - with() 验证参数:跟参数个数一致
    - 准确描述 $this->equalTo()
    - 模糊描述
  - `withConsecutive(array [])`
- 执行调用
- traits `getMockForAbstractClass()`
- abstract class `getMockForAbstractClass()`
- 对 Web 服务（Web Services）进行上桩或模仿 `getMockFromWsdl()`
- 工具
  - GoogleMock
    - 通过 C++ 多态实现对虚函数进行 Mock
    - 不支持 Free Function 以及非虚函数
    - 目前已经合并为 GoogleTest 的一个子模块
  - 《效能优化实践：C/C++单元测试万能插桩工具》
    - 通过 Hook 函数入口实现用 Mock 函数无缝替换原始函数
    - 内部开源工具
  - MySQL Server Mock
    - MySQL 官方提供的服务端 Mock 工具

#### Fakes

- 包含了生产环境下具体实现的简化版本的对象.比如模拟的数据库对象、文件描述符、网络连接等。

#### expections & errors

#### private & protected method

#### database

### mutation testing

## 结果

#### code coverage

```sh
sudo apt install php7.4-pcov
composer require --dev pcov/clobber

vendor/bin/phpunit --coverage-html tests/html --coverage-filter app/models --bootstrap tests/bootstrap.php
```

## 优化

- 编写
  - 测试的依赖关系:一个单元测试通常覆盖一个函数或方法中的一个特定路径。但是，测试方法并不一定非要是一个封装良好的独立实体。测试方法之间经常有隐含的依赖关系暗藏在测试的实现方案中。
    - 支持对测试方法之间的显式依赖关系进行声明。这种依赖关系并不是定义在测试方法的执行顺序中，而是允许生产者(producer)返回一个测试基境(fixture)的实例，并将此实例传递给依赖于它的消费者(consumer)们
    - 生产者(producer)，是能生成被测单元并将其作为返回值的测试方法。
    - 消费者(consumer)，是依赖于一个或多个生产者及其返回值的测试方法
    - 默认情况下，生产者所产生的返回值将“原样”传递给相应的消费者。这意味着，如果生产者返回的是一个对象，那么传递给消费者的将是一个指向此对象的引用。如果需要传递对象的副本而非引用，则应当用 @depends clone 替代 @depends。
    - 测试可以使用多个 @depends 标注。PHPUnit 不会更改测试的运行顺序，因此你需要自行保证某个测试所依赖的所有测试均出现于这个测试之前。
  - 数据供给器:以接受任意参数。这些参数由数据供给器方法提供。用 @dataProvider 标注来指定使用哪个数据供给器方法
  - 对异常进行测试:expectException()  expectExceptionCode()、expectExceptionMessage() 和 expectExceptionMessageRegExp()
  - 对 PHP 错误进行测试:PHPUnit\Framework\Error PHPUnit\Framework\Error\Notice 和 PHPUnit\Framework\Error\Warning
  - 对输出进行测试:断言（比如说）某方法的运行过程中生成了预期的输出（例如，通过 echo 或 print）
    - void expectOutputRegex(string $ regularExpression) 设置输出预期为输出应当匹配正则表达式  $regularExpression。
    - void expectOutputString(string $ expectedString) 设置输出预期为输出应当与  $expectedString 字符串相等。
    - bool setOutputCallback(callable $callback)  设置回调函数，用来做诸如将实际输出规范化之类的动作。
    - string getActualOutput()    获取实际输出。
  - 错误相关信息的输出:测试失败时，PHPUnit 全力提供尽可能多的有助于找出问题所在的上下文信息
- 命令行测试执行器
  - `phpunit ArrayTest`:在当前工作目录中寻找 ArrayTest.php
  - `phpunit UnitTest UnitTest.php`:源文件并加载之,类必须满足以下二个条件之一
    - 要么它继承自 PHPUnit\Framework\TestCase
    - 要么它提供 public static suite() 方法，这个方法返回一个 PHPUnit_Framework_Test 对象

## 术语

- SUT system under test

## 准则

- 单元测试必须经常跑
  - 错误做法：为了完成 KPI 写了一堆测试，跑一次就不管了
  - 正确做法：持续集成，自动化运行
- 从增量到存量，从主要到次要
  - 从覆盖新模块、新功能做起，单元测试先跑起来再说
  - 不要追求 100% 的覆盖率，但主要功能逻辑要完成覆盖测试
- 测试用例需要逐步积累
  - 上线前已经有了第一批用例，每次迭代都会增加新用例来覆盖变更

## 实践经验

- 思路：以黑盒指导功能验证，以白盒提升覆盖率
- 黑盒测试为主：
  - 黑盒测试验证功能逻辑实现是否正确
  - 不关心内部实现方式，代码优化重构用例仍可复用
- 白盒测试为辅：
  - 白盒测试关注黑盒测试用例遗漏的分支、路径
  - 可以聚焦于异常处理逻辑是否合理
  - 项目工期紧时可推迟进行
- 编码过程中，多多考虑代码的可测性，可以让单元测试事半功倍：
  - 开发过程及时编写测试用例，边开发边测试，不要等全部开发完毕了才开始写测试用例
  - 函数功能简单，避免随机性，以免测试结果不稳定
  - 函数减少输入输出，使简单的输入数据组合可以完成测试覆盖
  - 遵循 SOLID 原则

## 教训

- 不要被高覆盖率骗了
  - 单元测试的目标是发现问题，不是追求高覆盖率
  - 宏、模板等语法功能可能会使得覆盖率虚高
- Debug/Release 目标结果不一致
  - Debug 目标关闭优化，启用堆栈保护，某些错误代码可正常执行
  - 单测在 Debug 下跑完后，建议在 Release 下再跑一次

代码合并导致单测失败
- 小A和小B分别开发新功能，push 前单测都通过了，MR 后单测却挂了
- 使用持续集成发现问题

## 图书

- 单元测试的艺术
- 《xUnit 测试模式》Gerard Meszaros
- [xUnit Test Patterns: Refactoring Test Code](http://xunitpatterns.com/index.html)
- Instant Hands-on Testing with PHPUnit How-to

## 工具

- [JUnitGenerator V2.0](link)自动生成测试代码，需要安装
- [semaphore](https://semaphoreci.com/):Hosted CI/CD for teams that don’t like bottlenecks

### 框架

- GoogleTest 是老牌测试框架，功能完善，用户很多。
- Catch2 是现代化测试框架，提供了很多特色功能，依赖简单，可以一试。
- Boost.Test 是 Boost 自带的测试框架，依赖 Boost 的程序可以直接使用，功能强大。

## 参考

- [docs](https://junit.org/junit5/docs/current/user-guide/)
- [Writing Tests with JUnit 5](https://blog.jetbrains.com/idea/2020/09/writing-tests-with-junit-5/)
- [unit test](https://mkyong.com/unittest/)
- [PHPUnit 文档](http://www.phpunit.cn)
- [PHPUnit Manual](https://phpunit.readthedocs.io/zh_CN/latest/index.html)
