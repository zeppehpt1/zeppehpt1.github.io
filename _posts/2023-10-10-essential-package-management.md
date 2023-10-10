---
layout: post
title: Essential Arch Linux Package Management Commands
---

Search for a package with pacman  
```bash
sudo pacman -Ss query
```

Search for package with yay
```bash
yay -Ss query
```

Install community package via pacman 
```bash
sudo pacman -Syu package
```
Install aur/community package
```bash
yay package
```

Remove aur/community package + unnesessary dependencies
```bash
yay -Rns package
```

Update whole system
```bash
pacman -Syu
```
Or
```bash
yay
```

Update after changing mirrors
```bash
pacman -Syyu
```