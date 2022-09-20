# Node.Js

## NVM
> reference: https://github.com/creationix/nvm

<br />
#### install (2017/12/21 version)
```
$curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
or
$ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```
<br />

#### setup nvm path
```
### 正常Install時已經有script寫入了
在以下任一檔案 ~/.bash_profile, ~/.zshrc, ~/.profile, ~/.bashrc寫入
####start####
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
####end####
```
<br />

#### Commands
```
#nvm支援的nodeJS版本
$ nvm ls-remote
# 目前已經安裝的nodeJS版本
$ nvm list
# 安裝node版本(npm也會安裝)
$ nvm install node #直接最新版的
$ nvm install stable #直接最新版的
$ nvm install <版本號>
$ npm install --verbose # --verbose will show more states
$ npm cache clean --force
# 切換版本
$ nvm use <版本號>
# 設定default nodeJS版本
$ nvm alias default <版本號>
```
<br />

#### fix
##### !! nvm is not compatible with the npm config "prefix"
```
nvm is not compatible with the npm config "prefix"
option: currently set to "/ebs100_new/ubuntu/.nvm/versions/node/v9.8.0"
$ npm config delete prefix
$ npm config set prefix $NVM_DIR/versions/node/v9.8.0
```
<br />

## Node.js
#### Command
```
# 現在使用node版本
$ node -v
# 進node console
$ node
```

## NPM
> reference: https://docs.npmjs.com/

<br />
#### install
```
要先裝好nodejs or using NVM to install nodejs
$ nvm install node
$ npm install npm@latest -g
```
<br />

#### Commands
```
# 依據 package.json 進行下載plugin，並寫入package.json.lock做版本控制
$ npm install
# 安裝想要的package ## 若後面加 -g 會是global 安裝
$ npm install <package name>
# 移除package ## 若後面加 -g 會是global移除
$ npm uninstall <package name>
# 搜尋套件
$ npm search <package name>
# 列出global套件 (參數加上l可看詳細資訊)
$ npm ls -g
# 列出專案套件(在專案下) (參數加上l可看詳細資訊)
$ npm ls
```

## NPX
> reference: https://medium.com/itsems-frontend/whats-npx-e83400efe7f8

跟 NPM 的差異在於執行完後會移除不需要的安裝模組，且直接create project

```
$ npx create-react-app@version my-react-app
```

可以直接執行套件或Github檔案，請參閱reference



## change registry
> 切換 package 的下載來源

```
$ npm config get registry
> https://registry.npmjs.org/

$ npm config set registry https://you.wanted.source.url
$ npm config get registry
> https://you.wanted.source.url

```






