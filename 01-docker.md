# Docker
クックパッドは https://cookpad.com 以外にも様々なサービスを運用しており、それらのサービス一つ一つの中でたくさんのアプリケーションが動いています。
それらのアプリケーションのほとんどは Docker が利用されており、クックパッドの Docker 実行基盤の上では 1000 種類程のアプリケーションが動いています。

ここではアプリケーション開発に必要な Docker の基本の部分に触れてみます。

## やること
- Docker イメージをビルドをしてみる
- ビルドしたイメージを動かしてみる

## イメージのビルド
[hogelog/sample-sinatra-app](https://github.com/hogelog/sample-sinatra-app) というアプリケーションを手元でビルドしてみましょう。

```console
$ git clone https://github.com/hogelog/sample-sinatra-app.git
$ cd sample-sinatra-app/
$ docker build -t sample-app .
```

## イメージを動かしてみる
ビルドしたイメージを動かしてみましょう。

```console
$ docker run -it -p 4567:4567 sample-app
```

上記コマンドを実行すると以下のような実行結果が表示されるはずです。

> ```
> [2020-01-20 08:22:40] INFO  WEBrick 1.6.0
> [2020-01-20 08:22:40] INFO  ruby 2.7.0 (2019-12-25) [x86_64-linux]
> == Sinatra (v2.0.8.1) has taken the stage on 4567 for production with backup from WEBrick
> [2020-01-20 08:22:40] INFO  WEBrick::HTTPServer#start: pid=1 port=4567
> ```

http://localhost:4567/ を開いてみると "Hello world!" とだけ書かれた画面が表示されていれば正常です。

## docker-compose
docker-compose は複数のコンテナからなる Docker アプリケーションを定義・実行するツールです。
アプリケーションに必要なポート、ボリュームなどを指定できるので単体コンテナからなるアプリケーション開発時にもしばしば用いられます。

sample-sinatra-app のディレクトリで以下のコマンドを実行し、自分で `docker run ...` コマンドを実行した時と同様のアプリケーションが実行されていることを確認してみてください。

```console
$ docker-compose up
```

`docker-compose up` で作成・起動したアプリケーションは `docker-compose down` で停止・削除されます。

## アプリケーションを変更してみる
sample-sinatra-app というアプリケーションを編集して再度ビルドし、自分の変更がイメージに反映されていることを確認してみましょう。

### 構成
- Dockerfile
  - どのようにイメージをビルドするか定義しているファイルです
- docker-compose
  - docker-compose でどのようにアプリケーションを管理するか定義するファイルです
- Gemfile, Gemfile.lock
  - アプリケーションで利用するライブラリを指定しているファイルです
- app.rb
  - アプリケーションのロジックを記述しているファイルです

## 参考リンク
- https://docs.docker.com/engine/reference/commandline/build/
- https://docs.docker.com/engine/reference/run/
- https://docs.docker.com/compose/
- http://sinatrarb.com/

