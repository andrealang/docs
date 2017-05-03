---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# ランタイムに関するトラブルシューティング
{: #runtimes}

{{site.data.keyword.Bluemix}} ランタイムを使用する際に問題が発生する場合があります。多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}


## アプリがプッシュされたときに使用できないビルドパックが使用される
{: #ts_loading_bp}

アプリをプッシュしたときに、最新のビルドパック・コンポーネントを使用できない場合があります。使用できないコンポーネントがロードされないように組み込みメカニズムを備えたビルドパックを使用するか、アプリのプッシュや再ステージを行う前にアプリのキャッシュ・ディレクトリー内のコンテンツを削除します。 

ビルドパックが更新されてからアプリをプッシュまたは再ステージすると、最新のビルドパック・コンポーネントのロードが自動的に行われません。その結果、アプリは使用できないビルドパック・コンポーネントをキャッシュから使用することになります。アプリを最後にプッシュしてからビルドパックに適用された更新は実装されていません。
{: tsSymptoms}

ビルドパックによっては、すべての更新コンポーネントをインターネットから自動的にダウンロードして、いつでも最新バージョンを使用できるように構成されていないものもあります。
{: tsCauses} 

組み込みメカニズムを備えたビルドパックを使用して、使用できないコンポーネントをロードしないようにすることができます。例えば、以下のビルドパックを使用できます。
{: tsResolve}

  * [Cloud Foundry Java ビルドパック![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/java-buildpack){: new_window}。このビルドパックには、最新バージョンのビルドパックが使用されるように組み込みメカニズムが装備されています。このメカニズムによる処理方法について詳しくは、[extending-caches.md ![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}を参照してください。 
  * [Cloud Foundry Node.js ビルドパック![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}。このビルドパックは、環境変数を使用して同様の機能を提供します。この Node.js ビルドパックを有効にして、毎回インターネットからノード・モジュールをダウンロードするには、cf コマンド・ライン・インターフェースに次のコマンドを入力します。 	
  ```
  set NODE_MODULES_CACHE=false
  ```

使用中のビルドパックが最新のコンポーネントを自動的にロードするメカニズムを提供していない場合は、手動でキャッシュ・ディレクトリー内のコンテンツを削除し、アプリを再度プッシュします。次の手順を使用します。

 1. ヌル・ビルドパックのブランチ (例えば https://github.com/ryandotsmith/null-buildpack) をチェックアウトします。ブランチをチェックアウトする方法については、[Git Basics - Getting a Git Repository![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window} を参照してください。  
 2. `null-buildpack/bin/compile` ファイルに以下の行を追加して変更をコミットします。変更をコミットする方法については、[Git Basics - Recording Changes to the Repository ![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window} を参照してください。
  ```
rm -rfv $2/*
  ```
 3. 以下のコマンドを使用して、キャッシュを削除するように変更されたヌル・ビルドパックでアプリをプッシュします。このステップを完了すると、アプリのキャッシュ・ディレクトリー内にあるすべてのコンテンツが削除されます。
  ```
cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. 以下のコマンドを使用して、希望する最新のビルドパックでアプリをプッシュします。 
  ```
cf push appname -p app_path -b <latest_buildpack>
  ```
 
## PHP ビルドパックからの NOTICE メッセージ
{: #ts_phplog}

ログからの NOTICE を含むメッセージが表示されることがあります。このようなメッセージのロギングは、ロギング・レベルを変更すれば止めることができます。	

PHP ビルドパックを使用してアプリを {{site.data.keyword.Bluemix_notm}} にプッシュすると、以下のような `NOTICE` を含むメッセージが表示されることがあります。
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
PHP ビルドパックでは、error_log パラメーターはロギング・レベルを定義します。デフォルトでは、`error_log` パラメーターの値は **stderr notice** です。次の例は、Cloud Foundry が提供する PHP ビルドパックの `nginx-defaults.conf` ファイルに含まれる、デフォルトのロギング・レベル構成を示しています。詳しくは、[cloudfoundry/php-buildpack ![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window} を参照してください。
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
`NOTICE` メッセージは通知用であり、問題を示していない場合があります。これらのメッセージのロギングは、ビルドパックの nginx-defaults.conf ファイルに含まれるロギング・レベルを `stderr notice` から `stderr error` に変更することで停止できます。例:
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
デフォルトのロギング構成を変更する方法について詳しくは、『[error_log ![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}』を参照してください。
	

## サード・パーティーの Python ライブラリーを {{site.data.keyword.Bluemix_notm}} にインポートできない
{: #ts_importpylib}

サード・パーティーの Python ライブラリーを {{site.data.keyword.Bluemix_notm}} にインポートできない場合があります。問題を解決するには、構成ファイルを python アプリのルート・ディレクトリーに追加します。

サード・パーティーの Python ライブラリー、例えば `web.py` ライブラリーをインポートしようとすると、`cf push` コマンドが失敗します。
{: tsSymptoms}

Python アプリの構成情報が欠落しています。
{: tsCauses}

`requirements.txt` ファイルと `Procfile` ファイルを Python アプリのルート・ディレクトリーに追加します。以下の情報は、`web.py` ライブラリーをインポートしていると仮定しています。{: tsResolve}

 1. `requirements.txt` ファイルを Python アプリのルート・ディレクトリーに追加します。
 
 `requirements.txt` ファイルには、Python アプリに必要なライブラリー・パッケージとそのパッケージのバージョンが指定されています。以下の例には、`requirements.txt` ファイルの内容が示されています。ここで、`web.py==0.37` は、ダウンロードされる `web.py` ライブラリーのバージョンが 0.37 であることを示しています。`wsgiref==0.1.2` は、web.py ライブラリーに必要な Web サーバー・ゲートウェイ・インターフェースのバージョンが 0.1.2 であることを示しています。

	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 `requirements.txt` ファイルの構成方法について詳しくは、 「[Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)」を参照してください。

 2. `Procfile` ファイルを Python アプリのルート・ディレクトリーに追加します。`Procfile` ファイルには、Python アプリの開始コマンドを含めてください。以下のコマンドでは、*yourappname* が Python アプリの名前で、*PORT* は、アプリのユーザーから要求を受信するために Python アプリが使用しなければならないポート番号です。*$PORT* はオプションです。開始コマンドに PORT を指定しない場合は、アプリ内部にある `VCAP_APP_PORT` 環境変数下のポート番号が使用されます。 
	```
	web: python <yourappname>.py $PORT
	```

これでサード・パーティーの Python ライブラリーを {{site.data.keyword.Bluemix_notm}} にインポートできます。	


## 「インスタンスの詳細」ページの「アクション」ボタンが使用不可になっている
{: #ts_actionsbutton}

「インスタンスの詳細」ページの「アクション」ボタンが使用不可になっています。
{: tsSymptoms} 

この問題は、以下の理由で発生します。
{: tsCauses}

 * アプリが Java&trade; Web アプリではない。ランタイム管理ユーティリティー (RMU) がサポートするのは、Liberty ビルドパックでデプロイされた Web アプリのみです。
 * アプリが組み込みの Liberty ビルドパックでデプロイされていない。
 * アプリが古いバージョンの Liberty ビルドパックでデプロイされている。

問題の原因が古いバージョンの Liberty ビルドパックである場合は、{{site.data.keyword.Bluemix_notm}} でアプリを再デプロイしてください。それ以外の場合は、以下のクライアント・アプリケーションのログ・ファイルをサポート・チームにご提供ください。
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## トレース・ウィンドウまたはダンプ・ウィンドウを開くために資格情報が必要である
{: #ts_username}

トレース・ウィンドウまたはダンプ・ウィンドウを開くために、ユーザー名とパスワードが必要です。
{: tsSymptoms}

この問題は、ログイン・セッションのタイムアウトが原因で発生します。
{: tsCauses}

ユーザー名とパスワードを再入力してください。
{: tsResolve}


## トレース操作またはダンプ操作の実行中にエラーが発生する
{: #ts_target}

トレース操作またはダンプ操作の実行中にエラー・メッセージが表示されます。そのメッセージは、アプリのターゲット・インスタンスが実行状態にないことを示しています。
{: tsSymptoms}

```
インスタンス 0: トレース仕様が正常に設定されました (Instance 0: Trace specification is set successfully)
インスタンス 2: トレース仕様が正常に設定されました (Instance 2: Trace specification is set successfully)
インスタンス 1: アプリ abcd のターゲット・インスタンス 1 は実行状態にありません (Instance 1: Target instance 1 for app abcd is not in the running state.)。
インスタンス 3: トレース仕様が正常に設定されました (Instance 3: Trace specification is set successfully)
インスタンス 4: トレース仕様が正常に設定されました (Instance 4: Trace specification is set successfully)
```

この問題は、以下の理由で発生します。
{: tsCauses} 

  * トレースまたはダンプ管理の機能は、実行中のアプリ・インスタンスのみを対象としている。停止中、開始中、または異常終了状態のアプリ・インスタンスには、トレースまたはダンプ操作は使用できません。
  * トレースまたはダンプ・ダイアログが開く時点でアプリ・インスタンスの状況が移行中である。 

ウィンドウを閉じてから、再度開いてください。
{: tsResolve} 


## インスタンスに異なる traceSpecification 構成がある
{: #ts_different_config}

1 つのアプリに異なるインスタンスがある場合は、異なる traceSpecification 構成が表示されることがあります。
{: tsSymptoms}

この動作は、以下の理由で発生します。
{: tsCauses}

  * 1 つ以上のインスタンスの構成を以前に変更した。あるインスタンスの traceSpecification 構成を変更した場合、その変更は同じアプリの他のインスタンスには適用されません。例えば、アプリで log4j を使用していて、このアプリのインスタンスが 2 つあるものとします。インスタンス 0 のログ・レベルは info から debug に変更できますが、インスタンス 1 のログ・レベルは info のままになります。
  
  * アプリが拡大し、新規インスタンスが追加された。RMU は、既存のインスタンスの traceSpecification 構成を新規の拡大されたインスタンスに適用しません。新規インスタンスは、デフォルト構成を使用します。例えば、アプリで log4j を使用していて、それに 1 つのインスタンスがあるものとします。このインスタンスのログ・レベルを info から debug に変更できます。この変更を行った後に、アプリを 2 つのインスタンスに拡大した場合、新規インスタンスのログ・レベルは、debug ではなく info になります。

アクションは不要です。
この動作は予期されたものです。
{: tsResolve} 


## ディスク割り当て量の超過
{: #ts_diskquota}

アプリ・ログでディスク割り当て量の超過に気付くことがあります。

`「ディスク割り当て量の超過 (Disk quota exceeded)」`エラー・メッセージがアプリのログに示されます。
{: tsSymptoms}

この問題は、以下のいずれかの理由で発生します。
{: tsCauses} 

  * ダンプ・ファイルは実行中のアプリ・インスタンスと共に生成され、割り振られたディスク割り当て量を使い尽くします。デフォルトでは、1 つのアプリ・インスタンスあたりのディスク割り当て量は 1 GB です。
ディスク使用量を確認するには、**「ダッシュボード」>「アプリケーション」>「アプリ・ランタイム」**とクリックします。以下の例では、アプリの 2 つのインスタンスについての、ディスク使用量を含むランタイム情報を示しています。
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * ディスク割り当て量は、現在の組織の割り当て量によって制限されます。

以下のいずれかの方法を使用します。
{: tsResolve} 

  * ダンプ・ファイルをダウンロード後に削除します。
  * デプロイメント・マニフェストに以下の入力内容を含めて、ディスク割り当て量をもっと大きくしてアプリを再デプロイします。
    ```
	ディスク割り当て量: 2048
```
	
