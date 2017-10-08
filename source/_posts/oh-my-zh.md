---
title: oh-my-zh
id: 32
categories:
  - Base Linux/Unix System Environment
date: 2016-05-26 17:59:22
tags:
---

sudo pacman -S zsh
sudo pacman -S git wget
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh )"

Manual Installation

1\. Clone the repository:

git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
2\. Optionally, backup your existing ~/.zshrc file:

cp ~/.zshrc ~/.zshrc.orig
3\. Create a new zsh configuration file

You can create a new zsh config file by copying the template that we included for you.

cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
4\. Change your default shell

chsh -s /bin/zsh
5\. Initialize your new zsh configuration

Once you open up a new terminal window, it should load zsh with Oh My Zsh's configuration.