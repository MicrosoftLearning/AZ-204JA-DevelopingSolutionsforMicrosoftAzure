---
lab:
    title: 'ラボ: Azure Queue Storage を使用してメッセージを非同期に処理する'
    az204Module: 'モジュール 11: メッセージ ベース ソリューションを開発する'
    az020Module: 'モジュール 10: メッセージ ベース ソリューションを開発する'
    type: 'Answer Key'
---

# ラボ: Azure Storage キューを使用したメッセージの非同期処理
# 学生課題解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな特性を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイスの変更が発生する可能性があります。これらの変更により、ラボの指示と手順が一致しない場合があります。

Microsoft では、コミュニティから必要な変更要望を受けたときにトレーニング コースを更新します。ただし、クラウドの更新は頻繁に行われるため、トレーニング コンテンツの更新前に UI が変更される場合もあります。**その場合は、変更に適宜対応して、ラボで要求されている内容を処理してください。**

## 指示

### 開始する前に

#### ラボの仮想マシンへのログイン

次の認証情報を使用して、Windows 10 仮想マシン (VM) にログインします。
    
-   ユーザー名: **管理者**

-   パスワード: **Pa55w.rd**

> **注意**: 仮想ラボ環境に接続する手順は講師が説明します。

#### インストールされたアプリケーションのレビュー

Windows 10 デスクトップでタスク バーを探します。タスク バーには、この課題で使用するアプリケーションのアイコンが含まれています:
    
-   Microsoft Edge

-   Visual Studio Code

-   Azure Storage Explorer

