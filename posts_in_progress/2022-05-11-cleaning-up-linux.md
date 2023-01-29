---
layout: post
title: Clean up some linux space
---


use ncdu and manually delete large folders
```bash
ncdu
```

Select and determine folders that take up large amount of space.

```bash
sudo paccache -r
```

delete cached pacman files
```bash
conda clean --all
```

Deletes cached packages and files

```bash
sudo journalctl --vacuum-time=10d
```