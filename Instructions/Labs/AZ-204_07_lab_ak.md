---
lab:
    title: 'ラボ: サービス間でリソース シークレットに安全にアクセスする'
    az204Module: 'モジュール 07: セキュアなクラウド ソリューションの実装'
    az020Module: 'モジュール 07: セキュアなクラウド ソリューションの実装'
    type: 'Answer Key'
---

# ラボ: サービス間でリソース シークレットにより安全にアクセスする
# 学生課題解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな特性を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイスの変更が発生する可能性があります。これらの変更により、ラボの指示と手順が一致しない場合があります。

Microsoft では、コミュニティから必要な変更要望を受けたときにトレーニング コースを更新します。ただし、クラウドの更新は頻繁に行われるため、トレーニング コンテンツの更新前に UI が変更される場合もあります。**その場合は、変更に適宜対応して、ラボで要求されている内容を処理してください**。

## 指示

### 開始する前に

#### ラボ仮想マシンへのログイン

次の認証情報を使用して Windows 10 仮想マシンにログインします。
    
-   ユーザー名: **管理者**

-   パスワード: **Pa55w.rd**

> **注**: 仮想ラボ環境に接続する手順は講師が説明します。

#### インストールされたアプリケーションのレビュー

Windows 10 デスクトップでタスク バーを探します。タスク バーには、この課題で使用するアプリケーションのアイコンが含まれています:
    
-   Microsoft Edge

-   File Explorer

### エクササイズ 1: Azure リソースの作成

#### タスク 1: Azure portal を開く

1.  タスク バーで、「**Microsoft Edge**」 アイコンを選択します。

