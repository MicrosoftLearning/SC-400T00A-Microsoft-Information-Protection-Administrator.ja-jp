---
lab:
  title: 演習 1 - DLP ポリシーを管理する
  module: Module 2 - Implement Data Loss Prevention
---
# 演習 1 - DLP ポリシーを管理する

あなたは Contoso Ltd. が新しく採用したコンプライアンス管理者、Joni Sherman です。データ損失防止の目的で、組織の Microsoft 365 テナントを構成する任務を負っています。 Contoso Ltd. は米国で運転指導を提供している会社であり、顧客の機密情報が組織から流出しないようにする必要があります。

## タスク 1 - テスト モード で DLP ポリシーを作成する

この演習では、Microsoft Purview ポータルでデータ損失防止ポリシーを作成し、ユーザーによる機密データの共有を防止します。 作成する DLP ポリシーは、ユーザーがクレジット カード情報を含むコンテンツを共有したい場合に通知を行い、この情報を送信する正当な理由を提供する機会を提供します。 このブロックのアクションがユーザーに影響を与えないよう、このポリシーはテスト モードで実行されます。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

1. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動して、**Joni Sherman** として Microsoft Purview ポータルにログインします。 Joni のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. **[サインインの状態を維持しますか?]** ダイアログボックスが表示されたら、 **[今後、このメッセージを表示しない]** チェックボックスをオンにし、 **[いいえ]** を選択します。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで **[データ損失防止]** を展開し、**[ポリシー]** を選択します。

1. [**ポリシー**] ページで [**+ ポリシーの作成**] を選択し、新しいデータ損失防止ポリシーを作成するウィザードを起動します。

1. **[テンプレートの利用またはカスタム ポリシーの作成]** ページで、下にスクロールし、 **[カテゴリ]** で **[カスタム]** を選択し、 **[テンプレート]** で **[カスタム ポリシー]** を選択します。 既定では、どちらのオプションも既に選択されています。 **[次へ]** を選択します。

1. **[DLP ポリシーの名前の設定]** ページで、以下を入力します。

   - **名前**: クレジット カードの DLP ポリシー
   - **説明**: クレジット カード番号が共有されないよう保護する

1. **[次へ]** を選択します。

1. [**管理単位の割り当て**] ページで、[**次へ**] を選択します。

1. **[ポリシーを適用する場所の選択]** ページで **[Teams のチャットおよびチャネル メッセージ]** オプションのみを [有効] にし、 **[次へ]** を選択します。

1. **[ポリシー設定の定義]** ページで、 **[高度な DLP ルールを作成またはカスタマイズする]** を選択し、 **[次へ]** を選択します。

1. **[詳細な DLP ルールをカスタマイズする]** ページで、**[+ ルールの作成]** を選択します。

1. **[ルールの作成]** ポップアップ ページの **[名前]** フィールドに、 _「クレジット カード情報」_ と入力します。

1. **[条件]** で、**[+ 条件の追加]** を選択し、ドロップダウン メニューから **[コンテンツに含まれている]** を選択します。

1. 新しい **[コンテンツに含まれている]** 領域で、 **[追加]** を選択し、ドロップダウン メニューから **[機密情報の種類]** を選択します。

1. **[機密情報の種類]** ページで **[クレジット カード番号]** を選択し、**[追加]** を選択します。

1. **[ルールの作成]** ページで **[+ 条件の追加]** を選択し、ドロップダウン メニューから **[Microsoft 365 からコンテンツを共有する]** を選択します。

1. **[Microsoft 365 からコンテンツを共有する]** セクションで、 **[組織内の連絡先のみ]** オプションを選択します。

1. **[ルールの作成]** ページで、 **[+ アクションの追加]** を選択します。 **[Use actions to protect content when the conditions are met.] (アクションを使用して、条件が満たされた場合にコンテンツを保護します。)** で、 **[Microsoft 365 の場所にあるコンテンツへのアクセスを制限またはコンテンツを暗号化する]** を展開して、 **[すべてのユーザーをブロックします。]** を選択します。

