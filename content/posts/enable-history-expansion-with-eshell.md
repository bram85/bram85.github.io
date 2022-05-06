+++
title = "Enable history expansion with eshell"
author = ["Bram"]
date = 2022-05-06T16:27:00+02:00
lastmod = 2022-05-06T20:39:45+02:00
tags = ["til", "emacs"]
categories = ["Today I Learned"]
draft = false
+++

For some reason, history expansion through `!` notation is not enabled by default in Emacs eshell. The variable `eshell-expand-input-functions` needs to be extended as follows:
Add the following to your configuration:

```elisp
(add-to-list 'eshell-expand-input-functions 'eshell-expand-history-references)
```

or, to be specific, add it to the `eshell-hist-load-hook` otherwise the addition operation may complain that the list does not exist when eshell hasn't loaded yet. An example is shown below if you use `use-package`:

```elisp
(use-package eshell
  :commands eshell
  :hook
  (eshell-hist-load . (lambda () (add-to-list 'eshell-expand-input-functions 'eshell-expand-history-references))))
```
