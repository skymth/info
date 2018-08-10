# PostgreSQL

## インストール

### For mac

```
$ brew install postgresql
```
  
以下のように出力されれば成功
  
```
~/M/p/postgres ❯❯❯❯❯  postgres --version
postgres (PostgreSQL) 10.1
```

### For CentOS

- [CentOSにPostgreSQL9.5をインストールおよびテスト](https://qiita.com/SOJO/items/a1d97887d24c3e44596f)

### For Ubuntu
- [UbuntuにPostgreSQLをインストール](https://qiita.com/kaitoii11/items/7acd24cce5315792931f)


<br>

## 使ってみる

### サーバの起動

```
$ postgres -D /usr/local/var/postgres
```

### サーバのデーモン起動 & 停止

- 起動  

```
$ pg_ctl start -D /usr/local/var/postgres
```
- 停止  

```
$ pg_ctl stop -D /usr/local/var/postgres
```

### データベースの一覧
```
$ psql -l
```


### データベースへの接続

```
$ psql -d database -U user -h host
```
- -d: データベース名(未指定の場合、ログインユーザー名のデータベースに接続)
- -U: ユーザ名(未指定の場合、ログインユーザー名)
- -h: ホスト名(未指定の場合、localhost)

<br>

## データベース接続時に使うコマンド

⚠️ `psql -d postgres` で接続したとする

### psqlから抜け出す

```
postgres=# \q
```

### ユーザー一覧の表示

```
postgres=# \du
```

### データベース一覧の表示

```
postgres=# \l
```


### 他のデータベースに接続

```
postgres=# \c <dbname>
```

### ユーザーの作成

```
postgres=# create user <username>
```

### ユーザーにパスワードを持たせる

```
postgres=# \password <username>
...
Enter new password:
Enter it again:
```

### データベースの作成
```
postgres=# create database <dbname>;
```

### テーブルの作成

以下をpsql内で実行する

```
CREATE TABLE Staff
(
id    CHAR(4)    NOT NULL,
name   TEXT       NOT NULL,
age    INTEGER    ,
PRIMARY KEY (id)
);
```

もしくはこれを`.sql`ファイルにかき、ファイルからコマンドを実行できる。
また、ファイルを作成し、`creatdb`というコマンドがあるのでそれでもいいと思われる
**`createdb`については以下に詳細をかく**

### テーブル一覧の表示

```
postgres=# \z
```

### テーブル定義の表示

```
postgres=# \d <tablename>
```

### ファイルからコマンド実行

```
postgres=# \i filename.sql
```

### 履歴の表示

```
postgres=# \s
```

<br>

## createdb 

createdbは、新しいPostgreSQLデータベースを作成できる

通常、このコマンドを実行したデータベースユーザが、新しいデータベースの所有者になる。 ただ、コマンドを実行するユーザが適切な権限を持っている場合、-Oオプションを使用して別のユーザを所有者に指定することができる。

createdbはCREATE DATABASEというSQLコマンドのラッパです。 したがって、このユーティリティでデータベースを作成しても、これ以外の方法でサーバにアクセスしてデータベースを作成しても何も違いはない。


### オプション

#### dbname
- 作成するデータベースの名前を指定します。 この名前はクラスタ内の全てのPostgreSQLデータベースの中で一意でなければならない

#### -O owner
- 新しいデータベースの所有者となるデータベースユーザを指定する

以上以外のオプションが知りたい場合は以下を参照してください

[https://www.postgresql.jp/document/9.4/html/app-createdb.html](https://www.postgresql.jp/document/9.4/html/app-createdb.html)

<br>

## リファレンス
- [https://qiita.com/mm36/items/1801573a478cb2865242](https://qiita.com/mm36/items/1801573a478cb2865242)
- [https://www.postgresql.jp/document/9.4/html/app-createdb.html](https://www.postgresql.jp/document/9.4/html/app-createdb.html)
- [PostgreSQLコマンドチートシート](https://qiita.com/Shitimi_613/items/bcd6a7f4134e6a8f0621)