---
lab:
    title: 'ラボ: Event Grid イベントの公開とサブスクライブ'
    az204Module: 'モジュール 10: イベントベースのソリューションの開発'
    az020Module: 'モジュール 09: イベントベースのソリューションの開発'
    type: 'Answer Key'
---
    
# ラボ: Event Grid イベントの公開とサブスクライブ
# 学生課題解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな特性を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイスの変更が発生する可能性があります。これらの変更により、ラボの指示と手順が一致しない場合があります。

Microsoft では、コミュニティから必要な変更要望を受けたときにトレーニング コースを更新します。ただし、クラウドの更新は頻繁に行われるため、トレーニング コンテンツの更新前に UI が変更される場合もあります。**その場合は、変更に適宜対応して、ラボで要求されている内容を処理してください。**

## 指示

### 開始する前に

#### ラボの仮想マシンへのログイン

次の認証情報を使用して Windows 10 仮想マシン (VM) にログインします。
    
-   ユーザー名: **管理者**

-   パスワード: **Pa55w.rd**

> **注意**: 仮想ラボ環境に接続する手順は講師が説明します。

#### インストールされたアプリケーションのレビュー

Windows 10 デスクトップでタスク バーを探します。タスク バーには、この課題で使用するアプリケーションのアイコンが含まれています:
    
-   Microsoft Edge

-   Microsoft Visual Studio Code

