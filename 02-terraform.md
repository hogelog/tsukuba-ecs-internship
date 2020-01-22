# Terraform
<https://www.terraform.io/>

Infrastructure as Code を実現するためのツールで、HCL という設定記述言語を利用してリソースを定義し、terraform コマンドラインツールを使ってインフラを管理することができます。

今は過渡期ですが、クックパッドでは AWS 関連のインフラは Terraform で管理・運用しています。

Terraform は多様なプラグインにより様々なインフラに対応したツールであり、たとえば AWS のリソースを管理したい場合には terraform-provider-aws <https://github.com/terraform-providers/terraform-provider-aws> を利用します。

## AWS 環境の作成
- AWS アカウント
- Backend
- VPC
- IAM User
- ECR
- ECS Cluster
- ALB

## TBD

## 参考リンク
- <https://www.terraform.io/docs/index.html>
- <https://www.terraform.io/docs/providers/aws/>
- <https://www.terraform.io/docs/backends/types/s3.html>
- <https://docs.docker.com/engine/reference/run/>
- <https://docs.docker.com/compose/>
- <http://sinatrarb.com/>

