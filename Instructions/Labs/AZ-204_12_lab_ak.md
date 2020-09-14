---
lab:
    title: 'ラボ: Azure にデプロイされたサービスの監視'
    az204Module: 'モジュール 12: Azure ソリューションの監視と最適化'
    az020Module: 'モジュール 11: Azure ソリューションの監視と最適化'
    type: 'Answer Key'
---

# ラボ: Azure にデプロイされたサービスの監視
# 学生課題解答キー

## Microsoft Azure ユーザー インターフェイス

Microsoft クラウド ツールのダイナミックな特性を考えると、このトレーニング コンテンツの開発後に Azure ユーザー インターフェイスの変更が発生する可能性があります。これらの変更により、ラボの指示と手順が一致しない場合があります。

Microsoft は、コミュニティが必要な変更を行うと、このトレーニング コースを更新します。だたし、クラウドは頻繁に更新されるため、このトレーニングの内容が更新される前に UI が変更されるかもしれません。**その場合は、変更に適宜対応して、ラボで要求されている内容を処理してください。**

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

-   ファイル Explorer

-   Visual Studio Code

-   Windows PowerShell

### 演習 1: Azure リソースの作成と構成

#### タスク 1: Azure portal を開く

1.  タスク バーで、**Microsoft Edge** アイコンを選択します。

