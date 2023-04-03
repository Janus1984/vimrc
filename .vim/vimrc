
" -------------------------------------------------
" 👻common settings👻
" -------------------------------------------------
set nocompatible          " 关闭vi兼容模式
filetype plugin indent on " 开启文件类型检测
syntax on                 " 开启语法高亮
set mouse=a               " 开启鼠标
" set virtualedit=all        开启游标可以定位到没有字符的地方 

set splitbelow             " Open new windows below the current window.
set splitright             " Open new windows right of the current window.

" 显示不可见字符
set list
" 自定义显示的字符格式
set listchars=tab:▸\ ,trail:⋅,extends:❯,precedes:❮

"set nofoldenable           默认关闭代码折叠
" 可以修改 .vimrc.local 开启代码折叠
 "set foldenable
" set foldmethod=syntax

set backspace=indent,eol,start  " 智能回删

set number                " 显示行号          nu
set relativenumber        " 显示相对行号      rnu
set ruler                 " 显示标尺信息

set expandtab             " Tab 替换为空格    et
set smartindent           " 智能缩进          si

set softtabstop=4         " Tab 缩进单位      sts
set shiftwidth=4          " 自动缩进单位      sw
set encoding=utf-8        " UTF-8 编码
set showbreak=↳           " 显示折行符
set nowrap                " 禁止折行

set ignorecase            " 搜索忽略大小写    ic
set incsearch             " 搜索时实时高亮    is
set hlsearch              " 高亮所有搜索结果  hls

"set cursorcolumn           高亮当前列        cuc
set cursorline            " 高亮当前行        cul

set scrolloff=7           " 屏幕顶/底部保持 7 行文本
set laststatus=2          " 显示状态栏
"set showtabline=2          显示标签栏
set showcmd               " 显示输入的命令
set wildmenu              " Vim 命令行提示
set nobackup              " 不生成临时文件
set noswapfile            " 不生成 swap 文件
set autoread              " 自动加载外部修改
set confirm               " 弹出文件未保存确认

" 重新打开文件回到上次编辑的位置
if has("autocmd")
    au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
endif
" undo file
set history=1024
set undofile
set undodir=~/.vim/files/undo

let g:mapleader = "g"
let g:maplocalleader = ','

" -------------------------------------------------
" 👻key-map👻
" -------------------------------------------------

" map kj to esc 
inoremap kj <ESC>
" map H L to head/end of line
nnoremap <silent><expr> H (v:count == 0 ? '^' : '^^' . (v:count == 1 ? (v:count - 1) . 'l' : ''))
nnoremap <silent><expr> L (v:count == 0 ? '$' : '^$' . (v:count == 1 ? (v:count - 1) . 'h' : ''))
xnoremap <silent><expr> H (v:count == 0 ? '^' : '^^' . (v:count == 1 ? (v:count - 1) . 'l' : ''))
xnoremap <silent><expr> L (v:count == 0 ? '$' : '^$' . (v:count == 1 ? (v:count - 1) . 'h' : ''))

" map q to save all and quit; map Q to macro
nnoremap Q q
vmap Q <ESC>Q
nnoremap <silent> q :call <SID>uni_wq()<CR>
vmap q <ESC>q
nnoremap <silent> <C-q> :call <SID>uni_bd()<CR>
vmap <C-q> <ESC><C-q>
imap <C-q> <ESC><C-q>
tmap <C-q> <ESC><C-q>

function! s:uni_bd() abort
    let l:nr = win_getid()
    let l:wi = getwininfo(l:nr)[0]
    let l:ty = &buftype
    if l:ty == 'popup'
        FloatermKill
    elseif l:ty == 'quickfix'
        bd!
        cclose
    elseif l:wi.terminal == 1
        if exists('b:floaterm_cmd')
            FloatermKill
        else
            bd!
        endif
    else
        wa!
        bd!
    endif
endfunction

function! s:uni_wq() abort
    let l:nr = win_getid()
    let l:wi = getwininfo(l:nr)[0]
    let l:ty = &buftype
    if l:ty == 'popup'
        FloatermKill
    elseif l:ty == 'quickfix'
        q " cclose
    elseif l:wi.terminal == 1
        if exists('b:floaterm_cmd')
            FloatermKill
        else
            q!
        endif
    else
        wa!
        q!
    endif
