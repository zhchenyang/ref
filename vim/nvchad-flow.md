# Nvchad init

__`init.lua`__

1. load impatient for Speed up loading modules.

  ```lua
  local present impatient = pcall(require, 'impatient')

  if present then
  -- enable, impatient must be setup with:
    impatient.enable_profile()
  end
  ```

2. load core modules.
  
  ```lua
  -- define core modules
  local core_modules = {
      'core.options',
      'core.autocmds',
      'core.mappings',
  }

  -- load
  for _, module in iparis(core_modules) do
    local ok, err = pcall(require, module)
    if not ok then
      error('Error loading' .. module .. err)
    end
  end
  ```
3. load non plugin mappings

  ```lua
  require('core.mappings').misc()
  -- TODO figure out why load twice
  ```

4. load custom config if exist.

  ```lua
  if vim.fn.filereadable(vim.fn.stdpath 'config' .. '/lua/custom/init.lua') == 1 then
    local ok, err = pcall(require, 'custom')
    if not ok then
      vim.notify('Error loading custom/init.lua\n\n' .. err)
    end
    return
  end
  ```
## core modules

### options

```lua
local opt = vim.opt
local g   = vim.g

-- step one
local options = require('core.utils').load_config().options
```

#### step one

```lua
locat M = {}

M.load_config = function()
  local conf = require 'core.default_config'
  
  local chadrcExists, change = pcall('custom.chadrc')

  -- if exist, then merge its table into the default config's
  if chadrcExists then
    conf = vim.tbl_deep_extend('force', conf, change)
  end

  return conf
end
```


