# Hako

全て手動で実行すると ECS は先程のようにしてアプリケーションをデプロイ・実行することができます。

ECS を使ったデプロイをある程度定型化し、コマンドから簡単にデプロイできるようにした Hako <https://github.com/eagletmt/hako> というツールを用いてデプロイしてみます。

## hako deploy
tsukuba-playground のシェル内で以下のコマンドを実行してみましょう。

```console
$ gem install hako
```

### hako-nginx
https://github.com/eagletmt/hako-nginx

```console
$ git clone https://github.com/eagletmt/hako-nginx.git
$ cd hako-nginx
$ docker build -t hako-nginx .
$ docker tag hako-nginx:latest 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/hako-nginx:latest
$ docker push 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/hako-nginx:latest
```

## TBD

## 参考リンク
- <https://github.com/eagletmt/hako>