endfunction

" buffers switch
" <F1> save and switch to last buffer
" <F2> save and switch to previous buffer
" <F3> save and switch to next buffer
" <F4> close current buffer
nnoremap <silent> <F1> :wa<CR>:b#<CR>
nnoremap <silent> <F2> :wa<CR>:bp<CR>
nnoremap <silent> <F3> :wa<CR>:bn<CR>
nnoremap <silent> <F4> :bd<CR>
inoremap <silent> <F1> <ESC>
vnoremap <silent> <F1> <ESC>
vmap <F2> <ESC><F2>
imap <F2> <ESC><F2>
tmap <F2> <ESC><F2>
vmap <F3> <ESC><F3>
imap <F3> <ESC><F3>
tmap <F3> <ESC><F3>
vmap <F4> <ESC><F4>
imap <F4> <ESC><F4>
tmap <F4> <ESC><F4>

" C/C++ build and run
" <F5> configure and build project 
nnoremap <F5> :AsyncTasks project-build<CR>
vmap <F5> <ESC><F5>
imap <F5> <ESC><F5>
tmap <F5> <ESC><F5>
" <F6> only configure project;<C-F6> ccmake 
nnoremap <F6> :AsyncTasks project-config<CR>
vmap <F6> <ESC><F6>
imap <F6> <ESC><F6>
tmap <F6> <ESC><F6>
nnoremap <C-F6> :AsyncTasks project-ccmake<CR>
vmap <C-F6> <ESC><C-F6>
imap <C-F6> <ESC><C-F6>
tmap <C-F6> <ESC><C-F6>
" <F7> build and run single file
nnoremap <F7> :AsyncTasks file-build file-run<CR>
vmap <F7> <ESC><F7>
imap <F7> <ESC><F7>
tmap <F7> <ESC><F7>
" <F8> quickfix
nnoremap <silent> <F8> :wa<CR>:QFix<CR>
vmap <F8> <ESC><F8>
imap <F8> <ESC><F8>
tmap <F8> <ESC><F8>

" others
" <F9> 调出悬浮终端
nnoremap <silent> <F9> :FloatermToggle<CR>
tnoremap <silent> <F9> <C-\><C-n>:FloatermToggle<CR>
" <F10> 调出目录和标签树
nnoremap <silent> <F10> :wa<CR>:NERDTreeToggle<CR><C-w>l:Vista!!<CR><C-w>h
vmap <F10> <ESC><F10>
imap <F10> <ESC><F10>
tmap <F10> <ESC><F10>
" <F11> 暂时保留，系统默认是全屏
" <F12> 取消搜索高亮
" <Space>h 取消搜索高亮
nnoremap <silent> <Space>h :nohlsearch<CR>
" vmap <Space> <ESC><Space>
" imap <Space> <ESC><Space>
" tmap <Space> <ESC><Space>

" -------------------------------------------------
" 👻easymotion👻
" -------------------------------------------------
map t <Plug>(easymotion-bd-f)
nmap t <Plug>(easymotion-overwin-f)
map T <Plug>(easymotion-bd-w)
nmap T <Plug>(easymotion-overwin-w)
let g:EasyMotion_do_mapping = 0

" -------------------------------------------------
" 👻airline👻
" -------------------------------------------------
let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#buffer_nr_show=1
let g:airline#extensions#tabline#formatter = 'unique_tail_improved'

" -------------------------------------------------
" 👻vim-which-key👻 
" -------------------------------------------------
set timeoutlen=500        " Time to wait for a command
let g:which_key_fallback_to_native_key=1 " let 'gg' work correct
"nnoremap <silent> <leader> :WhichKey '<Space>'<CR>
nnoremap <silent> <Space>      :<C-u>WhichKey '<Space>'<CR>
nnoremap <silent> <localleader> :<C-u>WhichKey  ','<CR>
nnoremap <silent> g :<C-u>WhichKey  'g'<CR>

