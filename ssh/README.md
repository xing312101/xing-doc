# SSH

```
ssh-keygen -m PEM -t rsa -b 4096

ssh-keygen \
    -m PEM \
    -t rsa \
    -b 4096 \
    -C "xing312101@server" \
    -f ~/.ssh/otherKeys/privateKeyName \
    -N mypassphrase

-m PEM = 將金鑰格式設定為 PEM
-t rsa = 要建立的金鑰類型，在此案例中採用 RSA 格式
-b 4096 = 金鑰中的位元數，在此案例中為 4096
-C "xing312101@server" = 附加至公開金鑰檔案結尾以便輕鬆識別的註解，通常會以電子郵件地址作為註解
-f ~/.ssh/mykeys/myprivatekey = 私密金鑰檔案的檔案名稱
-N mypassphrase = 存取私密金鑰的密碼。
```

## ssh agent
```
eval $(ssh-agent -s)

ssh-add ~/.ssh/id_rsa
```

## proxy add agent
```
echo "Host *\n StrictHostKeyChecking no\n UserKnownHostsFile /dev/null\n ForwardAgent yes$(cat ~/.ssh/config)" > ~/.ssh/config
echo -e "Host * \n\tStrictHostKeyChecking no\n\tUserKnownHostsFile /dev/null" >> ~/.ssh/config
```


## pem key

```
ssh -i keyName.pem user@host
```

####public issue
vim  ~/.ssh/config
```
Host *
    PubkeyAcceptedKeyTypes +ssh-rsa
```

## Too many authentication failures
```
1.
ssh -o IdentitiesOnly=yes user@localhost

2. ~/.ssh/config
Host *
  IdentitiesOnly=yes
```


## add key in authorized_keys for ssh login
```
mkdir authorized_keys in ~/.ssh
```


## ssh socket
### using ssh/config
```
Host 10.10.10.115
  ControlMaster auto
  ControlPath path # like /.ssh/xxx_control or /tmp/serverNameControl
  ControlPersist 2h
```

### using SSH_SOCKET
> not success, need to check
#### set socket path
```
ENV_VARIABLE=socketPath
ex: ENV_VARIABLE=~/.ssh/user@hostName
```

#### use the sshsocket
1. create master connection
```
ssh -M -f -N -o ControlPath=$ENV_VARIABLE myUsername@targetServerName
```

2. use
```
ssh -o ControlPath=$ENV_VARIABLE user@hostName "echo 'Hello Xing'; ls"

scp -o ControlPath=$ENV_VARIABLE user@hostName:remoteFile.txt ./
```

#### close the sshsocket
```
ssh -S $ENV_VARIABLE -O exit user@hostName
```

## auto load ssh key
```
Host *
  UseKeychain yes
  AddKeysToAgent yes
  IdentityFile ~/.ssh/[your-secure-ssh-key-name]
```