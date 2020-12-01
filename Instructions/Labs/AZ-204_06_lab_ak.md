---
lab:
    title: 'ラボ: MSAL と .NET SDK を使用した Microsoft Graph の認証とクエリ'
    az204Module: 'モジュール 06: ユーザー認証と承認を実装する'
    az020Module: 'モジュール 06: ユーザー認証と承認を実装する'
    type: 'Answer Key'
---

# ラボ: MSAL および .NET SDK を使用した Microsoft Graph の認証とクエリ
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

### 演習 1: Azure Active Directory (Azure AD) アプリケーションの登録の作成

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、「Azure portal」(<https://portal.azure.com>)に移動します。

1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: Azure portal に初めてログインする場合は、ポータルのツアーが表示されます。ツアーをスキップしてポータルの使用を開始するには、「**開始**」 を選択します。

#### タスク 2: アプリケーションの登録を作成します。

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードから、「**Azure Active Directory**」 を選択します。

1.  「**Azure Active Directory**」 ブレードから、**管理** セクションの 「**アプリの登録**」 を選択します。     

1.  「**アプリの登録**」 セクションで、「**新規登録**」 を選択します。   

1.  「**アプリケーションの登録**」 セクションで、次の操作を実行します。

    1.  「**名前**」 テキスト ボックスに、「**graphapp**」を入力します。

    1.  「**サポートされているアカウントの種類**」 の一覧で、「**この組織ディレクトリのアカウントのみ (既定のディレクトリのみ - シングル テナント)**」 チェック ボックスをオンにします。

    1.  「**リダイレクト URI**」 ドロップダウン リストで、**パブリック クライアント/ネイティブ (モバイルとデスクトップ)** を選択します。

    1.  「**リダイレクト URI**」 テキスト ボックスに **http\://localhost** と入力します。

    1.  「**登録**」 を選択します。 

#### タスク 3: 既定のクライアントのタイプを有効にします。

1.  「**graphapp**」 アプリケーションの登録ブレードで、「**管理**」 セクションの 「**認証**」 を選択します。

1.  「**認証**」 セクションで、次のアクションを実行します。

    1.  「**既定のクライアントの種類**」 サブセクションで、「**はい**」 を選択します。

    1.  「**保存**」 を選択します。

#### タスク 4: 一意の識別子を記録します。

1.  **graphapp** アプリケーションの登録ブレードで、「**概要**」 を選択します。

1.  「**概要**」 セクションで、「**アプリケーション (クライアント) ID**」 テキスト ボックスの値を検索して記録します。この値は、このラボの後半で使用します。

1.  「**概要**」 セクションで、「**ディレクトリ (テナント) ID**」 テキスト ボックスの値を検索して記録します。この値は、このラボの後半で使用します。

#### レビュー

このエクササイズでは、新しいアプリケーションの登録を作成し、後に課題で必要となる重要な値を記録しました。

### 演習 2: MSAL.NET ライブラリを使用してトークンを取得します。

#### タスク 1: .NET プロジェクトを作成する

1.  「**スタート**」 画面で、「**Visual Studio Code**」 タイルを選択します。

1.  **ファイル** メニューで、「**フォルダを開く**」 を選択します。

1.  開いた **ファイル エクスプローラー** ウィンドウで、**Allfiles (F):\\Allfiles\\Labs\\06\\Starter\\GraphClient** を参照し、「**フォルダの選択**」 を選択します。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  open コマンド プロンプトで、次のコマンドを入力し、[Enter] を選択して、現在のフォルダに **GraphClient** という名前の新しい .NET プロジェクトを作成します。

    ```
    dotnet new console --name GraphClient --output .
    ```

    > **注**: **dotnet new** コマンドは、プロジェクトと同じ名前のフォルダーに新しい **コンソール** プロジェクトを作成します。

1.  コマンド プロンプトで次のコマンドを入力し、「Enter」 を選択して、NuGet から **Microsoft.Identity.Client** のバージョン 4.7.1 をインポートします。

    ```
    dotnet add package Microsoft.Identity.Client --version 4.7.1
    ```

    > **注**: **dotnet add packaget** コマンドは、NuGet から **Microsoft.Identity.Clien** パッケージを追加します。詳細については、[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/4.7.1) を参照してください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: プログラム クラスの変更

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルのコード エディター タブで、既存のファイルのすべてのコードを削除します。

1.  次のコード行を追加して、NuGet からインポートされた **Microsoft.Identity.Client** パッケージから **Microsoft.Identity.Client** 名前空間をインポートします。

    ```
    using Microsoft.Identity.Client;
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
    
1.  **Program** クラスで、次のコードを入力して新しい非同期 **Main** メソッドを作成します。

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Program** クラスで、次のコード行を入力して、**_clientId** という名前の新しい文字列定数を作成します。

    ```
    private const string _clientId = "";
    ```

1.  このラボで以前に記録した **アプリケーション（クライアント）ID** に値を設定して、**clientId** 文字列定数を更新します。

1.  **Program** クラスで、次のコード行を入力して、**tenantId** という名前の新しい文字列定数を作成します。

    ```
    private const string _tenantId = "";
    ```

1.  **tenantId** 文字列定数の値を、この課題で前に記録した "**Directory（tenant）ID**" に設定して更新します。

1.  **Program.cs** ファイルを確認します。現時点では以下が含まれているはずです。

    ```
    using Microsoft.Identity.Client;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;

    public class Program
    {
        private const string _clientId = "<app-reg-client-id>";        
        private const string _tenantId = "<aad-tenant-id>";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### タスク 3: Microsoft Authentication Library (MSAL) トークンの取得

1.  **Main** メソッドで、次のコード行を追加して、**[IPublicClientApplication](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication)** 型の *app* という名前の新しい変数を作成します。

    ```
    IPublicClientApplication app;
    ```

1.  **Main** メソッドで、静的な **[PublicClientApplicationBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder)** クラスを使用して、次のアクションを実行し、パブリック クライアント アプリケーション インスタンスを構築します。次にそれを *app* 変数に格納します。     

    1.  次のコード行を追加して、静的な **[PublicClientApplicationBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder)** クラスにアクセスします。

        ```
        PublicClientApplicationBuilder
        ```

    1.  **PublicClientApplicationBuilder** クラスの **[Create()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder.create)** メソッドを使用する別のコード行を追加し、*_clientId* 変数をパラメーターとして渡すことで、前のコード行を更新します。

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
        ```

    1.  列挙値 **[AzureCloudInstance.AzurePublic](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.azurecloudinstance)** および *_tenantId* 変数をパラメーターとして渡す、ベース **[AbstractApplicationBuilder<>](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1)** クラスの **[WithAuthority()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1.withauthority)** メソッドを使用するために別のコード行を追加して、前のコード行を更新します。

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
        ```

    1.  **http://localhost** の文字列値を渡して、ベース **AbstractApplicationBuilder<>** クラスの 「**[WithRedirectUri()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1.withredirecturi)** メソッドを使用する別のコード行を追加し、前のコード行を更新します。

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
        ```

    1.  **PublicClientApplication** クラスの **[Build()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder.build)** メソッドを使用する別のコード行を追加して、前のコード行を更新します。

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();
        ```

    1.  式の結果を *app* 変数に格納するコードを追加して、前のコード行を更新します。

        ```
        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();
        ```

1.  **Main** メソッドで、次のコード行を追加して、単一の値 **user.read** を持つ新しい汎用文字列 **[List<>](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)** を作成します。

    ```
    List<string> scopes = new List<string> 
    { 
        "user.read" 
    };
    ```

1.  **Main** メソッドで、次のコード行を追加して、タイプ **[AuthenticationResult](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.authenticationresult)** の*結果*という名前の新しい変数を作成します。

    ```
    AuthenticationResult result;
    ```

1.  **Main** メソッドで、次のアクションを実行して、トークンをインタラクティブに取得し、出力を *結果* 変数に格納します。

    1.  次のコード行を追加して、*app* 変数にアクセスします。

        ```
        app
        ```

    1.  前のコード行を更新するには、**IPublicClientApplicationBuilder** インターフェイスの **[AcquireTokenInteractive()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive)** メソッドを使用する別のコード行を追加し、パラメーターとして *scopes* 変数を渡します。

        ```
        app
            .AcquireTokenInteractive(scopes)
        ```

    1.  **[AbstractAcquireTokenParameterBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractacquiretokenparameterbuilder-1)** クラスの **[ExecuteAsync()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractacquiretokenparameterbuilder-1.executeasync)** メソッドを使用する別のコード行を追加して、前のコード行を更新します。

        ```
        app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

    1.  **await** キーワードを使用して、式を非同期的に処理するコードを追加して、前のコード行を更新します。
    
        ```
        await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

    1.  式の結果を *結果* 変数に格納するコードを追加して、前のコード行を更新します。
    
        ```
        result = await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

1.  **Main** メソッドで、**Console.WriteLine** メソッドを使用して **[AuthenticationResult.AccessToken](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.authenticationresult.accesstoken)** メンバーの値をコンソールにレンダリングする次のコード行を追加します。

    ```
    Console.WriteLine($"Token:\t{result.AccessToken}");
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read"
        };

        AuthenticationResult result;
        
        result = await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();

        Console.WriteLine($"Token:\t{result.AccessToken}");
    }
    ```

1.  **Program.cs** ファイルを保存します。

#### タスク 4: 更新アプリケーションをテストします

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルドエラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\06\\Solution\\GraphClient** フォルダーの **Program.cs** ファイルを確認します。

1.  実行中のコンソール アプリケーションは、既定のブラウザーのインスタンスを自動的に開きます。

1.  開いているブラウザー ウィンドウで、次の操作を実行します。

    1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

    1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: 再びログインするのではなく、既存の Microsoft アカウントを選択することもできます。

1.  「**要求されたアクセス許可**」 Web ページがブラウザー ウィンドウに自動的に開かれます。この Web ページで、次の操作を実行します。

    1.  要求されたアクセス許可を確認します。

    1.  「**承諾する**」 を選択します。

1.  現在実行中の Visual Studio Code アプリケーションに戻ります。

1.  現在実行中のコンソール アプリケーションからの出力にレンダリングされたトークンを確認します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### レビュー

この練習では、MSAL.NET ライブラリを使用して、Microsoft ID プラットフォームからトークンを取得しました。

### エクササイズ 3: .NET SDK を使用して Microsoft Graph をクエリします。

#### タスク 1: Microsoft Graph SDK を NuGet からインポートします。

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  コマンド プロンプトで次のコマンドを入力し、「Enter」 を選択して、バージョン 1.21.0 の **Microsoft.Graph** を NuGet からインポートします。

    ```
    dotnet add package Microsoft.Graph --version 1.21.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGetから  **Microsoft.Graph**  パッケージを追加します。詳細については、[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/1.21.0) を参照してください。

