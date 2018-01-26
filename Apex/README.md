## インストールからLambdaデプロイしてHelloworldまで
 
 - install
   - `$ curl https://raw.githubusercontent.com/apex/apex/master/install.sh | sh`

- `$ apex init`
```
             _    ____  _______  __
            / \  |  _ \| ____\ \/ /
           / _ \ | |_) |  _|  \  /
          / ___ \|  __/| |___ /  \
{
         /_/   \_\_|   |_____/_/\_\



  Enter the name of your project. It should be machine-friendly, as this
  is used to prefix your functions in Lambda.

    Project name: go

  Enter an optional description of your project.

    Project description: go

  [+] creating IAM go_lambda_function role
  [+] creating IAM go_lambda_logs policy
  [+] attaching policy to lambda_function role.
  [+] creating ./project.json
  [+] creating ./functions

  Setup complete, deploy those functions!
```

- ディレクトリ構成
```
.
├── event.json
├── functions
│   └── hello
│       └── main.go
├── pkg
│   └── darwin_amd64
│       └── github.com
│           └── aws
│               └── aws-lambda-go
│                   ├── lambda
│                   │   └── messages.a
│                   ├── lambda.a
│                   └── lambdacontext.a
├── project.json
└── src
    └── github.com
        └── aws
            └── aws-lambda-go
                ├─ ・・・
```
- GOPATHを設定

- GOのパッケージ取得
  - `$ go get -u github.com/aws/aws-lambda-go/lambda`

- `$ apex deploy`
```
   • creating function         env= function=hello
   • created alias current     env= function=hello version=1
   • function created          env= function=hello name=go_hello version=1
```

→ AWS LambdaにFunctionが作成される

- `$ go apex invoke hello < event.json`
> {"Answer:":"Hello !!"}
