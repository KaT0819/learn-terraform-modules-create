# Learn Terraform Modules Create

Learn what Terraform modules are and how to create one.

This repo is a companion repo to the [Build a Module learn tutorial](https://learn.hashicorp.com/tutorials/terraform/module-create?in=terraform/modules).


## モジュールのサンプル
S3の静的ウェブサイトの公開を行っているのでそのサンプルにもなる。


## 初期化
```
terraform init
# モジュールのインストール
terraform get
# デプロイ
terraform apply
```

## 動作確認
``` shell
# ファイルアップロード
aws s3 cp modules/aws-s3-static-website-bucket/www/ s3://$(terraform output -raw website_bucket_name)/ --recursive

# アクセス確認
curl https://$(terraform output -raw website_bucket_name).s3-us-west-2.amazonaws.com/index.html
curl https://$(terraform output -raw website_bucket_name).s3-us-west-2.amazonaws.com/error.html
```

## 破棄
``` shell 
# 先にS3にアップロードしたファイルを削除する
aws s3 rm s3://$(terraform output -raw website_bucket_name)/ --recursive

# 破棄
terrafrom destroy
```

