## [hexo](https://github.com/hexojs/hexo)

A fast, simple & powerful blog framework, powered by Node.js. <https://hexo.io>

- 配置：站点目录下的_config.yml为站点配置文件，主题目录下的_config.yml为主题配置文件
- [hexo-admin](https://github.com/jaredly/hexo-admin):An Admin Interface for Hexo <http://jaredly.github.io/hexo-admin/>
- [hexo-admin](https://github.com/barretlee/hexo-admin):小胡子优化版本
  - 按照官方的方式安装 hexo-admin
  - 下载修改的代码到一个文件夹，执行 `npm link`
  - 在 hexo 根目录下执行 `npm link hexo-admin`

```sh
brew install git
brew install node
npm install hexo-cli -g

cd filename
hexo init

# 新文章需先生成后再部署
hexo g(enerate)
hexo s(erver)

cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next

# hexo d ERROR Deployer not found: git
npm install hexo-deployer-git --save
# 修改_config.yml,添加仓库
type: git
repo: git@github.com:bluebird89/bluebird89.github.io.git
branch: hexo
hexo deploy

## 自动化
atom ~/.aliases
alias hgs="hexo g&&hexo s"
alias hgd="hexo g&&hexo d"
```

## [hugo](https://github.com/gohugoio/hugo)

The world’s fastest framework for building websites. <https://gohugo.io>

- deploy 通过Aerobatic[<https://gohugo.io/hosting-and-deployment/hosting-on-bitbucket/>]
- [hugo-academic](https://github.com/gcushen/hugo-academic):📝 The website builder for Hugo. Build and deploy a beautiful website in minutes! <https://sourcethemes.com/academic/>
- [Hugo Themes](https://themes.gohugo.io)
- 使用 Github Actions 自动部署 Hugo 站点
  - ``https://github.com/<YourName>/<YourName>.github.io` public
    - `.github/workflows/hugo.yml`
    - `public key` 作为网站文件仓库 `Settings > Deploy Keys`
  - `https://github.com/<YourName>/pages-hugo-source` private
    - `private key` 作为 Hexo 源文件仓库 `Settings > Secrets` 的 一个名叫 `DEPLOY_KEY` 的 `Actions secrets`
    - 查看 actions:`https://github.com/<YourName>/pages-hugo-source/actions`

```sh
## install
brew install hugo
sudo apt install hugo

hugo version

## init
hugo new site quickstart

cd quickstart
git init

## add theme
hugo new theme <THEMENAME>
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke;\

# config.toml:configuration file and add the Ananke theme.
echo 'theme = "ananke"' >> config.toml

hugo new posts/my-first-post.md

hugo server -D

config.toml  //配置文件

cd themes
git clone https://github.com/spf13/hyde

hugo -t themename // 测试主题效果
hugo server -t themename

hexo clean：删除网站（public）文件
hexo g：生成网站（public）文件
hexo d：将本地网站（public）文件同步到指定仓库（如：yourname.github.io）中

ssh-keygen -t rsa -b 4096 -C "$(git config user.email)" -f gh-pages -N ""
```

## [jekyll](https://github.com/jekyll/jekyll)

🌐 Jekyll is a blog-aware static site generator in Ruby <https://jekyllrb.com> static website generator，搭建静态博客，通过markdown文件自动生成html文件。Github Pages即靠Jekyll实现的。[官网](https://jekyllrb.com)

- 结构
  - _config.yml 是配置文件，最为重要，包含了所有配置信息
  - _includes 文件夹包含了将被反复利用的文件，比如footer，header
  - _layouts 文件夹包含了主页面的排版布局
  - _posts 文件夹将包含所有的日志文件，Markdown格式
- 配置
  - github新仓库 开启Github pages
  - 将代码推送到仓库
  - [访问页面](https://bluebird89.github.io/)
- 主题
  - [so-simple-theme](https://github.com/mmistakes/so-simple-theme):A simple Jekyll theme for words and pictures.
  - [jekyll-bootstrap](https://github.com/plusjade/jekyll-bootstrap):The quickest way to start and publish your Jekyll powered blog. 100% compatible with GitHub pages. <http://jekyllbootstrap.com>

```sh
gem install jekyll bundler
gem new myblog
bundle exec
jekyll serve
```

## [docsify](https://github.com/docsifyjs/docsify)

🃏 A magical documentation site generator. <https://docsify.js.org>

- 直接运行时转换 md 为 html, `/#/guide` => guide.md

```sh
npm i docsify-cli -g
makdir blog
docsify init ./

blog/     # Github Pages 根目录
   ├ _images/       # 图片
   ├ _media/        # 多媒体文件
   ├ basic/         # 基础知识
   ├ develop/       # 编程开发
   ├ keys/          # 热键速查
   ├ links/         # 友情链接
   ├ offer/         # 求职应聘
   ├ writing/       # 写作排版
   ├ _coverpage.md  # 封面
   ├ _navbar.md     # 导航栏
   ├ _sidebar.md    # 侧边栏
   ├ README.md   # docs README 文件
   ├ index.html  # 首页，在这里配置 docsify
   ├ CNAME       # 绑定自定义域名 notes.abelsu7.top
   ├ .nojekyll   # 阻止 GitHub Pages 忽略命名是下划线开头的文件
   ├ README.md  # Github 仓库 README 文件
   └ LICENSE    # MIT License

docsify serve ./
```

## [Halo](https://github.com/halo-dev/halo)

## [Typecho](http://typecho.org/)

- 外观
- 插件

```sh
# 登录 typecho提示 URL 为 http://127.0.0.1/index.php/action/login?name=admin&password=admin&referer=http%3A%2F%2F127.0.0.1%2Fadmin%2Findex.php&_=a6ca5a4fff943b47824c6b1f8af93cde 页面为 404 Not Found
# location ~ \.php$ {
location ~ .*\.php(\/.*)*$ {
```

## 优化

- 基于hugo网站（3个设置了github actions），一个设置了netlify，这样可以直接在github上修改内容，然后自动编译部署。
- 更新了一个旧的jekyl网站，把absolute_url改成relative_url。
- 做了一个新的jekyll网
- 总结一条：再也不想在自己电脑上更新网站了。都交给github。有点像侦探游戏，更像是做实验，需要从一分钟后网页的表象来诊断它哪里坏了。
- 为什么layout就是一团乱，命名我的theme都设置好了呀？嗯，想办法让网页变化，输出一些东西，比如site.url, post.url, relative_url到底是什么效果。
- 确保manipulation在发挥作用。
- 对于浪费的时间，只好安慰自己：这是一劳永逸，可以节约未来的时间。如果未来很短呢？比如浏览器不停在升级，css，javascript和其他网页构建一直在变化，终究这些网站会挂掉把。但我想他们现在应该能outlive me了。

## [WordPress](https://github.com/WordPress/WordPress)

WordPress, Git-ified. Synced via SVN every 15 minutes, including branches and tags! This repository is just a mirror of the WordPress subversion repository. Please do not send pull requests. Submit patches to <https://core.trac.wordpress.org/> instead. <https://wordpress.org/>

- 到 wordpress.com 注册帐户，获取用户的 API-Key，用来启用 Akismet 插件。Akismet 是 WordPress 下非常著名的反垃圾评论插件。
- 修改永久链接结构：默认情况下，WordPress 的永久链接结构类似于 ../?p=123 ，但我们推荐使用有利于搜索引擎优化的 URL 结构。本文作者建议采用 …/%category%/%postname%
- 使用系统缓存:Super Cache
- 创建网站地图：这是最基本一步，因为网站地图可以帮助搜索引擎来更轻松地抓取你网站的内容。可以使用 Google XML sitemap 插件来创建网站地图。
- 将 Feed 重定向到 feedburner：比如在你的博客的每个设计里修改所有的链接（尤其是 single.php, sidebar.php, footer.php 等）。我推荐使用 FeedSmith 插件来减少手动工作量。
- 添加跟踪代码：跟踪统计网站的性能是很必要的。你可以添加 Google 分析，StatCounter 或者其他的统计代码。根据我的额经验，Statcounter 是比较可靠并且载入速度快的。
- 提交网站到站长工具箱：我几乎没有注意到这点。不过，Google 站长工具箱有全部的功能，可以让你提交网站地图，显示网站搜索分析结果和网站上的错误。确实配得上站长工具箱的名字。
- 创建 robots.txt ：尽管有了站长工具箱，我还要说这个很重要。如果你有这个文件，可以分析一下；如果还没有，也可以使用 WordPress 的选项来创建一个。
- 设计：博客网站给读者的第一印象就是它的设计。注意好的设计应该包括重要的元素，比如搜索功能，Feed 订阅图标，导航菜单，并且便于阅读。你可以从这里挑选一些精选的 WordPress 主题。
- 开始写博客：告诉世界你要开始写博客了，说说你要写的内容，介绍一下你自己。要和访问者进行交流，你可以使用 Wp-contact form 插件来建立一个联系页面。
- 同时，别忘了创建 about 页面，因为访问者想了解你更多一些。

### 安装

- [安装地址](http://example.com/wp-admin/install.php)

### 插件

- [gutenberg](https://github.com/WordPress/gutenberg):Printing since 1440. Development hub for the editor focus in core. Plugin is available from the official WordPress repository. <https://wordpress.org/plugins/gutenberg/>

### 主题

- [sage](https://github.com/roots/sage):WordPress starter theme with a modern development workflow <https://roots.io/sage/>

### 优化

- 启动gzip压缩、安装wp super cache、使用公共cdn服务器

### [calypso](https://github.com/Automattic/wp-calypso)

The JavaScript and API powered WordPress.com <https://developer.wordpress.com/calypso/>

### 工具

- [VVV](https://github.com/Varying-Vagrant-Vagrants/VVV):An open source Vagrant configuration for developing with WordPress <https://varyingvagrantvagrants.org>
- [headless-wp-starter](https://github.com/postlight/headless-wp-starter):🔪 WordPress + React Starter kit
- [Apps](https://apps.wordpress.com)
- <https://sarah.dev/writing/>
- <https://github.com/brickspert/blog>
- <https://github.com/GavinZhuLei/vue-form-making>
- <https://github.com/fangzesheng/free-api>
- <https://github.com/zhisheng17/flink-learning>
- <https://github.com/DevinVinson/WordPress-Plugin-Boilerplate>
- <https://github.com/benweet/stackedit>
- <https://github.com/roots/sage>
- <https://github.com/digitalocean/nginxconfig.io>
- <https://github.com/future-architect/vuls>
- <https://github.com/woocommerce/woocommerce>
- <https://github.com/roots/bedrock>
- <https://github.com/wpscanteam/wpscan>
- <https://wp-cli.org/>

### 参考

- [Automattic](https://automattic.co)
- [kinsta](https://kinsta.com/):<https://kinsta.com/resources/>

## [gollum](https://github.com/gollum/gollum)

A simple, Git-powered wiki with a sweet API and local frontend.

## Farbox 2

## 博客资源

- [Work life](https://www.atlassian.com/blog)
- [一只特立独行的猪](http://guanzhou.pub/tag/)
- [schollz](https://schollz.com/)
- [lifesinger](https://github.com/lifesinger/blog):岁月如歌
- [前端精读](https://github.com/dt-fe/)
- [鸟窝](https://colobu.com/)
- [phodal](https://www.phodal.com/)
- [编程随想](https://program-think.blogspot.com/)

## 平台

- [mastodon](https://joinmastodon.org/)Social networking, back in your hands

## 文章

- [ProtoTeam](https://github.com/ProtoTeam/blog):蚂蚁数据体验技术团队的文章仓库
- [没有了老师，该如何学习？](http://www.cnblogs.com/qianqian-li/p/6028745.html)
- [How To Ask Questions The Smart Way](http://www.catb.org/esr/faqs/smart-questions.html)

## 工具

- 分发
  - [OpenWrite](https://openwrite.cn/)
  - [crawlab-team / artipub](https://github.com/crawlab-team/artipub):Article publishing platform that automatically distributes your articles to various media channels