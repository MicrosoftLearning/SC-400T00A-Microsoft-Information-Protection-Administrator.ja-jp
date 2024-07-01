---
lab:
  title: 演習 1 - 保持ポリシーを構成する
  module: Module 3 - Implement Data Lifecycle and Records Management
---

## WWL テナント - 使用条件

講師が指導するトレーニング配信の一環としてテナントを提供されている場合は、講師が指導するトレーニングでハンズオンラボをサポートする目的でテナントを利用できることに注意してください。

テナントを共有したり、ハンズオンラボ以外の目的で使用したりしないでください。 このコースで使われるテナントは試用版テナントであり、クラスが終了し、拡張機能の対象となっていない場合は、使用したりアクセスしたりすることはできません。

テナントを有料サブスクリプションに変換することはできません。 このコースの一環として取得したテナントは Microsoft Corporation の財産のままであり、当社はいつでもアクセス権とリポジトリを取得する権利を留保します。

# ラボ 3 - 演習 1 - 保持ポリシーを構成する

この演習では、Contoso Ltd. のシステム管理者である Joni Sherman のロールを実行します。 この企業はテキサスを本拠地としており、記録は 3 年を経過したら削除しても違法ではない、という州法を遵守するために保持ポリシーを実装する必要があります。

この法律を遵守するために、組織ではすべてのアイテムを 3 年間保持する保持計画を作成しています。

## タスク 1 – 全社的な保持ポリシーを作成する

この演習では、全社的な保持ポリシーを作成し、保持期間を適用し、ポリシーを適用する場所を設定します。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

1. **Microsoft Edge** で、 **`https://compliance.microsoft.com`** に移動して Microsoft Purview ポータルに **Joni Sherman** JoniS@WWLxZZZZZZ.onmicrosoft.com としてログインします (ZZZZZZ はラボ ホスティング プロバイダーによって提供される固有のテナント ID)。  Joni のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで、**[データ ライフサイクル管理]** を展開して **[Microsoft 365]** を選択します。

1. **[データ ライフサイクル管理]** ページの **[保持ポリシー]** タブで、 **[+ 保持ポリシーの新規作成]** を選択します。

1. **[保持ポリシーの名前を設定]** ページの **[名前]** と **[説明]** に、次の情報を入力します。

    - **名前**: 会社全体
    - **説明**: Teams を除くすべての場所

1. **[次へ]** ボタンを選択します。  

1. **[Policy Scope] (ポリシー スコープ)** ページで、**[次へ]** を選択します。

1. **[作成するアイテム保持ポリシーの種類を選択する]** 領域で、 **[静的]** を選択し、 **[次へ]** を選択します。

1. **[Choose where to apply this policy] (このポリシーを適用する場所の選択)** で、次を有効にします。

   - **Exchange メールボックス**
   - **SharePoint クラシック サイトとコミュニケーション サイト**
   - **OneDrive アカウント**
   - **Microsoft 365 グループのメールボックスとサイト**

1. [**次へ**] を選択します。

1. **[コンテンツを保持するか、削除するか、またはその両方を行うかを決定する]** ページで、**[特定の期間のアイテムを保持する]** セクションで、次の情報を入力します。

   - **アイテムを特定の期間保持する**: ドロップダウン リストから **[カスタム]** を選択します
   - [年] フィールドを **[3]** に変更します。
   - **保持期間開始の条件**:アイテムが最後に変更されたとき
   - **[保持期間の終了時]** :アイテムを自動的に削除する

1. [**次へ**] を選択します。

1. **[確認と完了]** ページで、**[送信]** を選択します。

1. ポリシーを作成したら、 **[完了]** を選択します。

Exchange メール、Microsoft 365 グループ、OneDrive、SharePoint サイトの場所に対する保持ポリシーが正常に作成されました。 この保持ポリシーでは、これらの場所にあるアイテムを、アイテムの最終変更日から 3 年間保持します。 このポリシーがテナントに適用されるまでに最大 24 時間かかる場合がありますが、次のステップに進むことができます。

## タスク 2 – フィルター付きの、場所に基づく保持ポリシーを作成する

ここでは、Teams の場所の保持ポリシーを作成します。 Teams のチャネルにはドキュメントを含めることができるで、それらはすべて保持されます。 組織では、限られた数のユーザーに Teams のチャットの保持期間を要求することにしました。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **`https://compliance.microsoft.com`** に移動します。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで、**[データ ライフサイクル管理]** を展開して **[Microsoft 365]** を選択します。