" -------------------------------------------------
" 👻NERDTree👻 
" -------------------------------------------------
nnoremap <Space>n :NERDTreeToggle<CR>
"nnoremap <C-n> :NERDTree<CR>
"nnoremap <silent> <F10> :wa<CR>:NERDTreeToggle<CR><C-w>l:Vista!!<CR>
"vmap <F10> <ESC><F10>
"imap <F10> <ESC><F10>
"tmap <F10> <ESC><F10>
" nnoremap <Space>f :NERDTreeFind<CR>

" -------------------------------------------------
" 👻vim-ibus👻
" -------------------------------------------------
let g:ibus#layout = 'rime'
let g:ibus#engine = 'Rime'

" -------------------------------------------------
" 👻LeaderF👻
" -------------------------------------------------
" don't show the help in normal made
let g:Lf_HideHelp = 1
let g:Lf_UseCache = 0
let g:Lf_UseVersionControlTool = 0
let g:Lf_IgnoreCurrentBufferName = 1
" popup mode
let g:Lf_WindowPosition = 'popup'
let g:Lf_PreviewInPopup = 1
let g:Lf_PreviewCode = 1
"let g:Lf_StlSeparator = { 'left': "\ue0b0", 'right': "\ue0b2", 'font': "DejaVu Sans Mono for Powerline" }
"let g:Lf_PreviewResult = {'Function': 0, 'BufTag': 0 }

let g:Lf_ShortcutF = ''
let g:Lf_ShortcutB = ''
noremap ,k :Leaderf rg<CR>
noremap ,o :Leaderf file<CR>
noremap ,b :Leaderf! buffer<CR>
noremap ,m :Leaderf! mru<CR>
noremap ,t :Leaderf! bufTag<CR>
noremap ,l :Leaderf line<CR>
noremap ,x :Leaderf command<CR>
noremap ,: :Leaderf! cmdHistory<CR>
noremap ,/ :Leaderf! searchHistory<CR>
noremap ,w :Leaderf! window<CR>
noremap ,h :Leaderf! marks<CR>
noremap ,j :Leaderf! jumps<CR>
noremap ,n :Leaderf function<CR>
noremap ,q :Leaderf quickfix<CR>

