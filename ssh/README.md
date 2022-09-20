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
