# 我的 MAC 设置

本文主要包括：brew、brew cask、iTerm2、安装 zsh 和配置、改建建议、推荐软件、值得购买的收费软件几个维度分享我的 Mac 基础工作环境和设置。

## 从终端开始

### 1. Homebrew

著名的包管理软件，每一个使用 Mac 开发开发者必须安装的软件包管理器。其中还有个广为流传的小故事：
> Homebrew 的作者 Max Howell，某日去 Google 面试被拒，原因是无法在白板上写出翻转二叉树的伪代码。于是怒气冲天的 Max 在推特中写道：
“Google：我们 90% 的工程师都在用你想别的软件（Homebrew），但是你没办法在白板上翻转二叉树，所以滚蛋吧。”

言归正传，安装请直接打开 `终端`，运行如下指令：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

安装完毕后，可以运行一下命令，验证状态：

```shell
brew doctor
```

我们可以使用 `brew search foo` 搜索包， `brew list` 查看已安装的包。可以在 `brew --help` 中查看其它的使用方法。

### 2. iTerm2 + zsh + oh-my-zsh + zsh-completions

首先你需要安装一个 iTerm2，这个软件远比 Mac 自带的终端软件好的多，至于为什么好，为什么不问问神奇的谷歌呢？

```shell
brew cask install iTerm2
```

然后你需要安装一些插件和配置

```shell
brew install zsh zsh-completions autojump
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

其中 Autojump 这个插件需要在 ~/.zshrc 中插入一行命令，直接在 iTerm2 中运行如下命令：

```shell
echo "\n# Autojump\n[ -f /usr/local/etc/profile.d/autojump.sh ] && . /usr/local/etc/profile.d/autojump.sh" >> ~/.zshrc
```

Autojump 是一个终端快速文件切换的命令工具，可以快速在历史文件夹中进行跳转。
[在 Github 可以查看更多用法](https://github.com/wting/autojump)

最后，我们需要载入刚刚的设置。当然也可以重启 iTerm2

```shell
source ~/.zshrc
```

### 3. tree

这是一个可以在命令行输出当前文件结构的命令，非常适合~~在博客装逼~~查看目录结构。

```shell
brew install tree
```

使用时直接输入命令 `tree`，就可以得到如下打印：

```shell
➜  fluttertips git:(master) ✗ tree
.
├── LICENSE
├── README.md
└── publish
    ├── advance
    ├── basic
    │   ├── basic-00-setupmymac.md
    │   └── basic-01-singleton.md
    ├── practice
    └── tools

5 directories, 4 files
```

## 安装必备软件

### 1. cask

cask 是 brew 的一个扩展，用来管理发布的软件。一般 cask 是默认安装的，如果找不到 cask，也可以用 brew 重新安装：

```shell
brew install cask
```

如果想查看已安装的软件可以运行：

```shell
brew cask list
```

### 1. 基本编辑器

VSCode 是我推荐的基础编辑器，可以用来写几乎所有的文件。如果你不是 Vim 或者 Emacs 的老炮，那这个作为 万物预览编辑器 还是不错的。

```shell
brew cask install visual-studio-code
```

**安装完毕后，我们需要开启对命令行的支持：**
在菜单栏 `查看` > `命令面板` 中，输入 `shell command` 找到 `Install ‘code' command in PATH` 选中即可。

**插件分享**
这是一些常用的插件，更多的插件和环境，可以根据需求查找。

`Bracket Pair Colorizer 2` 括号着色
`GitLens` Git 信息提示
`markdownlint` Markdown 着色和语法检测
`Markdown Preview Enhanced` Markdown 预览增强，支持流程图等
`Output Colorizer` 输出着色
`vscode-icons` 图标美化

### 2. 改键提效

#### karabiner-elements 改键神器

```shell
brew cask install karabiner-elements
```

我的习惯为将 `Caps Lock ⇪` （大小写切换键）更改为 `control ⌃` 键，将输入法切换更改为 `command ⌘ + 空格`，将 spotlight 更改为 `option ⌥ + 空格`。这样设置的好处是显而易见的，相比较左边的 `control ⌃`，`Caps Lock ⇪` 更加容易按到，而相比较将 `Caps Lock ⇪` 映射为 `⌃ + ⌘ + ⇧ + ⌥` 而言，适用性更广（如在命令行中经常使用到的 `control ⌃ + c`）。

我还会将 `control ⌃ + i/j/k/l` 映射成 `↑←↓→` 、 `control ⌃ + u/o` 映射成 `PageUp/PageDown` 这样我们就可以双手不离开键盘区域来快速移动光标了。当然对于 Vim 和 Emacs 选手而言，可以直接映射成对应的快捷键，这样就可以得到更加统一的按键体验。

另外值得一提的是，`control + h` 作为删除键使用的幸福感也非常强，在 mac 中模式实现了这个快捷键，但是在某些编辑器下是会冲突的。建议根据编辑器环境，将退格键设置成 `control ⌃ + h`。

这里有个简单的配置，安装好 karabiner-elements 之后，将这个配置文件覆盖到 `~/.config/karabiner` 目录下，就可以实现上述的配置。[简单配置](./src/000/karabiner.json)

### 3. 基础工具

#### 使用 `brew cask install` 命令安装基础工具

`google-chrome` 谷歌浏览器
`keka` 解压工具，因为 mac 不原生支持 7z/rar 等压缩格式。
`teamviewer` 远程协助
`aliwangwang` 阿里旺旺
`dingtalk` 钉钉，很多阿里技术直播也需要用到
`evernote` 印象笔记
`qq` 腾讯QQ
`wechat` 微信
`youdaodict` 有道词典
`sourcetree` Git 图形化界面
`boostnote` Markdown 笔记本
`aria2gui` 下载工具
`foxmail` 邮件客户端
`android-studio` 安卓开发工具
`docker` 容器环境
`kitematic` docker 可视化
`vritualbox` 虚拟机
`lantern` 蓝灯 VPN

如 `brew cask install google-chrome`

### 4. 效率工具

除了上面有说到的 `karabiner-elements` 之外，还有其他的可以提升效率的小工具推荐给大家：

**Manico** 收费，可以映射快捷键打开和隐藏应用。这个可以极大的减少使用触摸板的时间，根据内置的用量显示，我平均每天会使用大约200次。

**Moom** 收费，可以让窗口快速按照预设值进行停靠。可以让我们快速的最大化，或者填充半个屏幕。在普遍使用 MacBook Pro 的大环境下，也可以快速将窗口最大化到另外一个屏幕上。

**Bartender** 收费，可以让右上方的工具栏按照需求收起。让我们整个窗口看起来更加的整洁。另外我会将所有有干扰的软件提示（如 QQ）隐藏，这样我就得到了一个“专注的工作环境”，只有在我有间隙的时候，才会去查看微信和 QQ，降低被动干扰。

**1Password** 收费，虽然升级还要钱，但是还是很好用。不过我已经逐渐使用 Chrome 自带的密码工具生成和保存账号的密码，而且它再填充的时候也更加的便捷。

### 4. 关于使用 Google 搜索

作为程序员，经常要诊断一些程序抛出的疑难杂症，建议使用 Google 进行问题的搜索，如果没有 VPN 也可以直接访问 StackOverflow 进行问题的搜索。少用百度，保智商。