noremap ,i :<C-U><C-R>=printf("Leaderf! rg --current-buffer -e %s", expand("<cword>"))<CR><CR>
noremap ,a :<C-U><C-R>=printf("Leaderf! rg -e %s", expand("<cword>"))<CR><CR>
xnoremap ,i :<C-U><C-R>=printf("Leaderf! rg --current-buffer -F -e %s", leaderf#Rg#visual())<CR><CR>
xnoremap ,a :<C-U><C-R>=printf("Leaderf! rg -F -e %s", leaderf#Rg#visual())<CR><CR>
noremap ,. :<C-U>Leaderf! --recall<CR>

" -------------------------------------------------
" 👻asynctasks.vim👻	 
" -------------------------------------------------
"  https://github.com/skywind3000/asynctasks.vim
let g:asyncrun_open = 10
let g:asynctasks_term_pos = 'floaterm_reuse'
let g:asynctasks_term_rows = 10
let g:asynctasks_term_cols = 50
let g:asynctasks_term_reuse = 0
let g:asynctasks_term_focus = 0
let g:asyncrun_rootmarks = ['.tasks', '.root', '.git', '.svn', '.vscode']

function! AsyncTaskMultiple(first, ...)
    if len(a:000) >= 1
        if a:first == 0
            cclose
        else
            FloatermHide!
        endif
        let l:tmp = ""
        for task in a:000[1:]
            let l:tmp .= "'".l:task."',"
        endfor
        let l:tmp = l:tmp[:-1]
        let g:asyncrun_exit = "if g:asyncrun_code == 0 | call AsyncTaskMultiple(0, ".l:tmp.") | else | call AsyncTaskMultiple(0) | endif"
        exec "AsyncTask ".a:000[0]
    else
        let g:asyncrun_exit = ""
    endif
endfunction
command! -nargs=+ AsyncTasks   :call AsyncTaskMultiple(1, <f-args>)

" -------------------------------------------------
" 👻coc.nvim👻	 
" -------------------------------------------------
"https://github.com/neoclide/coc.nvim
let g:coc_global_extensions = ['coc-clangd', 'coc-pyright', 'coc-snippets', 'coc-pairs', 'coc-json', 'coc-git', 'coc-sh']
" Set internal encoding of vim, not needed on neovim, since coc.nvim using some
" unicode characters in the file autoload/float.vim
set encoding=utf-8

" TextEdit might fail if hidden is not set.
set hidden

" Some servers have issues with backup files, see #649.
set nobackup
set nowritebackup

" Give more space for displaying messages.
set cmdheight=1

" Having longer updatetime (default is 4000 ms = 4 s) leads to noticeable
" delays and poor user experience.
set updatetime=300

" Don't pass messages to |ins-completion-menu|.
set shortmess+=c

" Always show the signcolumn, otherwise it would shift the text each time
" diagnostics appear/become resolved.
if has("nvim-0.5.0") || has("patch-8.1.1564")
  " Recently vim can merge signcolumn and number column into one
  set signcolumn=number
else
  set signcolumn=yes
endif

" 补全列表长度
" https://zhuanlan.zhihu.com/p/565681501
set pumheight=10

" Use tab for trigger completion with characters ahead and navigate
" NOTE: There's always complete item selected by default, you may want to enable
" no select by `"suggest.noselect": true` in your configuration file
" NOTE: Use command ':verbose imap <tab>' to make sure tab is not mapped by
" other plugin before putting this into your config
inoremap <silent><expr> <TAB>
      \ coc#pum#visible() ? coc#pum#next(1) :
      \ CheckBackspace() ? "\<Tab>" :
      \ coc#refresh()
inoremap <expr><S-TAB> coc#pum#visible() ? coc#pum#prev(1) : "\<C-h>"

" Make <CR> to accept selected completion item or notify coc.nvim to format
" <C-g>u breaks current undo, please make your own choice
inoremap <silent><expr> <CR> coc#pum#visible() ? coc#pum#confirm()
                              \: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"

function! CheckBackspace() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <c-space> to trigger completion
if has('nvim')
  inoremap <silent><expr> <c-space> coc#pum#visible() ? coc#pum#confirm() : coc#refresh()
else
  inoremap <silent><expr> <c-@> coc#pum#visible() ? coc#pum#confirm() : coc#refresh()
endif  

" Use `[g` and `]g` to navigate diagnostics
" Use `:CocDiagnostics` to get all diagnostics of current buffer in location list.
nmap <silent> gl[ <Plug>(coc-diagnostic-prev)
nmap <silent> gl] <Plug>(coc-diagnostic-next)

" GoTo code navigation.
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gI <Plug>(coc-implementation)
nmap <silent> gD <Plug>(coc-declaration)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window.
nnoremap <silent> K :call <SID>show_documentation()<CR>

function! s:show_documentation()
  if (index(['vim','help'], &filetype) >= 0)
    execute 'h '.expand('<cword>')
  elseif (coc#rpc#ready())
    call CocActionAsync('doHover')
  else
    execute '!' . &keywordprg . " " . expand('<cword>')
  endif
endfunction

" Highlight the symbol and its references when holding the cursor.
autocmd CursorHold * silent call CocActionAsync('highlight')

" Symbol renaming.
nmap gR <Plug>(coc-rename)

" Formatting selected code.
"xmap <leader>f  <Plug>(coc-format-selected)
"nmap <leader>f  <Plug>(coc-format-selected)
xmap gf  <Plug>(coc-format-selected)
nmap gf  <Plug>(coc-format-selected)

augroup coc_group_ts_json
  autocmd!
  " Setup formatexpr specified filetype(s).
  autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
  " Update signature help on jump placeholder.
  autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
augroup end

" Applying codeAction to the selected region.
" Example: `<leader>aap` for current paragraph
xmap ga  <Plug>(coc-codeaction-selected)
nmap ga  <Plug>(coc-codeaction-selected)

" Remap keys for applying codeAction to the current buffer.
nmap gac  <Plug>(coc-codeaction)
" Apply AutoFix to problem on the current line.
nmap gaq  <Plug>(coc-fix-current)

" Run the Code Lens action on the current line.
nmap gal <Plug>(coc-codelens-action)

" Map function and class text objects
" NOTE: Requires 'textDocument.documentSymbol' support from the language server.
xmap if <Plug>(coc-funcobj-i)
omap if <Plug>(coc-funcobj-i)
xmap af <Plug>(coc-funcobj-a)
omap af <Plug>(coc-funcobj-a)
xmap ic <Plug>(coc-classobj-i)
omap ic <Plug>(coc-classobj-i)
xmap ac <Plug>(coc-classobj-a)
omap ac <Plug>(coc-classobj-a)

" Remap <C-f> and <C-b> for scroll float windows/popups.
if has('nvim-0.4.0') || has('patch-8.2.0750')
  nnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  nnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
  inoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? "\<c-r>=coc#float#scroll(1)\<cr>" : "\<Right>"
  inoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? "\<c-r>=coc#float#scroll(0)\<cr>" : "\<Left>"
  vnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  vnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
endif

" Use CTRL-S for selections ranges.
" Requires 'textDocument/selectionRange' support of language server.
nmap <silent> <C-s> <Plug>(coc-range-select)
xmap <silent> <C-s> <Plug>(coc-range-select)

" Add `:Format` command to format current buffer.
command! -nargs=0 Format :call CocAction('format')

" Add `:Fold` command to fold current buffer.
command! -nargs=? Fold :call     CocAction('fold', <f-args>)

" Add `:OR` command for organize imports of the current buffer.
command! -nargs=0 OrgImport   :call     CocAction('runCommand', 'editor.action.organizeImport')

" Add (Neo)Vim's native statusline support.
" NOTE: Please see `:h coc-status` for integrations with external plugins that
" provide custom statusline: lightline.vim, vim-airline.
set statusline^=%{coc#status()}
"set statusline^=%{get(b:,'coc_git_status','')}
autocmd User CocStatusChange redrawstatus

" Mappings for CoCList
" Show all diagnostics.
nnoremap <silent> gla :<C-u>CocList diagnostics<cr>
" Manage extensions.
nnoremap <silent> gle  :<C-u>CocList extensions<cr>
" Show commands.
nnoremap <silent> glc  :<C-u>CocList commands<cr>
" Find symbol of current document.
nnoremap <silent> glo  :<C-u>CocList outline<cr>
" Search workspace symbols.
nnoremap <silent> gls  :<C-u>CocList -I symbols<cr>
" Do default action for next item.
nnoremap <silent> glj  :<C-u>CocNext<CR>
" Do default action for previous item.
nnoremap <silent> glk  :<C-u>CocPrev<CR>
" Resume latest coc list.
nnoremap <silent> glp  :<C-u>CocListResume<CR>

" coc-snippets
" Use <C-l> for trigger snippet expand.
imap <C-l> <Plug>(coc-snippets-expand)
" Use <C-j> for select text for visual placeholder of snippet.
vmap <C-j> <Plug>(coc-snippets-select)
" Use <C-j> for jump to next placeholder, it's default of coc.nvim
let g:coc_snippet_next = '<c-j>'
" Use <C-k> for jump to previous placeholder, it's default of coc.nvim
let g:coc_snippet_prev = '<c-k>'
" Use <C-j> for both expand and jump (make expand higher priority.)
imap <C-j> <Plug>(coc-snippets-expand-jump)
" Use <leader>x for convert visual selected code to snippet
xmap gx  <Plug>(coc-convert-snippet)

" -------------------------------------------------
" 👻coc-clangd👻
" -------------------------------------------------
" https://github.com/clangd/coc-clangd
nnoremap <silent> gcs :<C-u>CocCommand clangd.symbolInfo<CR>
nnoremap <silent> gch :<C-u>CocCommand clangd.switchSourceHeader vsplit<CR>
nnoremap <silent> gcm :<C-u>CocCommand clangd.memoryUsage<CR>
nnoremap <silent> gca :<C-u>CocCommand clangd.ast<CR>
nnoremap <silent> <Space>ci :<C-u>CocCommand clangd.install<CR>
nnoremap <silent> <Space>cu :<C-u>CocCommand clangd.Update<CR>

" -------------------------------------------------
" 👻vim-floaterm👻
" -------------------------------------------------
" https://github.com/voldikss/vim-floaterm
let g:floaterm_wintype = 'float'                 "float, split, vsplit
let g:floaterm_position = 'center'
let g:floaterm_width = 0.7
let g:floaterm_height = 0.7
"let g:floaterm_wintype = 'split'
"let g:floaterm_position = 'botright'
"let g:floaterm_height = 6

"let g:floaterm_autoclose     = 1
"let g:floaterm_autoinsert    = 1
let g:floaterm_rootmarks = ['.project', '.hg', '.svn', '.root', '.tasks', '.git']
"todo: input this to floaterm esc: set norelativenumber nonumber noeol nolist showbreak= signcolumn=no

"function s:on_floaterm_gf() abort
  "let f = findfile(expand('<cfile>'))
  "if !empty(f)
    "FloatermHide
    "execute 'e ' . f
  "endif
"endfunction

"augroup floaterm_gf_key
"autocmd FileType floaterm nnoremap <silent><buffer> gf :call <SID>on_floaterm_gf()<CR>
"augroup end

" -------------------------------------------------
" 👻vista.vim👻
" -------------------------------------------------
" https://github.com/liuchengxu/vista.vim
" By default vista.vim never run if you don't call it explicitly.
"
nnoremap <silent> <Space>t <C-w>l:<C-u>Vista!!<CR>
" If you want to show the nearest function in your statusline automatically,
" you can add the following line to your vimrc

"function! NearestMethodOrFunction() abort
  "return get(b:, 'vista_nearest_method_or_function', '')
"endfunction

"set statusline+=%{NearestMethodOrFunction()}

"autocmd VimEnter * call vista#RunForNearestMethodOrFunction()

" -------------------------------------------------
" 👻markdown-preview👻
" -------------------------------------------------
nmap <Space>m <Plug>MarkdownPreviewToggle

" -------------------------------------------------
" 👻undotree👻
" -------------------------------------------------
nnoremap <Space>u :UndotreeToggle<CR>

" -------------------------------------------------
" 👻nerdcommenter👻
" -------------------------------------------------
let g:NERDCreateDefaultMappings = 0
let g:NERDDefaultAlign = 'left'
let g:NERDSpaceDelims = 1
nnoremap gcc <Plug>NERDCommenterToggle
vnoremap gcc <Plug>NERDCommenterToggle

" -------------------------------------------------
" 👻snippet👻
" -------------------------------------------------
let g:UltiSnipsExpandTrigger=" s"
let g:UltiSnipsJumpForwardTrigger="<c-b>"
let g:UltiSnipsJumpBackwardTrigger="<c-z>"

" If you want :UltiSnipsEdit to split your window.
let g:UltiSnipsEditSplit="vertical"

" -------------------------------------------------
" 👻kitty👻
" -------------------------------------------------
" fix kitty backgroud color dose not work well in vim
" these settings must be placed before setting the colorscheme
" Mouse support
set mouse=a
set ttymouse=sgr
set balloonevalterm
" Styled and colored underline support
let &t_AU = "\e[58:5:%dm"
let &t_8u = "\e[58:2:%lu:%lu:%lum"
let &t_Us = "\e[4:2m"
let &t_Cs = "\e[4:3m"
let &t_ds = "\e[4:4m"
let &t_Ds = "\e[4:5m"
let &t_Ce = "\e[4:0m"
" Strikethrough
let &t_Ts = "\e[9m"
let &t_Te = "\e[29m"
" Truecolor support
let &t_8f = "\e[38:2:%lu:%lu:%lum"
let &t_8b = "\e[48:2:%lu:%lu:%lum"
let &t_RF = "\e]10;?\e\\"
let &t_RB = "\e]11;?\e\\"
" Bracketed paste
let &t_BE = "\e[?2004h"
let &t_BD = "\e[?2004l"
let &t_PS = "\e[200~"
let &t_PE = "\e[201~"
" Cursor control
let &t_RC = "\e[?12$p"
let &t_SH = "\e[%d q"
let &t_RS = "\eP$q q\e\\"
let &t_SI = "\e[5 q"
let &t_SR = "\e[3 q"
let &t_EI = "\e[1 q"
let &t_VS = "\e[?12l"
" Focus tracking
let &t_fe = "\e[?1004h"
let &t_fd = "\e[?1004l"
execute "set <FocusGained>=\<Esc>[I"
execute "set <FocusLost>=\<Esc>[O"
" Window title
let &t_ST = "\e[22;2t"
let &t_RT = "\e[23;2t"

" vim hardcodes background color erase even if the terminfo file does
" not contain bce. This causes incorrect background rendering when
" using a color theme with a background color in terminals such as
" kitty that do not support background color erase.
let &t_ut=''


" -------------------------------------------------
" 👻vim-plug👻
" -------------------------------------------------

call plug#begin()

Plug 'preservim/nerdtree'
Plug 'zhmars/vim-ibus'
Plug 'liuchengxu/vista.vim'
Plug 'liuchengxu/vim-which-key'
Plug 'archibate/QFixToggle', {'on': 'QFix'}
Plug 'mbbill/undotree'
Plug 'easymotion/vim-easymotion'
Plug 'tpope/vim-repeat'
" Plug 'bfrg/vim-cpp-modern'

" text objects
Plug 'tpope/vim-surround'
Plug 'wellle/targets.vim'

" Snippets 
Plug 'honza/vim-snippets'

" text objects
Plug 'tpope/vim-surround'
Plug 'wellle/targets.vim'

" Snippets 
Plug 'honza/vim-snippets'

" float terminal
Plug 'voldikss/vim-floaterm'

" lsp
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" comment
Plug 'preservim/nerdcommenter'

" fuzzy Find
Plug 'Yggdroot/LeaderF' , { 'do': ':LeaderfInstallCExtension' }

" git
Plug 'tpope/vim-fugitive'

" asynctasks.vim
Plug 'skywind3000/asynctasks.vim' 
Plug 'skywind3000/asyncrun.vim'

" theme
Plug 'morhetz/gruvbox'
Plug 'joshdick/onedark.vim'
Plug 'sheerun/vim-polyglot'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'

" tmux
Plug 'christoomey/vim-tmux-navigator'
Plug 'tpope/vim-obsession'

" markdown
Plug 'iamcco/markdown-preview.nvim', { 'do': 'cd app && yarn install' }

" vimdoc 中文版
"Plug 'yianwillis/vimcdoc'

call plug#end()

" -------------------------------------------------
" 👻theme👻
" -------------------------------------------------
"Use 24-bit (true-color) mode in Vim/Neovim when outside tmux.
"If you're using tmux version 2.2 or later, you can remove the outermost $TMUX check and use tmux's 24-bit color support
"(see < http://sunaku.github.io/tmux-24bit-color.html#usage > for more information.)
" 真彩色在floatterm中的颜色太眼瞎了。
" if (empty($TMUX))
"   if (has("nvim"))
"     "For Neovim 0.1.3 and 0.1.4 < https://github.com/neovim/neovim/pull/2198 >
"     let $NVIM_TUI_ENABLE_TRUE_COLOR=1
"   endif
"   "For Neovim > 0.1.5 and Vim > patch 7.4.1799 < https://github.com/vim/vim/commit/61be73bb0f965a895bfb064ea3e55476ac175162 >
"   "Based on Vim patch 7.4.1770 (`guicolors` option) < https://github.com/vim/vim/commit/8a633e3427b47286869aa4b96f2bfc1fe65b25cd >
"   " < https://github.com/neovim/neovim/wiki/Following-HEAD#20160511 >
"   if (has("termguicolors"))
"     set termguicolors
"   endif
" endif

set t_Co=256               " 开启 256 色（若终端支持）
set background=dark
autocmd vimenter * ++nested colorscheme gruvbox
" colorscheme onedark

"hi LineNrAbove guifg=#cc6666 ctermfg=red
"hi LineNrBelow guifg=#66cc66 ctermfg=green
"hi Normal ctermbg=none
"hi SignColumn ctermbg=none
"hi FloatermNC guifg=gray
