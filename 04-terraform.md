# Terraform
<https://www.terraform.io/>

Infrastructure as Code を実現するためのツールで、HCL という設定記述言語を利用してリソースを定義し、terraform コマンドラインツールを使ってインフラを管理することができます。

今は過渡期ですが、クックパッドでは AWS 関連のインフラは Terraform で管理・運用しています。

Terraform は多様なプラグインにより様々なインフラに対応したツールであり、たとえば AWS のリソースを管理したい場合には terraform-provider-aws <https://github.com/terraform-providers/terraform-provider-aws> を利用します。

ここまでで利用した各種 AWS リソースについても、普段はあのように手で作るのではなく Terraform を利用しソースコード経由で作成・管理しています。

今回利用している AWS リソースの多くのものも tsukuba-ecs-internship-infra のコード内の `terraform/` 以下に含まれる Terraform コードにより作成されたものです。

（時間があればある程度デモ）

## 参考リンク
- <https://www.terraform.io/docs/index.html>
- <https://www.terraform.io/docs/providers/aws/>
- <https://www.terraform.io/docs/backends/types/s3.html>

