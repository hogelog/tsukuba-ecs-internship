# ECS

## ECR

以下のコマンドを [00. 事前準備](00-setup) で準備した tsukuba-playground のディレクトリで実行します。

```console
$ eval $(docker-compose run -T shell aws ecr get-login --region ap-northeast-1 --no-include-email)
$ docker pull 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/sample-app:latest
```

### sample-app
[01. Docker](01-docker) でビルドしたイメージを ECR にプッシュしてみます。

```console
$ docker tag sample-app 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/sample-app:latest
$ docker push 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/sample-app:latest
```

## ECS タスク定義の登録

## ECS サービスの登録

## TBD

## 参考リンク
- Amazon Elastic Container Service ドキュメント <https://docs.aws.amazon.com/ja_jp/ecs/>
- Amazon ECR ユーザガイド <https://docs.aws.amazon.com/ja_jp/AmazonECR/latest/userguide/>
