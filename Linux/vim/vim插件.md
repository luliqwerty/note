- vim-startify

```bash
很好，每次进入 vim 奶牛的话或令人发笑或令人深思
```

- nerdcommenter

```bash
the default <leader> key is  \ 
[count]<leader>cc |NERDCommenterComment|
给当前行或者选中的文本添加注释
Comment out the current line or text selected in visual mode.

[count]<leader>c<space> |NERDCommenterToggle|
切换注释状态 如果注释了就取消 没有就注释
Toggles the comment state of the selected line(s). If the topmost selected line is commented, all selected lines are uncommented and vice versa.

[count]<leader>cs |NERDCommenterSexy|
代码块注释选中的行
Comments out the selected lines with a pretty block formatted layout.

[count]<leader>cu |NERDCommenterUncomment|
取消注释选中的行
Uncomments the selected line(s).
```

- rainbow - 能够用颜色变化显示嵌套结构 不同（）{}会显示不同颜色
- vim-airline - 会在终端底部显示正在编辑什么文件等信息

- YouCompleteMe

```bash
"""""""""""" YouCompleteMe"""""""""""""""""""""""""""""""
set runtimepath+=~/.vim/bundle/YouCompleteMe
let g:ycm_collect_identifiers_from_tags_files = 1           " 开启 YCM 基于标签引擎
let g:ycm_collect_identifiers_from_comments_and_strings = 1 " 注释与字符串中的内容也用于补全
let g:syntastic_ignore_files=[".*\.py$"]
let g:ycm_seed_identifiers_with_syntax = 1                  " 语法关键字补全
let g:ycm_complete_in_comments = 1
let g:ycm_confirm_extra_conf = 0
let g:ycm_key_list_select_completion = ['<c-n>', '<Down>']  " 映射按键, 没有这个会拦截掉tab, 导致其他插件的tab不能用.
let g:ycm_key_list_previous_completion = ['<c-p>', '<Up>']
let g:ycm_complete_in_comments = 1                          " 在注释输入中也能补全
let g:ycm_complete_in_strings = 1                           " 在字符串输入中也能补全
let g:ycm_collect_identifiers_from_comments_and_strings = 1 " 注释和字符串中的文字也会被收入补全
let g:ycm_global_ycm_extra_conf='~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp/ycm/.ycm_extra_conf.py'
let g:ycm_show_diagnostics_ui = 0                           " 禁用语法检查
inoremap <expr> <CR> pumvisible() ? "\<C-y>" : "\<CR>" |            " 回车即选中当前项
nnoremap <c-j> :YcmCompleter GoToDefinitionElseDeclaration<CR>|     " 跳转到定义处
"let g:ycm_min_num_of_chars_for_completion=2                 " 从第2个键入字符就开始罗列匹配项
```

- LeaderF

```bash
模糊搜索插件，我现在还没有学会怎么使用
```

- nerdtree

```bash
只需要使用 CTRL + N 打开和关闭目录树就行
```