1. **[ルールの作成]** ページの **[ユーザーへの通知]** セクションで、スイッチを **[オン]** にしてユーザーへの通知を有効にします。

1. チェック ボックスをオンにして、 **[Notify users in Office 365 service with a policy tip] (ポリシー ヒントを使用して Office 365 サービスでユーザーに通知する)** を有効にします。

1. **［ユーザーによる上書き** で、**M365 サービスからの上書きを許可します。Exchange、Sharepoint、OneDrive、Teams でのユーザーによるポリシー制限の上書きを許可します。** のチェックボックスをオンにします。

1. **[上書きするには業務上の理由が必要です]** チェックボックスをオンにします。

1. **[インシデント レポート]** セクションの **[管理者のアラートとレポートでこの重大度レベルを使用する]** ドロップダウンで **[低]** を選択します。

1. **[ルールの作成]** ページで **[保存]** を選択し、 **[次へ]** を選択します。

1. [**ポリシー モード**] ページで、[**テスト モードでポリシーを実行する**] を選択し、[**シミュレーション モード中にポリシー ヒントを表示する**] を選択し、[**次へ**] を選択します。

1. **[ポリシーの確認と作成]** ページで設定を確認し、 **[送信]** を選択します。

1. **[新しいポリシーが作成されました]** ページで、 **[完了]** を選択します。

これで、Microsoft Teams のチャットおよびチャンネルでクレジット カード番号をスキャンし、ポリシーをオーバーライドする業務上の正当な理由をユーザーが提供できるようにする DLP ポリシーが作成されました。

## タスク 2 - DLP ポリシーを修正する

このタスクでは、前の手順で作成した既存の DLP ポリシーを変更して、メールでもクレジット カード情報をスキャンし、メール内のこのコンテンツをユーザーが共有する必要がある場合、ユーザーに通知します。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで **[データ損失防止]** を展開し、**[ポリシー]** を選択します。

1. [**ポリシー**] ページで、先ほど作成した [**クレジット カードの DLP ポリシー**] の横にあるチェック ボックスをオンにし、[**ポリシーの編集**] を選択してポリシー ウィザードを開きます。

1. **[DLP ポリシーの名前の設定]** ページで **[次へ]** を選択します。

1. [**管理単位の割り当て**] ページで、[**次へ**] を選択します。

1. **[ポリシーを適用する場所を選択する]** ページで、**[Exchange メール]** オプションを有効にしたら、**[ポリシーの確認と作成]** ページが開くまで **[次へ]** を選択します。

1. **[送信]** を選択して、行った変更をポリシーに適用します。

1. ポリシーが更新されたら、**[完了]** を選択します。

既存の DLP ポリシーが修正され、コンテンツを探してスキャンする場所が変更されました。

## タスク 3 - PowerShell に DLP ポリシーを作成する

このタスクでは、PowerShell を使用して、Contoso EmployeeID を保護し、それらが Exchange で共有されるのを防止する DLP ポリシーを作成します。 ユーザーには、機密データが共有されようとしていることと、Contoso EmployeeID が含まれるメールの送信はブロックされることが通知されます。

1. 引き続き Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインしている必要があります。

1. スタート メニューで、**Windows PowerShell** を選択します。

1. 次のコマンドレットを入力して、Exchange Online PowerShell モジュールの最新版をインストールします。

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. NuGet プロバイダー セキュリティ ダイアログで、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。 この処理は、完了までに時間がかかる場合があります。

1. 信頼されていないレポジトリ セキュリティ ダイアログで、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。 この処理は、完了までに時間がかかる場合があります。

1. 次のコマンドレットを入力して実行ポリシーを変更し、**Enter** キーを押します。

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