1.  コマンド プロンプトで次のコマンドを入力し、「Enter」 を選択して、**Microsoft.Graph.Auth** のバージョン 1.0.0-preview.2 を NuGet からインポートします。

    ```
    dotnet add package Microsoft.Graph.Auth --version 1.0.0-preview.2
    ```

    > **注**: **dotnet add package** コマンドは、NuGetから **Microsoft.Graph.Auth** パッケージを追加します。詳細については、 [Microsoft.Graph.Auth](https://www.nuget.org/packages/Microsoft.Graph.Auth/1.0.0-preview.2) を参照してください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションをビルドします。

    ```
    dotnet build
    ```

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### タスク 2: プログラム クラスの変更

1.  「**Visual Studio Code**」 ウィンドウの Explorer ペインで、**Program.cs** ファイルを開きます。

1.  **Program.cs** ファイルのコード エディター タブで、次のコード行を追加して、NuGet からインポートされた **Microsoft.Graph** パッケージから **Microsoft.Graph** 名前空間をインポートします。

    ```
    using Microsoft.Graph;
    ```
    
1.  次のコード行を追加して、NuGet からインポートされた **Microsoft.Graph.Auth** パッケージから **Microsoft.Graph.Auth** 名前空間をインポートします。

    ```
    using Microsoft.Graph.Auth;
    ```

1.  次の **using** ディレクティブが含まれている **Program.cs** ファイルを確認します。

    ```
    using Microsoft.Graph;    
    using Microsoft.Graph.Auth;
    using Microsoft.Identity.Client;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    ```

#### タスク 3: Microsoft Graph SDK を使用してユーザー プロファイル情報を照会します。

1.  **Main** メソッド内で、次のアクションを実行して不要なコードを削除します。

    1.  次のコード行を削除します。

        ```
        AuthenticationResult result;
        ```
    
    1.  次のコード ブロックを削除します。

        ```
        result = await app
                .AcquireTokenInteractive(scopes)
                .ExecuteAsync();
        ```
    
    1.  次のコード行を削除します。

        ```
        Console.WriteLine($"Token:\t{result.AccessToken}");
        ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read"
        };
    }
    ```

1.  **Main** メソッドで、次のコード行を追加して、コンストラクター パラメーターとして変数 *app* および *scopes* を渡す、タイプ **DeviceCodeProvider** の *provider* という名前の新しい変数を作成します。

    ```
    DeviceCodeProvider provider = new DeviceCodeProvider(app, scopes);
    ```

1.  **Main** メソッドで、次のコード行を追加して、変数 *provider* をコンストラクター パラメーターとして渡すタイプ **GraphServiceClient** の *client* という名前の新しい変数を作成します。

    ```
    GraphServiceClient client = new GraphServiceClient(provider);
    ```

1.  **Main** メソッドで、次のアクションを実行して **GraphServiceClient** インスタンスを使用し、REST API の相対 **/Me** ディレクトリに対して HTTP 要求を発行した応答を非同期的に取得します。

    1.  次のコード行を追加して、**クライアント** 変数の *Me* プロパティを取得します。

        ```
        client.Me
        ```

    1.  次のコード行を追加して以前のコード行を更新し、**Request()** メソッドを使用して HTTP 要求を表すオブジェクトを取得します。

        ```
        client.Me
            .Request()
        ```

    1.  **GetAsync()** メソッドを使用して、非同期的に要求を発行する別のコード行を追加し、前のコード行を更新します。

        ```
        client.Me
            .Request()
            .GetAsync()
        ```

    1.  **await** キーワードを使用して、式を非同期的に処理するコードを追加して、前のコード行を更新します。

        ```
        await client.Me
            .Request()
            .GetAsync()
        ```

    1.  式の結果を **User**  タイプの *myProfile* という名前の新しい変数に格納するコードを追加して、前のコード行を更新します。

        ```
        User myProfile = await client.Me
            .Request()
            .GetAsync();
        ```

1.  **Main** メソッドで、次のコード行を追加し、**Console.WriteLine** メソッドを使用して **User.DisplayName** メンバーの値をコンソールにレンダリングします。

    ```
    Console.WriteLine($"Name:\t{myProfile.DisplayName}");
    ```

1.  **Main** メソッドで、次のコード行を追加し、**Console.WriteLine** メソッドを使用して **User.Id** メンバーの値をコンソールにレンダリングします。

    ```
    Console.WriteLine($"AAD Id:\t{myProfile.Id}");
    ```

1.  **Main** メソッドを監視します。現在以下が含まれます。 

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read" 
        };

        DeviceCodeProvider provider = new DeviceCodeProvider(app, scopes);

        GraphServiceClient client = new GraphServiceClient(provider);

        User myProfile = await client.Me
            .Request()
            .GetAsync();

        Console.WriteLine($"Name:\t{myProfile.DisplayName}");
        Console.WriteLine($"AAD Id:\t{myProfile.Id}");
    }
    ```

1.  **Program.cs** ファイルを保存します。

#### タスク 4: 更新アプリケーションをテストします

1.  **Visual Studio Code** ウィンドウで、エクスプローラー ウィンドウのショートカットメニューを右クリックまたはアクティブにし、「**ターミナルで開く**」 を選択します。

1.  開いているコマンド プロンプトで次のコマンドを入力し、Enter キーを選択し、.NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

    > **注**: ビルドエラーがある場合は、**Allfiles (F):\\Allfiles\\Labs\\06\\Solution\\GraphClient** フォルダーの **Program.cs** ファイルを確認します。

1.  現在実行中のコンソール アプリケーションからの出力でメッセージを確認します。メッセージにコードの値を記録します。この値は、このラボの後半で使用します。

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、<https://microsoft.com/devicelogin> にアクセスします。

1.  **コードの入力** Web ページで、次の操作を実行します。

    1.  「**コード**」 テキストボックスに、この課題で前にコピーしたコードの値を入力します。

    1.  「**次へ**」 を選択します。  

1.  ログイン Web ページで、次の操作を実行します。

    1.  Microsoft アカウントの電子メール アドレスを入力し、 「**次へ**」 を選択します。

    1.  Microsoft アカウントのパスワードを入力し、「**サインイン**」 を選択します。

    > **注**: 再びログインするのではなく、既存の Microsoft アカウントを選択することもできます。

1.  現在実行中の Visual Studio Code アプリケーションに戻ります。

1.  現在実行中のコンソール アプリケーションで、Microsoft Graph 要求の出力を確認します。

1.  「**ターミナルの強制終了**」 または 「**ごみ箱**」 アイコンを選択して、現在開いているターミナルと関連するプロセスを閉じます。

#### レビュー

この練習では、SDK および MSAL ベースの認証を使用してMicrosoft Graphに問い合わせました。

### 演習 4: サブスクリプションのクリーンアップ 

#### タスク 1: Azure AD でのアプリケーションの登録の削除

1.  Azure portal が表示されているブラウザー ウインドウに戻ります。

1.  Azure portal のナビゲーション ペインで、「**すべてのサービス**」 を選択します。

1.  「**すべてのサービス**」 ブレードから、「**Azure Active Directory**」 を選択します。

1.  「**Azure Active Directory**」 ブレードから、**管理**セクションの 「**アプリの登録**」 を選択します。     

1.  「**アプリの登録**」 セクションで、この課題で前に作成した **graphapp** Azure AD アプリケーションの登録を選択します。

1.  **graphapp** セクションで、次の操作を実行します。

    1.  「**削除**」 を選択します。 

    1.  確認のポップアップ ダイアログ ボックスで、「**はい**」 を選択します。

#### タスク 2: アクティブなアプリケーションを閉じる

1.  現在実行中の Microsoft Edge アプリケーションを閉じます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

#### レビュー

この実習では、この課題で使用する アプリケーションの登録を削除してサブスクリプションをクリーンアップしました。
