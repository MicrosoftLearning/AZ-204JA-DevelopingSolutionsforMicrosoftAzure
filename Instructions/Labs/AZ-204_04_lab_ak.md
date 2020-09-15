---
lab:
    title: 'ラボ: ポリグロット データ ソリューションの構築'
    az204Module: 'モジュール 04: Cosmos DB ストレージを使用するソリューションの開発'
    az020Module: 'モジュール 04: Cosmos DB ストレージを使用するソリューションの開発'
    type: 'Answer Key'
---

# ラボ: ポリグロット データ ソリューションの構築
# 受講者ラボ解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな性質を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイス (UI) の変更が発生する可能性があります。これらの変更により、ラボの指示と手順が正しく一致しない場合があります。

Microsoft は、コミュニティが必要な変更を行うと、このトレーニング コースを更新します。だたし、クラウドは頻繁に更新されるため、このトレーニングの内容が更新される前に UI が変更されるかもしれません。**その場合は、変更に適宜対応して、ラボで要求されている内容を処理してください。**

## 指示

### 開始する前に

#### ラボの仮想マシンへのログイン

次の認証情報を使用して、Windows 10 仮想マシン (VM) にログインします。
    
-   ユーザー名: **Admin**

-   パスワード: **Pa55w.rd**

> **Note**：仮想ラボ環境に接続する手順は講師が説明します。

#### インストールされたアプリケーションのレビュー

Windows 10 デスクトップでタスク バーを探します。タスク バーには、この課題で使用するアプリケーションのアイコンが含まれています:
    
-   Microsoft Edge

-   File Explorer

-   Visual Studio Code

