---
lab:
    title: 'ラボ: Azure Storage SDK for .NET を使用して Azure Storage リソースとメタデータを取得する'
    az204Module: 'モジュール 03: BLOB ストレージを使用するソリューションを開発する'
    az020Module: 'モジュール 03: BLOB ストレージを使用するソリューションを開発する'
    type: 'Answer Key'
---

# ラボ: Azure Storage SDK for .NET を使用して Azure Storage リソースとメタデータを取得する
# 学生課題解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな特性を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイスの変更が発生する可能性があります。これらの変更により、ラボの指示と手順が一致しない場合があります。

Microsoft では、コミュニティから必要な変更要望を受けたときにトレーニング コースを更新します。ただし、クラウドの更新は頻繁に行われるため、トレーニング コンテンツの更新前に UI が変更される場合もあります。**その場合は、変更に適宜対応して、ラボで要求されている内容を処理してください。**

## 指示

### 開始する前に

#### ラボ仮想マシンへログインします

次の認証情報を使用して、Windows 10 仮想マシン (VM) にログインします。
    
-   ユーザー名: **Admin**

-   パスワード: **Pa55w.rd**

> **注意**: 仮想ラボ環境に接続する手順は講師が説明します。

#### インストールされたアプリケーションのレビュー

Windows 10 デスクトップでタスク バーを探します。タスク バーには、この課題で使用するアプリケーションのアイコンが含まれています:
    
-   Microsoft Edge

-   File Explorer

### エクササイズ 1: Azure リソースを作成

#### タスク 1: Azure portal を開く

1.  タスク バーで、「**Microsoft Edge**」 アイコンを選択します。

