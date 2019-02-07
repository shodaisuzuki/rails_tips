# low level cache

## RailsGuide
レベルキャッシュの最も効果的な実装方法は、Rails.cache.fetchメソッドを利用することです。このメソッドは、キャッシュの書き込みと読み出しの両方に対応しています。引数が1つだけの場合、キーを読み出し、キャッシュから値を取り出して返します。ブロックを引数として渡すと、キャッシュにヒットしなかった場合にブロックが実行されます。ブロックの戻り値は、指定のキャッシュキーの下にあるキャッシュに書き込まれます。キャッシュにヒットした場合は、ブロックを実行せずにキャッシュの値を返します。

```
def cache_users
  key = "cache_users

  Rails.cache.fetch("cache_users", expired_in: 60.minutes) do
    User.all.to_a
end
```

## 注意
キャッシュする値は、ブロックの中の値です。
`User.all`や`User.where()`などの返り値は`ActiveRecord_Relation`クラスのオブジェクトなので、
このオブジェクトをキャッシュしても、DB問い合わせは発生してしまいます。
DB問い合わせ結果をキャッシュしたい場合は`to_a`する事で、DB問い合わせ行い、問合せ結果を`Array`にした値をキャッシュさせます。

# 参考
https://railsguides.jp/caching_with_rails.html
https://qiita.com/srockstyle/items/3f1dad0c88c9ef4c5288
https://qiita.com/yamashun/items/bf9a3d29de749cf18f2e