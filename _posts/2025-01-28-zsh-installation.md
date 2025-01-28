---
title: How to install ZSH on Ubuntu
date: 2025-01-28 12:00:00 -500
categories: [linux, unbuntu, homelab, terminal, zsh. ohmyzsh, productivity]
tags: [linux, unbuntu, homelab, terminal, zsh. ohmyzsh, productivity]
---

Before getting into the nitty gritty of setting up applications I want a neat and functional terminal setup. Terminal customizations can be useful in increasing productivity outside of looking really cool.

With that being said, let's start!


## Installing ZSH Ubuntu
Being by installing zsh with root permissions:

```
sudo apt install zsh
```
- Enter root user password
- Type in *Y* to continue

Now we need to change the shell to zsh as we are still in the bash shell. You can do this by:
- Going to terminal's prefences
- For me in the generic Ubuntu terminall the tab I want is called **Unamed**
- Go to **Command**
- Run custom command
- Type in **zsh**

If for some reason the terminal or version your using doesn't have these options you can run the below command to change the shell for all users:

```
chsh -s $(which zsh)
```
- Once again enter password

Now let's exit and reopen the terminal to let the changes take effect
```
exit
```
Upon reopening there's a few questions for us.
The recommended route is 1,2,1,0.


## Oh My Zsh Installtion
Zsh allows for customization in the rc file ```nano ~/.zshrc```
But, we are going to install ohmyzh qhich gives out more customization out of the box.

```sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"```
- Y to make default shell
- enter root password


## Oh My Zsh Themes (Optional)
This looks good but we can make it even better with one of the oh my zsh themes which you can find here:

*These are optional as in the next step this will be overwritten. But, if you like the look you can definitely stop here and have a efficent terminal setup*

https://github.com/ohmyzsh/ohmyzsh/wiki/Themes

I really like the theme Jonathan so this is what I'll be using for now.
To edit we are going to nano in our ~/.zshrc file and set the variable ```ZSH_THEME="jonathan"```


## Oh My ZSH Plugins

Another cool feature with Oh My ZSH is their plugins. You can find the list of them below:
https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins

Two that I will be using for now:

```git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions```

```git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting```

After running these two commands now we must edit the .zshrc file to include plugins:

```plugins=(git zsh-autosuggestions zsh-syntax-highlighting)```

This is going to help our effeciency by suggesting common commands we use and highlighting for us.


## Nerd Font

Now we are going leverage nerdfont and more specifically powerlevel 10k for productivity customization.

Website here:
https://www.nerdfonts.com/

- Font download link for **Ubuntu**
https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/FiraMono

We need **FiraMono Regualr font** for Ubuntu. Install the raw file, then install font once on your system.

For nerdfont we are going to use **Powerlevel 10k** which will give us the icons, timestamps, and customizations we want.

```
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

- Edit zshrc file theme variable to:
```ZSH_THEME="powerlevel10k/powerlevel10k"```

- Answer all the questions to tailor your terminal to your liking. If you can't see the diamond in the first question that means you installed the wrong font so will need to double check that based of your system distrobution.

If for some reason you can't see the icons you will need to tell it to use the nerd font:
```
POWERLEVEL9K_MODE="nerdfont-complete"
```
Congratulations! You now have a effecient terminal that will give you details on how long a command took you to run, help you visualize file structure, which can all be great especially for beginners like me.

![alt-text](https://i.imgur.com/cCspbDF.png)