1.  開いているブラウザー ウィンドウで、「Azure portal」(<https://portal.azure.com>)に移動します。

1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: Azure portal に初めてログインする場合は、ポータルのツアーが表示されます。ツアーをスキップしてポータルの使用を開始するには、「**開始する**」 を選択します。

#### タスク 2: ストレージ アカウントの作成

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**ストレージ アカウント**」 を選択します。

1.  「**ストレージ アカウント**」 ブレードで、ストレージ インスタンスの一覧を表示します。

1.  「**ストレージ アカウント**」 ブレードで、「**追加**」 を選択します。

1.  「**ストレージ アカウントの作成**」 ブレードで、「**基本**」 などのタブを探します。

    > **注**: 各タブは、新しいストレージ アカウントを作成するための、ワークフロー内のステップを表しています。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します。
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。

    1.  「**リソース グループ**」 セクションで 「**新規作成**」 を選択し、「**StorageMedia**」と入力して 「**OK**」 を選択します。

    1.  「**ストレージ アカウント名**」 テキスト ボックスに、「**mediastor*[yourname]***」と入力します。

    1.  「**場所**」 ドロップダウン リストで、「**(US) 米国東部**」 リージョンを選択します。

    1.  「**パフォーマンス**」 セクションで、「**標準**」 を選択します。

    1.  「**アカウントの種類**」 ドロップダウン リストで、**StorageV2 (general purpose v2)** を選択します。

    1.  「**レプリケーション**」 リストで、**読み取りアクセス geo 冗長ストレージ (RA-GRS)** を選択します。

    1.  「**アクセス階層**」 セクションで、**Hot** が選択されていることを確認します。

    1.  **レビュー + 作成** を選択します。

1.  「**レビュー + 作成**」 タブで、前の手順で選択したオプションをレビューします。

1.  指定した構成を使用してストレージ アカウントを作成するには、「**作成**」 を選択します。 

    > **注**: 課題を進める前に、作成タスクが完了するまで待ちます。

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**ストレージ アカウント**」 を選択します。

1.  「**ストレージ アカウント**」 ブレードで、**mediastor*[yourname]*** ストレージ アカウント インスタンスを選択します。

1.  「**ストレージ アカウント**」 ブレードで 「**設定**」 セクションを見つけ、**プロパティ** リンクを選択します。

1.  「**プロパティ**」 セクションで、「**プライマリ Blob service エンドポイント**」 テキスト ボックスの値を記録します。

    > **注**: この値は、このラボの後半で使用します。

1.  「**ストレージ アカウント**」 ブレードで 「**設定**」 セクションを見つけ、**アクセス キー** リンクを選択します。

1.  「**アクセス キー**」 セクションで、次の操作を実行します。

    1.  「**ストレージ アカウント名**」 テキスト ボックスに値を記録します。
    
    1.  キーのいずれかを選択し、いずれかの **キー** ボックスに値を記録します。

    > **注**: これらの値は、この課題の後半で使用します。

#### レビュー

この演習では、ラボの残りの部分で使用する新しいストレージ アカウントを作成しました。

### 演習 2: コンテナーに BLOB をアップロードする

#### タスク 1: ストレージ アカウント コンテナーを作成する

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で前に作成した **StorageMedia** リソース グループを見つけて選択します。

1.  「**StorageMedia**」 ブレードで、 この課題で先ほど作成した **mediastor*[yourname]*** ストレージ アカウントを選択します。

1.  「**ストレージ アカウント**」 ブレードで、「**Blob サービス**」 セクションにある 「**コンテナー**」 を選択します。

1.  「**コンテナー**」 セクションで、「**+ コンテナー**」 を選択します。

1.  「**新規コンテナー**」 ポップアップ ウィンドウで、次の操作を実行します。
    
    1.  「**名前**」 テキスト ボックスに、「**raster-graphics**」と入力します。
    
    1.  「**パブリック アクセス レベル**」 ドロップダウン リストで 「**プライベート (匿名アクセスなし)**」 を選択し、「**OK**」 をクリックします。

1.  「**コンテナー**」 セクションで、「**+ コンテナー**」 を選択します。

1.  「**新規コンテナー**」 ポップアップ ウィンドウで、次の操作を実行します。
    
    1.  「**名前**」 テキスト ボックスに、「**compressed-audio**」と入力します。
    
    1.  「**パブリック アクセス レベル**」 ドロップダウン リストで 「**プライベート (匿名アクセスなし)**」 を選択し、「**OK**」 をクリックします。

1.  **「コンテナー」** セクションで、コンテナーの更新済み一覧を確認します。

#### タスク 2: ストレージ アカウント BLOB をアップロードする

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で前に作成した **StorageMedia** リソース グループを見つけて選択します。

1.  「**StorageMedia**」 ブレードで、 この課題で先ほど作成した **mediastor*[yourname]*** ストレージ アカウントを選択します。

1.  「**ストレージ アカウント**」 ブレードで、「**Blob サービス**」 セクションにある 「**コンテナー**」 を選択します。

1.  **コンテナー** セクションで、新しく作成された **raster-graphics** コンテナーを選択します。

1.	「**コンテナー**」 ブレードで、「**アップロード**」 を選択します。

1.	「**BLOB をアップロード**」 ウィンドウで、次の操作を実行します。

    1.  「**ファイル**」 セクションで、「**フォルダ**」 アイコンを選択します。

    1.  「**ファイル エクスプローラー**」 ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\Images** を参照して、**graph.jpg** ファイルを選択し、「**開く**」 を選択します。

    1.  「**ファイルが既に存在する場合は上書きする**」 チェックボックスがオンにチェックされていることを確認し、 「**アップロード**」 を選択します。 
    
    > **注**: この演習を続行する前に、BLOB がアップロードされるのを待ちます。

#### レビュー

この実習では、ストレージ アカウントにいくつかのプレースホルダー コンテナーを作成し、コンテナーの 1 つに BLOB を入力しました。

### エクササイズ 3: .NET SDK を使用してコンテナーにアクセスする

#### タスク 1: .NET プロジェクトを作成する

1.  「**スタート**」 スクリーンで、「**Visual Studio Code**」 タイルを選択します。

1.  「**ファイル**」 メニューで、「**フォルダーを開く**」 を選択します。

1.  「**ファイル エクスプローラー**」 ペインが開かれ、**Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\BlobManager** を参照し、「**フォルダーの選択**」 を選択します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力し、Enter キーを押して、現在のフォルダーに **BlobManager** という名前の新しい .NET Core プロジェクトを作成します。

    ```
    dotnet new console --name BlobManager --output .
    ```

    > **注**: **dotnet new** コマンドは、プロジェクトと同じ名前のフォルダーに新しい **コンソール** プロジェクトを作成します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して、NuGet から **Azure.Storage.Blobs** の 12.0.0 バージョンをインポートします。

    ```
    dotnet add package Azure.Storage.Blobs --version 12.0.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGet から **Azure.Storage.BLOB** パッケージを追加します。詳細については、[Azure Storage BLOB](https://www.nuget.org/packages/Azure.Storage.Blobs/12.0.0) にアクセスしてください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: プログラム クラスを変更してストレージにアクセスする

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルのコード エディター タブで、既存のファイルのすべてのコードを削除します。

1.  次のコード行を追加して、NuGet からインポートした **Microsoft.Azure.Blobs** パッケージから **Azure.Storage**、**Azure.Storage.Blobs**、**Azure.Storage.Blobs.Models** 名前空間をインポートします。

    ```
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    ```
    
1.  このファイルで使用される組み込み名前空間の **using** ディレクティブを追加するために、次のコード行を追加します。

    ```
    using System;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、新しい **Program** クラスを作成します。

    ```
    public class Program
    {
    }
    ``` 

1.  **Program** クラスに次のコード行を入力して、**blobServiceEndpoint** という名前の新しい文字列定数を作成します。

    ```
    private const string blobServiceEndpoint = "";
    ```

1.  この課題で前に記録したストレージ アカウントの **プライマリ Blob service エンドポイント** に値を設定して、**blobServiceEndpoint** 文字列定数を更新します。

1.  **Program** クラスに次のコード行を入力して、**storageAccountName** という名前の新しい文字列定数を作成します。

    ```
    private const string storageAccountName = "";
    ```

1.  このラボで前に記録したストレージ アカウントの **ストレージ アカウント名** に値を設定して、**storageAccountName** 文字列定数を更新します。

1.  **Program** クラスに次のコード行を入力して、**storageAccountKey** という名前の新しい文字列定数を作成します。

    ```
    private const string storageAccountKey = "";
    ```

1.  このラボで前に記録したストレージアカウントの **キー** に値を設定して、**storageAccountKey** 文字列定数を更新します。

1.  **Program** クラスで、次のコードを入力して新しい非同期 **Main** メソッドを作成します。

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Program.cs** ファイルを確認します。以下が含まれているはずです。

    ```
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    using System;
    using System.Threading.Tasks;

    public class Program
    {
        private const string blobServiceEndpoint = "<primary-blob-service-endpoint>";
        private const string storageAccountName = "<storage-account-name>";
        private const string storageAccountKey = "<key>";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### タスク 3: Azure Storage Blob サービス エンドポイントに接続する

1.  **Main** メソッドに次のコード行を追加して、コンストラクター パラメーターとして **storageAccountName** と **storageAccountKey** 定数を使用して、**StorageSharedKeyCredential** クラスの新しいインスタンスを作成します。

    ```
    StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
    ```

1.  **Main** メソッドに次のコード行を追加して、**blobServiceEndpoint** 定数と *accountCredentials* 変数をコンストラクター パラメーターとして使用して **BlobServiceClient** クラスの新しいインスタンスを作成します。

    ```
    BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
    ```

1.  **Main** メソッドに次のコード行を追加して、サービスからアカウント メタデータを取得する **BlobServiceClient** クラスの **GetAccountInfoAsync** メソッドを呼び出します。

    ```
    AccountInfo info = await serviceClient.GetAccountInfoAsync();
    ```
    
1.  **Main** メソッドに次のコード行を追加して、ウェルカム メッセージをレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
    ```
    
1.  **Main** メソッドに次のコード行を追加して、ストレージ アカウント名をレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
    ```
    
1.  **Main** メソッドに次のコード行を追加して、ストレージ アカウントの種類をレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
    ```
    
1.  **Main** メソッドに次のコード行を追加して、ストレージ アカウントの現在選択されている在庫保管単位 (SKU) をレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);	

        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);

        AccountInfo info = await serviceClient.GetAccountInfoAsync();

        await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
        await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
        await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
        await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、 **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。出力には、サービスから取得されたストレージ アカウントのメタデータが含まれています。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 4: 既存のコンテナーを列挙する

