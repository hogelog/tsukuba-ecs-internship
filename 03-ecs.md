# ECS
AWS には Amazon ECS という、Docker のマネージドオーケストレーションサービスがあります。

クックパッドでは、基本的に国内のサービスすべてで ECS を利用しています。 また、イギリスのブリストルを拠点に開発されているグローバルレシピサービスでは AWS の マネージド Kubernetes サービスである EKS も導入されています。

まず ECS のコンソールから操作し、実際にアプリケーションを ECS 環境上で動かしてみます。

## Amazon EC2 Container Registry (ECR)
ECR は AWS のマネージド Docker イメージレジストリです。まず手元でビルドした Docker イメージを自分で作成したリポジトリにプッシュするところまでやってみましょう。

### リポジトリの作成
<https://ap-northeast-1.console.aws.amazon.com/ecr/repositories?region=ap-northeast-1>
にアクセスし、"sample-app-komuro" のような名前のリポジトリを作成してみましょう。

### ECR へのプッシュ
以下のコマンドを [00. 事前準備](00-setup) で準備した tsukuba-playground のディレクトリで実行します。

```console
$ eval $(docker-compose run -T shell aws ecr get-login --region ap-northeast-1 --no-include-email)
Login Succeeded
```

次に [01. Docker](01-docker) でビルドしたイメージを ECR にプッシュしてみましょう。

```console
$ docker tag sample-app 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/sample-app-komuro:latest
$ docker push 342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/sample-app-komuro:latest
```

## ECS クラスタの作成
<https://ap-northeast-1.console.aws.amazon.com/ecs/home?region=ap-northeast-1#/clusters>
から ECS クラスタを作成してみましょう。

ここでは Fargate とよばれる、インスタンス管理をマネージドで行ってくれるタイプのクラスタを作成します。

## ECS タスク定義の登録
プッシュしたイメージを作成した ECS クラスタの上で動かすため「タスク」の定義を作成してみましょう。

タスクロール、タスクの実行 IAM ロールは事前に用意している以下のものを設定してください。
- タスクロール: EcsTask
- タスクの実行 IAM ロール: EcsTaskExecution

「コンテナの追加」から実行する Docker イメージを指定します。
先程プッシュした
342842859783.dkr.ecr.ap-northeast-1.amazonaws.com/sample-app-komuro:latest
のようなイメージを追加してみましょう。

ポートマッピングのコンテナポートに「80」、環境変数 PORT にも「80」を指定してください。

## ECS サービスの登録
登録したタスク定義を用いてクラスタにサービスを登録してみましょう。

ここで起動するサービスは

- クラスター VPC: cookpad-internship
- サブネット: c-public, d-public
- セキュリティグループ: http-open
- パブリック IP の自動割り当て: ENABLED
- ロードバランサの種類: なし

サービスが無事起動していれば起動したタスクのパブリック IP アドレスからアプリケーションにアクセスできるようになっているはずです。

## ALB への登録
ECS サービスに直接接続することはできました。ロードバランサの裏に ECS サービスを配置し、柔軟にスケールできる構成にしてみましょう。

Fargate タイプの ECS サービスを登録するには「ターゲットの種類」は「IP」を選んでください。

## 参考リンク
- Amazon Elastic Container Service ドキュメント <https://docs.aws.amazon.com/ja_jp/ecs/>
- Amazon ECR ユーザガイド <https://docs.aws.amazon.com/ja_jp/AmazonECR/latest/userguide/>
- Amazon ECR で AWS CLI を使用する <https://docs.aws.amazon.com/ja_jp/AmazonECR/latest/userguide/ECR_AWSCLI.html>
