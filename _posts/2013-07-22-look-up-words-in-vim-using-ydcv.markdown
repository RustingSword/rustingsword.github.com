---
title: 用ydcv在Vim里查单词
layout: post
tags:
  - software
  - Vim
---

1. 安装`ydcv`：`pacman -S ydcv`。`ydcv`是有道词典的命令行版本，类似于`Stardict`的`sdcv`，如果一直联着网的，用这个比较方便，因为可以查整个句子。

2. 在`.vimrc`里添加两个函数和对应的快捷键映射（抄自[`Github`上的一个脚本](https://github.com/gudezhi/vimfiles/blob/master/plugin/sdcv.vim)，不过我没有用split window来显示结果）：

        " look up current word under cursor
        function! SearchWord()
            let expr = '!ydcv -s ' .expand("<cword>")
            exec expr
        endfunction
            
        " translate selected text
        function! SearchWord_v(type, ...)
            let sel_save = &selection
            let &selection = "inclusive"
            let reg_save = @@
                
            if a:0
                silent exe "normal! `<" . a:type . "`>y"
            elseif a:type == 'line'
                silent exe "normal! '[V']y"
            elseif a:type == 'block'
                silent exe "normal! `[\<C-V>`]y"
            else
                silent exe "normal! `[v`]y"
            endif
                 
            let word = @@
            let expr = '!ydcv "' . word . '"'
            exec expr
                
            let &selection = sel_save
            let @@ = reg_save
        endfunction
                
        nnoremap <Leader>d :call SearchWord()<CR>
        vnoremap <Leader>d :<C-U>call SearchWord_v(visualmode(), 1)<cr>

3. `:source $MYVIMRC`

大功告成。查询光标下的单词或者visual模式里选中的内容，直接按`<Leader>d`就行。

效果图：

![查单词](img/word.png "查单词")

![查句子](img/sentence.png "查句子")

缺点有两个，一是可能有延迟，这个看网络情况，二是之前查询的结果会一直显示（Gvim里没这个问题，不过会显示终端下的颜色代码）。

顺便说一下，还有一个更简单的方法：`Vim`里有个命令是`K`，会调用`keywordprg`这个变量指定的程序查询光标下的单词，`keywordprg`的默认值是`man`，把这个改成`ydcv`可以实现同样的效果（也能在visual模式使用），可参考`:h keywordprg`。
