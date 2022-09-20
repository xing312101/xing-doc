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