1.  開いているブラウザー ウィンドウで、**Azure portal** (<https://portal.azure.com>) に移動します。

1.  Microsoft アカウントの電子メール アドレスを入力し、 **「次へ」** を選択します。

1.  Microsoft アカウントの**パスワード**を入力し、「**サインイン**」 を選択 します。

    > **注**: Azure portal に初めてサインインする場合は、ポータルのツアーが表示されます。ツアーをスキップしてポータルの使用を開始するには、「**開始**」 を選択します。

#### タスク 2: Azure ストレージ アカウントの作成

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**ストレージ アカウント**」 を選択します。

1.  「**ストレージ アカウント**」 ブレードで、ストレージ インスタンスの一覧を表示します。

1.  「**ストレージ アカウント**」 ブレードで、「**追加**」 を選択します。

1.  「**ストレージ アカウントの作成**」 ブレードで 「**基本**」 などのタブを探します。

    > **注**: 各タブは、新しいストレージ アカウントを作成するための、ワークフロー内のステップを表しています。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。

    1.  「**リソース グループ**」 セクションで 「**新規作成**」 を選択し、「**SecureFunction**」と入力したら 「**OK**」 を選択します。

    1.  「**ストレージ アカウント名**」 テキスト ボックスに、「**securestor*[yourname]***」 と入力します。

    1.  「**場所**」 ドロップダウン リストで、「**(米国) 米国東部**」 リージョンを選択します。

    1.  「**パフォーマンス**」 セクションで、「**Standard**」 を選択します。

    1.  「**Account kind**」 ドロップダウン リストで、「**StorageV2 (汎用 v2)**」 を選択します。

    1.  「**レプリケーション**」 ドロップダウン リストで、「**Locally-redundant ストレージ (LRS)**」 を選択します。

    1.  「**アクセス層**」 セクションで、「**ホット**」 が選択されていることを確認します。

    1.  「**レビューと作成**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用してストレージ アカウントを作成するには、「**作成**」 を選択します。 

    > **注**: このラボを進める前に、作成タスクが完了するまで待ちます。

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**ストレージ アカウント**」 を選択します。

1.  「**ストレージ アカウント**」 ブレードから、プレフィックス *securestor\** を持つストレージ アカウント インスタンスを選択します。

1.  「**ストレージ アカウント**」 ブレードで 「**設定**」 セクションを見つけ、「**アクセス キー**」 リンクを選択します。

1.  「**アクセス キー**」 ブレードでいずれかのキーを選択し、いずれかの 「**接続文字列**」 テキスト ボックスの値を記録します。この値は、この課題の後半で使用します。

    > **注**: どの接続文字列を選択しても問題ありません。これらは交換可能です。

#### タスク 3: Azure Key Vault を作成する

1.  Azure portal のナビゲーション ペインで、「**リソースを作成**」 リンクを選択します。

1.  「**新規**」 ブレードで、 おすすめサービスの一覧の上にある 「**Marketplace を検索**」 テキスト ボックスを見つけます。

1.  検索ボックスに「**Vault**」と入力し、Enter キーを押します。

1.  「**Marketplace**」 検索結果ブレードで、「**Key Vault**」 の結果を選択します。

1.  「**Key Vault**」 ブレードで、「**作成**」 を選択します。

1.  「**キー コンテナーの作成**」 ブレードから 「**基本**」 などのタブを見つけます。

    > **注**: 各タブは、新しいキー コンテナーを作成するためのワークフロー内のステップを表しています。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。
    
    1.  「**リソース グループ**」 セクションで、「**既存のものを使用**」 を選択し、一覧から 「**SecureFunction**」 を選択します。
    
    1.  「**Key Vault 名**」 テキストボックスに 「**securevault*[yourname]***」 と入力します。

    1.  「**リージョン**」 ドロップダウン リストで、「**米国東部**」 リージョンを選択します。
        
    1.  「**価格レベル**」 ドロップダウン リストで、「**Standard**」 を選択します。
    
    1.  「**論理削除**」 セクションで、「**無効**」 を選択します。

    1.  「**Review + create**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用してキー コンテナーを作成するには、「**作成**」 を選択します。

    > **注**: このラボを進める前に、作成タスクが完了するまで待ちます。

#### タスク 4: Azure Functions アプリの作成

1.  Azure portal のナビゲーション ペインで、「**リソースを作成**」 リンクを選択します。

1.  「**新規**」 ブレードで、 おすすめサービスの一覧の上にある 「**Marketplace を検索**」 テキスト ボックスを見つけます。

1.  検索テキスト ボックスに「**関数**」と入力し、Enter を押します。

1.  「**Marketplace**」 検索結果ブレードで、「**Function App**」 の結果を選択します。

1.  「**Function App**」 ブレードで、「**作成**」 を選択します。

1.  「**Function App**」 ブレードから、「**基本**」 などのタブを見つけます。

    > **注**: 各タブは、新しい関数アプリを作成するワークフローのステップを表しています。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。
    
    1.  「**リソース グループ**」 セクションで、「**既存のものを使用**」 を選択し、一覧から 「**SecureFunction**」 を選択します。
    
    1.  「**関数アプリ名**」 テキスト ボックスに 「**securefunc*[yourname]***」 と入力します。

    1.  「**発行**」 セクションで、「**コード**」 を選択します。

    1.  「**ランタイム スタック**」 ドロップダウン リストで、「**.NET Core**」 を選択します。

    1.  「**バージョン**」 ドロップダウン リストで、「**3.1**」 を選択します。

    1.  「**リージョン**」 ドロップダウン リストで、「**米国東部**」 リージョンを選択します。
    
    1.  「**次へ: ホスティング」** を選択します。

1.  「**ホスティング**」 タブで、次の操作を実行します:

    1.  「**ストレージ アカウント**」 ドロップダウン リストで、このラボで前に作成した **securestor*[yourname]*** ストレージ アカウントを選択します。

    1.  「**オペレーティング システム**」 セクションで、「**Windows**」 を選択します。

    1.  「**プランの種類**」 ドロップダウン リストで、「**従量課金プラン (サーバーレス)**」 オプションを選択します。

    1.  「**Review + create**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用して関数アプリを作成するには、「**作成**」 を選択します。 

    > **注**: このラボを進める前に、作成タスクが完了するまで待ちます。

#### レビュー

このラボでは、このラボで使用するすべてのリソースを作成しました。

### 演習 2: シークレットと ID の構成

#### タスク 1: システムに割り当てられたマネージド サービス ID の構成

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した **securefunc*[yourname]*** 関数アプリを選択します。

1.  「**App Service**」 ブレードで、「**設定**」 セクションから 「**ID**」 オプションを選択します。     

1.  「**ID**」 ペインから、「**システム割り当て**」 タブを見つけて、次のアクションを実行します。
    
    1.  「**状態**」 セクションで 「**オン**」 を選択し、「**保存**」 を選択します。
    
    1.  確認ダイアログ ボックスで 「**はい**」 を選択します。

    > **注**: このラボを進める前に、システムに割り当てられたマネージド ID が作成されるまで待ちます。

#### タスク 2: Key Vault シークレットの作成

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した **securevault*[yourname]*** キー コンテナーを選択します。

1.  「**キー コンテナー**」 ブレードの 「**設定**」 セクションにある 「**シークレット**」 リンクを選択します。

1.  **シークレット**ペインで、**生成/インポート**を選択します。

1.  「**シークレットの作成**」 ブレードで、次の操作を実行します。
    
    1.  「**アップロード オプション**」 ドロップダウン リストで、「**手動**」 を選択します。
    
    1.  「**名前**」 テキスト ボックスに、「**storagecredentials**」と入力します。
    
    1.  「**値**」 テキスト ボックスに、この演習で前に記録したストレージ アカウント接続文字列を入力します。
    
    1.  「**コンテンツの種類**」 テキスト ボックスは既定値のままにします。
    
    1.  「**アクティブ化する日を設定する**」 テキスト ボックスは既定値のままにします。
    
    1.  「**有効期限を設定する**」 テキスト ボックスは既定値のままにします。
    
    1.  「**有効**」 セクションで 「**はい**」 を選択し、「**作成**」 を選択します。
    
    > **注**: このラボを進める前に、シークレットが作成されるのを待ちます。

1.  シークレット ウィンドウに戻り、リスト内の 「**storagecredentials**」 項目を選択します。

1.  バージョン ウインドウで、**storagecredentials** シークレットの最新バージョンを選択します。

1.  シークレット バージョン ウインドウで、次の操作を実行します。
    
    1.  シークレットの最新バージョンのメタデータを確認します。
    
    1.  シークレットの値を表示するには、「**シークレット値の表示**」 を選択します。
    
    1.  後の演習で使用するため、「**シークレット識別子**」 テキスト ボックスの値を記録します。

    > **注**: 「**シークレット値**」 テキスト ボックスではなく、「**シークレット識別子**」 テキスト ボックスの値を記録しています。

#### タスク 3: キー コンテナー アクセス ポリシーの構成

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した  **securevault*[yourname]*** キー コンテナーを選択します。

1.  「**キー コンテナー**」 ブレードで、「**設定**」 セクションにある 「**アクセス ポリシー**」 リンクを選択します。

1.  アクセス ポリシー ウィンドウで、「**アクセス ポリシーの追加**」 を選択します。

1.  「**アクセス ポリシーの追加**」 ブレードで、次の操作を実行します。
    
    1.  「**プリンシパルの選択**」 リンクを選択します。
    
    1.  「**プリンシパル**」 ブレードから、**securefunc*[yourname]*** という名前のサービス プリンシパルを見つけてから選択し、次に 「**選択**」 を選択します。

        > **注意**: この演習で先ほど作成したシステム割り当てマネージド ID は、Azure 関数リソースと同じ名前になります。
    
    1.  「**キーのアクセス許可**」 リストは既定値に設定したままにします。
    
    1.  「**シークレットのアクセス許可**」 ドロップダウン リストで、「**GET**」 アクセス許可を選択します。
    
    1.  「**証明書のアクセス許可**」 リストは、既定値に設定したままにします。
    
    1.  「**承認されているアプリケーション**」 テキスト ボックスは、既定値のままにしておきます。
    
    1.  「**追加**」 を選択します。

1.  アクセス ポリシー ウィンドウに戻って、「**保存**」 を選択します。 

    > **注**: この演習を進める前に、アクセス ポリシーに対する変更が保存されるのを待ちます。

#### レビュー

この演習では、関数アプリにサーバー割り当てが行われたマネージド サービス ID を作成し、キー コンテナーでシークレットの値を取得するための適切なアクセス許可をその ID に付与しました。最後に、関数アプリ内で使用するシークレットを作成しました。

### エクササイズ3：関数アプリ コードの記述 

#### タスク 1: キー コンテナー派生アプリケーション設定を作成する 

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した  **securefunc*[yourname]*** 関数アプリを選択します。

1.  「**App Service**」 ブレードで、「**設定**」 セクションから 「**構成**」 オプションを選択します。

1.  「**構成**」 ペインから、次のアクションを実行します。
    
    1.  「**アプリケーションの設定**」 タブを選択し、「**新しいアプリケーション設定**」 を選択します。
    
    1.  「**アプリケーションの追加/編集**」 ポップアップ ウィンドウで、「**名前**」 テキスト ボックスに「**StorageConnectionString**」と入力します。
    
    1.  「**値**」 テキスト ボックスで、次の構文を使用して値を作成します。**@Microsoft.KeyVault(SecretUri=*Secret Identifier*)**

        > **注意**: 上記の構文を使用して、自分の**シークレット識別子**への参照を構築する必要があります。たとえば、シークレット識別子が **https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf** の場合、値は **@Microsoft.KeyVault(SecretUri=https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)** になります。
    
    1.  「**配置スロット設定**」 テキスト ボックスは、既定値のままにしておきます。

    1.  「**OK**」 を選択してポップアップ ウィンドウを閉じ、「**構成**」 セクションに戻ります。
    
    1.  ブレードで 「**保存**」 を選択して、設定を保持します。  

    1.  「**変更の保存**」 確認ポップアップ ダイアログで、「**続行**」 を選択します。

    > **注**: ラボを進める前に、アプリケーションの設定が保持されるまで待ちます。

#### タスク 2: HTTP によってトリガーされる関数を作成する

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した **securefunc*[yourname]*** 関数アプリを選択します。

1.  「**App Service**」 ブレードで、「**関数**」 セクションから 「**関数**」 オプションを選択ます。

1.  「**関数**」 ペインで、「**追加**」 ボタンを選択します。

1.  「**新しい関数**」 ポップアップ ダイアログで、次のアクションを実行します。
    
    1.  「**テンプレート**」 タブで、「**HTTP トリガー**」 を選択します。   

    1.  「**詳細**」 タブで、「**新しい関数**」 テキスト ボックスを見つけてから、「**FileParser**」と入力します。

    1.  「**詳細**」 タブで、「**承認**」 テキスト ボックスを見つけてから、「**匿名**」 を選択します。     

    1.  「**関数の作成**」 を選択します。

1.  「**関数**」 ブレードで、「**開発者**」 セクションから 「**コード + テスト**」 オプションを選択します。     

1.  関数エディターで、関数スクリプトの例を確認します。

    ```
    #r "Newtonsoft.Json"

    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Primitives;
    using Newtonsoft.Json;

    public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");

        string name = req.Query["name"];

        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
        name = name ?? data?.name;

        string responseMessage = string.IsNullOrEmpty(name)
            ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";

                return new OkObjectResult(responseMessage);
    }
    ```

1.  すべてのサンプル コードを**削除**し、関数エディターで、次のプレースホルダー関数をコピーして貼り付けます。

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        return new OkObjectResult("Test Successful");
    }
    ```

1.  「**保存**」 を選択して、関数コードに対する変更を保持します。 

1.  「**テスト/実行**」 を選択します。

1.  表示されるポップアップ ダイアログで、次の操作を実行します。

    1.  「**入力**」 タブで、「**実行**」 を選択します。

    1.  「**出力**」 タブで、「テスト成功」の出力メッセージを確認します。 

#### タスク 3: Key Vault 派生アプリケーション設定をテストする

1.  スクリプトの **Run** メソッド内の既存のコードを削除します。

1.  **Run** メソッドを確認すると、以下が含まれています。

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

1.  次のコード行を追加して、**Environment.GetEnvironmentVariable** メソッドを使用して、**StorageConnectionString** アプリケーション設定の値を取得します。

    ```
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  次のコード行を追加して、**OkObjectResult** クラス コンストラクターを使用して、 *connectionString* 変数の値を返します。
   
    ```
    return new OkObjectResult(connectionString);
    ```
    