1.  **Program** クラスに次のコードを入力して、非同期で単一の **BlobServiceClient** パラメーター型を持つ **EnumerateContainersAsync** という名前の新しい**プライベート静的**メソッドを作成します。

    ```
    private static async Task EnumerateContainersAsync(BlobServiceClient client)
    {        
    }
    ```

1.  **EnumerateContainersAsync** メソッドに次のコードを入力して、**BlobServiceClient** クラスの **GetBlobContainersAsync** メソッドの呼び出しの結果を反復処理する、非同期の **foreach** ループを作成します。

    ```
    await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
    {
    }
    ```

1.  **foreach** ループ内に次のコードを入力して、各コンテナーの名前を出力します。

    ```
    await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
    ```

1.  **EnumerateContainersAsync** メソッドを観察して、次のことが含まれているか確認します。

    ```
    private static async Task EnumerateContainersAsync(BlobServiceClient client)
    {        
        await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
        {
            await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
        }
    }
    ```

1.  **Main** メソッドの末尾に次のコードを入力し、**serviceClient** 変数をパラメーターとして *EnumerateContainersAsync* メソッドを呼び出します。

    ```
    await EnumerateContainersAsync(serviceClient);
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました
        
        await EnumerateContainersAsync(serviceClient);
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  「**Visual Studio Code**」 ウインドウで、エクスプローラー ウィンドウのショートカットにアクセスするか右クリックして、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、 **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。更新された出力には、アカウント内のすべての既存のコンテナーの一覧が含まれます。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### レビュー

このエクササイズでは、 Azure Storage SDK を使用して既存のコンテナーにアクセスしました。 

### 演習 4: .NET SDK を使用して BLOB Uniform Resource Identifiers（URI）を取得する

#### タスク 1: SDK を使用して既存のコンテナー内の BLOB を列挙する

1.  **Program** クラスに次のコードを入力して、非同期で **BlobServiceClient** と **文字列** の 2 つのパラメーター型を持つ、**EnumerateBlobsAsync** という名前の新しい **静的プライベート**メソッドを作成します。

    ```
    private static async Task EnumerateBlobsAsync(BlobServiceClient client, string containerName)
    {      
    }
    ```

1.  **EnumerateBlobsAsync** メソッドに次のコードを入力して、**containerName** パラメーターを渡す **BlobServiceClient** クラスの **GetBlobContainerClient** メソッドを使用して、**BlobContainerClient** クラスの新しいインスタンスを取得します。

    ```
    BlobContainerClient container = client.GetBlobContainerClient(containerName);
    ```

1.  **EnumerateBlobsAsync** メソッドに次のコードを入力し、列挙されるコンテナー名をレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Searching:\t{container.Name}");
    ```

