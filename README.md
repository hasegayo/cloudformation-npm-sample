## CloudFormation with NPM Sample

npm-scripts から AWS CLI を呼び出すことで CloudFormation を実行しています。

## 構成

|  Path  |  概要  |
| ---- | ---- |
|  [docker-files/*](./docker-files)  |  [Amazon ECR](https://aws.amazon.com/jp/ecr/) に登録する image 作成用の Dockerfile 置き場  |
|  [docs/*](./docs)  |  *.drawio, *.png ファイル, etc... 置き場  |
|  [examples/*](./examples)  |  サンプル置き場(〜工事中〜)  |
|  [templates/*](./templates)  |  master.yml から呼ばれる子テンプレート置き場  |
|  [master.yml](./master.yml)  |  templates/* のテンプレートを呼び出す親テンプレート |

## 実行環境

#### 1. Node.js インストール

ぐぐる。おすすめは、以下のバージョン管理ツールで入れる方法

| OS | app |
| ---- | ---- |
| macOS | [nodenv](https://github.com/nodenv/nodenv) |
| windows| [nodist](https://github.com/nullivex/nodist) |

#### 2. AWS CLI インストール

[公式のインストーラー](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-cliv2.html)が整備されてて便利。  
[AWS CLI のかんたん設定](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-configure.html#cli-quick-configuration) もやっておく

## テンプレートを書く
[templates/*](./templates) 配下に xxx.yml を作成し、それを master.yml から参照するネスト構成とする。  
[このへん](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/AWS_EC2.html)を参考に、気合で完成させる。

## デプロイ

`master.yml` を起点に CloudFormation を以下コマンドで実行する

```sh
npm run deploy:dev 
```

Sample-Dev という名前でスタックが作られるので、名前を変えたい場合は以下のように指定する（少し冗長だが）

```sh
npm run deploy:dev -- -- --stack-name="XXX"
```

> Successfully created/updated stack - XXX

というログが出たら、スタックの作成完了。  
スタックの進捗、及び成功/失敗については[AWS マネジメントコンソール](https://aws.amazon.com/jp/console/)から確認すること。

## スタックの停止、削除

これも[AWS マネジメントコンソール](https://aws.amazon.com/jp/console/)から行うこと。

## デプロイコマンドのカスタマイズ

[package.json](package.json) をいじる。