### 演習 1: Azure リソースを作成する

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、「Azure portal」(<https://portal.azure.com>)に移動します。

1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: Azure portal に初めてログインする場合は、ポータルのツアーが表示されます。ツアーをスキップしてポータルの使用を開始するには、「**開始**」 を選択します。

#### タスク 2: ストレージ アカウントの作成

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードで、「**ストレージ アカウント**」 を選択します。

1.  「**ストレージア カウント**」 ブレードで、ストレージ アカウントの一覧を表示します。

1.  「**ストレージ アカウント**」 ブレードで、「**追加**」 を選択します。

1.  「**ストレージ アカウントを作成**」 ブレードで、「**基本**」、「**タグ**」、「**レビュー + 作成**」 などのブレード上のタブを確認します。

    > **注**: 各タブは、新しいストレージ アカウントを作成するための、ワークフロー内のステップを表しています。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  **基本** タブを選択し、タブ領域で次の操作を実行します。
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。
    
    1.  「**リソース グループ**」 セクションで、「**新規作成**」 を選択し、「**MonitoredAssets**」 を入力し、「**OK**」 を選択します。
    
    1.  「**ストレージ アカウント名**」 テキスト ボックスに 「**asyncstor*[yourname]***」 と入力します。
    
    1.  「**場所**」 一覧で、「**(米国) 米国東部**」 地域を選択します。
    
    1.  「**パフォーマンス**」 セクションで、「**標準**」 を選択します。
    
    1.  「**アカウントの種類**」 の一覧で、「**StorageV2 (汎用v2)**」 を選択します。
    
    1.  「**レプリケーション**」 リストで、「**ローカル冗長ストレージ (LRS)**」 を選択します。
    
    1.  「**アクセス レベル (既定)**」 セクションで、「**ホット**」 が選択されていることを確認します。
    
    1.  「**レビュー + 作成**」 を選択します。

1.  **確認および作成**タブで、以前の手順で指定したオプションを確認します。

1.  「**作成**」 を選択して、指定した構成を使用してストレージ アカウントを作成します。

    > **注**: **デプロイ** ブレードで次に進む前に、作成タスクが完了するのを待ちます。

1.	「**デプロイ**」 ブレードの 「**リソースに移動**」 ボタンを選択して、新しく作成したストレージ アカウントに移動します。

1.	「**ストレージ アカウント**」 ブレードで 、「**設定**」 セクションを見つけ、「**アクセス キー**」 を選択します。

1.	「**アクセス キー**」 ブレードで、いずれかのキーを選択し、「**接続文字列**」 ボックスのいずれかの値を記録します。この値は、この課題の後半で使用します。

    > **注**: どの接続文字列を選択しても問題ありません。これらは交換可能です。

#### レビュー

この演習では、ラボの残りの部分で使用する新しい Azure Storage アカウントを作成しました。

### 演習 2: .NET プロジェクトで Azure Storage SDK を構成する 

#### タスク 1: .NET プロジェクトを作成する

1.  「**スタート**」 画面で、「**Visual Studio Code**」 タイルを選択します。

1.  「**ファイル**」 メニューで、「**フォルダーを開く**」 を選択します。

1.  開かれる **エクスプローラ** ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\11\\Starter\\MessageProcessor** を参照し、「**フォルダーの選択**」 を選択します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで、次のコマンドを入力し、「Enter」 を選択して、現在のフォルダーに **MessageProcessor** という名前の新しい .NET プロジェクトを作成します。

    ```
    dotnet new console --name MessageProcessor --output .
    ```

    > **注**: **dotnet new** コマンドは、プロジェクトと同じ名前のフォルダーに新しい **コンソール** プロジェクトを作成します。

1.  コマンド プロンプトで次のコマンドを入力し、「Enter」 を選択して NuGet から **Azure.Storage.Queues** のバージョン 12.0.0 をインポートします。

    ```
    dotnet add package Azure.Storage.Queues --version 12.0.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGet から **Azure.Storage.Queues** パッケージを追加します。詳細については、[Azure.Storage.Queues](https://www.nuget.org/packages/Azure.Storage.Queues/12.0.0) にアクセスしてください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: Azure Storage にアクセスするコードを書き込む

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルのコード エディター タブで、既存のファイルのすべてのコードを削除します。

1.  次のコード行を追加して、NuGet からインポートした **Azure.Storage.Queues** パッケージから  **Azure**、**Azure.Storage.Queues**、**Azure.Storage.Queues.Models** 名前空間をインポートします。

    ```
    using Azure;
    using Azure.Storage.Queues;
    using Azure.Storage.Queues.Models;
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

1.  **Program** クラスで、次のコード行を入力して、**storageConnectionString** という名前の新しい文字列定数を作成します。

    ```
    private const string storageConnectionString = "";
    ```

1.  このラボで前に記録したストレージ アカウントの **接続文字列** に値を設定して、**storageConnectionString** 文字列定数を更新します。

1.  **Program** クラスで、次のコード行を入力し、**messagequeue** の値を持つ **queueName** という名前の新しい文字列定数を作成します。

    ```
    private const string queueName = "messagequeue";
    ```

1.  **Program** クラスで、次のコードを入力して新しい非同期 **Main** メソッドを作成します。

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Program.cs** ファイルを確認します。現時点では以下が含まれているはずです。

    ```
    using Azure;
    using Azure.Storage.Queues;
    using Azure.Storage.Queues.Models;
    using System;
    using System.Threading.Tasks;

    public class Program
    {
        private const string storageConnectionString = "<storage-connection-string>";
        private const string queueName = "messagequeue";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### タスク 3: Azure Storage アクセスを検証する

1.  **Main** メソッドで、**QueueClient** 型の *client* という名前の新しい変数を作成して、ストレージ アカウントに接続する次のコード行を追加します。

    ```
    QueueClient client = new QueueClient(storageConnectionString, queueName);  
    ```

1.  **Main** メソッドで、次のコード行を追加して、キューがまだ存在しない場合に非同期で作成します。

    ```        
    await client.CreateAsync();
    ```

1.  **Main** メソッドで、次のコード行を追加して、「アカウント メタデータ」セクションのヘッダーをレンダリングします。

    ```
    Console.WriteLine($"---Account Metadata---");
    ```
    
1.  **Main** メソッドで、次のコード行を追加して、キュー エンドポイントの Uniform Resource Identifier (URI) をレンダリングします。

    ```
    Console.WriteLine($"Account Uri:\t{client.Uri}");
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        QueueClient client = new QueueClient(storageConnectionString, queueName);        
        await client.CreateAsync();

        Console.WriteLine($"---Account Metadata---");
        Console.WriteLine($"Account Uri:\t{client.Uri}");
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\11\\Solution\\MessageProcessor** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。出力には、キュー エンドポイントのメタデータが含まれています。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### レビュー

この演習では、.NET プロジェクトを構成して、ストレージ サービスにアクセスし、サービスを介して利用できるキューを操作しました。

### エクササイズ 3: キューにメッセージを追加します。 

#### タスク 1: キュー メッセージにアクセスするコードを書き込む

1.  **Main**メソッドで、次のコード行を追加して、"既存のメッセージ" セクションのヘッダーをレンダリングします。 

    ```
    Console.WriteLine($"---Existing Messages---");
    ```

1.  **Main** メソッド内で、次のアクションを実行して、キュー メッセージを取得するときに使用される変数を作成します。

    1.  次のコード行を追加して、*batchSize* という名前の **int** 型の変数を **10** の値で作成します。

        ```
        int batchSize = 10;
        ```

    1.  次のコード行を追加して、値が **2.5 秒** の *visibilityTimeout* という名前の **TimeSpan** 型の変数を作成します。   

        ```
        TimeSpan visibilityTimeout = TimeSpan.FromSeconds(2.5d);
        ```

1.  **Main** メソッド内で、キュー サービスから非同期的にメッセージのバッチを取得する次のアクションを実行します。

    1.  次のコード行を追加して、**QueueClient** クラスの **ReceiveMessagesAsync** 非同期メソッドを呼び出し、*batchSize* 変数と *visibilityTimeout* 変数をパラメーターとして渡します。

        ```
        client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

    1.  **await** キーワードを使用して、式を非同期的に処理するコードを追加して、前のコード行を更新します。

        ```
        await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

    1.  型 **[Response<QueueMessage[]>](https://docs.microsoft.com/dotnet/api/azure.response-1)** の *messages* という名前の新しい変数に式の結果を保存するコードを追加して、前のコード行を更新します。

        ```
        Response<QueueMessage[]> messages = await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

1.  **Main** メソッド内で、次のアクションを実行して、各メッセージのプロパティを反復処理してレンダリングします。

    1.  次のコード行を追加して、**[QueueMessage[]](https://docs.microsoft.com/dotnet/api/azure.storage.queues.models.queuemessage)** 型の *メッセージ* 変数の **[Value](https://docs.microsoft.com/dotnet/api/azure.response-1.value)** プロパティに格納されている各メッセージを反復処理する **foreach** ループを作成します。

        ```
        foreach(QueueMessage message in messages?.Value)
        {
        }
        ```

    1.  **foreach** ループ内に、各 **QueueMessage** インスタンスの **MessageId** プロパティと **MessageText** プロパティをレンダリングする別のコード行を追加します。
    
        ```
        Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
        ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました

        Console.WriteLine($"---Existing Messages---");
        int batchSize = 10;
        TimeSpan visibilityTimeout = TimeSpan.FromSeconds(2.5d);
        
        Response<QueueMessage[]> messages = await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);

        foreach(QueueMessage message in messages?.Value)
        {
            Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
        }
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、「Enter」 を選択して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\11\\Solution\\MessageProcessor** フォルダーの **Program.cs** ファイルを確認してください。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: メッセージ キュー アクセスをテストする

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\11\\Solution\\MessageProcessor** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。出力は、キューにメッセージがないことを示しています。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

1.  Azure portal のナビゲーション ペインで、「**リソース グループ**」 リンクを選択します。

1.  **リソース グループ**ブレードで、 この演習で前に作成した **AsyncProcessor** リソース グループを検索して選択します。

1.  **AsyncProcessor** ブレードで、 この課題で前に作成した **asyncstor*[yourname]*** ストレージ アカウントを選択します。

1.  **ストレージ アカウント**ブレードで、「**概要]**」 を選択 します。 

