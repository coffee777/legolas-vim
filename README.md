# legolas-vim

个人vim配置。**支持python、go等自动提示，支持python、go的函数跳转（python支持虚拟环境）。**最终效果图（由于性能问题，去掉了ctags，因为ycm是支持依赖库跳转的）：

![qq20161017-0](https://cloud.githubusercontent.com/assets/8017604/19426340/4def15cc-946e-11e6-891b-924f52486144.png)

支持Python自动补全的最好插件是YouCompleteMe。而YouCompleteMe需要比较高版本的vim(>=7.4.143)，所以，需要编译安装vim，参见相关文档[1]。另外还需要一些C库，参见相关文档[2]。

vim扩展管理器使用的是Vundle，参见相关文档[3]。

由于是为python开发打造。默认安装了pip等py开发必需品。公用开发工具默认安装（brew、zsh等）。


# Install & Update

**支持Ubuntu、Centos（需要先处理下问题5sudo vim的问题）、Mac OSX（默认基于brew安装新版vim）**，一键安装：

    cd ~ && rm -rf legolas-vim && git clone https://github.com/TTWShell/legolas-vim.git && cd legolas-vim && bash install.sh

如果用户修改了vimrc配置文件，运行以下命令更新即可：

    sudo bash install-plugins.sh

升级插件：

    sudo bash install-plugins.sh update


# 问题集锦

1. 安装过程中打开vim可能会提示找不到syntax.vim或者配色。syntax做一下ln s 操作即可。配色安装完毕会自动解决。

2. mac上有好用的brew。可以直接安装8.0以上版本的vim。可参考[Mac环境配置及python包安装的那些坑](http://www.ttwshell.com/article/mac-env-and-python-package-install-errors.html)：

        brew update
        export PATH=/usr/local/bin:$PATH  # 在／etc/profile 添加一下语句（使用zsh的在~/.zshrc添加即可）

3. mac由于并没有直接替换系统自带的vim。所以其他需要vim支持的工具需要修改配置。例如git：

        git config --global core.editor "/usr/local/bin/vim"

4. 关于字体

    [powerline-fonts](https://github.com/powerline/fonts)已经去掉了monaco_for_powerline。但是iterm2默认字体monaco非常好看，为了使用monaco并解决特殊符号乱码问题，所以Backup了一份。会自动安装。用户手动设置下iterm2字体配置即可（可搜索）。

5. 关于centos 使用sudo的问题（sudo: vim: command not found）

    参考[http://superuser.com/questions/548508/why-cant-i-sudo-some-commands-e-g-vim](http://superuser.com/questions/548508/why-cant-i-sudo-some-commands-e-g-vim)
    
6. 局域网安装问题

    **[使用privoxy和shadowsocks搭建局域网http代理](https://github.com/TTWShell/legolas-vim/wiki/使用privoxy和shadowsocks搭建局域网http代理)——局域网开发机安装legolas-vim解决方案！**


# 快捷键说明

1. NERDTree有按横向纵向布局模式打开文件的快捷，直接看help信息即可。
2. tab切换使用ngt即可。例如切换到第二个tab页，输入2gt。
3. 支持pycharm中的代码块缩进操作（使用tab、s-Tab）。
4. 支持全局搜索替换（多个文件搜索替换）。

## 自定义快捷键

| 命令 | 说明 |
| :--: | :--: |
| sv \<filename\> | 打开一个文件，纵向分割布局（新文件会在当前文件下方界面打开）|
| vs \<filename\> | 横向分割布局（新文件会在当前文件右侧界面打开）|
| Ctrl-h | 切换到左侧的分割窗口 |
| Ctrl-j | 切换到下方的分割窗口 |
| Ctrl-l | 切换到右侧的分割窗口 |
| Ctrl-k | 切换到上方的分割窗口 |
| Ctrl-g | 跳转到函数定义或者声明 |
| Ctrl-y, | emmet自动补全快捷 |
| -- | -- |
| F2 | 打开or关闭行号，同时打开or关闭gitgutter（文件变化提示） |
| F3 | 打开or关闭复制支持 |
| F4 | 折叠or展开代码（默认打开文件不折叠） |
| F5 | 打开or关闭目录树 |
| F6 | 打开or关闭语法检查（大文件时影响性能） |
| F7 | flake8 check |
| F8 | Glog，展示文件的git history |
| F9 | 配合Glog，查看文件前一个版本 |
| f10 | 配合Glog，查看文件后一个版本 |
| -- | -- |
| space | 折叠/展开代码 |
| -- | -- |
| Shift-i | 目录是否显示隐藏文件（NERDTree）。便于git开发，默认永远不显示.git。 |

## 跳转

| 命令 | 说明 |
| :--: | :--: |
| Ctrl-o | jump back to where you where before invoking the command 和 Ctrl-g、ctrl-i 配合使用 |
| ctrl-i | jump forward |
| ctrl-^ | 跳转到上一个编辑的文件 |
| -- | -- |
| zz | move current line to the middle of the screen |
| zt | move current line to the top of the screen |
| zb | move current line to the bottom of the screen |

## 搜索

| 命令 | 说明 |
| :--: | :--: |
| :/pattern\<CR\> | 搜索所有包含pattern的单词（向上搜索） |
| :?pattern\<CR\> | 搜索所有包含pattern的单词（向下搜索） |
| n | 朝同一方向搜索 |
| N | 反方向搜索 |
| :/ pattern\<CR\> | 单词前加空格，精确匹配 |
| :/^pattern\<CR\> | 搜索仅在行首出现 |
| :/pattern$\<CR\> | 搜索仅在行末出现 |
| \\^ \\$ | 特殊字符的搜索加反斜杠 |

## 搜索替换

[http://vim.wikia.com/wiki/Search_and_replace](http://vim.wikia.com/wiki/Search_and_replace)
[http://vim.wikia.com/wiki/Search_and_replace_in_multiple_buffers](http://vim.wikia.com/wiki/Search_and_replace_in_multiple_buffers)

| 命令 | 说明 |
| :-- | :--: |
| :s/foo/bar/g | Change each 'foo' to 'bar' in the current line. |
| :%s/foo/bar/g | Change each 'foo' to 'bar' in all the lines. |
| :5,12s/foo/bar/g | Change each 'foo' to 'bar' for all lines from line 5 to line 12 (inclusive). |
| :'a,'bs/foo/bar/g | Change each 'foo' to 'bar' for all lines from mark a to mark b inclusive (see Note below). |
| :'<,'>s/foo/bar/g | When compiled with +visual, change each 'foo' to 'bar' for all lines within a visual selection. Vim automatically appends the visual selection range ('<,'>) for any ex command when you select an area and enter :. Also, see Note below. |
| :.,$s/foo/bar/g | Change each 'foo' to 'bar' for all lines from the current line (.) to the last line ($) inclusive. |
| :.,+2s/foo/bar/g | Change each 'foo' to 'bar' for the current line (.) and the two next lines (+2). |
| :g/^baz/s/foo/bar/g | Change each 'foo' to 'bar' in each line starting with 'baz'. |
| -- | -- |
| :arg \*.py | All \*.py files in current directory. |
| :argadd \*.md | And all  \*.md files. |
| :arg | Optional: Display the current arglist. |
| :argdo %s/pattern/replace/ge \| update | Search and replace in all files in arglist. |


## 删除

| 命令 | 说明 |
| :--: | :--: |
| x | 删除当前光标处的字符 |
| X | 删除光标左边的字符 |
| D | 删除从当前光标到本行末尾的字符 |
| J | 删除两行之间的换行符 (亦可用于合并两行）|
| dmove | 删除从当前光标到move所给位置的字符 |
| dd | 删除当前行 |
| :line**d** | 删除指定行 |
| :line,line**d** | 删除指定范围内的行 |


# 相关文档

1. [Building-Vim-from-source](https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source)
2. [https://github.com/Valloric/YouCompleteMe](https://github.com/Valloric/YouCompleteMe)
3. [https://github.com/VundleVim/Vundle.vim](https://github.com/VundleVim/Vundle.vim)
4. [vim与Python真乃天作之合](http://codingpy.com/article/vim-and-python-match-in-heaven/)
5. [https://valloric.github.io/YouCompleteMe/](https://valloric.github.io/YouCompleteMe/)
6. [http://vim.wikia.com/wiki/Search_and_replace](http://vim.wikia.com/wiki/Search_and_replace)
7. [http://vim.wikia.com/wiki/Search_and_replace_in_multiple_buffers](http://vim.wikia.com/wiki/Search_and_replace_in_multiple_buffers)
