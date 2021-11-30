# cv
[keitakn](https://github.com/keitakn) の職務経歴、スキルシートです。

## 基本情報

| key | value |
|:---|:---|
|Name |KeitaKoga |
|Location |Tokyo |
|Twitter|https://twitter.com/keita_kn_web|
|Mail |keita.koga.work@gmail.com |
|GitHub |[keitakn](https://github.com/keitakn) |
|GitHub(Organization)|[nekonomokochan](https://github.com/nekonomokochan)|
|GitHub(友人と共同で運営しているOrganization)|[nekochans](https://github.com/nekochans)|
|Qiita|[keitakn](https://qiita.com/keitakn)|
|Zenn|[keitakn](https://zenn.dev/keitakn)|
|npm|[nekonomokochan](https://www.npmjs.com/~nekonomokochan)|
|Packagist|[nekonomokochan](https://packagist.org/profile/)|
|Speaker Deck|https://speakerdeck.com/keitakn|

# 得意な事

- テストコードや設計手法を工夫して、保守性・拡張性の高いシステムを構築する事
- 未知の技術でも比較的短い期間でキャッチアップを行う事
- アジャイル開発（スクラム）を用いたチームビルディング
- フロントエンドからインフラ構築（主にAWS）も含めたバックエンドまでWeb開発の一通りの工程を1人でこなす事が出来る事
- 相手に伝わりやすい非同期コニュニケーションを行う事が出来て、コミュニケーションの仕組みを構築出来る
  - （例1） [GitHubのコードレビューを受ける際に気をつける事](https://zenn.dev/keitakn/articles/github-code-review-reviewee)

主にリプレイスや新規開発案件で最も力を発揮出来るエンジニアだと思います。

現在の状況を見て最適なシステム構成を提案・実行させて頂きます。

またチームや組織の心理的な安全性を再重視しており、相手によって態度を変えない、フラットで丁寧なコミュニケーションを取る事を常に意識しております。

# あまり得意じゃない事

- Webデザイン（CSSは出来ますがUX等を考えたUIを作るスキルはありません）
- 背景・目的が不明確でただ言われた事だけをやる開発

# エンジニアリングで意識している事

フロントエンド、バックエンド、インフラ（クラウド）でそれぞれどのような事を意識しているかを記載しておきます。

### フロントエンドエンジニアとして意識している事

最近はNext.jsやReactをメインに扱っていますので、これらの技術を使った際の話を記載させて頂きます。

Propsにのみ依存する純粋なComponentと副作用を持つ部分を明確に分ける事を意識しています。

具体的には過去に強く影響を受けた [経年劣化に耐える ReactComponent の書き方](https://qiita.com/Takepepe/items/41e3e7a2f612d7eb094a) という記事に書かれているようにレイヤー毎に責務を分けてComponentを作成します。

テストコードに関しては以下の2つのテストにリソースを投入しています。

- カスタムフックのテスト（複数箇所から利用される事が多く、テストする価値が高い）
- E2Eテスト（フロントエンドの動作担保を行う為には、やはりE2Eテストが必須）

スナップショットテストや作成した関数に対する単体テスト等も場合によっては実装します。

Storybookに関しては、そのComponentが持つ振る舞いをStorybook上で全て表現しています。

またStorybookを静的Buildして、生成されたHTMLをS3 + Cloudfront等で閲覧出来る状態を作成しています。

これを行う事でUIの仕様が非エンジニアにも分かりやすくなります。

これは過去に関わった現場がやっていたのを真似しているのですが、UIに関するコミュニケーションを非常に円滑にしてくれるので、少々時間はかかりますが、行う価値がある方法だと思っています。

### バックエンドエンジニアとして意識している事

最近はGoをメインに書いていますので、その前提で記載させて頂きます。

あまり重厚なフレームワークは使わずに、Goの標準APIで小さなプロジェクトから始めるスタイルを取っています。

とは言え、テストを書きやすい構造にしておかないと後々プロジェクトが肥大化した際に困る事になるので、レイヤードアーキテクチャを最小しDDDライクな設計にする事が多いです。

テストコードはアプリケーション層（ユースケース層とも言う）に対して必ず実装するスタイルを取っています。

この形であれば後に大規模なリファクタリングが必要になった際もテストコードを頼りに進めやすいからです。

なおプロジェクトの規模によりますが、DBへの接続部分はモックを使わずにテスト用のDBを用意するスタイルを基本と考えています。（モックに差し替えられる設計にはした上で）

DBに意図した通りにデータが登録されるかどうかもバックエンドのAPIにとっては重要なファクターなのでテストコードで担保すべきという考えからです。

次に負荷対策についてですが、過去にはやった事がある最大規模のシステムは以下の通りです。

- 会員数が2000万人程度
- スループットの目標値が5000rps
- この負荷がかかった状態で参照系のAPIを150ms以内にレスポンスを返す事を目標にする

最近はAWS等のクラウド上にシステムを構築する事がほとんどなので、性能試験を行う際は、システムをスケールアウトした際にそれに伴って性能が向上する事を確認する事を意識しています。

### クラウドエンジニアとして意識している事

AWSをメインに扱っているので、その前提で記載させて頂きます。

AWSリソースはTerraformで構成管理を行うようにしています。

Terraform以外のツールとしてはServerless Frameworkを利用してLambda関数を管理する事が多いです。

誰がいつどのように変更したのかを把握するのと、環境構築手順をコード化して保存するのが目的です。

[AWS Well-Architected フレームワーク](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/index.ja.html) 等のAWSのベストプラクティスに準拠しセキュリティを意識した設計を心がけています。

## スキルレベル

スキルの習熟度の目安は下記の通りです。

あくまでも自己評価です。

- `S` : その技術における現時点でのベストプラクティスをある程度理解しており、実装出来る
- `A` : 業務レベルで普通に開発が出来る
- `B` : 業務経験ありだが経験が少ない
- `C` : 学習した事がある程度

### 言語

| 言語名     | スキルレベル | 備考                                                                                    |
|------------|--------------|-----------------------------------------------------------------------------------------|
| HTML       |       A      | フロントエンドをやっていた事もあるので普通に書けます。                              |
| CSS        |       A      | フロントエンドをやっていた事もあるので普通に書けます。                              |
| JavaScript |       S      | ブラウザ、Node.js共に経験あり、最新の仕様も把握しています。                               |
| TypeScript |       S      | ブラウザ、Node.js共に経験あり、最新の仕様も把握しています。                               |
| Go         |       S      | WebAPI（REST）とgRPCアプリケーションを開発した事があります、フレームワークは未使用。          |
| PHP        |       S      | ファーストキャリアで触れた言語です。最近は利用していません。                          |
| Ruby       |       A      | Ruby2.2、2.3の頃に利用していました、最近は利用していません。                              |
| Java       |       B      | 保守案件でJava8 + Spring Frameworkの組み合わせで少し開発した程度。                        |
| Scala      |       B      | PlayFramework2.4を少しだけ保守案件で触った程度、Gatlingでテストシナリオを書いていました。 |

JavaScript（TypeScript）がもっとも経験が長いです。最新の仕様にも追従出来ております。

PHPはファーストキャリアから扱っている言語で5年ほど扱っていましたが、最近触っていないので、最新の仕様には疎いです。（7.3系あたりで知識が止まっています）

最近、React、Next.jsでのフロントエンド開発やインフラ側のコードをAWS Lambdaで書く事が多いのでTypeScriptやGoを書く機会が一番多いです。

Rubyでもそこそこは戦えると自負しております。

Java, Scalaに関しては、まだ経験不足なところが否めないと感じております。

経験年数はあまり当てにならないと思いますので、私のGitHubを見て頂き、どの程度の技術力なのかを判断して頂くのが良いと思っております。

### フレームワーク（バックエンド）

| 名前             | スキルレベル | 備考                                                                                                     |
|------------------|--------------|----------------------------------------------------------------------------------------------------------|
| Zend Framework   |       A      | 一番最初に触ったフレームワークです。バージョンは1系でした。                                              |
| FuelPHP          |       A      | 1から導入した経験があります。                                                                            |
| Laravel          |       A      | 1から導入した経験があります。PHPでやるなら最近はこれがメインです。                                       |
| Express          |       S      | サーバーサイドでNode.jsをやる際に良く利用します。                                                        |
| Ruby on Rails    |       B      | 1から開発経験アリです。WebAPIの開発で利用しました。当時は4系だったので最新の仕様には追従出来ていません。 |
| Sinatra          |       A      | 1から開発経験アリです。                                                                                  |
| Spring Framework |       B      | 保守案件で少し触った程度で習熟度は高くありません。                                                       |
| Play Framework   |       B      | 2.4系を少しだけ保守案件で触った程度で習熟度は高くありません。                                            |

最近の自分の考えとしては、マイクロサービスアーキテクチャが主流になってきており、
フルスタックなフレームワークを駆使してモノリシックなシステムを開発するより、
Expressのような薄いフレームワークやAWS Lambdaのようなサービスを使って小規模で疎結合なシステムを構築していくのが良いと考えています。

もちろんモノリシックに作ったほうが早い場合も多々あるので全てのケースでは当てはまらないと思います。

Goに関してはフレームワークを利用せずに標準パッケージだけで小さなコンテナ用アプリケーションを作成するスタイルを取っています。

### フレームワーク、ライブラリ（フロントエンド）

| 名前     | スキルレベル | 備考                                                                                                     |
|---------|--------------|----------------------------------------------------------------------------------------------------------|
| jQuery  |       A      | JavaScriptで初めて触ったライブラリです。それなりに長く業務でも使っていましたが最近は全く触っていません。 |
| React   |       A      | 2015年頃からこれで開発をしています。ベストプラクティスもある程度は把握しています。                       |
| Vue.js  |       B      | Reactよりは習熟度が高くないですが、Vuexも含めたSPA開発を行った事があります。                             |
| Next.js |       A      | 新規開発のアプリケーションで複数回利用しました。                                                           |
| Nuxt.js |       A      | 新規開発のアプリケーションで複数回利用しました。                                                           |
| Angular |       C      | 1系の頃に少し学習しましたが最近は全く触っていません。                                                    |

最近はNext.js(React)がメインです。

少し前までは、Redux を使う事が多かったですが、最近は Redux を使わずに SWR や標準の React.Context を使う事もあります。

過去には Vue.js や Nuxt.js を導入した事もありますが、個人的には Vue.js よりも React が好きです。

Reactが好きな理由はAPIが比較的シンプルなのと、TypeScriptとの相性が良いからです。

npmを用いたフロントエンド周りの環境構築等も問題なく行う事が出来ます。

### DB

| 名前      | スキルレベル | 備考                                                                                   |
|-----------|--------------|----------------------------------------------------------------------------------------|
| MySQL     |       A      | 一番良く利用しています。5.1系の時代から5.7系までのバージョンを利用した経験があります。 |
| Redis     |       A      | オンプレでRedis Sentinelを使って自動フェイルオーバーの仕組みを構築した経験があります。 |
| memcached |       A      | キャリア初期の頃にCacheサーバーとして利用していました。                                |
| MongoDB   |       B      | 社内システムの構築時に一度だけ使った事があります。                                     |
| DynamoDB  |       B      | ServerlessアーキテクチャでAPIの認可基盤を開発した際に利用しました。                    |

上記に記載したDBは全て導入からチューニングまで対応しておりました。

ただしMongoDBだけは、アクセス数が限定可された社内システムでの利用だったので、高負荷時のパフォーマンス・チューニングの経験はありません。

MySQLに関しては、現在においても最も重要なRDBMSだと思っているので、設計やパフォーマンスチューニングにはそれなりに拘りを持っています。

※ DB設計に関する考えは [こちら](https://github.com/keitakn/web-developer-ojt/blob/master/docs/system-design/database.md) にまとまっています。

### Webサーバー

| 名前   | スキルレベル | 備考                                                                                  |
|--------|--------------|---------------------------------------------------------------------------------------|
| Apache |       A      | 2.2系をメインに触っていました。2.4系は一度だけWordPressのサイトを構築した時のみです。 |
| Nginx  |       A      | 最近はこちらのほうがメインで利用しています。                                          |

キャリアの初期の頃はPHPをApacheModuleとして動作させる形が多かったですが、最近はNginxがメインです。

### DevOps

| 名前           | スキルレベル | 備考                                                                               |
|----------------|--------------|------------------------------------------------------------------------------------|
| Vagrant        | S            | キャリア初期の頃から長く利用していましたが最近はDockerのほうが良く利用しています。 |
| Ansible        | S            | かなり複雑な設定も書いていたので大抵の事は可能だと思っております。                 |
| Terraform      | S            | AWSの構成管理でよく利用しています。                                                |
| Docker         | S            | 開発環境から本番環境まで様々な用途で利用しています。                               |
| Kubernetes     | C            | マイクロサービスの案件で利用しました。習熟度はまだ高くありません。                 |
| CircleCI       | B            | privateリポジトリのCIツールとしてよく利用していました。                            |
| TravisCI       | B            | 自分で公開しているnpmパッケージ等のCIツールとしてよく利用していました。            |
| GitHub Actions | A            | 最近ではCI・CDの構築にこれを用いる事が多いです。                                   |

最近の業務ではTerraformを用いたAWSの構成管理を行う事が多いです。

Dockerの運用に関してはAWS Fargateを使ってアプリケーションの実行環境構築を設計・構築した事があります。

Kubernetesはマイクロサービスでアプリケーションを設計する機会があり、その際に利用しました。

Kubernetesに関してはまだまだ運用経験が足りないので、ここは今後さらにスキルを伸ばしていきたいと思っています。

CI・CDの設定に関しては、GitHub Actionsを使う事が多いです。

### パブリッククラウド（AWS）

AWSで利用した事があるサービス一覧です。

| サービス名            | スキルレベル | 備考                                                                                         |
|-----------------------|--------------|----------------------------------------------------------------------------------------------|
| EC2                   |       S      | Webサーバーとして利用していました。                                                          |
| ECS                   |       A      | 最近はFargateを利用する機会が多いです。                                                      |
| ELB, ALB              |       S      | 今はALBをメインに使っています。                                                              |
| AWS Lambda            |       S      | 最近利用機会が多くなっています。REST APIやインフラ周りのタスク等様々な場面で利用しています。 |
| S3                    |       A      | 様々な用途で利用しています。                                                                 |
| CloudFront            |       A      | CDNとして利用しています。                                                                    |
| Route 53              |       A      | 利用しています。ドメインの購入もこちらのサービスを利用した事があります。                     |
| API Gateway           |       A      | AWS Lambdaと組み合わせて様々なAPIを開発した事があります。                                    |
| RDS                   |       A      | Multi-AZを意識した構成も構築した事があります。                                               |
| DynamoDB              |       A      | Lambdaと合わせてAPIサーバのDBとして利用した事があります。                                    |
| ElastiCache           |       A      | Laravel製のアプリケーションのキャッシュサーバとして利用しました。（Redisを利用）             |
| Cognito               |       A      | UserPoolを用いて認証基盤を構築。社内向け、エンドユーザー向け、両方構築経験があります。          |
| CloudFormation        |       B      | TerraformのほうがAWSの新機能への対応が早いので最近はあまり使っていません。                   |
| X-Ray                 |       B      | サーバーレスアプリケーションの監視・分析に利用しました。                                     |
| CodeDeploy            |       A      | EC2でのBlue/Greenデプロイの仕組みを構築した事があります。                                    |
| CodeBuild             |       A      | ECRへのプッシュ等、様々な用途で利用しています。                                              |
| Kinesis Data Firehose |       A      | アプリケーションログをS3バケットに転送する為に利用しました。                                 |
| Athena                |       A      | Firehoseで集めたログをSQLで検索する為に利用しました。                                        |
| EKS                   |       C      | マイクロサービスのアプリケーション基盤作成で利用しました。（それほど複雑な設定は行っていません）|
| Rekognition           |       A      | 画像に不適切な物が写っていないか確認する際に利用しました。個人サービスでも利用しています。|


VPCやCloudWatch等のAWSを利用すれば必ず利用するような物は含めておりません。

AWSは2015年頃から積極的に利用しており、0から上記のサービスを用いてインフラ全体（Webアプリケーションも含む）を構築した経験があります。

# 今興味がある技術

## Go

コンテナ技術との相性の良い点に魅力を感じています。

コンテナで動かすのが簡単でさらに言語の処理速度が高速なのでコンテナでアプリケーションを動かす事が多い現代には合っている言語だと感じています。

最近はLambdaや簡単なWebAPIはGoで書いています。

1度だけですが gRPC や Kubernetes と共に利用した事もあります。

## Kotlin

Goは小さなアプリケーションには非常に有用な言語ですが、ある程度の規模だとモダンな言語仕様を持つ言語が有効だと考えます。

以下の理由からKotlinに注目しています。

- Null安全、型推論等の最近のプログラミング言語のトレンドを抑えている
- SpringBoot等の超有名どころのフレームワークがKotlinに正式対応した事
- Scalaに比べて学習コストが低い印象でBetter Javaとしては今後こちらが伸びていきそうだから

## GCP

パブリッククラウドではAWSの1強だと思っていましたが、GKE等一部のサービスはAWSよりも使いやすい事や仕様が比較的シンプルなので、AWSの次に習得するべきクラウドだと考えています。

個人開発で最近利用を初めたので少しずつですが、習熟度は上がっています。

## GraphQL

フロントエンドをやっていた時にREAT APIとフロントエンドの連携部分で色々と試行錯誤をしていた中、[こちらのチュートリアル](https://www.howtographql.com/) をやった事で興味を持ちました。

また [AWS AppSync](https://aws.amazon.com/jp/appsync/) 等のマネージドサービスが登場した事も理由の1つです。

## Serverlessアーキテクチャ

現時点では全てのシステムをServerlessアーキテクチャで運用するのは必ずしも適切ではないと考えます。

しかし [Serverless Framework](https://serverless.com/) というOSSをメンテナンスしている人と関わりを持った事やこのOSSを使って開発をした際の開発体験の良さから今後伸びてくる分野だと思っています。

## Kubernetes
多くのパブリッククラウドがKubernetesのマネージドサービスに力を入れており、Kubernetesでアプリケーションを運用している前提で利用出来るOSSも増えて来ていると感じています。

デプロイ、オートスケール等全てをKubernetesで完結出来るのと、今後のコンテナ実行環境のデファクトスタンダードになっていく感じがあるので現在注目しています。

## Next.js
個人的にはVue.jsよりもReactのほうがTypeScriptの型システムの恩恵を受けやすい点（この点はVue.js3.0系でかなり改善されそうですが）やベストプラクティスを公式が積極的に情報発信している点などの理由で気に入っているのですが、Vue.jsベースのNuxt.jsのほうが機能が豊富でフレームワークとしての完成度は高いと思っていました。

しかし最近は Next.js が以下のような新機能を追加した事等で Nuxt.js との差が縮まっていると感じているので、注目しています。

- [動的ルーティング](https://nextjs-docs-ja.netlify.app/docs#%E5%8B%95%E7%9A%84%E3%81%AA%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0)
- [API ルート](https://nextjs-docs-ja.netlify.app/docs#api-%E3%83%AB%E3%83%BC%E3%83%88)
- [ISR(Incremental Static Regeneration)](https://nextjs.org/docs/basic-features/data-fetching#incremental-static-regeneration) のサポート

特にISRは自分が関わっている多くのサービスの応答速度を改善出来る可能性を秘めているので、注目しています。

友人と一緒に開発している個人サービス [LGTMeow](https://lgtmeow.com) でもNext.js で ISR を利用しています。

↓がソースコードです。

https://github.com/nekochans/lgtm-cat-frontend

# 主な職務経歴

## WordPress制のアプリケーションのフロントエンドをNext.jsを利用した形にリプレイス（2021）

### 業務概要

多くのサービスを運用しているクライアントの案件です。

WordPressで作成された医療系メディアサービスのフロントエンドの大幅改修です。

以下の問題を解決するのが目的です。

- 応徳速度が遅いので高速化したい
- フロントエンドに対しての要件が複雑化してきているので、それに耐えられる開発基盤を構築したい

また他のサービスのフロントエンドも同様の改修を予定しており、他のサービスのリプレイスが効率的に実行出来るように開発基盤を整える事も目的としています。

### 利用した技術

- React 17系
- Next.js 12系
- Storybook
- JEST
- ESLint
- Prettier
- Vercel

### プロジェクトの規模

プロダクトマネージャー（1名）、自分（1名）、デザイナー（1名）の合計3名。

### 主な成果

※ この案件は現在も仕掛中なので途中経過を記載します。

技術選定にはNext.jsを採用しました。

ISRがメディアサービスとの相性が良く、応答速度を大幅に改善出来る可能性があったのが最も大きな理由です。

Next.jsを動かす環境としてはVercelを選択しました。

Next.jsのメリットを最大限に享受する為にはVercelが最も無難な選択だと判断した為です。

HeaderやFooter等が色々なサービスで同じデザインで利用されていました。

デザイナーさんと協業しながら、GitHub Packagesを利用して共通のUIComponentとしてprivate packageとして利用出来る仕組みを構築しました。

package化する際は [smarthr-ui](https://github.com/kufu/smarthr-ui) 等を参考にしました。

これらの対応により以下の問題が解決する予定です。

- 応答速度の大幅改善
- フロントエンドの開発基盤と開発ルールが作成された

今後 [SmartHR Design System](https://smarthr.design/) のようにルールを整備して外部公開出来るくらいのクオリティに仕上げて行きたいと思っています。

## メール送信を行う為のAPIの開発（2021）

### 業務概要

多くのサービスを運用しているクライアントで同じ内容のメール送信処理を複数のアプリケーションから行っており、メール文言の修正等でも複数箇所の修正が必要な状態でした。

メール送信処理を一元化して管理しやすい状態にするのが目的です。

### 利用した技術

- Go
- AWS Lambda
- [SendGrid Web API v3](https://sendgrid.kke.co.jp/docs/API_Reference/Web_API_v3/index.html)
- Serverless Framework
- GitHub Actions
- Terraform

### プロジェクトの規模

プロダクトマネージャー（1名）、自分（1名）の合計2名。

### 主な成果

郵便番号から住所検索を行うAPIと同じくAWS Lambdaを利用しました。

メール送信用のサービスにはSendGridを利用しました。

リリース前には [IPウォームアップ](https://sendgrid.kke.co.jp/docs/Tutorials/D_Improve_Deliverability/ip_warmup.html) を行い大量送信時にも送信遅延が発生しないように考慮し、独自ドメインからメール送信が出来る設定も追加しました。

これにより以下の問題を解決する事が出来ました。

- メール送信ロジックを一元管理出来るようになった
- 元々SESを使っていたのだが、それに比べてメールの到達率が向上した
- SendGridに変えた事によってバウンスメールの管理も容易になった

試算だとこのままの事業成長を続けた場合、あと少しでLambdaの同時実行制限にかかってくる可能性が出てきました。その為、現在ははApp Runnerに移行しています。

## 郵便番号から住所検索を行う事が出来るAPIの開発（2021）

### 業務概要

多くのサービスを運用しているクライアントで郵便番号から住所を検索する処理が色々なところで行われており、郵便番号の一覧や住所マスタも各サービスでバラバラに管理されている状態でした。

様々なサービスで利用出来るように住所検索用の共通APIを作成する事が目的です。

### 利用した技術

- Go
- AWS Lambda
- [ケンオール](https://kenall.jp/docs/)
- Serverless Framework
- GitHub Actions

### プロジェクトの規模

プロダクトマネージャー（1名）、自分（1名）の合計2名。

### 自分の役割

アーキテクチャの選定、設計・開発、各サービス開発者向けのドキュメンテーション作成。

### 主な成果

Go + AWS Lambda で [ケンオール](https://kenall.jp/docs/) のAPIに通信を行い、住所情報を返すAPIを実装しました。

住所検索APIとして [ケンオール](https://kenall.jp/docs/) は新しいサービスですが、APIインターフェースの設計が非常に優れていて、かつ低料金で利用出来るので、採用しました。

それにより以下の問題を解決する事が出来ました。

- バラバラになっていた郵便番号から住所を取得する処理が統一された
- 住所マスタのメンテナンスが不要になった

CI/CDの設定はGitHub Actionsを用いて行いました。

スピード感を重視して AWS Lambda を利用しましたが、リリース後、アクセス数が増えてきており、Lambdaの同時実行制限にかかってくる可能性が出てきました。

コールドスタートも発生しているので、今後はApp Runnerに移行する可能性があります。

## クラウドファンディングサービスのメッセージ一斉送信機能の改善（2021）

### 業務概要

クラウドファンディングサービスでプロジェクトの実行者と支援者がメッセージのやり取りを出来る機能があるのですが、実行者が全ての支援者に一斉送信を行う際にタイムアウトが発生して送信出来ない問題がありました。

支援者が多いプロジェクトでも一斉送信が出来るように改修する事が目的です。

### 利用した技術

- Ruby on Rails（5系）
- Amazon Aurora（MySQL5.7互換）
- SendGrid

### プロジェクトの規模

プロダクトマネージャー（1名）、自分（1名）の合計2名。

### 自分の役割

メッセージ一斉送信機能を再構築する為に必要な課題出しや設計・開発。

### 主な成果

メール送信に時間がかかるという問題とDBへのデータのインサートに時間がかかるという問題がありました。

データ量が多く、テーブル構造を大幅に変える事が難しかったので、既存のテーブル構造を活かしつつ、一斉送信用の関連テーブルを作る事で対応しました。

メール送信にはSendGridを利用する事を提案し実現しました。

SendGridは1000件ずつアドレスを指定して送信出来るので、メールの送信時間を大幅に短縮出来る事が選定理由です。

また処理をDelayed Jobを使って非同期処理にしました。

その結果、以下の問題を解決出来ました。

- 改修前は3000件程度が限界だったが、20000件を超えても送信出来るようになった
- 非同期処理にした事でユーザーの待ち時間がなくなった

## クラウドファンディングサービスの認証基盤構築（2020〜2021）

### 業務概要

Rails の devise で構築された認証基盤を IDaaS（Identity as a Service）を利用した形に置き換える。

また初期リリースのスコープではないが、様々なサービスのIDを利用したソーシャルログインやパスワードログイン以外の認証手段も追加予定です。

### 利用した技術

- Go（CognitoUserPoolのカスタムLambdaやUserPoolのデータを操作するAPIを実装）
- React（16系）
- OpenAPI（V3）
- Terraform

### プロジェクトの規模

初期は開発リーダー1名、自分の2名。

途中から開発者2名と相談役の方が1名追加。

### 自分の役割

- 既存の認証基盤から新しい認証基盤にデータを移行する方法を設計・実装
- ログイン状態を維持出来る仕組みの設計
- Goを用いて、CognitoUserPoolのカスタムLambdaやUserPoolのデータを操作するAPIを実装
- ERBで作成されていた登録フォームやログインフォームをReactを使って再構築

### 主な成果

スケジュールも短めだったので、最初に案件概要を聞いた時は Auth0 を使う事でスムーズな認証基盤の移行が出来ると考えましたが、予算的な都合でより安価で運用出来るCognitoUserPoolを利用する事になりました。

CognitoUserPoolはAPIのレートリミットに厳しい制限があったり、カスタマイズLambdaやユーザー移行Lambdaを駆使しないと無停止でのデータ移行が難しかったりしたので、課題を解決する為に必要な技術検証を慎重に行いました。

その結果、以下のような状態を構築する事が出来ました。

- サービスを停止する事なく既存認証基盤から新しい認証基盤にデータを移行する仕組みが出来たので、長時間のメンテナンスによる機会損失を回避出来た
- 少ない工数でソーシャルログインの追加が行えるようになった（OpenIDConnectに準拠している必要はある）

## クラウドファンディングサービスの応援コメントを取得する機能をAPI化（2020）

### 業務概要

クラウドファンディングのプロジェクトには多くの応援コメントが投稿されますが、コメントが多すぎるプロジェクトではコメント表示遅延が発生していました。

コメントが多いプロジェクトでも正常に全てのコメントが表示されるようにする事が目的となります。

### 利用した技術

- React（16系）
- Ruby on Rails（5系）
- Amazon Aurora（MySQL5.7互換）
- OpenAPI（V3）

### プロジェクトの規模

プロダクトマネージャー（1名）、自分（1名）の合計2名。

他コードレビューなどに関わって頂いた方が3名ほど。

### 自分の役割

- OpenAPIのスキーマを用いてAPIの設計
- 上記スキーマを元にRailsでAPIの実装
- ERBで作成されていた画面をReactを使ってSPA化

### 主な成果

以下のような制約があり、厳しい状況でしたが、現場のエンジニアの方のサポートもあり何とか乗り切る事が出来ました。

- 優先度が高く、期日が短かった
- コメント取得用のテーブル構造を変更する事は時間的な制約上非常に難しい
- こちらの現場がOpenAPIのスキーマを導入してまだ間もない事もあり、決まっていないルールが多数あった
- この現場にアサインされて初の案件だったので、ドメイン知識がほぼ0の状態だった

こちらの現場では段階的にアプリケーションのマイクロサービス化を行っていた事もあり、現場のエンジニアの方と話し合った結果、以下の方針で実装する事になりました。

- コメントの表示部分はSPA化、スクロールする度に新しいコメントを取得して表示
- コメントを取得するAPIを実装（ページングも考慮する）

バックエンドのAPIを実装する際はスロークエリが発生しないように心掛け、フロント側の実装の際は React Developer Tools を見ながら、パフォーマンスを考慮し実装しました。

APIのインターフェースも後にDBのテーブル構造の変更を行った後でも、インターフェースを変えずに運用出来るように意識して設計しました。

またOpenAPIスキーマの設計の際は決まっていない事が多かったですが、現場のエンジニアの方と議論して一緒に設計の際のルール決めなども行いました。

以下の現象が解消されたので案件の目的は達成する事は出来たと思います。

- 大量のコメントが存在するプロジェクトでもコメントの表示遅延がなくなった
- スクロールを行う事で全てのコメントを確認出来るようになった（元々コメントの表示件数に上限が設置されていた）

## ユーザーに通知を送るAPIをKubernetes（EKS）上で開発（2020）

### 業務概要

ユーザーの様々なアクションに関して通知を送るAPIをマイクロサービスで開発。

（例）ユーザーが投稿した記事にコメントが付いた際や、コメントに返信があった際に通知を送る。

### 利用した技術

- AWS（EKS）
- Go
- gRPC
- Terraform

### プロジェクトの規模

自分と開発者1名。

### 自分の役割

- アーキテクチャ全体の決定
- Goを用いたgRPCでアプリケーションの開発

### 主な成果

- EKS上でアプリケーションを構築出来る基盤が出来た
- PHP中心の現場でGoでの開発の知見を広める事が出来た

Goでの開発能力を向上させる為、Goに詳しいエンジニア（社外の方です）に講師を依頼したりするなどを行い、積極的に技術情報をアウトプットする事を意識しました。

この現場はPHPが中心だったので、Goでも開発で注意すべき点や、PHPで書いていたコードをGoで書く場合、どのような点に気をつけるか？等を社内ドキュメントにまとめました。

これによってこのプロジェクトに深く関わっているメンバー以外もGoによる開発がある程度出来るようになりました。

リリースを行ったものの、予算的な都合で当初予定していたよりも小規模な形で運用する事になってしまいました。

時間的な理由でEKSの構成管理やCI/CD等の仕組みが納得出来る物に出来なかったのが悔やまれます。

自分がKubernetesやgRPCを扱うのが初めてだった事もありますが、もう少し深く技術調査をすべきでした。

Kubernetesを扱えた事自体は貴重な経験になったと思っています。

## AWSを用いたアプリケーションインフラ基盤の構築（2019）

### 業務概要

クラウド広告運用ツールの新環境の構築。

### 利用した技術

- AWS（様々のサービスを利用）
- Terraform

### プロジェクトの規模

自分とCTOの2名

### 自分の役割

- アーキテクチャ全体の決定
- Terraformを用いてマルチリージョンで運用可能なクラウド環境を構築

### 主な成果

- コード管理されていないインフラ環境がコードで管理されるようになった
- 海外進出の際にも他国のリージョンでアプリケーションが運用可能になった

## EC2のアプリケーションをAWS Fargateに移行（2018）

### 業務概要

EC2で運用中のアプリケーションをFargateで動作するように改修。

### 利用した技術

- AWS Fargate
- AWS CodeBuild
- ECR
- Docker Hub
- Terraform
- CircleCI
- Gatling（性能試験ツール）

### プロジェクトの規模

自分と開発者1名

### 自分の役割

- 全体的な方針決め
- Fargateのログを分析出来る基盤の構築
- 各アプリケーションのDockerfileの作成

### 主な成果

- コンテナベースになった事で開発者同士の環境差異による問題が減少
- デプロイ速度の高速化
- 運用料金の最適化

一部のアプリケーションは [Twelve-Factor App](https://12factor.net/ja/) の要件を満たすように改修を行いました。

個人としてもDocker運用の為の基本的なノウハウを蓄積する事が出来ました。

## 看護師向けのコミュニティサイトの全面リプレイス（2017）

### 業務概要

看護師さん向けのコミュニティサイトのDBも含めた全面リプレイス

### 利用した技術

- PHP7.2（Laravel5.5）
- TypeScript
- Next.js（React）
- Nuxt.js（Vue.js）
- AWS（様々なサービスを利用）
- JIRA（プロジェクト管理ツール）
- Confluence（ドキュメント管理ツール）
- GitHub
- CircleCI

### プロジェクトの規模

- 開発リーダー（自分）、開発者5名、プロジェクトマネージャー1名

### 自分の役割

- システム全体のアーキテクチャを決定
- スクラムマスターとしてスクラムチームの開発効率を上げる為に様々な施策を実施
- AWSを用いたインフラ構築全般（Terraform構成管理、デプロイの仕組み、ログ解析基盤）
- AWS Lambda + TypeScriptを用いたOpenIDConnectに準拠したAPIの認可基盤
- PHP7.2（Laravel5.5）を用いたWebAPIの開発
- Next.js, Nuxt.jsによるフロントエンドの開発
- CognitoUserPoolを用いたユーザーの認証基盤（管理サイトで利用）

### 主な成果

- モノリシックな構成からマイクロサービス（厳密なマイクロサービスではない）に移行した事でシステム全体が疎結合になった
- レガシーな開発手法を行っていたチームにAtlassian製品の導入やZenHub、AWSの導入等を行った事で開発効率が大幅に上がった
- 自走出来る開発チームを作り上げる事が出来たので、開発効率、品質共に大きく向上させる事が出来た

チームマネジメントからアーキテクチャの設計、インフラ構築、フロントエンド・バックエンドの開発・設計等、ほぼ全ての工程に関わる事が出来ました。

データ移行もトラブルが少なく、前回関わったリプレイス案件よりもスムーズにプロジェクト進行を行う事が出来ました。

[こちら](https://speakerdeck.com/keitakn/development-of-authorization-system-using-authlete-and-aws) はその時に作ったシステムの一部を紹介したスライドです。

## 某大手ECサイト 会員基盤の全面リプレイス（2016）

### 業務概要

老朽化していた会員基盤システムをDB構造等も含めて全面的にリプレイス。

会員数はこの時点で約2000万人程になります。

### 利用した技術

- Java8(API サーバ)
- Spring Framework4系
- Ruby on Rails 4（管理サイト）
- MySQL5.6
- Couchbase3系（バックエンドのキャッシュサーバとして利用）
- Redis ※APIが利用するメッセージングサーバとして利用
- AWS（ステージング環境、性能試験環境として利用）
- Vagrant
- Ansible
- Docker
- JIRA（プロジェクト管理ツール）
- Confluence（ドキュメント管理ツール）
- Bitbucket（Git管理ツール）
- Jenkins

### プロジェクトの規模

開発リーダー（自分）、技術顧問1名、開発者7名、ディレクター2名、プロジェクトマネージャー

### 自分の役割

- 開発リーダー（自分）
- 旧DBから新DBへのデータ移行計画の作成
- データ移行時のテストを自動化
- 全体的なシステムアーキテクチャを決定
- 新会員基盤APIの設計
- 新会員管理サイトの要件定義・設計・開発
- Ansibleを用いたサーバ構成管理
- APIの開発

### 主な成果

- DB構造の一新をした事で性能が大幅に向上し急激な会員数の増加にも耐えられるようになった
- 性能試験環境をAWSで構築した事により、ミドルウェアの性能試験を気軽に行えるようになった

大規模案件で技術負債が多く困難を極めましたが何とかやり遂げる事が出来ました。

この案件で主に学んだ事は以下の3つです。

- リプレイス案件で最も高難易度なのはデータの移行である事
- 少数精鋭のチームを作る事の重要性（頭数を揃えても開発スピードは上がらない）
- 技術検証を事前にやる事は非常に大切である

## 社内用認可基盤の開発（2015）

### 業務概要

社内向けのAPIを一元管理する為、OAuth2.0の仕組みを使った認可基盤を開発。

Amazon API Gatewayの簡易版のようなイメージです。

### 利用した技術

- Node.js（Express）
- Redis ※API Gatewayのキャッシュサーバとして利用
- PHP5.4.X（FuelPHP）※クライアントID等を管理する管理側のサイト
- MySQL5.5
- Jenkins
- JMeter

### プロジェクトの規模

プロジェクトマネージャー、設計・開発者（自分含め6名）

### 自分の役割

- クライアントID等を管理する管理側のサイトの要件定義〜設計、開発まで全て
- Node.jsでのAPIの実装・ユニットテストの作成、パフォーマンステストの実施

### 主な成果

- 今まで独自実装していたAPIの認証・認可の仕組みが一般的な仕組みに置き換わりました。
- APIのアクセス管理が出来るようになったのでどのクライアントがどの機能を利用しているか明確になりました。
- 今までのプロジェクトでは出来ていなかった、継続的インテグレーションが出来るようになり、リリース後の不具合が大幅に減少しました。

OAuthProviderの実装はOpenIDConnectの公式仕様を見ながら実装に落とし込む事が出来ました。

この案件でRFCや公式ドキュメント等の1次情報（主に英語の情報）を読むことの重要性を改めて理解しました。

## 社内用共通デプロイツールの改修（2014年）

### 業務概要

独自実装されたデプロイツール（テストなし、再現環境なし）を一般的なツールにリプレイス。

### 利用した技術

- Jenkins
- Capistrano（Ruby）

### プロジェクトの規模

自分、プロジェクトマネージャーの2名

### 自分の役割

- 要件定義〜設計、開発まで全て

### 主な成果

今まで俗に言う「秘伝のタレ」だったデプロイツールを一般的なツールに置き換える事で誰でもメンテナンスが出来るようになりました。

## 某大手ECサイト ソーシャルログイン機能を導入（2013年）

### 業務概要

某大手ECサイトにソーシャルログイン機能を導入。

初期リリースではFacebookとGoogleに対応しました。

### 利用した技術

- PHP5.3.X
- Zend Framework 1.X.XX
- Facebook API
- Google API

### プロジェクトの規模

自分（開発リーダー）、開発者1名、ディレクター1名の計3名

### 自分の役割

- 案件の要件定義
- 設計全般
- プログラム実装

### 主な成果

リリース後、一ヶ月で会員登録数が50万人増加しました。

会員登録という重要機能だったので、安全なOAuthクライアントの実装方法を調査し設計・実装しました。

この案件でOAuthやOpenIDConnectの基礎的な内容を理解する事が出来ました。

## 某大手ECサイト ユーザーの個人情報を取得するAPIを高速化（2013年）

### 業務概要

ユーザーの個人情報を取得するAPIの性能向上。

### 利用した技術

- PHP5.3.X
- Zend Framework 1.X.XX
- MySQL5.1系
- MySQL5.5系

### プロジェクトの規模

自分1人（レビュワーに先輩エンジニア1名）

### 自分の役割

- memcachedを利用したキャッシュの導入による処理高速化
- MySQLのクエリチューニングによるSQL実行速度の高速化
- MySQLサーバーのバージョンアップ

### 主な成果

テーブル構造が10年近く前から存在するレガシーな物という制約がある中でSQLの組み立てを工夫して性能改善を行いました。

平均応答速度が400msから150msに改善する事が出来ました。

性能的に実用レベルに達した事もあり、これ以降このAPIが実際のプロダクトで利用されるようになりました。

## 某大手ECサイト ユーザーの個人情報を取得するAPIを開発（2013年）

### 業務概要
ユーザーデータにアクセスしている機能をWebAPI化し分離する。

### 利用した技術

- PHP5.3.X
- Zend Framework 1.X.XX
- MySQL5.1系

### プロジェクトの規模

自分を含めエンジニア3名、ディレクター1名

### 自分の役割

- APIの開発・ユニットテストの作成
- APIの内部設計（外部設計は先輩エンジニアが担当）

### 主な成果

正社員エンジニアとしては初めての案件です。

ユニットテストが書かれていないクラスにも積極的にユニットテストを追加しテストの自動化に貢献しました。

コードレビューを通じて、変更に強い設計手法、Gitの運用ルール等を習得しました。

# こんな人達と働きたいです

- より良い仕組み、技術が出てきたら、今までの常識を捨てて柔軟に考え方を変えられる人達
- 精神的に自立した人（Give思考で物を考えられる、チーム、顧客、エンジニア業界に自ら価値を与える意思がある）
- 相手を独立した一人の人間として考え尊重出来る人達（チームにはコミットしつつ、個人の考えを尊重出来る人達）
- 技術の学習を自分に対する投資と捉えられる人達
- 技術情報の発信に関して理解がある人達

# 以下のような方々とはお仕事をお断りさせて頂きます

- 旧態依然的な価値観に囚われている人達（過度な権威主義、全体主義）
- 正当な評価制度が存在しない企業さん（仲良し人事が横行、バリューを出した人が正当に評価されない）
- 技術的な事情に対して経営層が理解していない企業さん（専門職に対する敬意がない現場と言える）
- 仕事に関係ない強制的な社内イベントへの参加が存在する現場（休日のBBQ、社員旅行等、存在しても不参加OKなら問題なし）
- 人に傲慢な態度を取ったり、人の人格を否定するような心理的安全を脅かす人がいる現場
- 年齢、性別、等の自分ではどうしようもない事で差別をする人間がいる現場
- 長期案件で厳密な納期確約を強要してくる現場（この件に関しては [こちら](https://qiita.com/keitakn/items/c30b7071ebfbf4b1b3e0) を見て頂きたいです）