1.  **Run** メソッドを確認すると、以下が含まれています。

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        return new OkObjectResult(connectionString);
    }
    ```

1.  「**保存**」 を選択して、関数コードに対する変更を保持します。 

1.  「**テスト/実行**」 を選択します。

1.  表示されるポップアップ ダイアログで、次の操作を実行します。

    1.  「**入力**」 タブで、「**実行**」 を選択します。

    1.  「**出力**」 タブで、関数から返される出力接続文字列を確認します。

#### レビュー

この演習では、サービス ID を使用して、Key Vault に格納されているシークレットの値を読み取り、関数アプリの結果としてその値を返しました。

### 演習 4: ストレージ アカウントの BLOB にアクセス

#### タスク 1: サンプルストレージ BLOB のアップロード

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、 この課題で前に作成した **securestor*[yourname]*** ストレージ アカウントを選択します。

1.  「**ストレージ アカウント**」 ブレードで、「**BLOB サービス**」 セクションの 「**コンテナー**」 リンクを選択します。

1.  「**Containers**」 セクションで、「**コンテナー**」 を選択します。

1.  「**新規コンテナー**」 ポップアップ ウィンドウで、次の操作を実行します。
    
    1.  「**名前**」 テキスト ボックスに、「**drop**」と入力します。
    
    1.  「**パブリック アクセス レベル**」 ドロップダウン リストで、「**BLOB (BLOBのみの匿名読み取りアクセス)**」 を選択して 「**OK**」 を選択します。

1.  「**コンテナー**」 セクションに戻り、新しく作成した 「**drop**」 コンテナーを選択します。

1.  「**コンテナー**」 ブレードで、「**アップロード**」 を選択します。

1.  「**BLOB のアップロード**」 ポップアップ ウィンドウで、次の操作を実行します。
    
    1.  「**ファイル**」 セクションで、「**フォルダー**」 アイコンを選択します。
    
    1.  「**エクスプローラー**」 ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\07\\Starter** に移動し、**records.json** ファイルを選択して、「**開く**」 を選択します。
    
    1.  「**ファイルが既に存在する場合は上書き**」 が選択されていることを確認し、「**アップロード**」 を選択します。  

    > **注**: この演習を続行する前に、BLOB がアップロードされるのを待ちます。

1.  「**コンテナー**」 ブレードから戻り、BLOB の一覧から 「**records.json**」 BLOB を選択します。

1.  「**BLOB**」 ブレードから、BLOB メタデータを見つけて、BLOB の URL をコピーします。

1.  タスク バーで、「**Microsoft Edge**」 アイコンを右クリックするか、ショートカットメニューを有効化したら、「**新しいウインドウ**」 を選択します。

1.  新しいブラウザー ウインドウで、BLOB 用にコピーした URL に移動します。

1.  これで、BLOB の JavaScript Object Notation (JSON) コンテンツが表示ているはずです。JSON の内容が表示されたブラウザー ウィンドウを閉じます。

1.  Azure portal が表示されたブラウザー ウィンドウに戻り、「**Blob**」 ブレードを閉じます。

1.  「**コンテナー**」 ブレードから戻り、「**アクセス レベル ポリシーの変更**」 を選択します。

1.  「**アクセス レベルの変更**」 ポップアップ ウィンドウで、次のアクションを実行します。
    
    1.  「**パブリック アクセス レベル**」 ドロップダウン リストで、「**プライベート (匿名アクセスなし)**」 を選択します。
    
    1.  「**OK**」 を選択します。

1.  タスク バーで、「**Microsoft Edge**」 アイコンを右クリックするか、ショートカットメニューを有効化したら、「**新しいウインドウ**」 を選択します。

1.  新しいブラウザー ウインドウで、BLOB 用にコピーした URL に移動します。

1.  リソースが見つからないことを示すエラー メッセージが表示されます。

    > **注**: エラー メッセージが表示されない場合は、ブラウザーがファイルをキャッシュしている可能性があります。エラー メッセージが表示されるまで、Ctrl+F5 を押してページを更新します。

#### タスク 2: .NET アプリケーション設定を追加する

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した **securefunc*[yourname]*** 関数アプリを選択します。

1.  「**App Service**」 ブレードで、「**設定**」 セクションから 「**構成**」 オプションを選択します。

1.  「**構成**」 ペインから、次のアクションを実行します。
    
    1.  「**アプリケーションの設定**」 タブを選択し、「**新しいアプリケーション設定**」 を選択します。
    
    1.  「**アプリケーション設定の追加/編集**」 ポップアップ ウィンドウの 「**名前**」 テキストボックスに、「**DOTNET_ADD_GLOBAL_TOOLS_TO_PATH**」 と入力します。
    
    1.  「**値**」 テキスト ボックスに、「**false**」と入力します。
    
    1.  「**配置スロット設定**」 テキスト ボックスは、既定値のままにしておきます。

    1.  「**OK**」 を選択してポップアップ ウィンドウを閉じ、「**構成**」 セクションに戻ります。
    
    1.  ブレードで 「**保存**」 を選択して、設定を保持します。  

    1.  「**変更の保存**」 確認ポップアップ ダイアログで、「**続行**」 を選択します。

    > **注**: ラボを進める前に、アプリケーションの設定が保持されるまで待ちます。

#### タスク 3: NuGet からストレージ アカウント SDK を取得する

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した **securefunc*[yourname]*** 関数アプリを選択します。

1.  「**App Service**」 ブレードで、「**開発ツール**」 セクションから 「**App Service Editor (プレビュー)**」 オプションを選択します。

1.  「**App Service Editor (プレビュー)**」 ペインから、「**移動 ->**」 を選択します。

1.  「**「App Service Editor**」 ブラウザーの画面で、**FileParser** フォルダーを展開し、コンテキスト メニューを開いてから、「**新しいファイル**」 を選択します。

1.  ダイアログ ボックスで 、「**function.proj**」と入力して Enter キーを押すと、空のコード エディターが表示されます。

1.  エディターで、次の構成コンテンツを挿入します。

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netstandard2.0</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
            <PackageReference Include="Azure.Storage.Blobs" Version="12.4.0" />
        </ItemGroup>
    </Project>
    ```

    > **注**: App Service Editor は、ファイルへの変更を自動的に保存します。この .proj ファイルには、[Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.4.0) パッケージのインポートに必要な NuGet パッケージの参照が含まれています。

