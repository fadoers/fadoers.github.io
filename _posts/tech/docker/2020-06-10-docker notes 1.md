---
layout: post
title: "docker notes 1"
subtitle: 'main features'
author: "LiYi"
header-style: text
tags:
  - java
  - tech
  - kotlin
---

1. Package Software into Standardized Units for Development, Shipment and Deployment
Flexible: Even the most complex applications can be containerized.
Lightweight: Containers leverage and share the host kernel, making them much more efficient in terms of system resources than virtual machines.
Portable: You can build locally, deploy to the cloud, and run anywhere.
Loosely coupled: Containers are highly self sufficient and encapsulated, allowing you to replace or upgrade one without disrupting others.
Scalable: You can increase and automatically distribute container replicas across a datacenter.
Secure: Containers apply aggressive constraints and isolations to processes without any configuration required on the part of the user.


### Vim-binding

Choose `evil`!


### Airline

It's there!


### Nerd Tree / File Sidebar

`SPC f t` for _file tree_. The keybindings for specific operations are very different w/ Vim NerdTree though.


### Shell / Terminal

I occasionally use [Neovim's terminal emulator](https://neovim.io/doc/user/nvim_terminal_emulator.html) but in most of the time I just `cmd + D` for iTerms splitted window. 

I even mappped `:D` into split-then-terminal to make the experience on par ;)

```vim
command! -nargs=* D  belowright split | terminal <args>
```

Anyways, Spacemacs does provide a `:shell` that naturally split a window below for terminal. The experience is not very good though.


### Tabs / Workspaces

I tend to open multiple _workspace_. Though people might found Vim tabs useful, I am exclusively use iTerm tabs for similar jobs. However Spacemacs is not living in a terminal.

[r/spacemacs - Vim-style tabs?](https://www.reddit.com/r/spacemacs/comments/5w5d2s/vimstyle_tabs/) gave me a good way to approximate the experience by using [Spacemacs Workspaces](http://spacemacs.org/doc/DOCUMENTATION.html#workspaces): `SPC l w <nth>` trigger a so-called "layout transient state" (I have no idea what's that mean) to open N-th workspaces, and use `gt`/`gT` to switch between.


### Fuzz File Name Search / Rg

`SPC f f`


### Buffers

`SPC b b`