1. **[データ ライフサイクル管理]** ページの **[保持ポリシー]** タブで、 **[+ 保持ポリシーの新規作成]** を選択します。

1. **[保持ポリシーの名前を設定]** ページの **[名前]** と **[説明]** に、次の情報を入力します。

   - **[名前]** : Teams 保持
   - **[説明]** : Teams の場所に対する保持

1. [**次へ**] を選択します。

1. **[Policy Scope] (ポリシー スコープ)** ページで、**[次へ]** を選択します。

1. **[作成するアイテム保持ポリシーの種類を選択する​]** ページで、 **[静的]** を選択してから、 **[次へ]** を選択します。

1. **[ポリシーを適用する場所の選択]** ページで、次を有効にします。

   - **Teams チャネル メッセージ**
   - **Teams チャット**
   - 他のすべての場所は無効のままにします。

1. [場所]: **[Teams のチャット]** で、 **[すべてのユーザー]** の下のテキスト リンクで **[編集]** を選択します。

1. **[Teams のチャット]** ポップアップ ページでユーザーを追加します。

    - Adele Vance
    - Pradeep Gupta

    >**注**: これら 2 人のユーザーを追加すると、 **[Teams のチャット]** の **[含まれる]** の設定が *[すべてのチーム]* から *[2 人のユーザー]* に変更されます。

1. **[完了]** を選択してから、 **[次へ]** を選択します。

1. **[コンテンツを保持するか、削除するか、またはその両方を行うかを決定する]** ページで、**[特定の期間のアイテムを保持する]** セクションで、次の情報を入力します。

   - **アイテムを特定の期間保持する**: ドロップダウン リストから **[カスタム]** を選択します
   - [年] フィールドを **[3]** に変更します。
   - **保持期間開始の条件**:アイテムが最後に変更されたとき
   - **[保持期間の終了時]** :アイテムを自動的に削除する

1. [**次へ**] を選択します。

1. **[確認と完了]** ページで、**[送信]** を選択します。

1. **[You successfully created a retention policy] (アイテム保持ポリシーが正常に作成されました)** ページで、**[完了]** を選択します。

Teams の場所に対する保持ポリシーが正常に作成されました。 すべての Teams チャネルの場所に 3 年間の保持期間を設定しました。 特定のユーザーにのみ適用されるように、Teams チャットの場所のフィルターを設定しました。

## タスク 3 – PowerShell で保持ポリシーを作成する

PowerShell を使用して同じ保持ポリシーを作成します

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

1. マウスの右ボタンで Windows ボタンを選択して管理者特権で PowerShell ウィンドウを開き、**[Windows PowerShell (管理者)]** を選択します。[ユーザー アカウント制御] ウィンドウが表示されたら、**[はい]** を選択します。

1. 次のコマンドレットを使用して、テナントのセキュリティ/コンプライアンス センターに接続します。

    ```powershell
    Connect-IPPSSession
    ```

1. サインインを要求するダイアログ ボックスが表示された場合は、**MOD 管理者** admin@WWLxZZZZZZ.onmicrosoft.com としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。  管理者のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. 次のコマンドレットを実行して、Teams を除くすべての場所に対する最初の保持ポリシーを作成します。

    ```powershell
    New-RetentionCompliancePolicy -Name "Company Wide PS" -ExchangeLocation All -ModernGroupLocation All -SharePointLocation All -OneDriveLocation All
    ```

1. 次のコマンドレットを実行して、保持期間を設定します。単位は、変更日を基準にした日数を使用します。

    ```powershell
    New-RetentionComplianceRule -Name "Company Wide PS Rule" -Policy "Company Wide PS" -RetentionDuration 1095 -ExpirationDateOption ModificationAgeInDays -RetentionComplianceAction Keep
    ```

1. 次のコマンドレットを実行して、Teams の場所に対する 2 つ目の保持ポリシーを作成します。

    ```powershell
    New-RetentionCompliancePolicy -Name "Teams Retention PS" -TeamsChannelLocation All -TeamsChatLocation "Adele Vance", "Pradeep Gupta"
    ```

1. 次のコマンドレットを実行して、日数を単位として保持期間を設定します。

    ```powershell
    New-RetentionComplianceRule -Name "Teams Retention PS Rule" -Policy "Teams Retention PS" -RetentionDuration 1095 -RetentionComplianceAction Keep
    ```