1.  **App Service Editor** のあるブラウザーの画面を閉じます。

#### タスク 4: 名前空間参照の更新

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 このラボで前に作成した 「**SecureFunction**」 リソース グループを見つけて選択します。

1.  「**SecureFunction**」 ブレードから、このラボで前に作成した **securefunc*[yourname]*** 関数アプリを選択します。

1.  「**App Service**」 ブレードで、「**関数**」 セクションから 「**関数**」 オプションを選択ます。

1.  「**関数**」 ペインで、既存の **FileParser** 関数を選択し、この関数のエディタを開きます。

1.  「**関数**」 ブレードで、「**開発者**」 セクションから 「**コード + テスト**」 オプションを選択します。     

1.  エディター内で、スクリプトの **Run** メソッド内の既存コードを削除します。

1.  コード ファイルに、次のコード行を追加して、**Azure.Storage** 名前空間の **using** ディレクティブを作成します。

    ```
    using Azure.Storage;
    ```

1.  コード ファイルで、次のコード行を追加して、**Azure.Storage.Blobs** 名前空間の **using** ディレクティブを作成します。

    ```
    using Azure.Storage.Blobs;
    ```

1.  **Azure.Storage.Blobs.Models** 名前空間の**using** ディレクティブを作成するには、次のコード行を追加します。

    ```
    using Azure.Storage.Blobs.Models;
    ```

