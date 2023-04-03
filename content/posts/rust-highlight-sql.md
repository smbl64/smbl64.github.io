---
title: "Highlight SQL strings in Rust"
summary: " "
date: 2023-04-03T18:03:53+02:00
draft: false
tags: ["rust", "neovim", "treesitter", "sql"]
---

If you are using Neovim with Treesitter, you can use query injections to highlight SQL in Rust strings.

To do so, create a queries folder in your Neovim runtime path:
```sh
mkdir -p ~/.config/nvim/after/queries/rust
cd ~/.config/nvim/after/queries/rust
```

Then create a file called `injections.scm` in that folder and paste this content there:

```scheme
; extends

; A general query injection
; Adapted from 
;  https://github.com/ray-x/go.nvim/blob/master/after/queries/go/injections.scm
([
   (string_literal)
   (raw_string_literal)
 ] @sql
 (#match? @sql "(SELECT|select|INSERT|insert|UPDATE|update|DELETE|delete).+(FROM|from|INTO|into|VALUES|values|SET|set).*(WHERE|where|GROUP BY|group by)?")
 (#offset! @sql 0 1 0 -1))
```

Restart your Neovim. After opening Rust files with SQL strings, they will have syntax highlighting.

You can see how it looks like in the screenshot below:
![Screenshot](/rust-sql-highlight.jpg)