PowerShell を使って保持期間を 3 年に設定した保持ポリシーを正常に作成しました。

<!-- ## Task 4 – Create Retention Policy with adaptive scope

In this exercise you will create a retention policy for the finance and legal department. The purpose of the policy is to comply with the law, retaining all legal related documents for 5 years. First you will create an adaptive scope including the legal and the retail department, then you will create a retention policy using this scope.

1. You should still be logged into Client 1 VM (LON-CL1) as the **lon-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.

1. In **Microsoft Edge**, the Microsoft Purview portal tab should still be open. If so, select it and proceed to the next step. If you closed it, then in a new tab, navigate to **`https://compliance.microsoft.com`**.

1. In the **Microsoft Purview** portal on the left navigation pane expand **Roles & scopes** then select **Adaptive scopes**.

1. On the **Adaptive scopes** page select **+ Create scope**.

1. On the **Name your adaptive policy scope** page input:

    - **Name**: Legal Documents Retention
    - **Description**: Retention for legal related documents

1. Select **Next**.

1. On the **Assign admin unit** page select **Next**.

1. On the **What type of scope do you want to create?** page select **Users** then select **Next**.

1. On the **Create the query to define users** page, under **User attributes** select the drop-down menu for **Attribute** then select **Department**.

1. Directly next to the attribute field select **is equal to** as the operator.

1. Input **Legal** in the **Value** field.

1. To add a second attribute, select **+ Add attribute** on the **Create the query to define users** page.

1. For the **Query operator**, **Attribute**, **Operator**, and **Value** input:

   - **Query operator**: Or
   - **Attribute**: Department
   - **Operator**: is equal to
   - **Value**: Retail

1. Ensure the checkboxes are selected next to each attribute then select **Next**.

1. On the **Review and finish** page select **Submit**.

1. On the **Your scope was created page** select **Done**.

1. In the **Microsoft Purview** portal, in the left navigation pane, expand **Data lifecycle management** then select **Microsoft 365**.

1. On the **Data lifecycle management** page select the **Retention policies** tab then select **+ New retention policy**.

1. On the **Name your retention policy** page input:

    - **Name**: Legal Data Retention
    - **Description**: Retention of all documents within the legal and retail departments.

1. Select **Next**.

1. On the **Policy Scope** page select **Next**.

1. On the **Choose the type of retention policy to create** page select **Adaptive** then select **Next**.

1. On the **Choose adaptive policy scopes and locations** page select **+ Add scopes**.

1. In the right flyout **Choose adaptive policy scopes** page select the checkbox for **Legal Documents Retention** then select the **Add** button.

1. Back on the **Choose locations to apply the policy** enable:

    - **Exchange mailboxes**
    - **OneDrive accounts**
    - Leave all other locations disabled.

1. Select **Next**.

1. On the **Decide if you want to retain content, delete it, or both** page, for the **Retain items for a specific period** section input:

    - **Retain items for a specific period**: 5 years
    - **Start the retention period based on**: When items were created
    - **At the end of the retention period**: Do nothing

1. Select **Next**.

1. On the **Review and finish** page select **Submit**.

1. Once your policy is created, select the **Done** button.

1. On the **You successfully created a retention policy** page select **Done**.

You have successfully applied an adaptive scope to a retention policy.

## Task 5 – Test adaptive scope policy

In this exercise you will verify the users affected by the adaptive scope and test the new adaptive retention policy.

>**Note**: When you create and submit a retention policy, it can take up to seven days for the retention policy to be applied.

1. To review the details of the adaptive scope retention policy, logged into  **lon-cl1\admin**, open a PowerShell window by selecting the Windows button with the right mouse button and then select Windows PowerShell.

1. Connect to the Security & Compliance Center in your tenant with the following cmdlet:

    ```powershell
    Connect-IPPSSession
    ```

1. If prompted with a sign in dialog box, sign in with Joni Sherman's account,  JoniS@WWLxZZZZZZ.onmicrosoft.com (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.

1. Run the following cmdlet to view all details of the adaptive scope policy:

    ```powershell
    Get-RetentionCompliancePolicy -Identity "Legal Data Retention"     -DistributionDetail | Format-List
    ```

1. Review the details. Certain parameters should have following statuses:

    - **Enabled**: True
    - **Mode**: Enforce
    - **DistributionStatus**: Success

You have verified the success of your adaptive scope.-->
