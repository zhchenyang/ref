# Inbox

## lua-vimscript bridge

Nvim Lua provide an interface to Vimscript variables and functions, and editor commands and options.

**vim.call({func}, {...})**
  
  Invokes vim-function or user-function {func} with arguments {...}.
  Equivalent to:
    __vim.fn[func]({...})

**vim.cmd({cmd})**

  Executes multiple lines of Vimscript at once. It is an alias to `nvim_exec`, where output is set to fasle. Thus it works identical to `:source`.
  Example:
    ```
    vim.cmd('echo 42')
    vim.cmd([[
      augroup My_groip
        autocmd!
        autocmd FileType c setlocal cindent
      augroup END
    ]])
    ```

**vim.fn.{func}({...})**

  Invokes vim-function or user-function {func} with arguments {...}.
  To call autoload functions, use the syntax:
    `vim.fn['some#function']({...})`
  Unlike vim.api.nvim\_call\_funtion() this converts directly between Vim objects and Lua objects.If the Vim function returns a float, it will be represented directly as a Lua number. Empty lists and dictionaries both are represented by an empty table.
  
## lua-vim-variables

The Vim editor global dictionaries `g: w: b: t: v:` can be accessed from Lua conveniently and idiomatically by referencing the `vim.*` Lua tables described below. In the way you can easily read and modify global Vimscript varibales from Lua.

__Example:__

  ```Lua
  vim.g.foo = 5
  print(vim.g.foo)
  vim.g.foo = nil
  vim.b[2].foo = 6
  ```

__vim.g__
  
  Global(`g:`) editor variables.
  key with no value returns `nil`

__vim.b__
  
  Buffer-scoped

__vim.w__
  
  Window-scoped

__vim.t__
  
  Tabpage-scoped

__vim.v__
  
  `v:` variables

__vim.env__
  
  Enviroment variables

## set-options

In Vimscript, there is an way to set options `set-options`. In Lua, the corresponding method is `vim.opt`.

`vim.opt` provides several conveniencesfor setting and controlling options form within Lua.

__Example__

  To set a boolean toggle:
    In Vimscript:
      ```Lua
      set number
      ```
    In Lua:
      ```Lua
      vim.opt.number = true
      ```

  To set an array of values:
    In Vimscript:
    ```Vimscript
    set wildignore=*.o,*.a,__pycache__
    ```
    In Lua:
    ```lua-vimscript
    vim.opt.wildignore = '*.o,*.a,__pycache__'
    -- or
    vim.opt.wildignore = {'*.o', '*.a', '__pycache__'}
    ```

  To replicate the behavior of `:set+=`, use:
    ```Lua
    -- vim.opt supports appending options via the "+" operator
    vim.opt.wildignore = vim.opt.wildignore + { "*.pyc", "node_modules" }

    -- or using the `:append(...)` method
    vim.opt.wildignore:append { "*.pyc", "node_modules" }
    ```

  To replicate the behavior of `:set^=`:
    \^ or :prepend
  To replicate the behavior of `:set-=`:
    \- or :remove
    
  To set a map of values:
    ```
    set listchars=space:_,tab:>~
    -- lua
    vim.opt.listchars = { space = '_', tab = '>~'}
    ```

`setlocal`: `vim.opt_local`
`setglobal`: `vim.opt_global`

above has some methods

* get
* append
* prepend
* remove
