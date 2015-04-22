---
layout: post
title: "My Vim Configuration"
date: 2014-04-09 18:35:16 +0800
comments: true
categories: Linux 
keywords: vim, vi, viminfo, vimrc, linux, ubuntu, mac, configuration
---

- This is the vim configuration of my mac. 
- edit the file in the /usr/share/vim named "vimrc"
- Some of them need to install some plugins and the command line will make sense
<!--more-->
```

" Configuration file for vim
set modelines=0     " CVE-2007-2438
set number
" Normally we use vim-extensions. If you want true vi-compatibility
" remove change the following statements
set nocompatible    " Use Vim defaults instead of 100% vi compatibility
set backspace=2     " more powerful backspacing 
" Don't write backup file if vim is being called by "crontab -e"
au BufWrite /private/tmp/crontab.* set nowritebackup
" Don't write backup file if vim is being called by "chpass"
au BufWrite /private/etc/pw.* set nowritebackup
set autoread
nmap <leader>w :w!<cr>
"map <leader>e :e! ~/.vim_runtime/vimrc<cr>
" autocmd! bufwritepost vimrc source ~/.vim_runtime/vimrc
set so=7
set ruler
set cmdheight=2
set hid
set magic
set noerrorbells
syntax enable

"ctag和taglist
let Tlist_Ctags_Cmd='/usr/local/bin/ctags'
let Tlist_Show_One_File=1
let Tlist_Exit_OnlyWindow=1
let Tlist_WinWidth=30
let Tlist_Process_File_Always=1
let Tlist_Use_SingleClick=1
let Tlist_Auto_Open=1
map<F8> :Tlist<CR>
set tags=tags;
set autochdir
 "nmap ct :!ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>

"配色
colorscheme desert
 
"python自动补全
let g:pydiction_location='/usr/share/vim/vim73/ftplugin/complete-dict'
let g:pydiction_menu_height=15
"winmanager
let g:winManagerwindowLayout='FileExplorer|TagList'
nmap wm :WMToggle<CR>

"nerdtree
let NERDChristmasTree=1
let NERDTreeAutoCenter=1
let NERDTreeMouseMode=2
let NERDTreeShowBookmarks=1
let NREDTreeShowFiles=1
let NERDTreeShowHidden=1
let NERDTreeShowLineNumbers=1
let NERDTreeWinPos='left'
let NERDTreeWinSize=31
"nnoremap f :NERDTreeToggle
nnoremap ff :NERDTree<CR>     

set smartcase
set hlsearch
set tabstop=4
set noexpandtab
set shiftwidth=4
set smarttab
set confirm
set autoindent
set cindent
set softtabstop=4
set history=700
set nobackup
set noswapfile
set ignorecase
set incsearch
set gdefault
set langmenu=zh_CN.UTF-8
set helplang=cn
set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [POS=%l,%v][%p%%]\ %{strftime(\"%d/%m/%y\     -\ %H:%M\")}
set laststatus=2

filetype on
filetype plugin on
filetype plugin indent on
filetype indent on
set viminfo+=!
set iskeyword+=_,$,@,%,#,-
set linespace=0
set backspace=2

set mouse=a
set selection=exclusive
set selectmode=mouse,key
set report=0
set shortmess=atl
set showmatch
"set fillchars=vert:\,stl:\,stlnc:\
set matchtime=5
 " 能够漂亮地显示.NFO文件
set encoding=utf-8
function! SetFileEncodings(encodings)
    let b:myfileencodingsbak=&fileencodings
    let &fileencodings=a:encodings
endfunction
function! RestoreFileEncodings()
    let &fileencodings=b:myfileencodingsbak
    unlet b:myfileencodingsbak
endfunction

au BufReadPre *.nfo call SetFileEncodings('cp437')|set ambiwidth=single
au BufReadPost *.nfo call RestoreFileEncodings()

" 高亮显示普通txt文件（需要txt.vim脚本）
au BufRead,BufNewFile *  setfiletype txt

" C的编译和运行
map <F5> :call CompileRunGcc()<CR>
func! CompileRunGcc()
exec "w"
exec "!gcc % -o %<"
exec "! ./%<"
endfunc

" C++的编译和运行
map <F6> :call CompileRunGpp()<CR>
func! CompileRunGpp()
exec "w"
exec "!g++ % -o %<"
exec "! ./%<"
endfunc

"Markdown to HTML  
nmap <leader>md :%!/usr/local/bin/Markdown.pl --html4tags <cr>

```