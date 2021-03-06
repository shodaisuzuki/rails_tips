# migrateファイルの単体テスト

migrateでは次の処理ができる事が期待されます。

* テーブル追加、カラム追加などの**追加処理**
* migrateで追加した定義の**ロールバック処理**

開発時は**テーブルを作る**、**カラムを追加する**など追加する事に意識が集中しがちです。
その為、ロールバックできない不完全なmigrateファイルを作成してしまう恐れがあるため、
次の様に自分が作成したmigrateファイルが正しく動くか確認します。

## 確認方法

1.いつも通り`$ rake db:migrate`
2.`rake db:migrate:redo`を実行して、きちんとロールバックできるmigrateファイルか確認する。

```
$ rake db:migrate
$ rake db:migrate:redo
```

`rake db:migrate:redo`コマンドは、1度ロールバックした後migrateします。
このコマンドで初めに記述した**migrateファイルの2つの処理が正しく動作するか**確認する事ができます。

* テーブル追加、カラム追加などの**追加処理**
* migrateで追加した定義の**ロールバック処理**

