---
title: Vim
type: docs
---

# Vim

## .vimrc

```sh
set nocompatible
set t_RV=
filetype off

call plug#begin('~/.vim/plugged')

Plug 'scrooloose/nerdtree'

call plug#end()

filetype plugin indent on
syntax enable
syntax on

autocmd vimenter * NERDTree | wincmd p
autocmd bufenter * if(winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | quit | endif

set clipboard=unnamed

set nobackup
set novisualbell
set visualbell t_vb=
set mouse=a

set ruler
set number
set showcmd
set showmode

set scrolloff=3
set backspace=indent,eol,start

set hlsearch
set incsearch
set showmatch
set ignorecase

set autoindent smartindent
set shiftwidth=4 softtabstop=4 tabstop=4 expandtab

set background=dark
set t_Co=265
colorscheme papercolor
```