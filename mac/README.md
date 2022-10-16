# Mac

## 修改 Lock Screen
Keyboard -> Shortcuts -> add a shortcut which named “Lock Screen”

## Mac audio bug
```
$ sudo killall coreaudiod
```

## zsh compinit: insecure directories, run compaudit for list.
```
$ compaudit
$ chmod -R 755 “dir”
```


## 美化 Terminal
> https://datasciocean.tech/others/beautify-terminal-on-macos/

#### 1. 下載 Oh My Zsh
```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

```

#### 2. 下載 Zsh 主題
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

vim ~/.zshrc

# ZSH_THEME="robbyrussell"
ZSH_THEME="powerlevel10k/powerlevel10k"
```

#### 3. 下載 Powerlevel10k 的字型 MesloLGS NF Regular.ttf
```
https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Regular.ttf
```

#### 4. 設定theme
```
p10k configure
```

