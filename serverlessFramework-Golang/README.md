# serverless-framework

- 環境
  - MacOS(10.11.6) 
  - Go(aws-sdk-go)のコードをaws-lambdaにデプロイする

- `$ npm install -g serverless`

- cd ${HOME}/go-serverlessFramework

- `$ serverless create -u https://github.com/serverless/serverless-golang/ -p myservice`
```
Serverless: Generating boilerplate...
Serverless: Downloading and installing "serverless-golang"...
Serverless: Successfully installed "myservice"
```
- `$ cd ${HOME}/go-serverlessFramework/myservice`
- $ export GOPATH=`` `pwd` ``
- `$ go get github.com/aws/aws-lambda-go/lambda`
- `$ GOOS=linux go build -o bin/main`
- `$ serverless deploy`
```
Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Creating Stack...
Serverless: Checking Stack create progress...
.....
Serverless: Stack create finished...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service .zip file to S3 (2.97 MB)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
...............
Serverless: Stack update finished...
Service Information
service: myservice
stage: dev
region: us-east-1
stack: myservice-dev
api keys:
  None
endpoints:
  None
functions:
  hello: myservice-dev-hello
```
- バージニア北部にfunctionができており、実行したら下記が表示された。
```
{
  "message": "Go Serverless v1.0! Your function executed successfully!"
}
```

### EC2インスタンスの情報を取得するコードをLambda上で実行した時のめも

1. `go get <github.com/xxx>`
1. input credentials
1. `serverless.yml`の `region` を `ap-northeast-1`に変更
1. 上記のLambdaへのデプロイした方法でデプロイして実行する


```
README.md      bin            main.go        pkg            serverless.yml src
```
- main.go
```
package main

import (
	"fmt"
	"github.com/aws/aws-lambda-go/lambda"
	"github.com/aws/aws-sdk-go/aws"
	"github.com/aws/aws-sdk-go/aws/credentials"
	"github.com/aws/aws-sdk-go/aws/session"
	"github.com/aws/aws-sdk-go/service/ec2"
)

func HandleRequest() {
	sess := session.Must(session.NewSession())
	creds := credentials.NewStaticCredentials()
	svc := ec2.New(
		sess,
		aws.NewConfig().WithRegion("ap-northeast-1").WithCredentials(creds),
	)
以下、情報取得のプログラムは省略
(https://github.com/yhidetoshi/clitoolgoaws)
```

- ログ出力
```
START RequestId: cf2b6237-03de-11e8-bf8d-c3e9b285f2ac Version: $LATEST
{
 InstanceNmae:	test
 InstanceType:	t2.micro
 AvailabilityZone:	ap-northeast-1c
 State:	stopped
 PrivateIP:	172.31.8.141
}
END RequestId: cf2b6237-03de-11e8-bf8d-c3e9b285f2ac 
```