### 演習 1: Azure 内にデータベース リソースを作成

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウインドウで、Azure potal ([portal.azure.com](https://portal.azure.com)) に移動します。

1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: Azure portal に初めてサインインする場合は、ポータルのツアーが表示されます。ツアーをスキップしてポータルの使用を開始するには、**>Get Started** を選択します。

#### Task 2: Azure SQL Database サーバー リソースを作成する

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  **すべてのサービス**ブレードで、**SQLサーバー** を選択します。

1.  **SQLサーバー**ブレードで、SQL サーバー インスタンスの一覧を探します。

1.  **SQL サーバー** ブレードで、**Add** を選択します。

1.  **SQL Database Server の作成** ブレードで、**基本**、**ネットワーク** および **追加設定** などブレードの上部にあるタブを確認します。

    > **注**: 各タブは、新しい Azure SQL Database サーバーを作成するためのワークフローのステップを表します。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

    1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  **Subscription** ドロップダウン リストは既定値に設定したままにします。
    
    1.  **リソース グループ** セクションで、**新規作成** を選択し、**PolyglotData** を入力し、**OK**を選択します。
    
    1.  **Server name** テキスト ボックスに、 **polysqlsrvr*[yourname]*** を入力します。
    
    1.  「**場所**」 ドロップダウン リストで、**米国東部 (米国)** を選択します。
    
    1.  **サーバー管理者ログイン** テキストボックスに、「**testuser**」と入力します。
    
    1.  **Password**テキスト ボックスに、**TestPa55w.rd** を入力します。
    
    1.  **パスワードの確認**テキスト ボックスに、再度 **TestPa55w.rd**と入力します。 

    1.  「**次へ: ネットワーク**」

1.  「**ネットワーク**」 タブから、次の操作を実行します。

    1.  「**Azure のサービスとリソースとリソースにこのサーバーへのアクセスを許可**」 セクションで、「**Yes**」を選択します。
    
    1.  「**確認および作成**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用して SQL Database サーバーを作成するには、**Create** を選択します。

    > **注**: この時点で、ラボでは、Azure SQL 論理サーバーのみを作成します。ラボの後半で Azure SQL データベース インスタンスを作成します。

    > **注**: このラボを進める前に、作成タスクが完了するまで待ちます。

#### タスク 3: Azure Cosmos DB アカウント リソースの作成

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**Azure Cosmos DB**」 を選択します。

1.  **Azure Cosmos DB** ブレードで、Azure Cosmos DB インスタンスの一覧を見つけます。

1.  「**Azure Cosmos DB**」 ブレードで 「**Add**」 をクリックします。

1.  「**Azure Cosmos DB アカウントの作成**」 ブレードで、「**基本**」、「**ネットワーク**」 および 「**タグ**」 などのブレードの上部にあるタブを確認します。

    > **注**: 各タブは、ワークフロー内の新しい Azure Cosmos DB アカウントを作成するためのステップを表します。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  「**サブスクリプション**」 リストは既定値に設定したままにします。
    
    1.  「**リソース グループ**」 セクションで、リストから 「**PolyglotData**」 を選択します。
    
    1.  「**AccountName**」 テキスト ボックスに 「**polycosmos*[yourname]***」 と入力します。
    
    1.  「**API**」 ドロップダウン リストで、「**コア (SQL)**」 を選択します。

    1.  「**Notebooks (プレビュー)**」 セクションで、「**オフ**」 を選択します。

    1.  「**Free レベルの割引の適用**」 セクションで、「**適用しない**」 を選択します。
    
    1.  **Location** ドロップダウン リストで、 **(US) East US** リージョンを選択します。
    
    1.  「**アカウントの種類**」 セクションで、「**非運用環境**」 を選択します。
    
    1.  「**Multi-region Writes**」 セクションで、「**Disable**」 オプションを選択します。
    
    1.  「**確認および作成**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用して Azure Cosmos DB アカウントを作成するには、「**Create**」 を選択します。

    > **注**: 課題を進める前に、作成タスクが完了するまで待ちます。

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  **リソース グループ** ブレードで、 この実習ラボで前に作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した **polycosmos*[yourname]***  Azure Cosmos DB アカウントを選択します。

1.  **Azure Cosmos DB アカウント** ブレードで、 **Settings**セクションを見つけて、**Keys**リンクを選択します。

1.  「キー」 ペインで、**PRIMARY CONNECTION STRING** テキストボックスに値を記録します。この値は、この課題の後半で使用します。

#### タスク 4: Azure Storage アカウント リソースの作成

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**ストレージ アカウント**」 を選択します。

1.  「**ストレージ アカウント**」 ブレードで、ストレージ インスタンスの一覧を表示します。

1.  「**ストレージ アカウント**」 ブレードで、「**追加**」 を選択します。

1.  「**ストレージ アカウントを作成**」 ブレード で、「**基本**」、「**詳細**」および 「**タグ**」 など、ブレードの上部にあるタブを確認します。

    > **注**: 各タブは、ワークフロー内の新しい Azure ストレージ アカウントを作成するためのステップを表します。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  **サブスクリプション** リストは既定値に設定したままにします。
    
    1.  「**リソース グループ**」 セクションで、リストから 「**PolyglotData**」 を選択します。
    
    1.  「**ストレージ アカウント名**」 テキスト ボックスに、「**polystor*[yourname]***」と入力します。
    
    1.  **Location** ドロップダウン リストで、 **(US) East US** リージョンを選択します。
    
    1.  「**パフォーマンス**」 セクションで、「**Standard**」 を選択します。
    
    1.  「**Account kind**」 ドロップダウン リストで、「**StorageV2 (汎用 v2)**」 を選択します。
    
    1.  「**レプリケーション**」 ドロップダウン リストで、「**Locally-redundant ストレージ (LRS)**」 を選択します。
    
    1.  **Access tier (既定)** セクションで、**Hot** が選択されていることを確認します。
    
    1.  「**確認および作成**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定した構成を使用してストレージ アカウントを作成するには、**作成** を選択します。

    > **注**: このラボを進める前に、作成タスクが完了するまで待ちます。

#### レビュー

この演習では、polyglot データ ソリューションに必要な全ての Azure のリソースを作成しました。

### 演習 2: データのインポートと検証

#### タスク 1: イメージ BLOB をアップロードする

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で先ほど作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した **polystor*[yourname]*** ストレージ アカウントを選択します。

1.  「**ストレージ アカウント**」 ブレードで、「**Blob service**」 セクションの 「**Containers**」 リンクを選択します。

1.  「**Containers**」 セクションで、「**+ Container**」 を選択します。

1.  **新しいコンテナー** には、以下のアクションがあります。: 
    
    1.  **名前** テキスト ボックスに、**images** と入力します。
    
    1.  「**パブリック アクセス レベル**」 ドロップダウン リストで、「**BLOB (BLOB 専用の匿名読み取りアクセスのみ)**」 を選択します。
    
    1.  **OK** を選択します。

1.  **コンテナー**セクションに戻 り、新しく作成した**イメージ**コンテナーを選択します。

1.  「**コンテナー**」 ブレードで、**設定** セクションを見つけて、**プロパティ**リンクを選択します。     

1.  「プロパティ」 ペインで、「**URL**」 テキスト ボックスに値を記録します。この値は、この課題の後半で使用します。

1.  ブレードから **概要** リンクを見つけて選択します。

1.  ブレードで、「**アップロード**」 を選択します。

1.  「**BLOB をアップロード**」 ポップアップで、次の操作を実行します。
    
    1.  **ファイル** セクションで、**フォルダー** アイコンを選択します。
    
1.  [**File Explorer**] ウィンドウで、**Allfiles(F):\\Allfiles\\Labs\\04\\Starter\\Images** を参照し、42 個の個別の **jpg** 画像ファイルをすべて選択してから、[**開く**] を選択します。
    
    1.  「**ファイルが既に存在する場合は上書き**」 が選択されていることを確認し、「**アップロード**」 を選択します。

    > **注**: このラボを続行する前に、全ての BLOB がアップロードされるのを待ちます。

#### タスク 2: SQL .bacpac ファイルのアップロード

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で先ほど作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した **polystor*[yourname]*** ストレージ アカウントを選択します。

1.  「**ストレージ アカウント**」 ブレードで、「**Blob service**」 セクションの 「**Containers**」 リンクを選択します。

1.  「**コンテナー**」 セクションで、「**+ コンテナー**」 を選択します。

1.  「**新しいコンテナー**」 ポップアップで、次のアクションを実行します。
    
    1.  「**名前**」 テキスト ボックスに、「**databases**」 を入力します。
    
    1.  「**パブリック アクセス レベル**」 ドロップダウン リストで、「**プライベート (匿名アクセスなし)**」 を選択します。
    
    1.  「**OK**」 を選択します。

1.  「**Containers**」 セクションに戻り、新しく作成した 「**データベース**」 コンテナーを選択します。

1.  「**コンテナー**」 ブレードで、「**アップロード**」 を選択します。

1.  「**BLOB をアップロード**」 ポップアップで、次の操作を実行します。
    
    1.  「**ファイル**」 セクションで、**フォルダー**アイコンを選択します。
    
    1.  **File Explorer**ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\04\\Starter**に移動し、**AdventureWorks.bacpac** ファイルを選択し、**開く** を選択します。
    
    1.  「**ファイルが既に存在する場合は上書き**」 が選択されていることを確認し、「**アップロード**」 を選択します。

    > **注**: この演習を続行する前に、BLOB がアップロードされるのを待ちます。

#### タスク 3: SQL Database のインポート

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で先ほど作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した **polysqlsrvr*[yourname]***  SQL サーバーを選択します。

1.  **SQL サーバー** ブレードで、**データベースのインポート** を選択します。

1.  **データベースのインポート** ブレードで、次の操作を実行します：

    1.  「**サブスクリプション**」 リストは既定値に設定したままにします。

    1.  「**ストレージ**」 オプションを選択します。

    1.  「**ストレージ アカウント**」 ブレード で、この実習ラボで作成済みの **polystor*[yourname]*** ストレージ アカウントを選択します。 

    1.  **コンテナー**ブレードで、このラボで以前に作成した **データベース** コンテナを選択します 。 

    1.  表示される**コンテナー** ブレード で、このラボで前に作成した **AdventureWorks.bacpac** BLOB を選択し、「**選択**」 を選択してブレードを閉じます。

    1.  **データベースのインポート** ブレードに戻り、**価格レベル** オプションを既定値のままにします。

    1.  「**データベース名**」 テキスト ボックスに、「**AdventureWorks**」 を入力します。

    1.  **Collation** テキスト ボックスは既定値のままにします。

    1.  **サーバー管理者ログイン** テキストボックスに、「**testuser**」 と入力します。
    
    1.  **Password** テキスト ボックスに、**TestPa55w.rd** を入力します。
    
    1.  「**OK**」 を選択します。

> **注**: このラボを続行する前に、データベースの作成を待ちます。インポート手順でファイアウォール関連のエラーが表示された場合は、ラボの前に SQL Server の [**Azure サービスにサーバーへのアクセスを許可する**] 設定を正しく構成していなかったことを意味します。  設定を確認し、空の **AdventureWorks** データベースを削除してから、インポートを再試行してください。
    
#### タスク 4: インポートされた SQL Database を使用する

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で先ほど作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した **polysqlsrvr*[yourname]***  SQL サーバーを選択します。

1.  「**SQL Server**」 ブレードで、ブレードから 「**セキュリティ**」 セクションを見つけ、「**ファイアウォールと仮想ネットワーク**」 リンクを選択します。

1.  ファイアウォールと仮想ネットワーク ペインで、次の操作を実行します。

    1.  「**クライアント IP を追加** を選択します。
    
    1.  「**保存**」 を選択します。

    1.  **Success!** 確認ダイアログで **OK** を選択します。   

    > **注**: この手順により、ローカルマシンがこのサーバーに関連付けられたデータベースにアクセスできるようになります。

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で先ほど作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した**AdventureWorks** SQL Databaseを選択します。

1.  「**SQL database**」 ブレードで、「**Settings**」 セクションをブレードから見つけ 「**Connection strings**」 リンクを選択します。

1.  「接続文字列」 ペインで、 「**ADO.NET (SQL Authentication)**」 テキスト ボックスに値を記録します。この値は、この課題の後半で使用します。

1.  次の操作を実行して、記録した接続文字列を更新します。

    1.  接続文字列内で *your_username*プレースホルダーを見つけ、 **testuser** に置き換えます。

    1.  接続文字列内で *your_password* プレースホルダーを見つけ、 **TestPa55w.rd** に置き換えます。

        >**注意**: たとえば、接続文字列がもともと ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID={your_username};Password={your_password};`` である場合、更新された接続文字列は ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID=testuser;Password=TestPa$$w0rd;`` となります。

1.  ブレードから 「**Query editor (preview)**」 リンクを見つけて選択します。

1.  クエリ エディタ ペインで、次の操作を実行します。

    1.  「**ログイン**」 テキスト ボックスに、「**testuser**」 を入力します。

    1.  **Password** テキスト ボックスに、**TestPa55w.rd** を入力します。

    1.  「**OK**」 を選択します。

1.  開いているクエリ エディターで、次のクエリを入力します。

    ```
    SELECT * FROM AdventureWorks.dbo.Models
    ```

1.  「**実行**」 を選択してクエリを実行し、結果を確認します。 

    > **注**: このクエリは、Web アプリケーションのホーム ページからモデルのリストを返します。

1.  クエリ エディターで、既存のクエリを次のクエリに置き換えます。

    ```
    SELECT * FROM AdventureWorks.dbo.Products
    ```

1.  「**実行**」 を選択してクエリを実行し、結果を確認します。 

    > **注**: このクエリは、各モデルに関連付けられている製品の一覧を返します。

#### レビュー

この演習では、Web アプリケーションで使用するすべてのリソースをインポートしました。

### エクササイズ 3: .NET コア Web アプリケーションを開いて構成する

#### タスク 1: Web アプリケーションを開いてビルドします。

1.  **スタート** 画面で、**Visual Studio コード** タイルを選択します。

1.  「**ファイル**」 メニューで、「**フォルダーを開く**」 を選択します。

1.  開かれる **File Explorer** ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\04\\Starter\\AdventureWorks** に移動し、「**フォルダの選択**」 を選択します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、「Enter」 を選択して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注**: **dotnet build** コマンドは、フォルダー内のすべてのプロジェクトをビルドする前に、不足している NuGet パッケージを自動的に復元します。

1.  端末に印刷されたビルドの結果を確認します。ビルドは問題なくまた、警告メッセージもなく正常に完了します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: SQL 接続文字列の更新

1.  **Visual Studio Code** ウインドウのエクスプローラーペインで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **appsettings.json** ファイルを開きます。

1.  3 行目の JavaScript Object Notation (JSON) オブジェクトで、 **ConnectionStrings.AdventureWorksSqlContext** パスを見つけます。現在値が空であることを確認します：

    ```
    "ConnectionStrings": {
        "AdventureWorksSqlContext": "",
        ...
    },
    ```

1.  このラボで前に記録したSQL データベース の **ADO.NET (SQL Authentication) connection string** に値を設定して、**AdventureWorksSqlContext** プロパティの値を更新します。

    > **注**: ここで、更新された接続文字列を使用することが重要です。portal からコピーされた元の接続文字列には、SQL Database への接続に必要なユーザー名とパスワードが存在しません。

1.  **appsettings.json** ファイルを保存します。

#### タスク 3: BLOB ベース URL の更新

1.  JSON オブジェクトの8行目で、**Settings.BlobContainerUrl** パスを見つけます。現在値が空であることを確認します：

    ```
    "Settings": {
        "BlobContainerUrl": "",
        ...
    }
    ```

1.  この演習で前に記録した **images** と名付けられた Azure Storage BLOB コンテナーの **URL** プロパティに値を設定して、**BlobContainerUrl** プロパティの値を更新します。

1.  **appsettings.json** ファイルを保存します。

#### タスク 4: Web アプリケーションを検証する

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Web** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Web\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを選択して .NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: **dotnet run** コマンドは、プロジェクトへの変更を自動的にビルドし、デバッガーを接続せずに Web アプリケーションを起動します。このコマンドは、実行中のアプリケーションの URL と割り当てられたポートを出力します。

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、現在実行中の Web アプリケーション (<http://localhost:5000>) に移動します。

1.  Web アプリケーションで、フロント ページに表示されるモデルの一覧を確認します。

1.  **ウォーター ボトル** モデルを見 つけて、「**詳細の表示**」 を選択します。

1.  **ウォーター ボトル** 製品詳細ページで 「**カートに追加**」 を見つけて、チェックアウト機能が現在無効になっていることを確認します。

1.  Web アプリケーションを表示するブラウザー ウィンドウを閉じます。

1.  **Visual Studio Code** ウィンドウに戻り、**Kill Terminal** または **Recycle Bin** アイコンを選択して、現在開いているターミナルと関連付けられているプロセスを閉じます。

#### レビュー

この演習では、Azure のリソースに接続するように ASP.NET Core Web アプリケーションを構成しました。

### 演習 4: SQL データを Azure Cosmos DB に移行する

#### タスク 1: 移行プロジェクトの作成

1.  **Visual Studio Code**ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、 **AdventureWorks.Migrate** と名付けられたnew .NET project を同じ名前のフォルダー内に作成します。

    ```
    dotnet new console --name AdventureWorks.Migrate
    ```

    > **注**: **dotnet new** コマンドは、プロジェクトと同じ名前のフォルダーに新しい **コンソール** プロジェクトを作成します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して、既存の **AdventureWorks.Models** プロジェクトへの参照を追加します。

    ```
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Models\AdventureWorks.Models.csproj
    ```

    > **注**: **dotnet add reference** コマンドは、**AdventureWorks.Models** プロジェクトに含まれるモデル クラスへの参照を追加します。

1.  コマンドプロンプトで次のコマンドを入力し、Enter キーを押して、既存の **AdventureWorks.Context** プロジェクトへの参照を追加します。

    ```
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Context\AdventureWorks.Context.csproj
    ```

    > **注**: **dotnet add reference** コマンドは、**AdventureWorks.Context** プロジェクトに含まれるコンテキスト クラスへの参照を追加します。

1.  コマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して、NuGet から **Microsoft.EntityFrameworkCore.SqlServer** のバージョン2.2.6をインポートします 。

    ```
    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 3.0.1
    ```

    > **注**: **dotnet add package** コマンドは、**NuGet** から **Microsoft.EntityFrameworkCore.SqlServer** パッケージを追加します。詳細については、次を参照してください。[Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/3.0.1)。

1.  コマンド プロンプトで次のコマンドを入力し、Enterキーを押して、NuGetから **Microsoft.Azure.Cosmos** の3.4.1バージョンをインポートします。

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.4.1
    ```

    > **注**: **dotnet add package** コマンドは、**NuGet** から **Microsoft.Azure.Cosmos** パッケージを追加します。詳細については、次を参照してください。[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.4.1)。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: .NET クラスの作成 

1.  **Visual Studio Code** ウィンドウのエクスプローラーで、**AdventureWorks.Migrate** プロジェクトを展開します。

1.  **Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルのコード エディタ タブで、既存のファイルのすべてのコードを削除します。

1.  次のコード行を追加して、参照先の **AdventureWorks.Models** および **AdventureWorks.Context** プロジェクトから **AdventureWorks.Models** および **AdventureWorks.Context** 名前空間をインポートします。

    ```
    using AdventureWorks.Context;
    using AdventureWorks.Models;
    ```

1.  次のコード行を追加して、NuGet からインポートした **Microsoft.Azure.Cosmos** パッケージから **Microsoft.Azure.Cosmos** 名前空間をインポートします。

    ```
    using Microsoft.Azure.Cosmos;
    ```

1.  次のコード行を追加して、NuGetからインポートされた **Microsoft.EntityFrameworkCore.SqlServer** パッケージから **Microsoft.EntityFrameworkCore** 名前空間をインポートします。

    ```
    using Microsoft.EntityFrameworkCore;
    ```

1.  このファイルで使用される組み込み名前空間の **using** ディレクティブを追加するために、次のコード行を追加します。

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、新しい **Program** クラスを作成します：

    ```
    public class Program
    {
    }
    ```

1.  **Program** クラス内で、次のコード行を入力して、**sqlDBConnectionString** と名付けられた新しい文字列定数を作成します。

    ```
    private const string sqlDBConnectionString = "";
    ```

1.  この課題で以前に記録した SQL Database の **ADO.NET (SQL 認証) 接続文字列** に値を設定して、**sqlDBConnectionString** 文字列定数を更新します。

    > **注**: ここで、更新された接続文字列を使用することが重要です。portal からコピーされた元の接続文字列には、SQL Database への接続に必要なユーザー名とパスワードが存在しません。

1.  **Program** クラス内で、次のコード行を入力して、**cosmosDBConnectionString** と名付けられた新しい文字列定数を作成します。 

    ```
    private const string cosmosDBConnectionString = "";
    ```

1.  この課題で先ほど記録した Azure Cosmos DB アカウントの **プライマリ接続文字列** に値を設定して、**cosmosDBConnectionString** 文字列定数を更新します。

1.  **Program** クラス内に次のコードを入力して、新しい非同期 **Main** メソッドを作成します。

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Main** メソッド内で、次のコード行を追加して、紹介メッセージをコンソールに出力します。

    ```
    await Console.Out.WriteLineAsync("Start Migration");
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 3: エンティティ フレームワークを使用して SQL Database レコードを取得する

1.  **Program.cs** ファイル内の **Program** クラスの **Main** メソッド内に、次のコード行を追加して、接続文字列値として *sqlDBConnectionString* 変数をパスする **AdventureWorksSqlContext** クラスの新しいインスタンスを作成します。

    ```
    using AdventureWorksSqlContext context = new AdventureWorksSqlContext(sqlDBConnectionString);
    ```

1.  **Main** メソッド内で、次のコードブロックを追加して統合言語クエリ (LINQ) を発行し、データベースからすべての**モデル**と子**製品**を取得して、メモリ内の **List<>** コレクションに保存します。

    ```
    List<Model> items = await context.Models
        .Include(m => m.Products)
        .ToListAsync<Model>();
    ```

1.  **Main** メソッド内で、次のコード行を追加して、 SQL Databaseからインポートされたレコードの数を出力します。

    ```
    await Console.Out.WriteLineAsync($"Total Azure SQL DB Records: {items.Count}");
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate\
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Core Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Migrate** フォルダーにある **Program.cs** ファイルを確認してください。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 4: Azure Cosmos DB にアイテムを挿入する

1.  **Program.cs** ファイル内の **Program** クラスの **Main** メソッド内に、次のコード行を追加して、接続文字列値として *cosmosDBConnectionString* 変数をパスする **CosmosClient** クラスの新しいインスタンスを作成します。

    ```
    using CosmosClient client = new CosmosClient(cosmosDBConnectionString);
    ```

1.  **Main** メソッド内で、次のコード行を追加して、Azure Cosmos DB アカウントに存在しない場合は **Retail** と名付けられた新しい **データベース** を作成します。

    ```
    Database database = await client.CreateDatabaseIfNotExistsAsync("Retail");
    ```

1.  **Main** メソッド内で、次のコードブロックを追加して、**/Category** のパーティション キー パスと **1000** 要求ユニットのスループットを有する Azure Cosmos DB アカウントに既に存在しない場合のみ、**Online** という名前の新しい **container** を作成します:

    ```
    Container container = await database.CreateContainerIfNotExistsAsync("Online",
        partitionKeyPath: $"/{nameof(Model.Category)}",
        throughput: 1000
    );
    ```

1.  **Main** メソッド内で、次のコード行を追加して、*count* と名付けられた **int** 変数を作成します:

    ```
    int count = 0;
    ```

1.  **Main** メソッド内で、次のコードブロックを追加して、 **items** コレクション内のオブジェクトを反復処理する **foreach** ループを作成します:

    ```
    foreach (var item in items)
    {
    }
    ```

1.  **Main** メソッドに含まれる **foreach** ループ内で、次のコード行を追加してオブジェクトを Azure Cosmos DB コレクションに **upsert** し、その結果を *document* と名付けられた **ItemResponse<>** タイプの変数に保存します。

    ```
    ItemResponse<Model> document = await container.UpsertItemAsync<Model>(item);
    ```

1.  **Main** メソッドに含まれる **foreach** ループ内で、次のコード行を追加して、各upsert 操作のアクティビティ IDを出力します。

    ```
    await Console.Out.WriteLineAsync($"Upserted document #{++count:000} [Activity Id: {document.ActivityId}]");
    ```

1.  **Main** メソッド (**foreach** ループの外側) に戻り、次のコード行を追加して、Azure Cosmos DBにエクスポートされたドキュメントの数を出力します。

    ```
    await Console.Out.WriteLineAsync($"Total Azure Cosmos DB Documents: {count}");
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Migrate** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Migrate\
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Migrate** フォルダーにある **Program.cs** ファイルを確認してください。

#### タスク 5: 移行の実行

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを押して、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: **dotnet run** コマンドは、コンソール アプリケーションを起動します。

1.  初期 SQL レコード数、個々の upsert アクティビティ識別子、Azure Cosmos DBドキュメントの最終数など、スクリーンに出力されるさまざまなデータを確認します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 6: 移行の検証

1.  Azure portal と統合した **Microsoft Edge** ブラウザー ウィンドウに戻ります。

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で先ほど作成した **PolyglotData** リソース グループを見つけて選択します。

1.  **PolyglotData** ブレードで、 この実習ラボで前に作成した **polycosmos*[yourname]***  Azure Cosmos DB アカウントを選択します。

1.  「**Azure Cosmos DB アカウント**」 ブレードで、ブレードから 「**Data Explorer**」 リンクを見つけて選択します。

1.  Data Explorer ペインで、**Retail** データベースノードを展開します。

1.  「**Online**」 コンテナー ノードを展開し 「**New SQL Query**」 を選択します。

    > **注**: このオプションのラベルは非表示になっている可能性があります。Data Explorer ペインの上部にあるアイコンにカーソルを合わせると、ラベルが表示されます。

1.  表示されるクエリ タブで、次のテキストを入力します。

    ```
    SELECT * FROM models
    ```

1.  **Execute Query**を選択し、クエリが返す JSON モデルの一覧を確認します。 

1.  クエリ エディタに戻り、既存のテキストを次のテキストに置き換えます。

    ```
    SELECT VALUE COUNT(1) FROM models
    ```

1.  「**Execute Query**」 を選択し、 **COUNT** 集計操作の結果を確認します。

1.  「**Visual Studio Code**」 ウィンドウに戻ります。

#### レビュー

この演習では、Entity Framework と .NET SDK for Azure Cosmos DB を使用して、SQL Database から Azure Cosmos DB にデータを移行しました。

### エクササイズ 5: .NET を使用して Azure Cosmos DB にアクセスする

#### タスク 1: Cosmos SDK および参照を使用してライブラリを更新する

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Context** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Context\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して NuGet から **Microsoft.Azure.Cosmos** をインポートします。

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.4.1
    ```

    > **注**: **dotnet add package** コマンドは、**NuGet** から **Microsoft.Azure.Cosmos** パッケージを追加します。詳細については、次を参照してください。[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.4.1)。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: Azure Cosmos DB に接続するために .NET コードを書き込む

1.  **Visual Studio Code** ウィンドウのエクスプローラー ペインで、**AdventureWorks.Context** プロジェクトを展開します。

1.  ショートカットメニューにアクセスするか、**AdventureWorks.Context** フォルダーノードのショートカット メニューを右クリックまたはアクティブにして、「**新しいファイル**」 を選択します。

1.  新しいファイルプロンプトで、**AdventureWorksCosmosContext.cs** と入力します。

1.  **AdventureWorksCosmosContext.cs** ファイルのコード エディタ タブで、次のコード行を追加して、参照されている **AdventureWorks.Models** プロジェクトから **AdventureWorks.Models** 名前空間をインポートします。

    ```
    using AdventureWorks.Models;
    ```

1.  次のコード行を追加して、NuGet からインポートした **Microsoft.Azure.Cosmos** パッケージから **Microsoft.Azure.Cosmos** と **Microsoft.Azure.Cosmos.Linq** 名前空間をインポートします。

    ```
    using Microsoft.Azure.Cosmos;
    using Microsoft.Azure.Cosmos.Linq;
    ```

1.  このファイルで使用される組み込み名前空間の **using** ディレクティブを追加するために、次のコード行を追加します。

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、**AdventureWorks.Context** 名前空間ブロックを追加します。

    ```
    namespace AdventureWorks.Context
    {
    }
    ```

1.  **AdventureWorks.Context** 名前空間内で、次のコードを入力して、新しい **AdventureWorksCosmosContext** クラスを作成します。

    ```
    public class AdventureWorksCosmosContext
    {
    }
    ```

1.  このクラスが **AdventureWorksProductContext** インターフェイスを実装することを示す仕様を追加して、**AdventureWorksCosmosContext** クラスの宣言を更新します。

    ```
    public class AdventureWorksCosmosContext : IAdventureWorksProductContext
    {
    }
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のコード行を入力して、*_container* と名付けられた読み取り専用の新しい **コンテナー** 変数を作成します。

    ```
    private readonly Container _container;
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しいコンストラクターを追加します。

    ```
    public AdventureWorksCosmosContext(string connectionString, string database = "Retail", string container = "Online")
    {
    }
    ```

1.  コンストラクター内で、 **CosmosClient** クラスの新しいインスタンスを作成してから、クライアントから **データベース**と**コンテナー** インスタンスの両方を取得するために、次のコード ブロックを追加ます。

    ```
    _container = new CosmosClient(connectionString)
        .GetDatabase(database)
        .GetContainer(container);
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しい **FindModelAsync** メソッドを追加します。

    ```
    public async Task<Model> FindModelAsync(Guid id)
    {
    }
    ```

1.  **FindModelAsync** メソッド内で、次のコード ブロックを追加して LINQ クエリを作成し、それを反復子に変換し、結果セットを反復処理して、結果セットの単一のアイテムを返します。

    ```
    var iterator = _container.GetItemLinqQueryable<Model>()
        .Where(m => m.id == id)
        .ToFeedIterator<Model>();

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しい **GetModelsAsync** メソッドを追加します。

    ```
    public async Task<List<Model>> GetModelsAsync()
    {
    }
    ```

1.  **GetModelsAsync** メソッド内で、次のコードブロックを追加して SQL クエリを実行し、クエリ結果の反復子、結果セットの反復子を取得して、すべての結果の和集合を返します。

    ```
    string query = $@"SELECT * FROM items";

    var iterator = _container.GetItemQueryIterator<Model>(query);

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches;
    ```

1.  **AdventureWorksCosmosContext** クラス内で、次のシグネチャを持つ新しい **FindProductAsync** メソッドを追加します。

    ```
    public async Task<Product> FindProductAsync(Guid id)
    {
    }
    ```

1.  **FindProductAsync** メソッド内で、次のコード ブロックを追加して SQL クエリを実行し、クエリ結果反復子を取得し、結果セットを反復処理して、結果セットの単一のアイテムを返します。

    ```
    string query = $@"SELECT VALUE products
                        FROM モデル
                        JOIN products in models.Products
                        WHERE products.id = '{id}'";

    var iterator = _container.GetItemQueryIterator<Product>(query);

    List<Product> matches = new List<Product>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  **AdventureWorksCosmosContext.cs** ファイルを保存します。

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Context** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Context\
    ```
    
1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Context** フォルダーにある **AdventureWorksCosmosContext.cs** ファイルを確認します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 3: Azure Cosmos DB 接続文字列の更新

1.  **Visual Studio Code** ウインドウのエクスプローラーペインで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **appsettings.json** ファイルを開きます。

1.  JSON オブジェクトの4行目で **ConnectionStrings.AdventureWorksCosmosContext** パスを見つけます。現在値が空であることを確認します:

    ```
    "ConnectionStrings": {
        ...
        "AdventureWorksCosmosContext": "",
        ...
    },
    ```

1.  このラボで前に記録したAzure Cosmos DB アカウントの **PRIMARY CONNECTION STRING列** に値を設定して、**AdventureWorksCosmosContext** プロパティの値を更新します。

1.  **appsettings.json** ファイルを保存します。

#### タスク 4: .NET アプリケーションのスタートアップ ロジックを更新する

1.  **Visual Studio Code** ウインドウのエクスプローラーペインで、**AdventureWorks.Web** プロジェクトを展開します。

1.  **Startup.cs** ファイルを開きます。

1.  **Startup** クラスで、既存の **ConfigureProductService** メソッドを見つけます。

    ```
    public void ConfigureProductService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksProductContext, AdventureWorksSqlContext>(provider =>
            new AdventureWorksSqlContext(
                _configuration.GetConnectionString(nameof(AdventureWorksSqlContext))
            )
        );
    }
    ```

    > **注**: 現在の製品サービスでは、データベースとして SQL を使用します。

1.  **ConfigureProductService** メソッド内で、既存のすべてのコード行を削除します。

    ```
    public void ConfigureProductService(IServiceCollection services)
    {
    }
    ```

1.  **ConfigureProductService** メソッド内で、次のコードブロックを追加して、製品プロバイダーをこのラボで前に作成した **AdventureWorksCosmosContext** 実装に変更します。

    ```
    services.AddScoped<IAdventureWorksProductContext, AdventureWorksCosmosContext>(provider =>
        new AdventureWorksCosmosContext(
            _configuration.GetConnectionString(nameof(AdventureWorksCosmosContext))
        )
    );
    ```

1.  **Startup.cs** ファイルを保存します。

#### タスク 5: .NET アプリケーションが Azure Cosmos DB に正常に接続することを検証する

1.  **Visual Studio Code** ウインドウで、ショートカットメニューにアクセスするか、Explorerペインを右クリックし、**ターミナルで開く** を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力して Enter キーを押し、ターミナル コンテキストを **AdventureWorks.Web** フォルダーに切り替えます。

    ```
    cd .\AdventureWorks.Web\
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを選択して .NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: **dotnet run** コマンドは、プロジェクトへの変更を自動的にビルドし、デバッガーを接続せずに Web アプリケーションを起動します。このコマンドは、実行中のアプリケーションの URL と割り当てられたポートを出力します。

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、現在実行中の Web アプリケーション (<http://localhost:5000>) に移動します。

1.  Web アプリケーションで、フロント ページに表示されるモデルの一覧を確認します。

1.  **Touring-1000** モデルを見つけて、「**詳細の表示**」 を選択します。

1.  **Touring-1000** 製品の詳細ページで、次の操作を実行します。

    1.  「**オプションの選択**」 ボックスの一覧 で、「**Touring-1000 Yellow, 50, $2,384.07**」 を選択します。
    
    1.  「**カートに追加**」 を見つけて、チェックアウト機能が無効のままであることを確認します。 

1.  Web アプリケーションを表示するブラウザー ウィンドウを閉じます。

1.  **Visual Studio Code** ウィンドウに戻り、**Kill Terminal** または **Recycle Bin** アイコンを選択して、現在開いているターミナルと関連付けられているプロセスを閉じます。

#### レビュー

この演習では、.NET SDK を使用して Azure Cosmos DB コレクションを照会する C# コードを作成しました。

### エクササイズ 6: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開く

1.  ポータルで、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、署名 (\>) アンダースコア文字 (\_) より大きく表されます。

1.  サブスクリプションを使用して Cloud Shell を初めて開く場合は、**Azure Cloud Shell へようこそウィザード** を使って、初めて使用する Cloud Shell を構成できます。ウィザードで次のアクションを実行します。
    
    1.  シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるダイアログ ボックスが表示されます。既定の設定を受け入れ、「**ストレージの作成**」 を選択します。
    
    > **注**: Cloud Shell が最初のセットアップ手順を完了するまで待ってから、ラボを進めます。Cloud Shell の構成オプションに気付かない場合は、このコースのラボで既存のサブスクリプションを使用している可能性が高いです。新しいサブスクリプションを使用しているという前提で課題を記述します。

#### タスク 2: リソース グループを削除する

1.  プロンプトで次のコマンドを入力し、Enter キーを押して **PolyglotData** リソース グループを削除します。

    ```
    az group delete --name PolyglotData --no-wait --yes
    ```
    
1.  ポータルの Cloud Shell ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の Microsoft Edge アプリケーションを閉じます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

#### レビュー

この実習では、この課題で使用するリソース グループを削除することで、サブスクリプションをクリーンアップしました。