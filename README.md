# CloudFormationStudy
Studying is fun for me. CloudFormation.

## What's CloudFormation ?

* EC2やELBなどを使ったAWSサービスのシステム構築、設定ファイル（テンプレート）を元に行えるサービス
* テンプレートを自由に作成できるため、自分好みのシステム構成が可能
* テンプレートは、AWSのサービスを操るための新しい言語

## Use Case

* 一度テンプレートを作成すれば、同じ構成を再現できる
   * 開発環境の構築
   * Blogシステム、Webシステム、ゲームプラットフォームなど、同じ仕組みでアプリやデータが異なるようなもの
* ベストプラクティスが盛り込まれたテンプレートを使用可能
  * システムアーキテクチャの再利用
* 起動時にパラメーターを渡せる
  * DBのエンドポイントをEC2に渡せる

### What's Stack ?

* リソースの集合体のこと
* スタック単位でリソースの管理が可能。スタック破棄を実行すると、スタックに紐作りソースを破棄することが可能
* 使用するリソースおよびリソースの構築順は、テンプレートの依存関係で決定

### What's Template ?

* AWS TemplateFormationVersion
  * テンプレートのバージョン。2010-09-09固定。
* Description
  * 説明文
* Parameters
  * CloudFormation実行時に後で変更可能なパラメーターを列挙。
    * スタック構築時に値の入力が可能
    * データ型、デフォルト値、最小最大値など設定可能
    * 入力したパラメーター値は、テンプレート中で "Ref"を使用して参照可能
    * ユーザー名、パスワード、ドメインなどの可変部分に便利
* Mappings
  * Hashtableのようなもの。キーに応じて値を特定できる。
    * キーとバリューのテーブル
    * たとえば、入力値やリージョンによって値が変わるようなものを決めるような使い方
      * "Fn::FindInMap”で値を取得
* Couditions
  * Parameters、他のCondition、Mappingから条件判断し結果に応じてリソースを作成可能
* Resources
  * EC2やRDSなど、スタックを構成するリソースを定義
    * EC2やELB,RDSなど、起動するサービスを設定
    * リソースごとに決められたパラメーターを設定する
* Outputs
  * スタック構築後に表示・取得したい値。
    * たとえばアクセスURLや、DBの通信先情報、作ったIAMユーザー名など、あとで使用するもの
    * マネジメントコンソールから確認できるので、スタックに関する情報を出力すると便利

## Note

### Check Stack

```
aws cloudformation validate-template --template-body file://[YAML_FILE_PATH]
```

### Create Stack 

```
aws cloudformation create-stack --template-body file://[YAML_FILE_PATH] --stack-name [STACK_NAME]
```

### Create Stack (Parameter Stack)

```
aws cloudformation create-stack --template-body file://[YAML_FILE_PATH] --parameters file://[JSON_FILE_PATH] --stack-name [STACK_NAME]
```

### Create Stack (w/ Create IAM Resource)
```
aws cloudformation create-stack --template-body file://[YAML_FILE_PATH] --parameters file://[JSON_FILE_PATH] --stack-name [STACK_NAME] --capabilities CAPABILITY_NAMED_IAM
```

### Delete Stack

```
aws cloudformation delete-stack --stack-name [STACK_NAME]
```

## Recommended Plugin

### Visual Studio Code Extention

* [CloudFormation support for Visual Studio Code](https://github.com/aws-scripting-guy/cform-VSCode)
  * スケルトン作成：YAMLファイルを作成後に ```start``` とタイプする。

* [AWS CloudFormation Linter](https://github.com/aws-cloudformation/cfn-python-lint)

* [Sort lines](https://github.com/Tyriar/vscode-sort-lines)

#### cli Linter

```
cfn-lint [YAML_FILE_PATH]
```

### Ansible

```
ansible-playbook -i aws_ec2.yml site.yml
```

### Describe instance

```
aws ec2 describe-instances
```

### Create AMI

```
aws ec2 create-image --instance-id i-XXXXXX --no-reboot --name ami-demo_`date "+%Y%m%d-%H%M%S"` [--dry-run]
```

## Overview

![TODO](https://github.com/YusukeOno/CloudFormationStudy/wiki/img/overview.png "Overview")

## Reference Link

* DefaultVPCをawscliで作成する  
https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html#create-default-vpc

* 参考にさせていただいたリポジトリ構成  
https://qiita.com/y-ohgi/items/89f07e866713185799f5

* [AWSマイスターシリーズ] AWS CloudFormation  
https://www.slideshare.net/AmazonWebServicesJapan/aws-aws-cloudformation

* AWS CloudFormationベストプラクティス  
https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/best-practices.html

* AWS CloudFormationのテンプレート  
https://aws.amazon.com/jp/cloudformation/resources/templates/