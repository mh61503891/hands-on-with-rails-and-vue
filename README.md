theme: Simple, 1
autoscale: true
slidenumbers: true
footer: © Masayuki Higashino

# [fit] Ruby on Rails 5.1 + Vue 2.4ハンズオン

当日までに以下の2つを実施しておいてください。

* **1.1 プロジェクトの新規作成**  (p.2)
* **1.2 サーバの起動**  (p.3)

理由は下記の通りです。

1. 会場の無線LANではおそらくライブラリのダウンロードに耐えられないため。（ダウンロードするファイルサイズがRubyとJavaScriptのライブラリで合わせて200MBを超えます。）
2. Rails環境のセットアップとトラブルシュートする時間の確保が難しいため。

---
# 1.1 プロジェクトの新規作成

```bash
$ gem install bundler
$ gem install rails
$ mkdir hands-on-with-rails-and-vue
$ cd hands-on-with-rails-and-vue
$ rails new . --skip-turbolinks --webpack=vue
$ yarn add vue-i18n vue-router vuex
$ yarn add axios es6-promise bootstrap-vue
```

---
# 1.2 サーバの起動

コンソールその1: Railsサーバの起動

```bash
$ bundle exec rails server
```

コンソールその2: Webpackを使ったJavaScriptのビルドサーバの起動

```bash
$ bundle exec bin/webpack-dev-server
```
---
# 2.1 Ruby関連パッケージの確認

* Gemfile: 使用するRuby関連のライブラリが記述されている。使用するライブラリのバージョンの範囲を指定できる。
* Gemfile.lock: Gemfileを元に生成される。このプロジェクトで使用するライブラリのバージョンが記述されている。
* bundle exec を経由して実行することでGemfile.lockに記述されているライブラリだけを使うように制限をかけられる。つまりGemfile.lockが同じであれば同じライブラリのバージョンが使われることを保証できる。

---
# 2.2 JavaScript関連パッケージの確認

* package.json: 使用するJavaScript関連のライブラリが記述されている。使用するライブラリのバージョンの範囲を指定できる。
* yarn.lock: package.jsonを元に生成される。役割はGemfile.lockと同じ。
* 今はnpmコマンドよりyarnの方がオススメ。将来的には分からん。

---
# 3.1 （おまけ）デフォルトで入っているライブラリのメモ

* sqlite3.gem: SQLite3は同時書込に弱いので本番環境ではpg.gemやmysql2.gemを使った方が良い。もしActionCable[^1]とかの非同期通信でDBに書込するならSQLite3では同時書込に失敗して頻繁にエラーが出て使い物になりません。PostgreSQLであればPub/Subに対応しているのでActionCableのアダプタにもなって一石二鳥。ただしActionCableでの非同期処理にしっかり性能を要求するのであればActionCableのアダプタをRedisとかにした方が良い。
* turbolinks.gem: 決まれば動作がかなり軽くなる。他のJavaScriptのライブラリとの共存において注意を払わないといけないことが増える。わりとコードが汚くなる気がする。決まれば動作がかなり軽くなる（2回目）。けど実装しんどい。以下ループ。
* coffee-rails.gem: うーん。そろそろES6で書いた方が良いんじゃない？

[^1]: Railsに入っているWebSocketのフレームワーク

---
# 作成中🐈
