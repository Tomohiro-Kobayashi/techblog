+++
title = 'AWS Cli CheatSheet'
date = 2024-01-16T17:08:24+09:00
draft = false
description = "AWS CLIのコマンドのメモ"
image = "/techblog/images/aws-cli/aws-cli.webp"
imageBig = "/techblog/images/aws-cli/aws-cli.webp"
categories = ["AWS", "CLI", "CheatSheet"]
authors = ["Tomohiro"]
avatar = "/techblog/images/common/icon.webp"
+++

# 概要

自分用 AWS CLI コマンドのチートシート

## S3

### ファイルアップロード
```cl
aws s3 cp {filePath} s3://{bucketName}/{prefix}{fileName} --profile={EnvName}
```
e.g.
aws s3 cp test.jsonl s3://project-test-qa/snapshot/id=A00001/test.jsonl --profile=project-qa


#### memo
S3へのPutコマンドとして作用します。  
cpコマンドでファイルをアップロードするとLambdaのPUTトリガーが起動します。

### ファイル削除
```cl
aws s3 rm s3://{bucketName}/{prefix}{fileName} --profile={EnvName}
```
e.g.
aws s3 rm s3://project-test-qa/snapshot/id=A00001/test.jsonl --profile=project-qa

## EC2

### EC2起動
```cl
aws ec2 start-instances --instance-id {instance-id} --profile {profile}
```

### EC2停止
```cl
aws ec2 stop-instances --instance-id {instance-id} --profile {profile}
```

## Lambda
