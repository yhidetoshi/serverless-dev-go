　# Apex
 
 
 ## HelloWorldまで
 
 - install
   - `$ curl https://raw.githubusercontent.com/apex/apex/master/install.sh | sh`

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

- `go apex invoke hello < event.json`
> {"Answer:":"Hello !!"}