1.  「**概要**」 セクションで、「**エクスプローラで開く**」 を選択します。

1.  「**Azure Storage Explorer**」 ウィンドウで、「**Azure Storage Explorer を開く**」 を選択します。

    > **注**: ポータルを使用して Storage Explorer を初めて開く場合 は、ポータルが将来これらのタイプのリンクを開くことを許可するように求められる場合があります。プロンプトを受け入れる必要があります。

1.  **Azure Storage Explorer** アプリケーションで、Azure アカウントにサインインするように求めるメッセージが表示されます。次の操作を実行してログインします。

    1.  ポップアップ ダイアログで、「**ログイン**」 を選択します。 

    1.  「**Azure Storage への接続**」 ウィンドウで、「**Azure アカウントの追加**」 を選択し、「**Azure 環境**」 リストで 「**Azure**」 を選択し、 「**次へ**」 を選択します。

    1.  「**アカウントにログインする**」 ポップアップ ウィンドウで、Microsoft アカウントのメール アドレスを入力し、「**次へ**」 を選択します。

    1.  「**アカウントにログインする**」 ポップアップ ウィンドウ内で、Microsoft アカウントのパスワードを入力し、「**ログイン**」 を選択します。

    1.  「**アカウント管理**」 ウィンドウで、「**適用**」 を選択します。

    1.  サブスクリプション情報が入力された**エクスプローラー**ウィンドウに戻ることを確認します。

