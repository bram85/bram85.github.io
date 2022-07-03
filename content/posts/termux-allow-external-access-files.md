+++
title = "Termux: allow external apps to access files"
author = ["Bram"]
date = 2022-07-03T09:39:00+02:00
lastmod = 2022-07-03T09:39:52+02:00
categories = ["Tech"]
draft = false
+++

From one day to another, `termux-open` no longer worked, external apps were no longer able to access the Termux storage. It turns out this is fixed with adding a line to ~/.termux/termux.properties:

```text
allow-external-apps=true
```
