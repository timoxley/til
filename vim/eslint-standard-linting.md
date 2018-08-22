# Switch ALE linters based on presence of `.eslintrc` in any parent dir

The config below dynamically switches the [ALE](https://github.com/w0rp/ale) linter between `eslint` & `standard`, based on presence of an `.eslintrc` in
any parent dir of currently open file.


```vim
" switch linters based on existence of .eslintrc* in any parent directory of current file
autocmd FileType javascript let g:ale_linters = {
\  'javascript': globpath(join(ale#path#Upwards(expand('%:p:h')), ','), '.eslintrc*') != '' ? [ 'eslint', 'flow' ] : [ 'standard', 'flow' ],
\}
```

Remove 'flow' option if you don't need it.

----

Vim's `globpath` combined with [`ale#path#Upwards`](https://github.com/w0rp/ale/blob/a366d325a7c69fa20a3ab69ff8359bcd37d1487a/autoload/ale/path.vim#L155-L177) is a neat way to "glob up" in vimscript. 

Also note there's many other neat path utilities in [`ale/autoload/ale/path.vim`](https://github.com/w0rp/ale/blob/a366d325a7c69fa20a3ab69ff8359bcd37d1487a/autoload/ale/path.vim). 
Wouldn't take much to extract these to be standalone vimscript if you needed them outside the context of ALE.

### Previously

I was using the below config to switch between eslint & standard however this won't correctly detect eslint unless you have an `.eslintrc*` file in the directory you opened vim from.

```vim
autocmd FileType javascript let g:ale_linters = {
\  'javascript': glob('.eslintrc*', '.;') != '' ? [ 'eslint', 'flow' ] : [ 'standard', 'flow' ],
\}
```