1.  **EnumerateBlobsAsync** メソッドに次のコードを入力して、**BlobContainerClient** クラスの **GetBlobsAsync** メソッドの呼び出しの結果を反復処理する非同期の **foreach** ループを作成します。

    ```
    await foreach (BlobItem blob in container.GetBlobsAsync())
    {        
    }
    ```

1.  **foreach** ループ内に次のコードを入力して、各 BLOB 名を出力します。

    ```
     await Console.Out.WriteLineAsync($"Existing Blob:\t{blob.Name}");
    ```

1.  **EnumerateBlobsAsync** メソッドを観察して、次のことが含まれているか確認します。

    ```
    private static async Task EnumerateBlobsAsync(BlobServiceClient client, string containerName)
    {      
        BlobContainerClient container = client.GetBlobContainerClient(containerName);
        
        await Console.Out.WriteLineAsync($"Searching:\t{container.Name}");
        
        await foreach (BlobItem blob in container.GetBlobsAsync())
        {        
             await Console.Out.WriteLineAsync($"Existing Blob:\t{blob.Name}");
        }
    }
    ```

1.  **Main** メソッドの最後に次のコードを入力して、**raster-graphics** の値を持つ *existingContainerName* という名前の変数を作成します。

    ```
    string existingContainerName = "raster-graphics";
    ```