1. **PowerShell** ウィンドウで、次のように入力し、

    ```powershell
    Connect-IPPSSession
    ```

   次に、**Joni Sherman**JoniS@WWLxZZZZZZ.onmicrosoft.com としてサインインします。 Joni のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. 次のコマンドを PowerShell に入力し、すべての Exchange メールボックスをスキャンする DLP ポリシーを作成します。

    ```powershell
    New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
    ```

1. 次のコマンドを PowerShell に入力し、前のステップで作成した DLP ポリシーに DLP ルールを追加します。

    ```powershell
    New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
    ```

1. 次のコマンドを使用して、"**EmployeeID の DLP ルール**" を確認します。

    ```powershell
    Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
    ```

これで、PowerShell を使用して Exchange で Contoso EmployeeID をスキャンする DLP ポリシーが作成されました。

## タスク 4 - DLP ポリシーをテストする

このタスクでは、前のタスクで作成した DLP ポリシーをテストします。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には Joni Sherman としてログインしておく必要があります。

1. Microsoft Edge ブラウザー ウィンドウを開き、 **https://outlook.office.com/** に移動します。

1. 左上にある **[新しいメール]** ボタンを選択して、新しいメール メッセージを作成します。

1. **[宛先]** フィールドに 「_Megan_」と入力し、**Megan Bowen** のメール アドレスを選択します。

1. [件名] フィールドに、 _「従業員情報に関するヘルプ」_ と入力します。

1. メールの本文には、次の内容を入力します。

    ``` text
    Please help me with the start dates for the following employees:
    ABC123456
    DEF678901
    GHI234567

    Thank you, 
    Joni Sherman
    ```

1. メッセージ ウィンドウの右上にある **[送信]** ボタンを選択して、メールを送信します。

1. メールが配信不能であり、DLP ポリシーによってブロックされたことを示すメッセージを受信します。

      ![[ロールの管理] オプションのスクリーンショット](../Media/dlp-email-blocked.png)

これで、DLP ポリシーのテストに成功しました。

## タスク 5 - テスト モードでポリシーをアクティブにする

このタスクでは、テストモードで作成したクレジット カード情報の DLP ポリシーをアクティブ化し、保護アクションを強化します。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで **[データ損失防止]** を展開し、**[ポリシー]** を選択します。

1. [**ポリシー**] ページで [**クレジット カードの DLP ポリシー**] の横にあるチェック ボックスをオンにし、[**ポリシーの編集**] を選択してポリシー ウィザードを開きます。

1. **[ポリシー モード]** ページが表示されるまで **[次へ]** を選択し、 **[すぐに有効にする]** を選択します。

1. **[ポリシーの確認と作成]** で **[送信]** を選択します。

1. **[Policy updated] (ポリシーが更新されました)** ページで、 **[完了]** を選択します。

DLP ポリシーがアクティブ化されました。 ポリシーはクレジット カード情報を共有しようとする試みを探知すると、それをブロックし、ユーザーにはそのブロックのアクションをオーバーライドする業務上の正当な理由を提供することを許可します。

## タスク 6 - ポリシーの優先順位を修正する

DLP ポリシーを 2 つ作成したところで、より制限の厳しいポリシーが、より制限の緩いポリシーより優先して処理されるようにします。 このため、EmployeeID の DLP ポリシーにより高い優先順位を与えます。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで **[データ損失防止]** を展開し、**[ポリシー]** を選択します。

1. **[ポリシー]** タブで **[EmployeeID の DLP ポリシー]** の横にある 3 つの縦向きドットを選択し、 **[アクション]** の選択項目を開いて **[先頭へ移動]** を選択します。

1. **[データ損失防止]** ウィンドウで、 **[更新]** を選択し、[ポリシー] タブの **[順序]** の列で優先順位を確認します。

1. 右上にある Joni のプロフィール画像を含む円を選択し、[**サインアウト**] を選択して、次の演習のために Joni のアカウントからサインアウトします。

DLP ポリシーの優先順位が修正されました。 両方のポリシーが同じコンテンツに一致する場合、より高い優先順位を持つアクションが実行されます。