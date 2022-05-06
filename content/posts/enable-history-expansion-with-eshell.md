+++
title = "Enable history expansion with eshell"
author = ["Bram"]
date = 2022-05-06T16:27:00+02:00
lastmod = 2022-05-06T16:36:47+02:00
tags = ["til", "emacs"]
categories = ["Today I Learned"]
draft = false
+++

For some reason, history expansion through `!` notation is not enabled by default in Emacs eshell. The variable eshell-expand-input-functions needs to be extended as follows:
Add the following to your configuration:

```elisp
(add-to-list 'eshell-expand-input-functions 'eshell-expand-history-references)
```
