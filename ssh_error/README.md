# Mac10.13.2 (HighSierra)にアップデートした後にSSHができなくなった時の対処法


## エラー
  
Macのアップデート後に、sshを使ってのリモート作業をした時に、以下のようなエラーがでた、、、

```
"Unable to negotiate with "xxx" port "xxx": no matching cipher found. Their offer: aes128-cbc, 3des-cbc, blowfish-cbc, cast128-cbc, arcfour, aes192-cbc, aes256-cbc, rijndael-cbc @ lysator.liu.se"
```

???
なんだこれ、
エラーを調べてみると

SSH クライアントがSSH サーバーによってサポートされない弱い暗号を使用することによって SSH 接続をセットアップしようとすると、SSH エラーが発生することがある。サポートされている暗号の名前を示すエラー・メッセージが SSH クライアントに表示される。

らしい、、、

*参照*:[SSH 接続エラーの解決](https://www.ibm.com/support/knowledgecenter/ja/STAV45/com.ibm.sonas.doc/sonas_ssh_con_err.html)

<br>

## 対処法

```
sudo vim /etc/ssh/ssh_config
```
で以下のようにコメンアウトをとる。

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc
```


![ssh_config.png](https://qiita-image-store.s3.amazonaws.com/0/192279/e2817db3-6051-a566-2585-3711e8c7eb62.png)


エラー解消！！！！



