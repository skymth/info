## MySQL Command

### 起動方法
---
```
mysql -u (ユーザー名) = 起動
mysql -u (ユーザー名) -p = パスワードを入力して起動
```
```
> use (データベース名)
> set password for root@localhost=password('設定したいパスワード');
```
<br>

**パスワードを回避してバックグラウンドで実行する方法<br>**

```
mysqld_safe --skip-grant-tables &
mysql
```
<br>

### データを確認
---
```
> select * from (テーブル名)
```
### データベース内のtable作成
---

(例文) 以下を実行すると

```sh
 > CREATE TABLE test ( 
 > id INTEGER(11) NOT NULL AUTO_INCREMENT, 
 > name VARCHAR(20), 
 > title VARCHAR(64),
 > price INT(32),
 > PRIMARY KEY (id) );
```
 <br>

| Fiels      | type        | NULL         | Key          | Default      | Extra          |
|:-----------|------------:|:------------:|:------------:|:------------:|:--------------:|
| id         | int(11)     | NO           | PRI          | NULL         | auto_increment |
| name       | varchar(20) | YES          |              | NULL         |                |
| title      | varchar(64) | YES          |              | NULL         |                |
| price      | int(32)     | YES          |              | NULL         |                |


こんな感じのテーブルが出来上がる
<br>

### データベースの中身を見る
---

```
> show databases;
```
<br>

### データベース内のテーブル確認
---
- テーブルを表示

```
> show tables;
```
- テーブルの削除

```
> drop table users;
```
- テーブルの構造を表示

```
> desc <テーブル名>
```
- テーブル内のデータの確認

```
> select * from <テーブル名>
```
- テーブル内のデータを縦に表示にする

```
> select <フィールド名> from <テーブル名>
```
- レコードの挿入(挿入するレコード一覧)

```
> insert into users =values ();
```
- レコードの更新

```
> update <テーブル名> set where id=?
```
? の部分は適宜変える

- レコードの削除

```
> delete from <テーブル名> where <フィールド名>
```
<br>

### インクリメントする方法
---

MySQLの値を1増やす（インクリメントする）方法です。

たとえば、アクセス数のカウントなどに使えます。

以下の例は、testというテーブルの、idが1のレコードの、カラムの１つであるcountを1増やしています。

```
> update test set count = count + 1 where id = 1;

```

### ユーザーを追加する方法
---

```
> CREATE USER user;
> CREATE USER user IDENTIFIED BY [PASSWORD] 'password';
```

### 権限を与える方法
---

グローバルレベル:

```
> GRANT 権限 ON *.* TO 'user'@'localhost';
```
データベースレベル:

```
> GRANT 権限 ON db_name.* TO 'user'@'localhost';
```
テーブルレベル:

```
> GRANT 権限 ON db_name.table_name TO 'user'@'localhost';
```
カラムレベル:

```
> GRANT 権限 (カラム1, ...) ON db_name.table_name TO 'user'@'localhost';
```


### 作成済みのテーブルのカラムを操作
---

- カラムを作成<br>
```
> alter table <テーブル名> add <カラム名> <カラムのオプション> after <カラム名>;
```

<!>また指定したカラムの後に挿入する場合は次のように「AFTER」の後にカラム名

- カラムの削除<br>
```
> alter table <テーブル名> drop <カラム名>;
```

