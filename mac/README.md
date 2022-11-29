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

## Handle ram when sleep mode
```
pmset -g // query the status
pmset -g custom

$ sudo pmset -a hibernatemode 0
– 0 = 記憶體持續供電，若斷電的話資料全部消失
– 3 = 記憶體資料寫到硬碟，記憶體持續供電，因此可以快速回復
– 25 = 記憶體資料寫到硬碟，全電腦斷電
```

## Disable Swap
```
csrutil status // query SIP status
sysctl -a vm.compressor_mode // query the status

1. Disable SIP in Recovery Mode
$ csrutil disable
// after disable restart mac

2. set the vm_compressor
$ sudo nvram boot-args="vm_compressor=2"
// reboot again

3. reboot and check the status and vm.compressor_mode

4. Enable SIP in Recovery Mode
$ csrutil enable --without nvram


```