1.  **Main** メソッドの末尾に次のコードを入力して、パラメーターとして **serviceClient** と *existingContainerName* 変数を渡して、*EnumerateBlobsAsync* メソッドを呼び出します。

    ```
    await EnumerateBlobsAsync(serviceClient, existingContainerName);
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました
        
        await EnumerateContainersAsync(serviceClient);

        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、 **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。更新された出力には、既存のコンテナーと BLOB に関するメタデータが含まれます。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: SDK を使用して新しいコンテナーを作成する

1.  **Program** クラスに次のコードを入力して、非同期で 2 つのパラメーター型の **BlobServiceClient** と **string** を持つ **GetContainerAsync** という名前の新しい **private static** メソッドを作成します。

    ```
    private static async Task<BlobContainerClient> GetContainerAsync(BlobServiceClient client, string containerName)
    {      
    }
    ```

1.  **GetContainerAsync** メソッドに次のコードを入力して、**containerName** パラメーターを渡す **BlobServiceClient** クラスの **GetBlobContainerClient** メソッドを使用して **BlobContainerClient** クラスの新しいインスタンスを取得します。

    ```
    BlobContainerClient container = client.GetBlobContainerClient(containerName);
    ```

1.  **GetContainerAsync** メソッドに次のコードを入力して、**BlobContainerClient** クラスの **CreateIfNotExistsAsync** メソッドを呼び出します。

    ```
    await container.CreateIfNotExistsAsync(PublicAccessType.Blob);
    ```

1.  **GetContainerAsync** メソッドに次のコードを入力して、作成された可能性のあるコンテナー名をレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"New Container:\t{container.Name}");
    ```

1.  **GetContainerAsync** メソッドに次のコードを入力して、**GetContainerAsync** メソッドの結果として、**container** という名前の **BlobContainerClient** クラスのインスタンスを返します。

    ```
    return container;
    ```  

1.  **GetContainerAsync** メソッドを確認します。以下が含まれているはずです。

    ```
    private static async Task<BlobContainerClient> GetContainerAsync(BlobServiceClient client, string containerName)
    {      
        BlobContainerClient container = client.GetBlobContainerClient(containerName);
        
        await container.CreateIfNotExistsAsync(PublicAccessType.Blob);
        
        await Console.Out.WriteLineAsync($"New Container:\t{container.Name}");
        
        return container;
    }
    ```

1.  **Main** メソッドの最後に次のコードを入力して、**vector-graphics** の値を持つ *newContainerName* という名前の変数を作成します。

    ```
    string newContainerName = "vector-graphics";
    ```

1.  **Main** メソッドの最後に次のコードを入力して、**GetContainerAsync** メソッドを呼び出し、パラメーターとして *serviceClient* と *newContainerName* 変数を渡し、結果を *BlobContainerClient* 型の **containerClient** という名前の変数に格納します。

    ```
    BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました
        
        await EnumerateContainersAsync(serviceClient);

        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);
        
        string newContainerName = "vector-graphics";
        BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、 **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。更新された出力には、既存のコンテナーと BLOB に関するメタデータが含まれます。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 3: ポータルを使用して新しい BLOB をアップロードする

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  「**リソース グループ**」 ブレードで、 この課題で前に作成した **StorageMedia** リソース グループを見つけて選択します。

1.  「**StorageMedia**」 ブレードで、 この課題で先ほど作成した **mediastor*[yourname]*** ストレージ アカウントを選択します。

1.  「**ストレージ アカウント**」 ブレードで、「**Blob サービス**」 セクションにある 「**コンテナー**」 を選択します。

1.  「**コンテナー**」 セクションで、新しく作成された **vector-graphics** コンテナーを選択します。

1.	「**コンテナー**」 ブレードで、「**アップロード**」 を選択します。

1.	「**BLOB をアップロード**」 ウィンドウで、次の操作を実行します。

    1.  「**ファイル**」 セクションで、「**フォルダー**」 アイコンを選択します。

    1.  「**ファイル エクスプローラー**」 ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\Images** を参照し、**graph.svg** ファイルを選択して、「**開く**」 を選択します。

    1.  「**ファイルが既に存在する場合は上書きする**」 チェックボックスがオンにチェックされていることを確認し、 「**アップロード**」 を選択します。 
    
    > **注**: この演習を続行する前に、BLOB がアップロードされるのを待ちます。

#### タスク 4: SDK を使用して BLOB URI にアクセスする

1.  **Program** クラスに次のコードを入力して、非同期で 2 つのパラメーター型 **BlobContainerClient** と **string** を持つ、**GetBlobAsync** という名前の新しい **private static** メソッドを作成します。

    ```
    private static async Task<BlobClient> GetBlobAsync(BlobContainerClient client, string blobName)
    {      
    }
    ```

1.  **GetBlobAsync** メソッドに次のコードを入力して、**BlobName** パラメーターを渡す **BlobContainer** クラスの **GetBlobClient** メソッドを使用して、**BlobClient** クラスの新しいインスタンスを取得します。

    ```
    BlobClient blob = client.GetBlobClient(blobName);
    ```

1.  **GetBlobAsync** メソッドに次のコードを入力して、参照された BLOB の名前をレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Blob Found:\t{blob.Name}");
    ```

