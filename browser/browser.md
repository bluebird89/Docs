## Brower

- [Chrome](./chrome.md) 基于 Webkit
  - Edge
  - [mightyapp](https://www.mightyapp.com/)
  - [brave-browser](https://github.com/brave/brave-browser):Brave browser for Desktop and Laptop computers running Windows, OSX, and Linux <https://www.brave.com>
- [Firefox](./firefox.md) 自研 Gecko 内核
- Safari 基于 Webkit 内核
  - 像JavaScript引发的alert窗口或file组件打开的窗口，都属于模态窗口，它们会阻塞所有主线程中正在执行的JavaScript代码
- Opera
  - adds unlimited VPN service to its
- [beaker](https://beakerbrowser.com/):Beaker is a peer-to-peer browser with tools to create and host websites.
- [browsershots](http://browsershots.org/)
- [qutebrowser](https://www.qutebrowser.org)
- [Tor](http://torproject.lu/)
- vivaldi
- [Onion](https://onionbrowser.com/)
  - [](https://tor-browser.en.softonic.com/mac)
  - [Deep](https://github.com/mr-likar/DeepWeb)
- [Nessie](https://www.radsix.com/) an extremely simple web browser for Windows

```sh
curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add -

echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser
```

## 功能

- 搜索快捷键
- PWA

## [Bookmarklets](https://www.ph-uhl.com/0010-Bookmarklets/)

- Like a tiny Add-on for your browser. You drag it into your bookmark-bar and when you click it, it does something

## Chromium

- 成为现代浏览器的事实标准，市场占有率也一骑绝尘。在服务端、桌面还是移动端，甚至据传 SpaceX 火箭亦搭载了基于 Chromium 开发的控制面板。

### 渲染引擎

- 目前使用 Blink 作为渲染引擎，基于 webkit 定制而来的，核心逻辑位于项目仓库的 `third_party/blink/` 目录下。
- 功能
	- 解析并构建 DOM 树。Blink 引擎会把 DOM 树转化成 C++ 表示的结构，以供 V8 操作。
	- 调用 V8 引擎处理 JavaScript 和 Web Assembly 代码，并对 HTML 文档做特定操作。
	- 处理 HTML 文档定义的 CSS 样式
	- 调用 Chrome Compositor，将 HTML 对应的元素绘制出来。
		- 会调用 OpenGL，未来还会支持 Vulkan。
		- 在 Windows 平台上，该阶段还会调用 DirectX 库处理；
		- 在处理过程中，OpenGL 还会调用到 Skia，DirectX 还会调用到 ANGLE。

![[browser_render.png]]

#### 沙箱保护原理 / 机制

- 渲染引擎涉及大量 C++ 编写的组件，出现漏洞概率不小。因此，基于纵深防御理念浏览器引入了涉及三层结构。
- 渲染引擎等组件不直接与系统交互，而是通过一个被称为 MOJO 的 IPC 组件与浏览器引擎通讯（也被称为：broker），再与系统交互。进而可以实现：即便沙箱中的进程被攻破，但无法随意调用系统 API 产生更大的危害。有点类似：即便攻破了一个容器实例，在没有逃逸或提权漏洞的情况下，宿主机安全一定程度上不受影响（实际上，浏览器的 Sandbox 和容器隔离的部分技术原理是相似的）。
- 浏览器渲染引擎、GPU、PPAPI 插件以及语音识别服务等进程是运行在沙箱中的。此外不同系统平台下的部分服务也会受沙箱保护，例如 Windows 下打印时调用的 PDF 转换服务、icon 浏览服务；MacOS 下 NaCl loader、需要访问 IOSurface 的镜像服务等。查阅 Chromium 项目文件 sandbox_type.h 和 sandbox_type.cc 中的源码定义

##### 沙箱实现

- 在 Windows 平台上，Chrome 组合使用了系统提供的 Restricted Token、Integrity Level、The Windows job object、The Windows desktop object 机制来实现沙盒。其中最重要的一点是，把写操作权限限制起来，这样攻击这就无法通过写入文件或注册表键来攻击系统。
- 在 Linux 系统上
	- 第一层沙箱采用 setuid sandbox 方案。
		- 主要功能封装在二进制文件 chrome_sandbox 内，在编译项目时需要单独添加参数 “ninja -C xxx chrome chrome_sandbox” 编译，可以通过设置环境变量 CHROME_DEVEL_SANDBOX 指定 Chrome 调用的 setuid sandbox 二进制文件。
		- setuid sandbox 主要依赖两项机制来构建沙盒环境：CLONE_NEWPID 和 CLONE_NEWNET 方法。
		- CLONE_NEWPID 一方面会借助 chroots，来限制相关进程对文件系统命名空间的访问；另一方面会在调用 clone() 时指定 CLONE_NEWPID 选项，借助 PID namespace，让运行在沙盒中的进程无法调用 ptrace() 或 kill() 操作沙盒外的进程。
		- 而 CLONE_NEWNET 则用于限制在沙盒内进程的网络请求访问，值得一提的是，使用该方法需要 CAP_SYS_ADMIN 权限。
		- 这也使得当 Chrome 组件在容器内运行时，沙箱能力所需的权限会和容器所管理的权限有冲突；我们无法用最小的权限在容器里启动 Chrome 沙箱
		- 由于 setuid sandbox 方案存在一定短板。自 Chrome 44 版本起已推荐 namespaces sandbox 来替代 setuid sandbox 方案，其主要依赖于 Linux 内核提供的 user namespaces 机制
	- 第二层沙箱采用 Seccomp-BPF 方案，用来限制进程访问内核特定攻击面。
		- 通过将 Seccomp 和 BPF 规则结合，实现基于用户配置的策略白名单，对系统调用及其参数进行过滤限制。

### 浏览器内核

- 管理收藏夹、cookies 以及保存的密码等重要用户信息
- 负责处理网络通讯相关的事务
- 在渲染引擎和系统间起中间人的角色。渲染引擎通过 Mojo 与浏览器内核交互，包含组件：download、payments 等等。

### 漏洞攻击利用场景分析

- 服务器端
	- 禁用沙盒的 chromium headless 应用
		- 随着 Phantomjs 项目停止维护，Chromium headless 已经成为 Headless Browser 的首选。在日常开发、测试、安全扫描、运维中，有许多地方会用到 Headless Browser，包括不限于以下场景：
			- 前端测试
			- 监控
			- 网站截图
			- 安全扫描器
			- 爬虫
		- 如果程序本身使用的 Chromium 存在漏洞，且访问的 URL 可被外部控制，那么就可能受到攻击最终导致服务器被外部攻击者控制。
		- 以常见的使用 Chrome headless 的爬虫为例，如果在一些网站测试投放包含 exploit 的链接，有概率会被爬虫获取，相关爬取逻辑的通常做法是新建 tab 导航至爬取到的链接。此时，如果爬虫依赖的 chromium 应用程序更新不及时，且启动时设置了 --no-sandbox 参数，链接指向页面内的 exploit 会成功执行，进而允许攻击者控制爬虫对应的服务器。
	- 浅议攻击方式
- 客户端
	- 客户端内置 Webview 浏览器窗口
	
## 工具

- [browsh](https://github.com/browsh-org/browsh):A fully-modern text-based browser, rendering to TTY and browsers <https://www.brow.sh>
- [push.js](https://github.com/Nickersoft/push.js):The world's most versatile desktop notifications framework 🌎 <https://pushjs.org>
- [CodeMirror](https://github.com/codemirror/CodeMirror):In-browser code editor <http://codemirror.net/>
- [xterm.js](https://github.com/xtermjs/xterm.js):A terminal for the web <https://xtermjs.org/>
- [OctoLinker](OctoLinker/OctoLinker):OctoLinker – Available on Chrome, Firefox and Opera <https://octolinker.github.io>
- [muon](https://github.com/brave/muon):Build browsers and browser like applications with HTML, CSS, and JavaScript <https://discord.gg/TcT5tX2w>
- [KodExplorer](https://github.com/kalcaddle/KodExplorer):A web based file manager,web IDE / browser based code editor <http://kodcloud.com>
- [browser-sync](https://github.com/BrowserSync/browser-sync):Keep multiple browsers & devices in sync when building websites. <http://browsersync.io>
- [floccus](https://github.com/marcelklehr/floccus):Sync your bookmarks across browsers via Nextcloud, WebDAV or a local file (and thus any file sync solution)

## 参考

- [How browser rendering works — behind the scenes](https://blog.logrocket.com/how-browser-rendering-works-behind-the-scenes-6782b0e8fb10/)
- [浏览器的工作原理：新式网络浏览器幕后揭秘](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