1.  **Azure Storage Explorer** アプリケーションの**エクスプローラー**ペインで、このラボで以前に作成した **asyncstor*[yourname]*** ストレージ アカウントを検索して展開します。

1.  **asyncstor*[yourname]*** ストレージ アカウント内で、「**キュー**」 ノードを検索して展開します。

1.  「**キュー**」 ノードで、.NET コードを使用してこの課題で前に作成した **messagequeue** キューを開きます。 

1.  「**messagequeue**」 タブで、「**メッセージの追加**」 を選択します。

1.  「**メッセージの追加**」 ポップアップ ウィンドウで、次の操作を実行します。

    1.  「**メッセージ テキスト**」 テキスト ボックスに、値 **Hello World** を入力します。

    1.  「**有効期限**」 テキスト ボックスに、値 **12** を入力します。

    1.  「**有効期限**」 ドロップダウン リストで、「**時間**」 を選択します。

    1.  「**Base 64 でメッセージ本文をエンコードする**」 チェック ボックスが選択されていないことを確認します。

    1.  「**OK**」 を選択します。

1.  「**Visual Studio Code**」 ウィンドウに戻り 、「Explorer」 ペインのショートカット メニューを右クリックまたはアクティブにして、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\11\\Solution\\MessageProcessor** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。出力には、作成した新しいメッセージが含まれます。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 3: キューに入れられたメッセージを削除する

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルの 「コード エディター」 タブで 、**Main** メソッド内の既存の **foreach** ループを検索します。

    ```
    foreach(QueueMessage message in messages?.Value)
    {
        Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
    }
    ```

1.  **foreach** ループ内で、**QueueMessage** クラスの **DeleteMessageAsync** メソッドを呼び出すコードの新しい行を追加し、*メッセージ* 変数の **MessageId** プロパティと **PopReceipt** プロパティを渡します。

    ```
    await client.DeleteMessageAsync(message.MessageId, message.PopReceipt);
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました
        
        foreach(QueueMessage message in messages?.Value)
        {
            Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
            await client.DeleteMessageAsync(message.MessageId, message.PopReceipt);
        }
    }
    ```

1.  **Program.cs** ファイルを **保存** します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\11\\Solution\\MessageProcessor** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。ラボで以前に作成したメッセージは、まだ削除されていないため、引き続き存在します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

1.  Storage Explorer に戻り、このラボで以前に作成した **asyncstor*[yourname]*** ストレージ アカウントを検索して展開します。

1.  **asyncstor*[yourname]*** ストレージ アカウントで、「**キュー**」 ノードを検索して展開します。

1.  「**キュー**」 ノードで、.NET コードを使用してこの課題で前に作成した **messagequeue** キューを開きます。 

