# CloudFormationStudy
Studying is fun for me. CloudFormation.

## Note.

### Create Stack 

```
aws cloudformation create-stack --stack-name practice-20201128 --template-body file://./01_practice/init.yaml
```

### Delete Stack

```
aws cloudformation delete-stack --stack-name practice-20201128
```

## Recommended Plugin

### Visual Studio Code Extention

* [AWS CloudFormation Linter](https://github.com/aws-cloudformation/cfn-python-lint)

* [Sort lines](https://github.com/Tyriar/vscode-sort-lines)

#### cli Linter

```
cfn-lint [path to YAML file]
```

## Reference Link

https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html#create-default-vpc