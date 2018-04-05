# Vim-Haskell-Manual

## Abstract

This is document for person who is suffered by ghc-mod but still loves vim. It would recommend to use Manjaro or Arch linux for Haskell.

## Prerequisite

* [Stack](https://www.haskellstack.org/)
* [Neovim](https://neovim.io/)
* [Vim Plug](https://github.com/junegunn/vim-plug)
* [tmux](https://github.com/gpakosz/.tmux)

## Installtion

### Installation List

* Haskell - IDE - Engine
* Brittany (For Arch, use AUR package)
* tmux (Oh-my-tmux)

### Installation Procedure

#### 1) HIE

Check your ghc version. By stack, you can get ghc >= 8.2.2

```bash
git clone https://github.com/haskell/haskell-ide-engine
cd haskell-ide-engine
stack install
```

#### 2) Brittany

For Arch or Manjaro,

```bash
yaourt -Syua brittany
```

#### 3) Vimrc

Basic Neovim Setting

```vim
" Syntax Highlighting
if has("syntax")
    syntax on
endif

" Indent
set autoindent
set cindent

" Line Number
set nu

" Highlight
set cursorline

" On
syntax on
filetype plugin indent on

" Tab to Space
set expandtab
set shiftwidth=2
set tabstop=2

let base16colorspace=256
```


Useful Haskell vim-plug list

```vim
" Haskell
Plug 'enomsg/vim-haskellconcealplus'
Plug 'neovimhaskell/haskell-vim'
Plug 'vim-syntastic/syntastic'
" -- Require : Haskell-IDE-Engine
Plug 'autozimu/LanguageClient-neovim', {
    \ 'branch': 'next',
    \ 'do': './install.sh'
    \ }
" -- Require : Brittany
Plug 'sbdchd/neoformat'
Plug 'itchyny/vim-haskell-indent'
Plug 'mpickering/hlint-refactor-vim'

" Code Completion
Plug 'ervandew/supertab'
Plug 'Raimondi/delimitMate'
Plug 'Shougo/deoplete.nvim', { 'do': ':UpdateRemotePlugins' }

" Indent
Plug 'godlygeek/tabular'

" Tmux
Plug 'jpalardy/vim-slime'
```

And Setting for Haskell

```vim
" Vim Slime
let g:slime_target="tmux"

" Tabularize
let g:haskell_tabular = 1

vmap a= :Tabularize /=<CR>
vmap a; :Tabularize /::<CR>
vmap a- :Tabularize /-><CR>

" HIE
let g:LanguageClient_serverCommands = {
	\ 'haskell': ['hie', '--lsp']
	\ }

" Deoplete
let g:deoplete#enable_at_startup = 1
```

If you bother to customize vim, then there is wonderful solution! - Just get my neovim script.

```bash
# If you don't have .config/nvim then should type next command
mkdir -p .config/nvim/

# Should do
git clone https://github.com/Axect/Vim
cp Vim/init.vim .config/nvim/init.vim
nvim +PlugInstall
```

#### Additional tmux setting

```tmux
bind s setw synchronize-panes on
bind S setw synchronize-panes off
```

## Procedure

1. Open `tmux`
2. Split Vertically & Synchronize pane (`C-b, s`)
3. Move to project folder & Unsync (`C-b, S`)
4. Turn on neovim in one pane, and ghci in the other pane
5. By vim-slime, we can send code to ghci by `C-c-c`
6. If finish then `:! stack build`
7. And also you can use `:! stack exec <your_project_name>`