1.  **Run** メソッドを確認すると、以下が含まれています。

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

#### タスク 5: ストレージ アカウント コードを記述する

1.  **Environment.GetEnvironmentVariable** メソッドを使用して **StorageConnectionString** アプリケーション設定の値を取得するには、**Run** メソッド内に次のコード行を追加します。

    ```
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  *connectionString* 変数をコンストラクターに渡すことによって、**BlobServiceClient** クラスの新しいインスタンスを作成するには、次のコード行を追加します。

    ```
    BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
    ```

1.  **BlobServiceClient.GetBlobContainerClient** メソッドを使用するために次のコード行を追加し、**ドロップ**コンテナー名を渡して、この実習ラボで前に作成したコンテナーを参照する **BlobContainerClient** クラスの新しいインスタンスを作成します。

    ```
    BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
    ```

1.  **BlobContainerClient.GetBlobClient** メソッドを使用する次のコード行を追加し、**records.json** BLOB名を渡して、この実習ラボで前にアップロードした BLOB を参照する **BlobClient** クラスの新しいインスタンスを作成します。

    ```
    BlobClient blobClient = containerClient.GetBlobClient("records.json");
    ```
    
1.  **Run** メソッドを確認すると、以下が含まれています。

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
    }
    ```

#### タスク 6: BLOB のダウンロード

