+++
title = 'AWS Cli CheatSheet'
date = 2024-01-16T17:08:24+09:00
draft = false
description = "AWS CLIのコマンドのメモ"
image = "/techblog/images/common/noimage.webp"
imageBig = "/techblog/images/common/noimage.webp"
categories = ["AWS", "CLI", "CheatSheet"]
authors = ["Tomohiro"]
avatar = "/techblog/images/common/icon.webp"
+++

# 概要

自分用 AWS CLI コマンドのチートシート

## S3

### ファイルアップロード

aws s3 cp {filePath} s3://{bucketName}/{prefix}{fileName} --profile={EnvName}

e.g.

```cl
aws s3 cp test.jsonl s3://project-test-qa/snapshot/id=A00001/test.jsonl --profile=project-qa
```

#### memo
S3へのPutコマンドとして作用します。  
cpコマンドでファイルをアップロードするとLambdaのPUTトリガーが起動します。

### ファイル削除

aws s3 rm s3://{bucketName}/{prefix}{fileName} --profile={EnvName}

e.g.

```cl
aws s3 rm s3://project-test-qa/snapshot/id=A00001/test.jsonl --profile=project-qa
```

## EC2

## Lambda
