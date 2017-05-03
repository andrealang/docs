---


copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} とは
{: #bluemixoverview}

{{site.data.keyword.Bluemix}} は、Platform as a Service (PaaS) と Infrastructure as a Service (IaaS) を組み合わせた、{{site.data.keyword.IBM_notm}} の革新的なクラウド・コンピューティング・プラットフォームです。また、{{site.data.keyword.Bluemix_notm}} は、ビジネス・アプリケーションを迅速に作成するために PaaS および IaaS と簡単に統合できる、クラウド・サービスの豊富なカタログを備えています。
{:shortdesc}

これから規模を拡大する予定の中小企業であっても、さらに分離を必要とする大企業であっても、{{site.data.keyword.Bluemix_notm}} にはニーズに合うクラウド・デプロイメントが揃っています。お客様は境界のないクラウド内で開発を行うことができ、このクラウドで、{{site.data.keyword.IBM_notm}} が提供するパブリック {{site.data.keyword.Bluemix_notm}} サービスにお客様の専用サービスを接続することができます。お客様およびお客様のチームは、{{site.data.keyword.Bluemix_notm}} でアプリ、サービス、およびインフラストラクチャーにアクセスし、既存のデータ、システム、プロセス、PaaS ツール、および IaaS ツールを使用できます。開発者は、使用可能なサービスおよびランタイム・フレームワークの急成長しているエコシステムを利用して、他言語プログラミング・アプローチによってアプリケーションを作成できます。
 
{{site.data.keyword.Bluemix_notm}} を使用すれば、新規のアプリのテストや実行のためにハードウェアに多額の投資を行う必要がなくなります。代わりに、IBM がすべてを管理し、使用した分だけ課金されるようになります。{{site.data.keyword.Bluemix_notm}} は、パブリック、[専用](/docs/dedicated/index.html)、および[ローカル](/docs/local/index.html)の統合デプロイメント・モデルを提供しています。 

アイデアを方向付けから、開発サンドボックス、そしてグローバル分散実稼働環境に移行させることができます。グローバル分散実稼働環境では、計算およびストレージ・インフラストラクチャー、オープン・ソース・プラットフォームのサービスとコンテナー、{{site.data.keyword.IBM_notm}}、Watson などからのソフトウェア・サービスとツールを備えることができます。{{site.data.keyword.Bluemix}} は、プラットフォーム自体の能力を超えて、柔軟なデプロイメントも提供します。{{site.data.keyword.Bluemix}} リソースをオンプレミス、専用プライベート・クラウド環境、またはパブリック・クラウドでプロビジョンし、3 つすべてのタイプの環境からのリソースを単一のダッシュボードで管理します。
 
パブリック環境および専用環境にデプロイされたすべての {{site.data.keyword.IBM_notm}} クラウド・リソースは、世界中にある {{site.data.keyword.CloudDataCent}} ロケーションからお客様が選択した場所でホストされます。{{site.data.keyword.CloudDataCents_notm}} は、地域的冗長性、すべてのデータ・センターおよび PoP を接続するグローバル・ネットワーク・バックボーン、および厳格なセキュリティー管理とレポート作成を備えています。
{{site.data.keyword.CloudDataCents_notm}}を使用することで、
{{site.data.keyword.IBM_notm}} は、最も要求の高い拡張、セキュリティー、コンプライアンス、およびデータ常駐のニーズを満たすことができます。 

{{site.data.keyword.IBM_notm}} では、以下を可能にします。

* 世界中にあるセキュアな {{site.data.keyword.CloudDataCents_notm}}にハイパフォーマンスの計算およびストレージ・インフラストラクチャーをデプロイする。
* {{site.data.keyword.IBM_notm}}、オープン・ソース・コミュニティー、およびサード・パーティー開発者からの広範囲に及ぶクラウド・サービスと機能をテストして採用する。
* プライベート・ネットワークおよび API 機能を使用して、単一の拡張が容易なクラウド・プラットフォームから、ご使用のすべてのレガシー・システムおよびアプリに接続する。
* ビジネスのニーズやワークロード要求の変化に応じて、リソースをリアルタイムで拡張および縮小する。

### アプリ
{: #bluemixoverviewapplications}

「アプリ」ダッシュボードは、アプリを稼働させるため、およびアプリを実行中に管理するために必要なすべてのものを備えています。{{site.data.keyword.Bluemix_notm}} では、以下のようなさまざまなボイラープレートおよびランタイムが用意されています。

* ボイラープレートは、アプリケーションとその関連するランタイム環境、および特定のドメインの事前定義サービスのためのテンプレートです。 
* ランタイムは、アプリを実行するために使用されるリソース・セットであり、さまざまなタイプのアプリのコンテナーとして提供されます。

{{site.data.keyword.Bluemix_notm}} では、アプリを実行するための方法として、例えば Cloud Foundry や {{site.data.keyword.containerlong}} など、さまざまな方法が用意されています。{{site.data.keyword.containerlong}} は、{{site.data.keyword.Bluemix_notm}} 上のホストされたクラウド環境で Docker コンテナーを実行するために使用します。 

イベント・ドリブンの分散コンピューティングのために、{{site.data.keyword.openwhisk}} を使用できます。{{site.data.keyword.openwhisk_short}} は、イベントに応えて、または、Web アプリやモバイル・アプリからの HTTP を介した直接起動に応えて、アプリケーション・ロジックを実行します。
 
{{site.data.keyword.Bluemix_notm}} Mobile サービスを使用して、事前に作成され、管理された、拡張が容易なクラウド・サービスをご使用のモバイル・アプリに取り込むことができます。 

### サービス
{: #bluemixoverviewservices}

「サービス」ダッシュボードでは、{{site.data.keyword.IBM}} およびサード・パーティー・プロバイダーから使用可能な {{site.data.keyword.Bluemix_notm}} サービスにアクセスできます。これには、Watson、IoT、Analytics、Mobile、DevOps の各サービスがあります。

* {{site.data.keyword.IBM_notm}} DevOps サービスおよび {{site.data.keyword.Bluemix_notm}} Garage Method を使用して適切な機能のみを備えることで、革新的な新規アプリケーションをより迅速かつ低コストで提供します。DevOps のプラクティスを取り入れてイノベーションとアジリティーの文化を作り出すと、反復プラクティスを使用し、市場に対応して方向転換することができます。
* ブロックチェーンは、ビジネス・プロセスを簡素化しながら、信頼、アカウンタビリティー、および透明性を確立する新しい世代のトランザクション・アプリケーション用のピアツーピアの分散レジャー・テクノロジーです。  
* Watson は、音声、視覚、データの各 API の完全なスイートを備えたコグニティブ・コンピューティングの力をアプリに提供します。Watson サービスを使用したコグニティブ・プラットフォームをデプロイすることで、最も複雑なビジネスの問題を解決できます。
* {{site.data.keyword.IBM_notm}} により、豊富な機能を持ち、統合されたクラウド・データベースおよびデータと分析サービスを使用して、より多くのことを実行できます。 
* {{site.data.keyword.IBM_notm}} の IoT サービスにより、アプリは、接続されたデバイス、センサー、およびゲートウェイと通信し、それらが収集したデータを取り込むことができます。レシピを利用すると、簡単にデバイスを IoT クラウドに接続できます。その後、アプリでリアルタイム API および REST API を使用してデバイスと通信し、収集対象として設定したデータを取り込むことができます。 
* {{site.data.keyword.IBM_notm}} は、マルチプラットフォーム・アプリ、ネイティブ・アプリ、またはハイブリッド・アプリをモニターおよびテストできるようにしながら、そのようなアプリを作成できるモバイル・バックエンド・インフラストラクチャーを提供します。アナリティクス、セキュリティー、ユーザー・インサイト、継続的デリバリーで、アプリを強化することもできます。 
 
{{site.data.keyword.Bluemix_notm}} は、試すことができる試験的サービスも提供しています。サービス・タイプおよび使用可能かどうかについて詳しくは、[{{site.data.keyword.Bluemix_notm}} サービス](/docs/services/index.html)を参照してください。


### インフラストラクチャー
{: #bluemixoverviewinfrastructure}

「インフラストラクチャー」ダッシュボードは、クラウド・インフラストラクチャーのニーズに適合した各種サービスを提供します。

{{site.data.keyword.Bluemix_notm}} インフラストラクチャーは、入手可能な最高のパフォーマンスを発揮するクラウド・インフラストラクチャーを提供します。{{site.data.keyword.Bluemix_notm}} インフラストラクチャーは、最も広範なクラウド・コンピューティング・オプションが揃ったデータ・センターを世界中に持ち、すべてを統合して自動化する 1 つのプラットフォームです。{{site.data.keyword.CloudDataCents_notm}}は、一流のコンピューティング、ストレージ、およびネットワーキングの機能を豊富に揃えています。各ロケーションは同様に構築され、装備され、運用されています。したがって、弊社の拠点のどこででもお客様はまったく同じ機能と可用性を得られます。ロケーションは、業界で最も先進のネットワーク内ネットワークによって接続されています。このネットワークは、パブリック、プライベート、内部管理の別個のネットワークを統合し、ネットワークの総コストを抑えて、より良いアクセスと、より速いスピードを提供します。また、データ・センターとネットワークは、単一の専有管理システムを共有します。単一の管理ツールにより、すべてのベアメタル・サーバー、仮想サーバー、およびストレージ・デバイスを含むすべてを制御できます。これらはすべて、API、ポータル、およびモバイル・アプリケーションからアクセス可能です。

{{site.data.keyword.Bluemix_notm}} インフラストラクチャーは、シームレスな単一プラットフォームで、強力なベア・メタル・サーバーと柔軟な仮想サーバーを提供します。すべてがオンデマンドで提供され、月単位または時間単位の期間で請求されます。ベアメタル・サーバーは、プロセッサー集中型およびディスク入出力集中型のワークロードに対して直接的な処理能力を提供し、お客様の仕様どおりに構成できます。仮想サーバーでは、高速デプロイメント、柔軟な拡張容易性、および従量課金 (PAYG) の請求が可能です。ハイパフォーマンス・コンピューティングのために、時間単位または月単位で使用可能なグラフィックス処理装置 (GPU) サーバーを使用して、クラウドの機能を向上させることができます。 

{{site.data.keyword.Bluemix_notm}} インフラストラクチャー・オファリングは、3 層のネットワークに接続され、パブリック・トラフィック、プライベート・トラフィック、および管理トラフィックがセグメント化されます。お客様の {{site.data.keyword.Bluemix_notm}} アカウントのインフラストラクチャーは、無料でプライベート・ネットワークを介して、そのようなインフラストラクチャー間でデータを転送する場合があります。ベアメタル・サーバー、仮想サーバー、およびクラウド・ストレージなどのインフラストラクチャー・オファリングは、パブリック・ネットワークを介して、{{site.data.keyword.Bluemix_notm}} カタログ内の他のアプリケーションおよびサービス (Watson サービス、コンテナー、ランタイムなど) に接続します。そのような 2 つのタイプのオファリング間で転送されるデータは、計測され、標準パブリック・ネットワーク帯域幅レートで課金されます。

## {{site.data.keyword.Bluemix_notm}} コンソールの使用
{: #bluemixoverviewui}

{{site.data.keyword.Bluemix_notm}} コンソールにアクセスすると、メニュー・バーに、登録、ログイン、資料へのアクセス、およびカタログへのアクセスのためのリンクやボタンが表示されます。ログイン後には、以下のようにご使用のアカウント・タイプに応じて、メニュー・バーには、ハンバーガー・メニュー ![ハンバーガー・アイコン](../icons/icon_hamburger.svg) および追加リンクが含まれています。

* 新規 {{site.data.keyword.Bluemix_notm}} ユーザーの場合、ハンバーガー・メニュー ![ハンバーガー・アイコン](../icons/icon_hamburger.svg) を使用して、「アプリ」、「サービス」、または「インフラストラクチャー」の各ダッシュボード間で切り替えることができます。サポートおよびアカウント・オプションへのリンクが表示され、**「カタログ」**リンクを使用して、{{site.data.keyword.Bluemix_notm}}、計算、およびインフラストラクチャーのサービスにアクセスできます。 
* 既存のユーザーで、{{site.data.keyword.Bluemix_notm}} と {{site.data.keyword.BluSoftlayer}} アカウントをリンクしている場合、ハンバーガー・メニュー ![ハンバーガー・アイコン](../icons/icon_hamburger.svg) を使用して、「アプリ」、「サービス」、または「インフラストラクチャー」の各ダッシュボード間で切り替えることができます。サポートおよびアカウント・オプションへのリンクが表示され、**「カタログ」**リンクを使用して、{{site.data.keyword.Bluemix_notm}}、計算、およびインフラストラクチャーのサービスにアクセスできます。 
* {{site.data.keyword.Bluemix_notm}} アカウントを使用している既存のユーザーの場合、ハンバーガー・メニュー ![ハンバーガー・アイコン](../icons/icon_hamburger.svg) を使用して、「アプリ」ダッシュボードおよび「サービス」ダッシュボード間で切り替えることができます。サポートおよびアカウント・オプションへのリンクが表示され、**「カタログ」**リンクを使用して、{{site.data.keyword.Bluemix_notm}} サービスおよび計算サービスにアクセスできます。 
* {{site.data.keyword.BluSoftlayer}} アカウントを使用している既存のユーザーで、そのアカウントを {{site.data.keyword.Bluemix_notm}} にまだリンクしていない場合、メニュー・バーには、{{site.data.keyword.BluSoftlayer}} で以前使用可能だったリンク (KnowledgeLayer ヘルプへのアクセス、連絡オプション、通知、チケットのオープン、ログインなど) が表示されます。また、「インフラストラクチャー」ダッシュボードへのリンク、サポートおよびアカウント・オプションへのリンクも表示されます。 

## {{site.data.keyword.Bluemix_notm}} Cloud Foundry アーキテクチャー
{: #architecture}

一般に、Cloud Foundry で {{site.data.keyword.Bluemix_notm}} 上のアプリを実行する際にオペレーティング・システムやインフラストラクチャー層について気にする必要はありません。ルート・ファイル・システムやミドルウェア・コンポーネントなどの層は抽象化されているため、ユーザーはアプリケーション・コードに集中できます。ただし、アプリケーションがどこで実行されているか詳細を知る必要がある場合は、これらの層について詳しく学ぶことができます。
 

詳しくは、『[{{site.data.keyword.Bluemix_notm}} のインフラストラクチャー層の表示 (Viewing Bluemix infrastructure layers)](/docs/manageapps/infra.html#viewinfra)』を参照してください。

開発者は、ブラウザー・ベースのユーザー・インターフェースを使用して {{site.data.keyword.Bluemix_notm}} のインフラストラクチャーと対話することができます。また、cf という、Cloud Foundry コマンド・ライン・インターフェースを使用して、Web アプリをデプロイすることもできます。

クライアント (モバイル・アプリ、外部で稼動するアプリ、{{site.data.keyword.Bluemix_notm}} でビルドされるアプリ、あるいはブラウザーを使用している開発者) は {{site.data.keyword.Bluemix_notm}} でホストされているアプリと対話します。クライアントは、REST API または HTTP API を使用し、{{site.data.keyword.Bluemix_notm}} を経由して要求をアプリ・インスタンスまたはコンポジット・サービスのいずれかに経路指定します。

次の図は、{{site.data.keyword.Bluemix_notm}} Cloud Foundry アーキテクチャーの概要を示したものです。

![{{site.data.keyword.Bluemix_notm}} アーキテクチャー](images/arch.png)

図 1. {{site.data.keyword.Bluemix_notm}} Cloud Foundry アーキテクチャー

待ち時間またはセキュリティーを考慮して、アプリはさまざまな {{site.data.keyword.Bluemix_notm}} の地域にデプロイすることができます。1 つの地域にデプロイすることも、複数地域にまたがってデプロイすることも選択できます。
詳しくは、『[地域](whatisbluemix.html#ov_intro_reg)』を参照してください。


![複数地域のアプリケーション開発](images/multi-region.png)

図 2. 複数地域のアプリケーション・デプロイメント

## {{site.data.keyword.Bluemix_notm}} Cloud Foundry の仕組み
{: #howwork}

アプリを {{site.data.keyword.Bluemix_notm}} Cloud Foundry にデプロイする場合は、そのアプリをサポートするのに十分な情報を使用して {{site.data.keyword.Bluemix_notm}} を構成する必要があります。

* モバイル・アプリの場合、{{site.data.keyword.Bluemix_notm}} には、モバイル・アプリがサーバーとの通信に使用するサービスなどの、モバイル・アプリケーションのバックエンドを表す成果物が含まれています。
* Web アプリの場合、ランタイムおよびフレームワークに関する情報が {{site.data.keyword.Bluemix_notm}} に伝達されるようにする必要があります。それにより、{{site.data.keyword.Bluemix_notm}} がそのアプリを実行するのに適した実行環境をセットアップすることができます。

モバイルおよび Web の両方を含め、各実行環境は他のアプリの実行環境から分離されています。実行環境は、これらのアプリが同じ物理マシン上にあったとしても互いに分離されます。以下の図は、{{site.data.keyword.Bluemix_notm}} Cloud Foundry でのアプリのデプロイメント管理方法の基本的なフローを示しています。

![アプリのデプロイ](images/deploy.png)

図 3. アプリのデプロイ

アプリを作成し、{{site.data.keyword.Bluemix_notm}} Cloud Foundry にデプロイすると、{{site.data.keyword.Bluemix_notm}} 環境は、そのアプリ、またはそのアプリが表す成果物の送信先となる適切な仮想サーバーを決定します。モバイル・アプリの場合、モバイル・バックエンド・プロジェクションが {{site.data.keyword.Bluemix_notm}} 上に作成されます。クラウドで実行されるモバイル・アプリのコードはすべて、結局は {{site.data.keyword.Bluemix_notm}} 環境で実行されます。
Web アプリの場合、クラウドで実行されるコードは、開発者が {{site.data.keyword.Bluemix_notm}} にデプロイするアプリ自体です。仮想サーバーの決定は、以下を含むいくつかの要因に基づいて行われます。

* マシン上に既に存在する負荷
* その仮想サーバーがサポートするランタイムまたはフレームワーク

仮想サーバーが選択された後、各仮想サーバー上のアプリケーション・マネージャーは、そのアプリに適切なフレームワークとランタイムをインストールします。その後、アプリをそのフレームワークにデプロイすることができます。デプロイメントが完了すると、アプリケーション成果物が開始されます。

以下の図は、複数のアプリがデプロイされている仮想サーバー (Droplet Execution Agent (DEA) とも呼ばれる) の構造を示しています。

![仮想サーバーの設計](images/container.png)

図 4. 仮想サーバーの設計

各仮想サーバーで、アプリケーション・マネージャーは {{site.data.keyword.Bluemix_notm}} インフラストラクチャーの残りの部分と通信し、この仮想サーバーにデプロイされたアプリを管理します。各仮想サーバーには、アプリを分離し保護するためのコンテナーがあります。それぞれのコンテナーに、{{site.data.keyword.Bluemix_notm}} は各アプリに必要な、適切なフレームワークとランタイムをインストールします。

アプリがデプロイされた時、そのアプリに Web インターフェース (Java Web アプリ用など)、またはその他の REST ベースのサービス (モバイル・アプリに公開されているモバイル・サービスなど) が含まれている場合、そのアプリのユーザーは、通常の HTTP 要求を使用してそのインターフェースまたはサービスと通信することができます。

![{{site.data.keyword.Bluemix_notm}} アプリの呼び出し](images/execute.png)

図 5. {{site.data.keyword.Bluemix_notm}} アプリの呼び出し

各アプリは、そのアプリに関連付けられた 1 つ以上の URL を持つことができますが、それらはすべて {{site.data.keyword.Bluemix_notm}} エンドポイントを指していなければなりません。要求が着信すると、{{site.data.keyword.Bluemix_notm}} はその要求を調べ、対象のアプリを判別し、要求を受け取るアプリのインスタンスを選択します。


### 地域
{: #ov_intro_reg}

{{site.data.keyword.Bluemix_notm}} の地域は、アプリをデプロイ可能な定義済みの地理上の区域です。異なる地域で、
アプリケーション管理に同じ {{site.data.keyword.Bluemix_notm}} インフラストラクチャー、
課金に同じ使用量詳細ビューを使用して、アプリおよびサービス・インスタンスを作成できます。顧客に最も近い地域を選択して、この地域にアプリをデプロイすることで、アプリケーションの待ち時間を短くすることができます。
また、セキュリティー問題に対応するために、アプリケーション・データを保存しておく地域を選択することも可能です。
複数地域でアプリを構築すると、1 つの地域が使用不可になっても、別の地域にあるアプリが稼働し続けます。使用する各地域で、リソースの割当量は同じです。

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用すると、別の地域に切り替えて、その地域のスペースで作業することができます。ユーザー・アカウント設定リンクをクリックし、**「地域」**セレクターを展開し、リストから必要な地域を選択します。

cf コマンド・ライン・インターフェースを使用する場合は、作業する {{site.data.keyword.Bluemix_notm}} 地域に接続するために、cf api コマンドを使用して地域の API エンドポイントを指定します。例えば、
{{site.data.keyword.Bluemix_notm}} ヨーロッパ・英国地域に接続するには、次のコマンドを入力します。


```
cf api https://api.eu-gb.{{site.data.keyword.Bluemix_notm}}.net
```

各地域に固有の接頭部が割り当てられています。
{{site.data.keyword.Bluemix_notm}} には、次の地域と、地域接頭部が用意されています。


<!-- PRODUCTION ONLY: Ensure that URLs are production URLs, not stage1-->

| **地域名** | **地理的位置** | **地域接頭部** | **cf API エンドポイント** | **UI コンソール** |       
|-----------------|-------------------------|-------------------|---------------------|----------------|
| 米国南部地域 | ダラス、米国 | ng | api.ng.bluemix.net | console.ng.bluemix.net |
| 英国地域 | ロンドン、イングランド | eu-gb | api.eu-gb.bluemix.net | console.eu-gb.bluemix.net |
| シドニー地域 | シドニー、オーストラリア | au-syd | api.au-syd.bluemix.net | console.au-syd.bluemix.net |
{: caption="Table 1. {{site.data.keyword.Bluemix_notm}} region list" caption-side="top"}


### {{site.data.keyword.Bluemix_notm}} の回復力
{: #resiliency}

{{site.data.keyword.Bluemix_notm}} は、ユーザーのニーズに応じて拡張が容易であり、高可用性を維持し、問題からの復旧速度も速い、拡張が容易で回復力のあるアプリおよびアプリケーション成果物をホストするよう設計されています。{{site.data.keyword.Bluemix_notm}} は、相互作用の状態をトラッキングするコンポーネント (ステートフル) とトラッキングしないコンポーネント (ステートレス) を分離します。この分離により、{{site.data.keyword.Bluemix_notm}} は必要に応じてアプリを柔軟に移動し、スケーラビリティーと回復力を確保できます。

アプリの 1 つ以上のインスタンスを実行させることができます。単一のアプリに対して複数のインスタンスがある場合、そのアプリがアップロードされるのは 1 回のみです。ただし、{{site.data.keyword.Bluemix_notm}} は、要求された数のアプリ・インスタンスをデプロイし、それらをできる限り多くの仮想サーバーに分散します。

アプリの外のステートフル・データ・ストア (例えば、{{site.data.keyword.Bluemix_notm}} で提供されているいずれかのデータ・ストア・サービス上のステートフル・データ・ストア) にすべての永続データを保存する必要があります。メモリー内またはディスク上にキャッシュされたデータはすべて再始動後も使用できない可能性があるので、単一の {{site.data.keyword.Bluemix_notm}} インスタンスのメモリー・スペースまたはファイル・システムを、短い単一トランザクション・キャッシュとして使用できます。単一インスタンスのセットアップの場合、{{site.data.keyword.Bluemix_notm}} のステートレスな性質により、アプリへの要求が中断される可能性があります。ベスト・プラクティスは、可用性を確保するために、各アプリケーションに少なくとも 3 個のインスタンスを使用することです。

すべての {{site.data.keyword.Bluemix_notm}} インフラストラクチャー、Cloud Foundry コンポーネント、および {{site.data.keyword.IBM_notm}} 固有の管理コンポーネントが高い可用性を持っています。インフラストラクチャーの複数インスタンスを使用して、負荷のバランスが保たれます。

### SoR との統合
{: #sor}

{{site.data.keyword.Bluemix_notm}} は、クラウド環境内にある、以下の 2 つの広範なカテゴリーのシステムを接続することで、開発者を支援できます。 

* *SoR* にはビジネス・レコードを保管するアプリとデータベースが含まれており、標準化されたプロセスを自動化します。 
* *SoE* は SoR の有用性を拡張する機能で、これによりユーザーが SoR をより有効に活用できるようになります。

{{site.data.keyword.Bluemix_notm}} で作成するアプリと SoR を統合することで、ユーザーは次のアクションを実行できます。

 * セキュア・コネクターをオンプレミスにダウンロードしてインストールすることで、アプリとバックエンド・データベースとの間のセキュア通信を可能にする。
 * セキュアな方法でデータベースを呼び出す。
 * データベースとカスタマー・リレーションシップ・マネジメント・システムなどのバックエンド・システムとの統合フローから API を作成する。
 * アプリに対して公開したいスキーマおよびテーブルのみを公開する。
 * {{site.data.keyword.Bluemix_notm}} 組織管理者として、
自分の組織メンバーのみに表示されるプライベート・サービスとして API を公開する。
 
SoRを {{site.data.keyword.Bluemix_notm}} で作成するアプリと統合するには、Cloud Integration サービスを使用します。Cloud Integration サービスを使用すれば、Cloud Integration API を作成し、その API を組織のプライベート・サービスとして公開できます。

<dl>
<dt>Cloud Integration API</dt>
    <dd>Cloud Integration API により、Web API を通してファイアウォールの後ろにある SoR への保護されたアクセスが提供されます。Cloud Integration API を作成する際には、Web API を通してアクセスしたいリソースを選択し、許可されたオペレーションを指定し、API にアクセスするための SDK とサンプルを組み込みます。Cloud Integration API の作成方法について詳しくは、『[Cloud Integration 入門](/docs/services/CloudIntegration/CldInt_GetStart.html)』を参照してください。</dd>
<dt>プライベート・サービス</dt>
    <dd>プライベート・サービスは、 Cloud Integration API、SDK、およびライセンス・ポリシーから構成されます。また、サービス・プロバイダーからのドキュメンテーションや他の項目がプライベート・サービスに含まれる場合もあります。Cloud Integration API をプライベート・サービスとして公開できるのは、組織管理者のみです。自分が利用できるプライベート・サービスを表示するには、{{site.data.keyword.Bluemix_notm}} カタログで「プライベート (Private)」チェック・ボックスを選択します。
Cloud Integration サービスに接続せずに、プライベート・サービスを選択してアプリにバインドすることができます。プライベート・サービスのアプリへのバインドは、他の {{site.data.keyword.Bluemix_notm}} サービスの場合と同じ方法で行います。プライベート・サービスとして API を公開する方法については、プライベート・サービスとしての API の公開を参照してください。</dd>
</dl>

#### シナリオ: SoR と接続するための機能豊富なモバイル・アプリを作成する
{: #scenario}

{{site.data.keyword.Bluemix_notm}} は、オンプレミス・データをやりとりするアプリを提供するために、モバイル・アプリ、クラウド・サービス、およびエンタープライズ SoR を統合できるプラットフォームを提供します。

例えば、ファイアウォールの背後のオンプレミスに存在するカスタマー・リレーションシップ・マネジメント・システムと対話するモバイル・アプリを作成することができます。ユーザーは、機能豊富なモバイル・アプリを作成できるように、SoR をセキュアな方法で呼び出して、{{site.data.keyword.Bluemix_notm}} のモバイル・サービスを活用することができます。

まず、統合開発者が、モバイル・バックエンド・アプリを {{site.data.keyword.Bluemix_notm}} で作成します。自分が一番熟知している Node.js ランタイムを使用するモバイル・クラウド・ボイラープレートを使用します。

次に、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェース内で Cloud Integration サービスを使用し、セキュア・コネクターを介して API を公開します。統合開発者はセキュア・コネクターをダウンロードし、オンプレミスにインストールして、API とデータベースとの間のセキュアな通信を可能にします。データベース・エンドポイントの作成後、すべてのスキーマを調べて、API としてアプリに公開するテーブルを抽出することができます。

統合開発者は、関心のある利用者にモバイル通知を送信するために  プッシュ・サービスを追加します。また、Twitter API で新規顧客のレコードが作成された際にツイートするために、ビジネス・パートナー・サービスも追加します。

次に、アプリケーション開発者が {{site.data.keyword.Bluemix_notm}} にログインし、Android 開発ツールキットをダウンロードして、統合開発者が作成した API を呼び出すコードを作成します。ユーザーが自分のモバイル・デバイスに情報を入力できるようにするモバイル・アプリを開発できます。その後、そのモバイル・アプリは顧客管理システムで顧客のレコードを作成します。レコードの作成時に、アプリはモバイル・デバイスに対して通知をプッシュし、その新規レコードに関するツイートを開始します。

## {{site.data.keyword.Bluemix_notm}} の前提条件
{: #prereqs}

{{site.data.keyword.Bluemix_notm}} プラットフォームを使用するための前提条件は限られていますが、少しあります。
{:shortdesc}

### ブラウザー
{: #browsers}

以下のリストに、{{site.data.keyword.Bluemix_notm}} に最小限必要なブラウザー・ソフトウェアを指定します。

 * Chrome: ご使用のオペレーティング・システムの最新バージョン
 * Firefox: ご使用のオペレーティング・システムの最新バージョンおよび ESR 45
 * Internet Explorer: バージョン 11
 * Safari: Mac の最新バージョン

### Cloud Foundry
{: #cf}

バージョン 6.5.1 以降の Cloud Foundry コマンド・ライン・インターフェース 

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [{{site.data.keyword.Bluemix_notm}} とは? ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/bluemix/what-is-bluemix/){:new_window}
* [使用を開始するには ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/bluemix/getting-started/){:new_window}
* [{{site.data.keyword.Bluemix_notm}} の新機能](/docs/whatsnew/index.html)
* [ハイブリッド・モデルについて ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/bluemix/hybrid/){:new_window}
* [アカウントの管理](/docs/admin/adminpublic.html#mngacct)
* [{{site.data.keyword.Bluemix_notm}} 用語集](/docs/overview/glossary/index.html)