1.  キュー内のメッセージの空のリストを監視します。

    > **注**: キューを更新する必要がある場合があります。

#### レビュー

この演習では、.NET ライブラリを使用して、ストレージ キューから既存のメッセージを読み取り、削除しました。

### 演習 4: .NET を使用して新しいメッセージをキューに入れる

#### タスク 1: キュー メッセージを作成するコードを書き込む

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **BlobContext.cs** ファイルの 「コード エディター」 タブで、既存の **Main** メソッドを検索します。

1.  **Main** メソッド内に、「New Messages」セクションのヘッダーをレンダリングする新しいコード行を追加します。

    ```
    Console.WriteLine($"---New Messages---");
    ```

1.  **Main** メソッドで、次のアクションを実行して、メッセージを非同期的に作成および送信します。

    1.  次のコード行を追加して、値が **Hi, Developer!** の *greeting* という名前の新しい文字列変数を作成します。

        ```
        string greeting = "Hi, Developer!";        
        ```

    1.  次のコード行を追加して、*greeting* 変数をパラメーターとして使用して、**QueueClient** クラスの **SendMessageAsync** メソッドを呼び出します。

        ```
        await client.SendMessageAsync(greeting);        
        ```

    1.  次のコード行を追加して、送信したメッセージのコンテンツをレンダリングします。

        ```
        Console.WriteLine($"Sent Message:\t{greeting}");        
        ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        \\ 簡潔にするために既存のコードが削除されました
        
        Console.WriteLine($"---New Messages---");
        string greeting = "Hi, Developer!";
        await client.SendMessageAsync(greeting);
        
        Console.WriteLine($"Sent Message:\t{greeting}");
    }
    ```

1.  **Program.cs** ファイルを **保存** します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\11\\Solution\\MessageProcessor** フォルダーの **Program.cs** ファイルを確認してください。

1.  現在実行中のコンソール アプリケーションからの出力を監視します。送信した新しいメッセージの内容が出力にあるはずです。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: Storage Explorer を使用してキューに登録されたメッセージを表示する

1.  Storage Explorer に戻り、このラボで前に作成した **asyncstor*[yourname]*** ストレージ アカウントを検索し展開します。

1.  **asyncstor*[yourname]*** ストレージ アカウントで、「**キュー**」 ノードを検索して展開します。

1.  「**キュー**」 ノードで、.NET コードを使用してこの課題で前に作成した **messagequeue** キューを開きます。 

1.  キュー内のメッセージの一覧で、単一の新しいメッセージを監視します。

    > **注**: キューを更新する必要がある場合があります。

#### レビュー

この演習では、ストレージキュー用の .NET ライブラリを使用して、キューに新しいメッセージを作成しました。

### エクササイズ 5: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開き、リソース グループを一覧表示する

1.  Azure portal のナビゲーション ウィンドウで、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、署名 (\>) アンダースコア文字 (\_) より大きく表されます。

1.  サブスクリプションを使用して Cloud Shell を初めて開く場合は、**Azure Cloud Shell へようこそウィザード** を使って、初めて使用する Cloud Shell を構成できます。ウィザードで次の操作を実行します。
    
    -   シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるダイアログ ボックスが表示されます。既定の設定を受け入れ、「**ストレージの作成**」 を選択します。 

    > **注**: Cloud Shell が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。Cloud Shellの構成オプションが通知されない場合は、このコースのラボで既存のサブスクリプションを使用している可能性が高いと考えられます。新しいサブスクリプションを使用しているという前提で課題を記述します。

#### タスク 2: リソース グループの削除

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを選択して **AsyncProcessor** リソース グループを削除します。

    ```
    az group delete --name AsyncProcessor --no-wait --yes
    ```
    
1.  ポータルの Cloud Shell ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の Microsoft Edge アプリケーションを閉じます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

1.  現在実行中の Azure Storage Explorer アプリケーションを閉じます。

#### レビュー

この実習では、この演習で使用したリソース グループを削除してサブスクリプションをクリーンアップしました。