### 演習 1: Azure のリソースを作成する

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、「Azure portal」(<https://portal.azure.com>)に移動します。

1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: Azure portal に初めてログインする場合は、ポータルのツアーが表示されます。ツアーをスキップしてポータルの使用を開始するには、「**開始**」 を選択します。

#### タスク 2: Azure Cloud Shell を開く

1.  ポータルで、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、署名 (\>) アンダースコア文字 (\_) より大きく表されます。

1.  サブスクリプションを使用して初めて Cloud Shell を開く場合は、「**Azure Cloud Shell へようこそウィザード**」 を使用して Cloud Shell を構成できます。ウィザードで次の操作を実行します。
    
    -   シェルの使用を開始するための新しいストレージ アカウントを作成するかどうかを確認するダイアログ ボックスが表示されたら、既定の設定をそのまま使用し、「**ストレージの作成**」 を作成します。 

    > **注**: Cloud Shell が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。**Cloud Shell** の構成オプションが表示されない場合、最も可能性が高い原因は、このコースのラボで既存のサブスクリプションを使用していることだと考えられます。新しいサブスクリプションを使用しているという前提で課題を記述します。

1.  Azure portal の **Cloud Shell** コマンド プロンプトで次のコマンドを入力し、Enter キーを選択して Azure コマンド ライン インターフェイス (Azure CLI) ツールのバージョンを取得します。

    ```
    az --version
    ```

#### タスク 3: Microsoft.EventGrid プロバイダーの登録を表示する

1.  ポータルの **Cloud Shell** コマンド プロンプトで、次の操作を実行します。

    1.  次のコマンドを入力し、Enter キーを押すと、Azure CLI のルート レベルにあるサブグループとコマンドの一覧が表示されます。

        ```
        az --help
        ```

    1.  次のコマンドを入力し、Enter キーを選択すると、リソース プロバイダーで使用できるコマンドの一覧が表示されます。

        ```
        az provider --help
        ```

    1.  次のコマンドを入力して Enter を選択すると、現在登録されているすべてのプロバイダーが一覧表示されます。

        ```
        az provider list
        ```

    1.  次のコマンドを入力してから Enter キーを選択すると、現在登録されているプロバイダーの名前空間のみが一覧表示されます。

        ```
        az provider list --query "[].namespace"
        ```

    1.  現在登録されているプロバイダーのリストをレビューします。プロバイダーの一覧に現在、**Microsoft.EventGrid** プロバイダーが含まれている点に注意してください。

1.  Cloud Shell ウィンドウを閉じます。

#### タスク 4: カスタム Event Grid トピックを作成する

1.  Azure potalのナビゲーション ペインで、**リソースの作成** を選択します。

1.  「**新規**」 ブレードで、「**Marketplace を検索**」 テキスト ボックスを見つけます。

1.  検索テキスト ボックスに 「**Event Grid**」 と入力し、Enter キーを選択します。

1.  「**すべて**」 の検索結果ブレードで、「**Event Grid トピック**」 の結果を選択します。

1.  「**Event Grid ピック**」 ブレードで 「**作成**」 を選択します。

1.  「**トピックの作成**」 ブレードで、次のアクションを実行します。

    1.  「**名前**」 テキスト ボックスに 「**hrtopic*[yourname]***」 と入力します。
    
    1.  「**リソース グループ**」 セクションで 「**新規作成**」 を選択し、**PubSubEvents** と入力して 「**OK**」 を選択します。

    1.  「**場所**」 ドロップダウン リストで、「**(US) 米国東部**」 リージョンを選択します。

    1.  「**イベント スキーマ**」 ドロップダウン リストから 「**Event Grid スキーマ**」 を選択し、「**作成**」 を選択します。
  
    > **注**: Azure がトピックの作成を完了するのを待ってから、課題を進めます。アプリの作成時に通知が届きます。

#### タスク 5: Azure Event Grid ビューアーを Web アプリにデプロイする

1.  Azure potalのナビゲーション ペインで、**リソースの作成** を選択します。

1.  「**新規**」 ブレードで、「**Marketplace を検索**」 テキスト ボックスを見つけます。

1.  検索ボックスに 「**Web**」 と入力し、Enter キーを押します。

1.  「**すべて**」 の検索結果ブレードで 「**Web アプリ**」 の結果を選択します。

1.  「**Web アプリ**」 ブレードで 「**作成**」 を選択します。

1.  2 番目の 「**Web アプリ**」 ブレードで、「**基本**」 などのブレードのタブを見つけます。

    > **注**: 各タブは、ワークフローで新しい Web アプリを作成するためのステップを表します。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで次の操作を実行します。
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。
    
    1.  「**リソース グループ**」 セクションで 「**PubSubEvents**」 を選択します。

    1.  「**名前**」 テキスト ボックスに「**eventviewer*[yourname]***」 と入力します。

    1.  「**発行**」 セクションで、「**Docker コンテナー**」 を選択します。

    1.  「**オペレーティング システム**」 セクションで、「**Linux**」 を選択します。

    1.  「**リージョン**」 ドロップダウン リストで 「**米国東部**」 のリージョンを選択します。

    1.  「**Linux プラン (米国東部)**」 セクションで 「**新規作成**」 を選択します。 

    1.  「**名前**」 テキスト ボックスに「**EventPlan**」という値を入力し、「**OK**」 を選択します。

    1.  「**SKU とサイズ**」 セクションを既定値のままにします。

    1.  「**次へ: Docker**」。

1.  「**Docker**」 タブで次の操作を実行します。

    1.  「**オプション**」 ドロップダウン リストから 「**単一のコンテナー**」 を選択します。

    1.  「**イメージのソース**」 ドロップダウン リストで 「**Docker Hub**」 を選択します。

    1.  「**アクセスの種類**」 ドロップダウン リストから 「**パブリック**」 を選択します。

    1.  「**イメージとタグ**」 テキスト ボックスに **microsoftlearning/azure-event-grid-viewer:latest** と入力します。

    1.  「**確認および作成**」 を選択します。

1.  「**レビュー + 作成**」 タブで、前の手順で選択したオプションをレビューします。

1.  指定した構成を使用して Web アプリを作成するには、「**作成**」 を選択します。 
  
    > **注**: Azure が Web アプリの作成を完了するのを待ってから、課題を進めます。アプリの作成時に通知が届きます。

#### レビュー

この実習では、この課題の残りの部分で使用する Event Grid トピックと Web アプリを作成しました。

### 演習 2: Event Grid サブスクリプションを作成する

#### タスク 1: Event Grid ビューアー Web アプリケーションにアクセスする

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  「**リソース グループ**」 ブレードで、この課題で以前に作成した **PubSubEvents** リソース グループを選択します。

1.  **PubSubEvents** ブレードで、この課題で以前に作成した **eventviewer*[yourname]*** Web アプリを選択します。

1.  「**App Service**」 ブレードの 「**設定**」 で、「**プロパティ**」 リンクを選択します。

1.  「**プロパティ**」 セクションで、「**URL**」 テキスト ボックスの値を記録します。この値は、このラボの後半で使用します。

1.  「**概要**」 を選択します。

1.  「**概要**」 セクションで 「**参照**」 を選択 します。

1.  現在実行中の **Azure Event Grid ビューアー** Web アプリケーションを監視します。この Web アプリケーションは、残りの課題で実行したままにしておきます。

    > **注**: この Web アプリケーションは、イベントがエンドポイントに送信されるとリアルタイムで更新されます。課題全体のイベントを監視するためにこれを使用します。

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

#### タスク 2: 新しいサブスクリプションを作成する

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  「**リソース グループ**」 ブレードで、この課題で以前に作成した **PubSubEvents** リソース グループを選択します。

1.  「**PubSubEvents**」 ブレードで、 このラボで以前に作成した **hrtopic*[yourname]*** Event Grid トピックを選択します。

1.  「**Event Grid トピック**」 ブレードで 「**+ イベント サブスクリプション**」 を選択します。

1.  「**イベント サブスクリプションの作成**」 ブレードで次の操作を実行します。

    1.  「**名前**」 テキスト ボックスに「**basicsub**」と入力します。

    1.  「**イベント スキーマ**」 の一覧で 「**Event Grid スキーマ**」 を選択します。
    
    1.  「**エンドポイントのタイプ**」 の一覧で 「**Web hook**」 を選択します。

    1.  「**エンドポイント**」 を選択します。

    1.  「**Web hook の選択**」 ダイアログ ボックスの 「**サブスクライバー エンドポイント**」 テキスト ボックスに、以前に記録した **Web App URL** 値を入力します。**https://** のプレフィックスと **/api/updates** のサフィックスが使用されていることを確認し、「**選択の確定**」 を選択します。

        >**注意**: たとえば、**Web App URL** の値が **http://eventviewerstudent.azurewebsites.net/** の場合、「**サブスクライバー エンドポイント**」 は **https://eventviewerstudent.azurewebsites.net/api/updates** になります。

    1.  「**作成**」 を選択します。
  
    > **注**: Azure がサブスクリプションの作成を完了するのを待ってから、課題を進めます。アプリの作成時に通知が届きます。

#### タスク 3: サブスクリプション検証イベントを監視する

1.  **Azure Event Grid ビューアー** の Web アプリケーションを表示するブラウザー ウィンドウに戻ります。

1.  サブスクリプション作成プロセスの一環として作成された **Microsoft.EventGrid.SubscriptionValidationEvent** イベントをレビューします。

1.  イベントを選択して、その JSON コンテンツを確認します。

1.  Azure portal で現在開いたブラウザー ウィンドウに戻ります。

#### タスク 4: サブスクリプションの認証情報を記録する

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  「**リソース グループ**」 ブレードで、この課題で以前に作成した **PubSubEvents** リソース グループを選択します。

1.  「**PubSubEvents**」 ブレードで、 このラボで以前に作成した **hrtopic*[yourname]*** Event Grid トピックを選択します。

1.  「**Event Grid トピック**」 ブレードで 「**トピックのエンドポイント**」 フィールドの値を記録します。この値は、このラボの後半で使用します。

1.  「**設定**」 カテゴリで 「**アクセス キー**」 リンクを選択します。

1.  「**アクセス キー**」 セクションで 「**キー 1**」 テキスト ボックスの値を記録します。この値は、このラボの後半で使用します。

#### レビュー

この演習では、新しいサブスクリプションを作成して登録を検証し、新しいイベントをトピックに発行するために必要な認証情報を記録しました。

### エクササイズ 3: .NET から Event Grid イベントを発行する

#### タスク 1: .NET プロジェクトを作成する

1.  「**スタート**」 画面で 「**Visual Studio Code**」 タイルを選択します。

1.  「**ファイル**」 メニューで、「**フォルダーを開く**」 を選択します。

1.  表示された 「**ファイル エクスプローラー**」 ウィンドウで 「**Allfiles (F):\\Allfiles\\Labs\\10\\Starter\\EventPublisher**」 を参照してから 「**フォルダーの選択**」 を選択します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  open コマンド プロンプトで次のコマンドを入力し、Enter を選択して、現在のフォルダーで **EventPublisher** という名前の新しい .NET プロジェクトを作成します。

    ```
    dotnet new console --name EventPublisher --output .
    ```

    > **注**: **dotnet new** コマンドは、プロジェクトと同じ名前のフォルダーに新しい**コンソール** プロジェクトを作成します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを選択して、NuGet から **Microsoft.Azure.EventGrid** のバージョン 3.2.0 をインポートします。

    ```
    dotnet add package Microsoft.Azure.EventGrid --version 3.2.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGet から **Microsoft.Azure.EventGrid** パッケージを追加します。詳細については、[Microsoft.Azure.EventGrid](https://www.nuget.org/packages/Microsoft.Azure.EventGrid/3.2.0) を参照してください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: Event Grid に接続する Program クラスを変更します。

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルのコード エディター タブで、既存のファイルのすべてのコードを削除します。

1.  次のコード行を追加して、**Microsoft.Azure.EventGrid** をインポートし、NuGetからインポートした **Microsoft.Azure.EventGrid** パッケージから **Microsoft.Azure.EventGrid.Models** 名前空間をインポートします。

    ```
    using Microsoft.Azure.EventGrid;
    using Microsoft.Azure.EventGrid.Models;
    ```
    
1.  このファイルで使用される組み込み名前空間の **using** ディレクティブを追加するために、次のコード行を追加します。

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    ```

1.  次のコードを入力して、新しい **Program** クラスを作成します。

    ```
    public class Program
    {
    }
    ``` 

1.  **Program** クラスで次のコード行を入力して、**topicEndpoint** という新しい文字列定数を作成します。

    ```
    private const string topicEndpoint = "";
    ```

1.  **topicEndpoint** 文字列定数を更新します。その値を、この課題で以前に記録した Event Grid トピックの**トピック エンドポイント**の値に設定してください。

1.  **Program** クラスで次のコード行を入力して、**topicKey** という新しい文字列定数を作成します。

    ```
    private const string topicKey = "";
    ```

1.  **topicKey** 文字列定数を更新します。その値を、この課題で以前に記録した Event Grid トピックの **キー** に設定してください。

1.  **Program** クラスで、次のコードを入力して新しい非同期 **Main** メソッドを作成します。

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Program.cs** ファイルを監視します。この中には以下のコード行が含まれているはずです。

    ```
    using Microsoft.Azure.EventGrid;
    using Microsoft.Azure.EventGrid.Models;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;

    public class Program
    {
        private const string topicEndpoint = "<topic-endpoint>";
        private const string topicKey = "<topic-key>";
        
        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### タスク 3: 新しいイベントを発行する

1.  **Main** メソッドで次のアクションを実行して、イベントのリストをトピック エンドポイントに発行します。

    1.  次のコード行を追加し、**topicKey** 文字列定数をコンストラクター パラメーターとして使用し、**TopicCredentials()** タイプの **credentials** という名前の新しい変数を作成します。

        ```
        TopicCredentials credentials = new TopicCredentials(topicKey);
        ```

    1.  次のコード行を追加して、**credentials** 変数をコンストラクター パラメーターとして使用し、 **EventGridClient()** 型の **client** という名前の新しい変数を作成します。

        ```
        EventGridClient client = new EventGridClient(credentials);
        ```

    1.  次のコード行を追加して、**List<EventGridEvent>** 型の **events** という名前の新しい変数を作成します。

        ```
        List<EventGridEvent> events = new List<EventGridEvent>();
        ```

    1.  次のコード行を追加して、anonymous 型の **firstPerson** という名前の新しい変数を作成します。

        ```
        var firstPerson = new
        {
            FullName = "Alba Sutton",
            Address = "4567 Pine Avenue, Edison, WA 97202"
        };
        ```

    1.  次のコード ブロックを追加して、**EventGridEvent** 型の **firstEvent** という名前の新しい変数を作成します。その後、サンプル データを使い、**EventGridEvent** 変数を設定します。

        ```
        EventGridEvent firstEvent = new EventGridEvent
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Employees.Registration.New",
            EventTime = DateTime.Now,
            Subject = $"New Employee: {firstPerson.FullName}",
            Data = firstPerson,
            DataVersion = "1.0.0"
        };
        ```

    1.  次のコード行を追加し、**firstEvent** インスタンスを **events** リストに追加します。

        ```
        events.Add(firstEvent);
        ```

    1.  次のコード行を追加し、anonymous 型の **secondPerson** という名前の新しい変数を作成します。

        ```
        var secondPerson = new
        {
            FullName = "Alexandre Doyon",
            Address = "456 College Street, Bow, WA 98107"
        };
        ```

    1.  次のコード ブロックを追加し、**EventGridEvent** 型の **secondEvent** という名前の新しい変数を作成します。その後、サンプル データを使い、**EventGridEvent** 変数を設定します。

        ```
        EventGridEvent secondEvent = new EventGridEvent
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Employees.Registration.New",
            EventTime = DateTime.Now,
            Subject = $"New Employee: {secondPerson.FullName}",
            Data = secondPerson,
            DataVersion = "1.0.0"
        };
        ```

    1.  次のコード行を追加して、**secondEvent** インスタンスを **events** リストに追加します。

        ```
        events.Add(secondEvent);
        ```

    1.  次のコード行を追加し、 **topicEndpoint** 変数から **Hostname** を取得します。

        ```
        string topicHostname = new Uri(topicEndpoint).Host;
        ```

    1.  次のコード行を追加し、パラメーターとして **topicHostname** と **events** を使い、**[EventGridClient.PublishEventsAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.eventgrid.eventgridclient.publisheventswithhttpmessagesasync)** メソッドを呼び出します。

        ```
        await client.PublishEventsAsync(topicHostname, events);
        ```

    1.  次のコード行を追加し、**イベント公開済み**メッセージをコンソールに表示します。

        ```
        Console.WriteLine("Events published");
        ```

1.  **Main** メソッドをレビューします。この中には以下が含まれているはずです。

    ```
    public static async Task Main(string[] args)
    {
        TopicCredentials credentials = new TopicCredentials(topicKey);
        EventGridClient client = new EventGridClient(credentials);

        List<EventGridEvent> events = new List<EventGridEvent>();

        var firstPerson = new
        {
            FullName = "Alba Sutton",
            Address = "4567 Pine Avenue, Edison, WA 97202"
        };

        EventGridEvent firstEvent = new EventGridEvent
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Employees.Registration.New",
            EventTime = DateTime.Now,
            Subject = $"New Employee: {firstPerson.FullName}",
            Data = firstPerson,
            DataVersion = "1.0.0"
        };
        events.Add(firstEvent);

        var secondPerson = new
        {
            FullName = "Alexandre Doyon",
            Address = "456 College Street, Bow, WA 98107"
        };
        
        EventGridEvent secondEvent = new EventGridEvent
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Employees.Registration.New",
            EventTime = DateTime.Now,
            Subject = $"New Employee: {secondPerson.FullName}",
            Data = secondPerson,
            DataVersion = "1.0.0"
        };
        events.Add(secondEvent);

        string topicHostname = new Uri(topicEndpoint).Host;
        await client.PublishEventsAsync(topicHostname, events);

        Console.WriteLine("Events published");
    }
    ```

1.  **Program.cs** ファイルを保存します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルド エラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\EventPublisher** フォルダーの **Program.cs** ファイルをレビューします。

1.  現在実行中のコンソール アプリケーションからの成功メッセージ出力を確認します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 4: 公開されたイベントを監視する

1.  **Azure Event Grid ビューアー** Web アプリケーションを使用してブラウザー ウィンドウに戻ります。

1.  コンソール アプリケーションによって作成された **Employees.Registration.New** イベントをレビューします。

1.  いずれかのイベントを選択し、その JSON コンテンツをレビューします。

1.  Azure portal に戻ります。

#### レビュー

この演習では、.NET コンソール アプリケーションを使用して、Event Grid トピックに新しいイベントを発行しました。

### 演習 4: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開く

1.  Azure portal で、「**Cloud Shell**」 アイコンを選択し、新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、署名 (\>) アンダースコア文字 (\_) より大きく表されます。

1.  サブスクリプションを使用して Cloud Shell を初めて開く場合は、**Azure Cloud Shell へようこそウィザード** を使って、初めて使用する Cloud Shell を構成できます。ウィザードで次の操作を実行します。
    
    1.  シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるダイアログ ボックスが表示されます。既定の設定を受け入れ、「**ストレージの作成**」 を選択します。 

    > **注**: Cloud Shell が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。Cloud Shell の構成オプションが表示されない場合は、このコースの課題で既存のサブスクリプションを使用している可能性が高いと考えられます。新しいサブスクリプションを使用しているという前提で課題を記述します。

#### タスク 2: リソース グループを削除する

1.  次のコマンドを入力し、Enter を選択して **PubSubEvents** リソース グループを削除します。

    ```
    az group delete --name PubSubEvents --no-wait --yes
    ```
    
1.  ポータルの Cloud Shell ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の Microsoft Edge アプリケーションを閉じます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

#### レビュー

この実習では、この課題で使用するリソース グループを削除することで、サブスクリプションをクリーンアップしました。
