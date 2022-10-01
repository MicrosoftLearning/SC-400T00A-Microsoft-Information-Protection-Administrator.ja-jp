---
lab:
  title: 演習 5 - 回復を目的とした電子情報開示の使用
  module: Module 3 - Implement Data Lifecycle and Records Management
ms.openlocfilehash: 18e5cc590d10cdd35f2986a989b58fa07e4d472a
ms.sourcegitcommit: 53488624251b6cf8f79f2d1ff561e3f334764821
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2022
ms.locfileid: "147694949"
---
# <a name="lab-3---exercise-5---use-ediscovery-for-recovery"></a>ラボ 3 - 演習 5 - 回復を目的とした電子情報開示の使用

この演習では、Contoso Ltd. のコンプライアンス管理者である Joni Sherman のロールを実行します。 この組織はテキサスにあり、地元の法律を守るために保持ポリシーを実装する必要があります。 "Uniform Preservation of Private Business Records Act" (事業に関する非公開記録の統一保存に関する法律) では、記録を法律の下で違反行為とならずに破棄することができると規定されています。この法律を守るために、組織は、すべてのアイテムを組織内で 3 年間保持するための保持計画を作成しました。

### <a name="task-1--create-ediscovery-case"></a>タスク 1 – 電子情報開示ケースの作成

この演習では、電子情報開示ケースを作成し、Megan Bowen が送信した Mark 8 Project に関する情報が含まれるメールの検索を開始します。 法務部は、この情報に対するコンプライアンス レビューを要求しました。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. ポータルの左側のナビゲーション ウィンドウで、 **[電子情報開示]** を展開し、 **[コア]** を選択します。

1. **[電子情報開示 (Standard)]** ページの上部で、 **[+ ケースの作成]** を選択します。

1. **[新しいケース]** ページで、 **[名前]** フィールドに「*Mark 8 Project Case*」と入力し、 **[説明]** に *「このケースは、Mark 8 Project に関する Megan Bowen のメールを評価するために使用されます。」* と入力して、 **[保存]** を選びます

1. **[コア電子情報開示 (Standard)]** ページに戻り、"**Mark 8 Project Case**" を選んでケースを開きます。

1. [ケース] ビューで、**[検索]** タブを選択します。

1. 新しい検索を開始するには、 **[+ 新しい検索]** を選択します。

1. **[名前と説明]** ページで、名前に「*Mark 8 Project*」と入力して、 **[次へ]** を選びます。

1. **[場所]** ページで、 **[Exchange メールボックス]** を **[有効]** にしてから、 **[ユーザー、グループ、チームを選択]** を選びます。

1. **[Exchange メールボックス]** ページで、「*Megan Bowen*」を検索して、Megan のメールボックスを選びます。  **[完了]** を選択します。

1. **[場所]** ページで、 **[オンプレミスのユーザー用にアプリ コンテンツを追加する]** チェックボックスをオフにして、 **[次へ]** を選びます。

1. **[キーワード]** 領域の **[検索条件の定義]** ページで、「*Mark 8*」と入力して、 **[次へ]** を選びます。

1. **[検索の確認と作成]** ウィンドウで、**[送信]** を選択します。

1. 検索を作成したら、**[完了]** を選択します。

電子情報開示ケースが正常に作成され、Megan Bowen が送信または受信した、Mark 8 Project に関する情報が含まれるすべてのメールが検索されました。

### <a name="task-2--assign-records-management-and-ediscovery-manager-permissions"></a>タスク 2 – Records Management および eDiscovery Manager のアクセス許可を割り当てる

このタスクでは、タスク 1 で見つけたデータを、法務部に提供する PST ファイルにエクスポートする準備をします。 最初に、レコード管理ロールをコンプライアンス管理者に割り当てる必要があります。 これを行わないと、検索結果をエクスポートすることができません。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 右上隅にある **Joni Sherman** の **プロファイル画像** を選んで、 **[サインアウト]** を選びます。その後、ブラウザーを閉じます。

1. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動し、Microsoft Purview ポータルに **MOD 管理者** admin@WWLxZZZZZZ.onmicrosoft.com としてログインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 管理者のパスワードは、ラボ ホスティング プロバイダーから支給されます。 

1. 左側のナビゲーション ペインで、**[アクセス許可]** を選択し、**[Microsoft Purview ソリューション]** の下にある **[役割]** を選択します。  **[Records Management]** ロールを選択します。

1. **[レコード管理]** ペインで、 **[メンバー]** カテゴリの横にある **[編集]** を選びます。

1. **[メンバーの選択]**、**[+ 追加]** の順に選択します。
 
1. 「**Joni Sherman**」を検索し、名前の前にあるチェックボックスを選択して、**[追加]** を選択します。

1. メンバー一覧が変更されていることを確認したら、**[完了]** を選択します。

1. **[保存]** 、 **[閉じる]** の順に選びます。

1. **[Role groups for Microsoft Purview solutions]\(Microsoft Purview ソリューションのロール グループ\)** で、 **[電子情報開示マネージャー]** ロールを選びます。

1. **[電子情報開示マネージャー]** ペインで、 **[電子情報開示マネージャー]** カテゴリの横にある **[編集]** を選びます。

1. **[Editing Choose eDiscovery Manager]\(電子情報開示マネージャーの選択の編集\)** ペインで、 **[電子情報開示マネージャーの選択]** を選びます。

1. **[+ 追加]** を選び、「**Joni Sherman**」を検索し、名前の前にあるチェックボックスをオンにして、 **[追加]** を選びます。