1.  開いているブラウザー ウィンドウで、「Azure portal」(<https://portal.azure.com>)に移動します。

1.  サインイン ページで、Microsoft アカウントのメール アドレスを入力し、「**次へ**」 を選択します。

1.  Microsoft アカウントのパスワードを入力し、[**サインイン**] を選択します。

> **注**: Azure portal に初めてサインインする場合は、ダイアログ ボックスにポータルを見学するオファーが表示されます。ツアーをスキップしてポータルの使用を開始するには、「**開始する**」 を選択します。

#### タスク 2: Application Insights リソースを作成する

1.  Azure potalのナビゲーション ペインで、**リソースの作成** を選択します。

1.  [**新規**] ブレードで、[**Marketplace を検索**] というテキスト ボックスを探します。

1.  検索テキスト ボックスに 「**Insights**」と入力し、Enter キーを押します。

1.  「**Marketplace**」 検索結果ブレードで、**Application Insights** の結果を選択します。

1.  「**Application Insights**」 ブレードで、「**作成**」 を選択します。

1.  「**Basics**」 など、2 番目の 「**Application Insights**」 ブレードからタブを見つけます。

    > **注**: 各タブは、ワークフローで新しい Application Insights インスタンスを作成するためのステップを表します。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。
    
    1.  「**リソース グループ**」 セクションで、「**新規作成**」 を選択し、「**MonitoredAssets**」 を入力し、「**OK**」 を選択します。
    
    1.  「**名前**」 テキスト ボックスに 「**instrm*[yourname]***」 と入力します。
    
    1.  「**リージョン**」 ドロップダウン リストで、「**米国東部**」 のリージョンを選択します。
    
    1.  「**確認および作成**」 を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  「**作成**」 を選択し、指定された構成を使用して Application Insights インスタンスを作成します。   

    > **注**: この課題を進める前に、作成タスクが完了するのを待ちます。

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  **リソース グループ** ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを選択します。

1.  「**MonitoredAssets**」 ブレードで、この課題で以前に作成した **instrm*[yourname]*** Application Insights アカウントを選択します。

1.  **Application Insights** ブレードの 「**構成**」 カテゴリーで 「**プロパティ**」 リンクを選択します。     

1.  「**プロパティ**」 セクションで、「**インストルメンテーション キー**」 テキスト ボックスの値を確認します。このキーは、Application Insights に接続するため、クライアント アプリケーションによって使われます。

#### タスク 3: Azure App Services リソースを使用して Web アプリを作成する

1.  Azure potalのナビゲーション ペインで、**リソースの作成**を選択します。

1.  [**新規**] ブレードで、[**Marketplace を検索**] というテキスト ボックスを探します。

1.  検索ボックスに「**Web**」と入力し、Enter キーを押します。

1.  「**Marketplace**」 の検索結果ブレードで、「**Web アプリ**」 の結果を選択します。

1.  「**Web アプリ**」 ブレードで、「**作成**」 を選択します。

1.  「**Basics**」 など、2 番目の 「**Web アプリ**」 ブレードからタブを探します。   

    > **注**: 各タブは、ワークフローで新しい Web アプリを作成するためのステップを表します。いつでも 「**確認および作成**」 を選択して、残りのタブをスキップできます。

1.  「**基本**」 タブで、次の操作を実行します:
    
    1.  「**サブスクリプション**」 テキスト ボックスは既定値のままにします。
    
    1.  「**リソース グループ**」 ドロップダウン リストで、「**MonitoredAssets**」 を選択します。
    
    1.  「**名前**」 テキスト ボックスに「***smpapi\***[yourname]***」と入力します。

    1.  「**発行**」 セクションで 「**コード**」 を選択します。

    1.  「**ランタイム スタック**」 ドロップダウン リストで 「**.NET Core 3.1 (LTS)**」 を選択します。

    1.  「**オペレーティング システム**」 セクションで 「** Windows**」 を選択します。

    1.  「**リージョン**」 ドロップダウン リストで 「**米国東部**」 リージョンを選択します。

    1.  「**Windows プラン (米国東部)**」 セクションで、「**新規作成**」 を選択し、「**名前**」 テキスト ボックスに 「**MonitoredPlan**」 の値を入力して 「**OK**」 を選択します。

    1.  「**SKU とサイズ**」 セクションを既定値のままにします。

    1.  「**次へ: 監視**」 を選択します。

1.  「**モニタリング**」 タブで、次の操作を実行します。

    1.  「**Application Insights を有効にする**」 セクションで 「**はい**」 を選択します。

    1.  「**Application Insights**」 ドロップダウン リストで、 この課題で以前に作成した **instrm*[yourname]*** Application Insights アカウントを選択します。

    1.  **「確認および作成」** を選択します。

1.  「**レビューと作成**」 タブで、前の手順で選択したオプションを確認します。

1.  指定された構成を使用して Web アプリを作成するには、「**作成**」 を選択します。   

    > **注**: 課題を進める前に、作成タスクが完了するのを待ちます。

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  **リソース グループ** ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを選択します。

1.  **MonitoredAssets** ブレードで、 この課題で以前に作成した ***smpapi\***[yourname]*** Web アプリを選択します。

1.  **App Service** ブレードの 「**設定**」 カテゴリで、「**構成**」 リンクを選択します。

1.  「**構成**」 セクションで、次の操作を実行します:
    
    1.  「**アプリケーション設定**」 タブを選択します。

    1.  API に関連付けられているシークレットを表示するには、「**値を表示**」 を選択します。

    1.  **APPINSIGHTS\_INSTRUMENTATIONKEY** キーに対応する値を確認します。この値は、Web Apps リソースの構築時に自動的に設定されました。

1.  「**App Service**」 ブレードの 「**設定**」 セクションで、「**プロパティ**」 リンクを選択します。

1.  「**プロパティ**」 セクションで、「**URL**」 テキスト ボックスの値を記録します。ラボの後半でこの値を使用して、API に対して要求を行います。

#### タスク 4: Web アプリの自動スケーリング オプションを構成する

1.  **App Services** ブレードの 「**設定**」 カテゴリーで、「**スケール アウト (App Service プラン)**」 リンクを選択します。

1.  「**スケール アウト**」 セクションで、次の操作を実行します。
    
    1.  「**カスタム自動スケーリング**」 を選択する
    
    1.  「**自動スケーリング設定名**」 テキスト ボックスで「**ComputeScaler**」と入力します。
    
    1.  「**リソース グループ**」 の一覧で、「**MonitoredAssets**」 を選択します。
    
    1.  「**縮尺モード**」 セクションで、「**メトリックに基づくスケール**」 を選択します。
    
    1.  「**インスタンスの制限**」 セクション内の 「**最小**」 テキスト ボックスに、**2** と入力します。
    
    1.  「**インスタンスの制限**」 セクション内の 「**最大**」 テキスト ボックスに、**8** と入力します。
    
    1.  「**インスタンスの制限**」 セクション内の 「**既定**」 テキスト ボックスで、「**3**」と入力します。
    
    1.  「**規則の追加**」 を選択します。「**縮尺ルール**」 ポップアップ ダイアログで、すべてのボックスを既定値に設定したままにして 「**追加**」 を選択します。
    
    1.  セクション内で 「**保存**」 を選択します。  

    > **注**: 保存操作が完了するのを待ってから、この課題を進めます。

#### レビュー

この演習では、この課題の残りの部分で使用するリソースを作成しました。

### 演習 2: Application Insights を使用してローカル Web アプリケーションを監視する 

#### タスク 1: .NET Core Web API プロジェクトを構築する

1.  タスク バーで、**Visual Studio コード** アイコンを選択します。

1.  「**ファイル**」 メニューで、「**フォルダーを開く**」 を選択します。

1.  「**ファイル エクスプローラー**」 ウィンドウで、 **Allfiles (F):\\Allfiles\\Labs\\12\\Starter\\Api**を参照し、「**フォルダーの選択**」 を選択します。

1.  「**Visual Studio コード**」 ウインドウで、「エクスプローラー」 ペインを右クリックするか、ショートカット メニューを有効にしてから 「**ターミナルで開く**」 を選択します。

1.  **開いた** コマンド プロンプトで次のコマンドを入力し、Enter を選択して現在のディレクトリに **SimpleApi** という名前の新しい .NET Web API アプリケーションを作成します。

    ```
    dotnet new webapi --output . --name SimpleApi
    ```

1.  コマンド プロンプトで次のコマンドを入力し、Enter を選択して、NuGetから **Microsoft.ApplicationInsights** のバージョン 2.13.0 を現在のプロジェクトにインポートします。

    ```
    dotnet add package Microsoft.ApplicationInsights --version 2.13.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGet から **Microsoft.ApplicationInsights** パッケージを追加します。詳細については、「[Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/2.13.0)」 を参照してください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを選択して、NuGet から **Microsoft.ApplicationInsights.AspNetCore** のバージョン 2.13.0 をインポートします。

    ```
    dotnet add package Microsoft.ApplicationInsights.AspNetCore --version 2.13.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGet から **Microsoft.ApplicationInsights.AspNetCore** パッケージを追加します。詳細については、 [Microsoft.ApplicationInsights.AspNetCore](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore/2.13.0) を参照してください。

1.  コマンド プロンプトで次のコマンドを入力し、Enter を選択して、NuGet から **Microsoft.ApplicationInsights.PerfCounterCollector** のバージョン 2.13.0 を現在のプロジェクトに追加します。

    ```
    dotnet add package Microsoft.ApplicationInsights.PerfCounterCollector  --version 2.13.0
    ```

    > **注**: **dotnet add package** コマンドは、NuGet から **Microsoft.ApplicationInsights.PerfCounterCollector** パッケージを追加します。詳細については、[Microsoft.ApplicationInsights.PerfCounterCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector/2.13.0) を参照してください。


1.  コマンド プロンプトで次のコマンドを入力し、Enter を選択して .NET Web アプリを構築します。

    ```
    dotnet build
    ```
    
#### タスク 2: HTTPS を無効にして Application Insights を使用するようにアプリケーション コードを更新する

1.  「**Visual Studio コード**」 ウインドウの 「Explorer」 ペインで、**Startup.cs** ファイルを選択してエディターでファイルを開きます。

1.  エディターの 「**Startup**」 クラスで、39 行目の次のコード行を検索して削除します。

    ```
    app.UseHttpsRedirection();
    ```

    > **注**: このコード行は、HTTPS を使用するよう Web アプリに強制します。この課題では不要です。

1.  **Startup** クラスで、この課題で以前に作成した Application Insights リソースからコピーしたインストルメンテーション キーに値が設定されている **INSTRUMENTATION_KEY** という新しい静的文字列定数を追加します。

    ```
    private const string INSTRUMENTATION_KEY = "{your_instrumentation_key}";
    ```

    > **注**: たとえば、 インストルメンテーション キーが ``d2bb0eed-1342-4394-9b0c-8a56d21aaa43``の場合、コード行は ``private const string INSTRUMENTATION_KEY = "d2bb0eed-1342-4394-9b0c-8a56d21aaa43";`` になります。

1.  **スタートアップ** クラス内で **ConfigureServices** メソッドを見つけます。

    ```
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
    }
    ```

1.  **ConfigureServices** メソッドの最後に新しいコード行を追加し、提供されたインストルメンテーション キーを使用して Application Insights を構成します。

    ```    
    services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);
    ```

1.  以下を含む必要がある **ConfigureServices** メソッドを観察します。 

    ```
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
        services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);        
    }
    ```

1.  **Startup.cs** ファイルを保存します。

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションを構築します。

    ```
    dotnet build
    ```

#### タスク 3: API アプリケーションをローカルでテストする

1.  コマンド プロンプトで次のコマンドを入力し、Enter キーを押して .NET Web アプリケーションを実行します。

    ```
    dotnet run
    ```

1.  タスク バーで、**Microsoft Edge** アイコンのコンテキスト メニューを開き、新しいブラウザー ウィンドウを開きます。 

1.  開いているブラウザー ウインドウで、ポート **5000** の **localhost** でホストされているテスト アプリケーションの **/weatherforecast** 相対パスに移動します。
    
    > **注**: 完全な URL は http://localhost:5000/weatherforecast です

1.  http://localhost:5000/weatherforecast アドレスを表示しているブラウザー ウインドウを閉じます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

#### タスク 4: Application Insights で指標を取得する

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

1.  ポータルで 「**リソース グループ**」 を選択します。 

1.  「**リソース グループ**」 ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを見つけて選択します。

1.  「**MonitoredAssets**」 ブレードで、この課題で以前に作成した **instrm*[yourname]*** Application Insights アカウントを選択します。

1.  「**Application Insights**」 ブレードから、ブレードの中央にあるタイルで、表示されている指標を確認します。具体的には、発生したサーバー要求の数と平均サーバー応答時間を確認します。

    > **注**: 要求が Application Insights の指標グラフに表示されるまでに、最大 5 分かかる場合があります。

#### レビュー

この演習では、ASP.NET を使用して API を作成し、アプリケーション指標を Application Insights にストリームするよう構成しました。次に、Application Insights ダッシュボードを使用して、API のパフォーマンスの詳細を表示しました。

### エクササイズ 3: Application Insights を使用して Web アプリを監視する

#### タスク 1: Web アプリにアプリケーションをデプロイする

1.  タスク バーで、**Visual Studio コード** アイコンを選択します。

1.  「**ファイル**」 メニューで、「**フォルダーを開く**」 を選択します。

1.  「**ファイル エクスプローラー**」 ウィンドウで、 **Allfiles (F):\\Allfiles\\Labs\\12\\Starter\\Api** を参照し、「**フォルダーの選択**」 を選択します。

1.  「Visual Studio コード」 ウインドウで、「Explorer」 ペインをクリックするか、ショートカット メニューを有効にして、「**ターミナルで開く**」 を選択します。

1.  open コマンド プロンプトで次のコマンドを入力し、Enter キーを押して Azure コマンド ライン インターフェイス (CLI) にログインします。

    ```
    az login
    ```

1.  ブラウザー ウィンドウで、次の操作を実行します:
    
    1.  Microsoft アカウントの電子メール アドレスを入力し、 [**次へ**] を選択します。
    
    1.  Microsoft アカウントのパスワードを入力し、 [**サインイン**] を選択します。

1.  現在開いているコマンド プロンプト アプリケーションに戻ります。  

    > **注**: サインイン プロセスが完了するのを待ちます。

1.  コマンド プロンプトで次のコマンドを入力して Enter を選択し、**MonitoredAssets** リソース グループ内のすべてのアプリを一覧表示します。

    ```
    az webapp list --resource-group MonitoredAssets
    ```

1.  次のコマンドを入力して Enter を選択し、プレフィックス **smpapi\*** があるアプリを見つけます。

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')]"
    ```

1.  次のコマンドを入力して Enter を選択し、プレフィックス **smpapi\*** がある単一のアプリの名前のみをレンダリングします。

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')].{Name:name}" --output tsv
    ```

1.  次のコマンドを入力して Enter を選択し、現在のディレクトリを **Allfiles (F):\\Allfiles\\Labs\\12\\Starter** ディレクトリ (デプロイ ファイルを含む) に変更します。

    ```
    cd F:\Allfiles\Labs\12\Starter\
    ```

1.  次のコマンドを入力して Enter を選択し、この課題で以前に作成した Web アプリに **api.zip** ファイルをデプロイします。

    ```
    az webapp deployment source config-zip --resource-group MonitoredAssets --src api.zip --name <name-of-your-api-app>
    ```

    > **注**: *name-of-your-api-app* プレースホルダーを、この課題で以前に作成した Web アプリの名前に置き換えます。このアプリ名は、以前のステップで最近クエリしました。   

    > **注**: この課題を進める前に、デプロイが完了するのを待ちます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  **リソース グループ** ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを選択します。

1.  **MonitoredAssets** ブレードで、 この課題で以前に作成した ***smpapi\***[yourname]*** Web アプリを選択します。

1.  **App Service** ブレードで、「**参照**」 を選択します。新しいブラウザー ウインドウまたはタブが開き、「404 (見つかりません)」エラーが返されます。

1.  ブラウザーのアドレス バーで、現在の URL の末尾にサフィックス **weatherforecast** を追加してURL を更新し、Enter を選択します。

    > **注**: たとえば、URL が https://smpapistudent.azurewebsites.net の場合、新しい URL は https://smpapistudent.azurewebsites.net/weatherforecast となります。

1.  API を使用した結果として返される JavaScript Object Notation (JSON) 配列を確認してください。

#### タスク 2: Web Apps の詳細なメトリック コレクションを構成する

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

1.  Azure potal の左側のナビゲーション ペインで、「**リソース グループ**」 を選択します。

1.  **リソース グループ** ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを選択します。

1.  **MonitoredAssets** ブレードで、 この課題で以前に作成した ***smpapi\***[yourname]*** Web アプリを選択します。

1.  **App Service** ブレードで 「**Application Insights**」 を選択します。   

1.  **Application Insights** ブレードから、次の操作を実行します。

    1.  **Application Insights** が 「**有効**」 に設定されていることを確認します。

    1.  「**アプリケーションのインストルメント化**」 セクションで 「**NET**」 タブを選択します。

    1.  「**コレクション レベル**」 セクションで 「**推奨**」 を選択 します。

    1.  「**プロファイラー**」 セクションで 「**オン**」 を選択します。

    1.  「**スナップショットのデバッガー**」 セクションで 「**オフ**」 を選択します。

    1.  「**SQL コマンド**」 セクションで 「**オフ**」 を選択します。

    1.  「**適用**」 を選択します。

    1.  確認ダイアログで 「**はい**」 を選択します。 

1.  **Application Insights** ブレードを閉じます。

1.  **App Service** ブレードに戻る場合は、「**参照**」 を選択します。新しいブラウザー ウインドウまたはタブが開き、「404 (見つかりません)」エラーが返されます。

1.  ブラウザーのアドレス バーで、現在のURLの末尾にサフィックス **/weatherforecast** を追加してURL を更新し、Enter を選択します。

    > **注**: たとえば、URL が https://smpapistudent.azurewebsites.net の場合、新しい URL は https://smpapistudent.azurewebsites.net/weatherforecast となります。

1.  API を使用した結果として返される JSON 配列を確認してください。

1.  JSON 配列へのアクセスに使用した URL を記録します。

    > **注**: 前の手順の例を使用して、URL ``https://smpapistudent.azurewebsites.net/weatherforecast`` を記録します。

#### タスク 3: Application Insights で更新された指標を取得する

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

1.  ポータルで 「**リソース グループ**」 を選択します。 

1.  「**リソース グループ**」 ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを見つけて選択します。

1.  「**MonitoredAssets**」 ブレードで、この課題で以前に作成した **instrm*[yourname]*** Application Insights アカウントを選択します。

1.  「**Application Insights**」 ブレードから、ブレードの中央にあるタイルで、表示されている指標を確認します。具体的には、発生したサーバー要求の数と平均サーバー応答時間を確認します。

    > **注**: 要求が Application Insights の指標グラフに表示されるまでに、最大 5 分かかる場合があります。

#### タスク 4: Application Insights でリアルタイムの指標を表示する

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

1.  ポータルで 「**リソース グループ**」 を選択します。 

1.  「**リソース グループ**」 ブレードで、 この課題で以前に作成した **MonitoredAssets** リソース グループを見つけて選択します。

1.  「**MonitoredAssets**」 ブレードで、この課題で以前に作成した **instrm*[yourname]*** Application Insights アカウントを選択します。

1.  **Application Insights** ブレードで、「**調査**」 セクションの 「**Live Metrics Stream**」 を選択します。

1.  タスク バーで、**Microsoft Edge** アイコンのコンテキスト メニューを開き、新しいブラウザー ウィンドウを開きます。 

1.  新しいブラウザー ウインドウで、この課題で記録済みの URL に移動します。

1.  JSON 配列の結果を確認します。

1.  Azure potal を表示しており、現在開いているブラウザー ウインドウに戻ります。

1.  更新された **Live Metrics Stream** ブレードを監視します。

    > **注**: 「**受信要求**」 セクションは数秒以内に更新され、Web アプリに対して行った要求が表示されます。

#### レビュー

この演習では、Web アプリケーションを Azure App Service にデプロイし、同じ Application Insights のインスタンスから指標を監視しました。

### 演習 4: サブスクリプションのクリーンアップ 

#### タスク 1: Azure Cloud Shell を開く

1.  Azure potalの上部で、**Cloud Shell** アイコンを選択して新しいシェル インスタンスを開きます。

    > **注**: **Cloud Shell** アイコンは、署名 (\>) アンダースコア文字 (\_) より大きく表されます。

1.  サブスクリプションを使用して Cloud Shell を初めて開く場合は、**Azure Cloud Shell へようこそウィザード** を使って、初めて使用する Cloud Shell を構成できます。ウィザードで次の操作を実行します。
    
    1.  シェルを使用して開始する新しいストレージ アカウントを作成するよう求めるダイアログ ボックスが表示されます。既定の設定を受け入れ、「**ストレージの作成**」 を選択します。 

    > **注**: Cloud Shell が初回のセットアップ手順を完了するのを待ってから、ラボを進めます。Cloud Shell の構成オプションが表示されない場合は、このコースの課題で既存のサブスクリプションを使用している可能性が高いと考えられます。新しいサブスクリプションを使用しているという前提で課題を記述します。

#### タスク 2: リソース グループを削除する

1.  次のコマンドを入力してから、Enter を選択して **MonitoredAssets** リソース グループを削除します。

    ```
    az group delete --name MonitoredAssets --no-wait --yes
    ```
    
1.  ポータルの Cloud Shell ペインを閉じます。

#### タスク 3: アクティブなアプリケーションを閉じる

1.  現在実行中の Microsoft Edge アプリケーションを閉じます。

1.  現在実行中の Visual Studio Code アプリケーションを閉じます。

#### レビュー

この実習では、この課題で使用するリソース グループを削除することで、サブスクリプションをクリーンアップしました。
