---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# フィードの実装
{: #openwhisk_feeds}

{{site.data.keyword.openwhisk_short}} はオープンな API をサポートしています。この API では、どのユーザーでもイベント・プロデューサー・サービスを**パッケージ**内の**フィード**として公開できます。このセクションでは、ユーザー独自のフィードを提供する際に選択できる、アーキテクチャーや実装に関するいくつかのオプションについて説明します。

この資料は、独自のフィードを公開しようとしている上級 {{site.data.keyword.openwhisk_short}} ユーザーを対象としています。ほとんどの {{site.data.keyword.openwhisk_short}} ユーザーはこのセクションをスキップしても問題ありません。

## フィードのアーキテクチャー

フィードの作成には、少なくとも 3 つのアーキテクチャー・パターンがあります。**フック**、**ポーリング**、および**接続**です。

### フック
*フック*・パターンの場合、別のサービスが公開する [webhook](https://en.wikipedia.org/wiki/Webhook) ファシリティーを使用してフィードをセットアップします。この戦略では、URL に直接 POST してトリガーを発生させるように、webhook を外部サービスで構成します。これは、頻度が低いフィードを実装するのに適した、非常に簡単で最高に魅力的な選択肢です。

<!-- The github feed is implemented using webhooks.  Put a link here when we have the open repo ready -->

### ポーリング
ポーリング・パターンの場合、定期的にエンドポイントをポーリングして新しいデータをフェッチする {{site.data.keyword.openwhisk_short}} *アクション* を準備します。このパターンは、比較的簡単に構築できますが、当然ながらイベントの頻度はポーリング間隔によって制限されます。

### 接続
接続パターンの場合、分離されたサービスをどこかに置き、そのサービスでフィード・ソースへの持続的な接続を保持します。接続ベースの実装は、ロング・ポーリングを介して、または、プッシュ通知をセットアップするため、サービス・エンドポイントと対話する可能性があります。

<!-- Our cloudant changes feed is connection based.  Put a link here to
an open repo -->

<!-- What is the foundation for the Message Hub feed? If it is "connections" then lets put a link here as well -->

## フィードとトリガーの違い

フィードとトリガーは密接に関連していますが、技術的には別々の概念です。   

- {{site.data.keyword.openwhisk_short}} は、システムに流入してくる**イベント**を処理します。

- **トリガー**は、技術的にはイベントのクラスの名前です。各イベントは正確に 1 つのトリガーに属します。トリガーは、トピック・ベースの Pub-Sub システムにおける*トピック* に似ています。**ルール** *T -> A* は、「トリガー *T* からイベントが到着すると、必ずトリガー・ペイロードを使用してアクション *A* を起動する」ことを意味します。

- **フィード**は、イベントからなるストリームであり、それらのイベントのすべてがトリガー *T* に属します。フィードは**フィード・アクション**によって制御され、フィード・アクションが、フィードを形成しているイベントのストリームの作成、削除、休止、および再開を処理します。通常、フィード・アクションは、通知を管理する REST API を介して、イベントを生成する外部サービスと対話します。

##  フィード・アクションの実装

*フィード・アクション* は、通常の {{site.data.keyword.openwhisk_short}} *アクション* ですが、以下のパラメーターを受け入れる必要があります。
* **lifecycleEvent**:「CREATE」、「DELETE」、「PAUSE」、または「UNPAUSE」のいずれか
* **triggerName**: このフィードから生成されるイベントを含むトリガーの完全修飾名
* **authKey**: 上記トリガーの所有者である {{site.data.keyword.openwhisk_short}} ユーザーの基本認証資格情報

フィード・アクションは、フィードを管理するために必要な他のパラメーターも受け入れることができます。例えば、cloudant changes フィード・アクションは、*'dbname'*、*'username'* などのパラメーターを受け取ることを予期しています。

ユーザーが **--feed** パラメーターを指定して CLI からトリガーを作成すると、適切なパラメーターが設定されたフィード・アクションがシステムによって自動的に起動されます。

例として、バインドされたパラメーターとしてユーザー名とパスワードを使用して、ユーザーが `cloudant` パッケージ用に `mycloudant` バインディングを作成済みであるとします。ユーザーが CLI から次のコマンドを実行するとします。

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

この結果、システムは以下と同等のことを内密に実行します。

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

*changes* という名前のフィード・アクションは上に示したパラメーターを受け入れます。このアクションは、Cloudant からのイベントのストリームを (適切な構成と共に、トリガー *T* に向けて) セットアップするために必要なすべてのアクションを実行することを期待されています。    

Cloudant *changes* フィードのアクションは、期せずして、接続ベースのアーキテクチャーで実装した *cloudant trigger* サービスと直接対話するようになっています。その他のアーキテクチャーについては下で説明します。

同様のフィード・アクション・プロトコルが `wsk trigger delete` でも起こります。    

## フックを使用したフィードの実装

イベント・プロデューサーが webhook/コールバック機能をサポートしている場合、フックを介したフィードを簡単にセットアップできます。

この方法を使用する場合、OpenWhisk 外部の永続的サービスはまったく*必要ありません*。すべてのフィード管理は、サード・パーティー webhook API と直接交渉するステートレス {{site.data.keyword.openwhisk_short}} *フィード・アクション* を通して自然に起こります。

フィード・アクションは、`CREATE` によって起動されると、他のサービスのために単に webhook を 1 つインストールし、それによって、そのリモート・サービスに OpenWhisk 内の適切な `fireTrigger` URL に通知を POST するよう依頼します。

その webhook は、次の例のように、URL に通知を送信するよう指示される必要があります。

`POST /namespaces/{namespace}/triggers/{triggerName}`

POST 要求を含むこの形式は、トリガー・イベントのパラメーターを定義する JSON 文書として解釈されます。
{{site.data.keyword.openwhisk_short}} ルールは、これらのトリガー・パラメーターをアクションに渡して、イベントの結果として発生するようにします。

## ポーリングを使用したフィードの実装

持続的な接続も外部サービスも必要なく、フィード・ソースを完全に OpenWhisk 内部でポーリングするように、{{site.data.keyword.openwhisk_short}} *アクション* をセットアップすることが可能です。

webhook が使用可能でないが、大容量または待ち時間の少ない応答時間を必要としないフィードの場合、ポーリングは魅力的な選択肢です。

ポーリング・ベースのフィードをセットアップするために、フィード・アクションは `CREATE` のために呼び出されたときに以下のステップを実行します。

1.   フィード・アクションは、`whisk.system/alarms` フィードを使用して、適切な間隔で定期的トリガー (*T*) をセットアップします。
2.   フィード開発者は、リモート・サービスをポーリングして新規イベントがあれば返すという単純な `pollMyService` アクションを作成します。
3.  フィード・アクションは、*ルール* *T -> pollMyService* をセットアップします。

この手順は、分離したサービスをまったく必要とせずに全面的に {{site.data.keyword.openwhisk_short}} アクションを使用して、ポーリング・ベースのトリガーを実装します。

## 接続を介したフィードの実装

上記 2 つのアーキテクチャーは、単純で実装が簡単です。しかし、高性能なフィードが必要な場合は、持続的な接続とロング・ポーリング、あるいは類似した技法に代わるものはありません。

{{site.data.keyword.openwhisk_short}} アクションは短時間実行でなければならないため、アクションがサード・パーティーへの持続的な接続を保持することはできません。代わりに、
常に稼働する分離したサービス (OpenWhisk の外部) を用意する必要があります。これらは*プロバイダー・サービス* と呼ばれます。プロバイダー・サービスは、ロング・ポーリングまたは他の接続ベースの通知をサポートする、サード・パーティー・イベント・ソースへの接続を保持できます。

プロバイダー・サービスは、{{site.data.keyword.openwhisk_short}} *フィード・アクション* がフィードを制御するのを可能にする REST API を提供する必要があります。プロバイダー・サービスは、イベント・プロバイダーと {{site.data.keyword.openwhisk_short}} との間でプロキシーとして動作します。つまり、サード・パーティーからイベントを受け取ると、トリガーを発生させることでそれらのイベントを {{site.data.keyword.openwhisk_short}} に送信します。

Cloudant *changes* フィードは規範的な例です。これが立ち上げる `cloudanttrigger` サービスは、持続的な接続を介して Cloudant 通知と {{site.data.keyword.openwhisk_short}} トリガーの間を仲介します。
<!-- TODO: add a reference to the open source implementation -->

同様のパターンで *alarm* フィードが実装されます。

接続ベースのアーキテクチャーは、パフォーマンスが最も高い選択肢ですが、ポーリングおよびフックのアーキテクチャーに比べると、オペレーションにかかるオーバーヘッドは多くなります。   
