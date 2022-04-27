+++
title = "Emacs Lisp: Expand macros"
author = ["Bram"]
lastmod = 2022-04-27T20:56:46+02:00
tags = ["til", "emacs", "lisp", "elisp"]
categories = ["Today I Learned"]
draft = true
+++

To expand a macro, the `pp-macroexpand-last-sexp` is a useful function. It's like `pp-eval-last-sexp`, but opens a new buffer with the expanded code without evaluation.

For example, it's easy to inspect the magic behind `use-package`:

```elisp
(use-package org)
```

is transformed by `pp-macroexpand-last-sexp` to:

```elisp
(progn
  (straight-use-package 'org)
  (defvar use-package--warning117
    #'(lambda
        (keyword err)
        (let
            ((msg
              (format "%s/%s: %s" 'org keyword
                      (error-message-string err))))
          (display-warning 'use-package msg :error))))
  (condition-case-unless-debug err
      (if
          (not
           (require 'org nil t))
          (display-warning 'use-package
                           (format "Cannot load %s" 'org)
                           :error))
    (error
     (funcall use-package--warning117 :catch err))))
```

Of course it becomes more elaborate with `:config`, `:bind`, `:hook` flags, but you get the idea.