1. メンバー一覧が変更されていることを確認したら、**[完了]** を選択します。

1. **[保存]** 、 **[閉じる]** の順に選びます。

コンプライアンス管理者に、検索結果をエクスポートし、レコード管理タスクを実行するためのアクセス許可が正常に付与されました。 ユーザーにアクセス許可が適用されるまで最大 60 分かかる場合がありますが、次のタスクに進むことができます。

### <a name="task-3--export-data-from-ediscovery-case"></a>タスク 3 - 電子情報開示ケースからのデータのエクスポート

このタスクでは、タスク 1 で見つけたデータをエクスポートする準備をして、法務部に提供できるようにします。  アクセス許可がご利用のテナントで使用可能となるまでに、最大 60 分かかる可能性があることを覚えておいてください。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインしておきます。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 右上隅にある **MOD 管理者** の **プロファイル画像** を選んで、 **[サインアウト]** を選びます。その後、ブラウザーを閉じます。

1. **Microsoft Edge** を開き、 **https://compliance.microsoft.com** に移動して、Microsoft Purview ポータルに **Joni Sherman** JoniS@WWLxZZZZZZ.onmicrosoft.com としてログインします (ZZZZZZ はラボ ホスティング プロバイダーによって提供される固有のテナント ID)。  Joni のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. **Microsoft Purview** ポータルの左側のナビゲーション ウィンドウで、 **[電子情報開示]** を展開して、 **[Standard]** を選びます。

1. "**Mark 8 Project Case**" を選んで、そのケースを開きます。

1. **[検索]** タブを選択し、 **[Mark 8 Project]** の検索を選択します。

    >[!TIP]
    電子情報開示検索にデータが含まれていない場合は、検索のパラメーターを考慮してください。 Megan のメールボックスには、*Mark 8* プロジェクトに関するいくつかのメッセージが含まれているはずです。  されていない場合は、検索のキーワードを、Megan のメールボックスにある既存のメールのいずれかの用語に変更することを検討してください。  たとえば、Megan の既存のメールには、よく "planner" という用語が出現します。  エクスポート処理の対象となるものが存在するには、検索にデータが含まれている必要があります。

1. **[Mark 8 Project]** ダイアログで、 **[アクション]** ボタンのドロップダウンを選択し、 **[結果のエクスポート]** を選択します。

1. **[結果のエクスポート]** ペインの **[出力オプション]** で、オプションを確認します。  **[エクスポート]** ボタンを選択します。

    [//]: <> (LOD テナントでは要求が状態コード 500 で失敗しました - 前の M365 Dev テナントでは動作しました)

1. **[コンプライアンス]** ウィンドウが表示されたら、 **[OK]** を選びます。

1. ケース画面の **[エクスポート]** タブを選択します。  先ほど作成されたエクスポートをダブルクリックします。

1. [エクスポート] ペインの **[キーのエクスポート]** で、 **[クリップボードにコピー]** を選択し、 **[結果のダウンロード]** を選択します。
  
1. プロンプトが表示されたら、電子情報開示エクスポート ツールをインストールするために、ブラウザーで **[開く]** を選択してから、 **[インストール]** を選択します。

1. 表示されるダイアログ ボックスで、前にクリップボードにコピーしたキーを貼り付けます。  ファイルをダウンロードする適切な場所を選びます。 **[スタート]** を選択します。 

見つけたデータを正常にエクスポートしました。

### <a name="task-4--perform-search--purge-on-mailboxes"></a>タスク 4 - メールボックスでの検索と消去の実行

調査によって何人かのユーザーがフィシング メールを受信したことがわかり、あなたは、環境内のすべてのメールボックスでこのようなメールを削除する仕事を任せられました。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. Purview ポータルの左側のナビゲーション ペインで、 **[コンテンツ検索]** を選びます。

1. **「+ 新しい検索」** を選択します。

1. **[名前と説明]** ウィンドウで、 **[名前]** に「*フィッシング メールの削除*」と入力して、 **[次へ]** を選びます。

1. **[場所]** セクションで **[Exchange メールボックス]** を選んで、 **[次へ]** を選びます。

1. **[検索条件の定義]** ページの **[キーワード]** フィールドに、「*From:phishingmail@outlook.com AND subject:"Password changed"*」と入力し、**[次へ]** を選択します。

1. **[検索の確認と作成]** ウィンドウで、**[送信]** を選択します。 次に、 **[完了]** を選びます。

1. 検索を作成したら、**[セキュリティ & コンプライアンス PowerShell]** を使用して消去を開始する必要があります。 スタート メニューで、管理者として **Windows PowerShell** を実行することを選択します。

1. **[PowerShell]** ウィンドウで、次のコマンドレットを使用して、**MOD 管理者** としてサインインします。

    ```powershell
    Connect-IPPSSession
    ```

1. **PowerShell** ウィンドウで次のコマンドを入力します。

    ```powershell
    New-ComplianceSearchAction -SearchName "Phishing mail removal" -Purge -PurgeType HardDelete
    ```

1. PowerShell で Yes の「**Y**」を入力して **Enter** キーを押し、操作を確定します。

特定のメールを探すための新しいコンテンツ検索を正常に作成し、ユーザーのメールボックスからフィッシング メールを削除するために消去操作を行いました。 消去操作は、組織管理ロールのメンバーとしてのみ行うことができ、コンプライアンス管理者はこれに該当しません。

# <a name="proceed-to-lab-3---exercise-6"></a>ラボ 3 - 演習 6 に進む