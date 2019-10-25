# Getting Started with CodeBuild

## Create S3 buckets for Input and Output

```shell
aws s3 mb s3://codebuild-us-west-2-1strategy-sandbox-acct-input-bucket
aws s3 mb s3://codebuild-us-west-2-1strategy-sandbox-acct-output-bucket
```

## Create CodeBuild Service Role

```shell
aws iam create-role --role-name CodeBuildServiceRole --description "CodeBuild Service Role" --assume-role-policy-document file://CodeBuild/assume-role.json --path /service-role/
```

```shell
aws iam put-role-policy --role-name CodeBuildServiceRole --policy-name CodeBuildServiceRolePolicy --policy-document file://CodeBuild/base-policy.json
```

## Create CodeBuild Project

```shell
aws codebuild create-project --cli-input-json file://create-project.json
```

## Create CodePipeline Role

```shell
aws iam create-role --role-name AWS-CodePipeline-CodeBuild-Service-Role --description "CodePipeline Service Role" --assume-role-policy-document '{"Version":"2012-10-17","Statement":{"Effect":"Allow","Principal":{"Service":"codepipeline.amazonaws.com"},"Action":"sts:AssumeRole"}}'
```

```shell
aws iam put-role-policy --role-name AWS-CodePipeline-CodeBuild-Service-Role --policy-name CodePipelineCodeBuildServiceRolePolicy --policy-document file://CodePipeline/codepipeline-policy.json
```

## Create Pipeline

```shell
aws codepipeline create-pipeline --cli-input-json file://CodePipeline/pipeline.json
```