1.  **GetBlobAsync** メソッドに次のコードを入力して、**GetBlobAsync** メソッドの結果として、**blob** という名前の **BlobClient** クラスのインスタンスを返却します。

    ```
    return blob;
    ```

1.  **GetBlobAsync** メソッドを確認します。以下が含まれているはずです。

    ```
    private static async Task<BlobClient> GetBlobAsync(BlobContainerClient client, string blobName)
    {      
        BlobClient blob = client.GetBlobClient(blobName);
        await Console.Out.WriteLineAsync($"Blob Found:\t{blob.Name}");
        return blob;
    }
    ```

1.  **Main** メソッドの最後に次のコードを入力して、 **graph.svg** の値を持つ *uploadedBlobName* という名前の変数を作成します。

    ```
    string uploadedBlobName = "graph.svg";
    ```

1.  **Main** メソッドの最後に次のコードを入力して、**GetBlobAsync** メソッドを呼び出し、パラメーターとして *containerClient* と *uploadedBlobName* 変数を渡す、**BlobClient** 型の *blobClient* という名前の変数に結果を格納します。

    ```
    BlobClient blobClient = await GetBlobAsync(containerClient, uploadedBlobName);
    ```

1.  **Main** メソッドの末尾に次のコードを入力して、**blobClient** 変数の *Uri* プロパティをレンダリングします。

    ```
    await Console.Out.WriteLineAsync($"Blob Url:\t{blobClient.Uri}");
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました
        
        await EnumerateContainersAsync(serviceClient);

        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);
        
        string newContainerName = "vector-graphics";
        BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
        
        string uploadedBlobName = "graph.svg";
        BlobClient blobClient = await GetBlobAsync(containerClient, uploadedBlobName);

        await Console.Out.WriteLineAsync($"Blob Url:\t{blobClient.Uri}");
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、 **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。更新された出力には、BLOB にオンラインでアクセスするための最終的な URL が含まれます。この URL の値を記録して、後でラボで使用します。

    > **注**: URL は次の文字列に似ている可能性があります: **https://mediastor*[yourname]*.blob.core.windows.net/vector-graphics/graph.svg**

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 5: ブラウザーを使用して URI をテストする

1.  タスク バーで、「**Microsoft Edge**」 アイコンを右クリックするか、ショートカットメニューを有効化したら、「**新しいウインドウ**」 を選択します。

1.  新しいブラウザー ウインドウで、この課題で前に BLOB 用にコピーしておいた URL に移動します。

1.  これで、ブラウザー ウィンドウにスケーラブル ベクター グラフィック (SVG) ファイルが表示されます。

#### レビュー

この実習では、Storage SDK を使用してコンテナーを作成し BLOB を管理しました。 

### エクササイズ 5: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開き、リソース グループを一覧表示する

1.  Azure portal のナビゲーション ウィンドウで、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、署名 (\>) アンダースコア文字 (\_) より大きく表されます。

1.  サブスクリプションを使用して Cloud Shell を初めて開く場合は、**Azure Cloud Shell へようこそウィザード** を使って、初めて使用する Cloud Shell を構成できます。ウィザードで次の操作を実行します。
    
    1.  シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるダイアログ ボックスが表示されます。既定の設定を受け入れ、「**ストレージの作成**」 を選択します。 

    > **注**: Cloud Shell が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。Cloud Shellの構成オプションが通知されない場合は、このコースのラボで既存のサブスクリプションを使用している可能性が高いと考えられます。新しいサブスクリプションを使用しているという前提で課題を記述します。

#### タスク 2: リソース グループの削除

1.  プロンプトで次のコマンドを入力し、Enter キーを押して **StorageMedia** リソース グループを削除します。

    ```
    az group delete --name StorageMedia --no-wait --yes
    ```
    
1.  ポータルの Cloud Shell ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.     現在実行中の Microsoft Edge アプリケーションを閉じます。

#### レビュー

この演習では、この課題で使用するリソース グループを削除して、サブスクリプションをクリーンアップしました。