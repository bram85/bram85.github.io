+++
title = "Use tab-bar-history-mode instead of winner-mode"
author = ["Bram"]
date = 2022-05-21T08:04:00+02:00
lastmod = 2022-05-21T08:04:26+02:00
tags = ["emacs"]
categories = ["Tech"]
draft = false
+++

`winner-mode` is a minor mode in Emacs which remembers your window configurations. You can go back to an older window configuration, by default with _C-c &lt;left&gt;_ (and _C-c &lt;right&gt;_ to move forward). However, `winner-mode` is tab-unaware, which messes up your window configuration when you've switched tabs in the meantime. Luckily, there is `tab-bar-history-mode` which does the same, except it stores the window configuration per tab. By using the same bindings as `winner-mode` it becomes a drop-in replacement.

```elisp
(use-package tab-bar
  :config
  (tab-bar-history-mode)
  :bind
  ("C-c <left>" . tab-bar-history-back)
  ("C-c <right>" . tab-bar-history-forward))
```

Note that `tab-bar-history-back` and `tab-bar-history-forward` do not behave well when called interactively from a minibuffer window. The minibuffer may actually change the window configuration, pushing one to the history, which results in `tab-bar-history-back` popping the window configuration you were looking at in the first place, so essentially becoming a no-op. By binding these functions to some keys, the functions behave as they should.