1.  **BlobClient.DownloadAsync** メソッドを使用して、 参照される BLOB のコンテンツを非同期にダウンロードし、その結果を *response* という変数に格納するには、次のコード行を追加します。

    ```
    var response = await blobClient.DownloadAsync();
    ```

1.  次のコード行を追加して、**FileStreamResult** クラス コンストラクターを使用することで、 *content* 変数に格納されたさまざまなコンテンツを返します。

    ```
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

1.  **Run** メソッドを確認すると、以下が含まれています。

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
        var response = await blobClient.DownloadAsync();
        return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    }
    ```

1.  「**保存**」 を選択して、関数コードに対する変更を保持します。 

1.  「**テスト/実行**」 を選択します。

1.  表示されるポップアップ ダイアログで、次の操作を実行します。

    1.  「**入力**」 タブで、「**実行**」 を選択します。

    1.  「**出力**」 タブで、ストレージ アカウントに格納されている **$/drop/records.json** BLOB の出力内容を確認します。

#### レビュー

この演習では、C\# コードを使用してストレージ アカウントにアクセスし、BLOB の内容をダウンロードしました。

### エクササイズ 5: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開き、リソース グループを一覧表示する

1.  Azure portal のナビゲーション ウィンドウで、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、大なり記号 () とアンダースコア文字 (\_) で表されます。

1.  サブスクリプションを使用して Cloud Shell を初めて開く場合は、**Azure Cloud Shell へようこそウィザード**を使って、初めて使用する Cloud Shell を構成できます。ウィザードで次の操作を実行します。
    
    1.  シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるダイアログ ボックスが表示されます。既定の設定を受け入れ、「**ストレージの作成**」 を選択します。 

    > **注**: Cloud Shell が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。Cloud Shell の構成オプションが表示されない場合は、このコースのラボで既存のサブスクリプションを使用している可能性が高いと考えられます。ラボは、新しいサブスクリプションを使用しているという前提で記述されます。

#### タスク 2: リソース グループの削除

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して **SecureFunction** リソース グループを削除します。

    ```
    az group delete --name SecureFunction --no-wait --yes
    ```
    
1.  ポータルの Cloud Shell ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.     現在実行中の Microsoft Edge アプリケーションを閉じます。

#### レビュー

この実習では、この課題で使用するリソース グループを削除することで、サブスクリプションをクリーンアップしました。
