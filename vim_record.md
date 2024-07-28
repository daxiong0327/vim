## vim练习
最开始的练习使用vimtutor来做, 里面有很多自己以前从没用过的命令。可以极大的提升编辑效率。

```shell
# 直接在终端输入 vimtutor 进行练习

vimtutor

```
因为目前手上只有Mac os 系统，所以一下的配置都偏向于Mac系统。但是对于windows 系统和Linux来说原理也是一样的。只是快捷键的配置略有不同。

## Mac 安装 macvim

```shell
brew install macvim
# 创建软连接
ln -s /usr/local/bin/mvim /usr/local/bin/vim

```
## vundle 
Vundle 是 Vim bundle 的简称,使用 git 来管理 vim 插件

```shell
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

## vimrc 文件配置

```vim
vim ~/.vimrc

"Vundle 配置

set nocompatible	"required 关闭与vi的兼容模式

filetype off		"required 禁用文件类型检查
set rtp+=~/.vim/bundle/Vundle.vim "set the runtime path to include Vundle and initialize
call vundle#begin()
"-------------------------------------------
" Vundle 管理
Plugin 'gmarik/Vundle.vim' "let Vundle manage Vundle, required
Plugin 'vim-scripts/indentpython.vim'
Plugin 'vim-scripts/syntastic'
Plugin 'nvie/vim-flake8'
Plugin 'Valloric/YouCompleteMe'
Plugin 'scrooloose/nerdtree'
Plugin 'Exafunction/codeium.vim'
"markdown 插件--------
Plugin 'plasticboy/vim-markdown'
"补全 python
Plugin 'davidhalter/jedi'
" 自动补全括号的插件，包括小括号，中括号，以及花括号
Plugin 'jiangmiao/auto-pairs'
" 可以快速对齐的插件
Plugin 'junegunn/vim-easy-align'
" 可以使 nerdtree 的 tab 更加友好些
Plugin 'jistr/vim-nerdtree-tabs'
" 查看当前代码文件中的变量和函数列表的插件，
" 可以切换和跳转到代码中对应的变量和函数的位置
" 大纲式导航, Go 需要 https://github.com/jstemmer/gotags 支持
Plugin 'majutsushi/tagbar'
" Vim状态栏插件，包括显示行号，列号，文件类型，文件名，以及Git状态
Plugin 'vim-airline/vim-airline'
" 下面两个插件要配合使用，可以自动生成代码块
Plugin 'SirVer/ultisnips'
Plugin 'honza/vim-snippets'

" 快速跳转
Plugin 'easymotion/vim-easymotion'
" go 主要插件
Plugin 'fatih/vim-go', { 'tag': '*' }
" go 中的代码追踪，输入 gd 就可以自动跳转
Plugin 'dgryski/vim-godef'

" All of your Plugins must be added before the following line
call vundle#end()            " required

" -------------------------------------------- 基础配置
set number 			"显示行号
set nowrap			"禁止换行
set tabstop=4 		"设置 Tab 宽为 4 个空格
set scrolloff=3		"距离顶部和底部3行
set encoding=utf-8	"编码格式
set fenc=utf-8		"编码
set mouse=a			"启用鼠标
set hlsearch		"搜索高亮
set clipboard=unnamed "将vim中无名寄存器中的内容与系统剪贴板同步
set statusline+=\{…\}%3{codeium#GetStatusString()} "获取codeium状态
set cursorline 		"突出显示当前行
" set cursorcolumn 	" 突出显示当前列
set showmatch 		" 显示括号匹配
syntax on			"语法高
" tab 缩进
set tabstop=4 		" 设置Tab长度为4空格
set shiftwidth=4 	" 设置自动缩进长度为4空格
set autoindent 		" 继承前一行的缩进方式，适用于多行注释
" 退出插入模式指定类型的文件自动保存
au InsertLeave *.go,*.sh,*.py,*.c,*.h,*.java,*.md,*.cpp write

"----------------------------------------------
" YouCompleteMe 配置
let g:ycm_global_ycm_extra_conf = '~/.vim/bundle/YouCompleteMe/.ycm_extra_conf.py'
let g:ycm_collect_identifiers_from_tag_files = 1
let g:ycm_confirm_extra_conf = 0
let g:ycm_key_list_select_completion = ['<D-j>', '<Down>']
let g:ycm_key_list_previous_completion = ['<D-k>', '<Up>']
" 启用语法错误检查
let g:ycm_show_diagnostics_ui = 1

" 禁用自动补全弹出窗口
let g:ycm_auto_trigger = 1

" 设置补全触发键
"inoremap <silent> <D-Space> <C-x><C-o>

" 设置 GoToDefinitionElseDeclaration 快捷键
nmap <leader>gd :YcmCompleter GoToDefinitionElseDeclaration<CR>

"开启关闭文件目录快捷键设置---------------------------------
map <F1> :NERDTreeToggle<CR>
" 设置快捷键来开启或关闭预览
" 这里使用 mp 来切换预览
nmap mp :MarkdownPreviewToggle<CR>

"----------------------------------------------
" 窗口分割快捷键映射

" Command + d 竖向拆分
noremap vs :vsplit<CR>
" Command + D 横向拆分
noremap hs :split<CR>
" Command + w 关闭当前窗口
noremap cw :close<CR>

" 移动窗口
nnoremap wh <C-w>h
nnoremap wj <C-w>j
nnoremap wk <C-w>k
nnoremap wl <C-w>l

" 关闭当前窗口
nnoremap cw :close<CR>

"----------------------------------------------
" 普通模式下光标跳转快捷键
nnoremap co <C-o>
nnoremap ci <C-i>
" 可视化模式下光标跳转快捷键
vnoremap co <C-o>
vnoremap ci <C-i>
```

## Codeium 插件

```shell
# vim 安装
git clone https://github.com/codeium-org/codeium.vim ~/.vim/bundle/codeium.vim


配置方法：
https://blog.benehub.tech/how-to-install-the-codeium-plugin-on-vim-and-neovim
```

## YouCompleteMe 编译


```shell
git submodule update --init --recursive # 更新库
install.py --go-completer --rest-completer --verbose # 支持python go rust
```



## 快捷键
```txt
gd 跳转到函数的声明

```
