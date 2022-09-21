---
ms.openlocfilehash: 868b12d70dbc7c26d12f3543c0cbed7ddaec1000
ms.sourcegitcommit: b50f9a265cf3a73ace7cbec4b5cb6f7420acc139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2022
ms.locfileid: "141151322"
---
# <a name="lab-3---exercise-4---use-ediscovery-for-recovery"></a>ラボ 3 - 演習 4 - 回復を目的とした電子情報開示の使用

この演習では、Contoso Ltd. のコンプライアンス管理者である Joni Sherman のロールを実行します。 この組織はテキサスにあり、地元の法律を守るために保持ポリシーを実装する必要があります。 「Uniform Preservation of Private Business Records Act」(事業に関する非公開記録の統一保存に関する法律) では、記録を法律の下で違反行為とならずに破棄することができると規定されています。この法律を守るために、組織は、すべてのアイテムを組織内で 3 年間保持するための保持計画を作成しました。

### <a name="task-1--create-ediscovery-case"></a>タスク 1 – 電子情報開示ケースの作成

この演習では、電子情報開示ケースを作成し、Megan Bowen が送信した Mark 8 Project に関する情報が含まれるメールの検索を開始します。 法務部は、この情報に対するコンプライアンス レビューを要求しました。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** JoniS@WWLxZZZZZZ.onmicrosoft.com としてログインしておく必要があります (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。  Joni のパスワードは、ラボ ホスティング プロバイダーから支給されます。 

2. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動して、**Joni Sherman** として Microsoft 365 コンプライアンス ポータルにログインします。

3. ポータルの左側のナビゲーション ペインで、 **[電子情報開示]** を展開し、 **[コア]** を選択します。

4. **「コア電子情報開示」** ページで **「+ ケースの作成」** を選択します。

5. **ケース名** フィールドに「*Mark 8 Project Case*」と入力し、 **「ケースの説明」** に「*このケースは、Mark 8 Project に関する Megan Bowen のメールを評価するために使用されます。* 」と入力して、 **「保存」** を選択します。

6. **[コア電子情報開示]** ページで、 **[Mark 8 Project Case]** をクリックして、そのケースを開きます。

7. 「ケース」ビューで、 **「検索」** タブを選択します。

8. 新しい検索を開始するには、 **[+ 新しい検索]** を選択します。

9. **[名前と説明]** ページで、名前として「*Mark 8 Project*」と入力し、 **[次へ]** を選択します。

10. **[場所]** ページで **[Exchange メールボックス]** を **[有効]** にし、 **[ユーザー、グループ、チームを選択]** を選択します。

11. **「メールボックスの交換」** ダイアログで、 *「Megan Bowen」* を検索し、Megan のメールボックスを選択します。  **[Done]** を選択します。

12. **「場所」** ページで、 **「オンプレミス ユーザーのアプリ コンテンツを追加する」** チェックボックスをオフにして、 **「次へ」** を選択します。

13. **「キーワード」** 領域の **「検索条件の定義」** ページで、 *「Mark 8」* と入力し、 **「次へ」** を選択します。

14. **「検索の確認と作成」** ウィンドウで、 **「送信」** を選択します。

15. 検索を作成したら、 **「完了」** を選択します。

電子情報開示ケースが正常に作成され、Megan Bowen が送信または受信した、Mark 8 Project に関する情報が含まれるすべてのメールが検索されました。

### <a name="task-2--assign-records-management-and-ediscovery-manager-permissions"></a>タスク 2 – Records Management および eDiscovery Manager のアクセス許可を割り当てる

このタスクでは、タスク 1 で見つけたデータを、法務部に提供する PST ファイルにエクスポートする準備をします。 最初に、レコード管理ロールをコンプライアンス管理者に割り当てる必要があります。 これを行わないと、検索結果をエクスポートすることができません。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

2. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動して、**MOD 管理者** として Microsoft 365 コンプライアンス ポータルにログインします。  Joni Sherman としてサインアウトする必要がある場合があります。 

3. 左側のナビゲーション ペインで、 **[アクセス許可]** を選択し、 **[コンプライアンス センター]** の下にある **[役割]** を選択します。  **[Records Management]** ロールを選択します。

4. ロールの概要ウィンドウで、 **「メンバー」** カテゴリの横にある **「編集」** を選択します。

5. **「メンバーの選択」** 、 **「+ 追加」** の順に選択します。
 
6. 「**Joni Sherman**」を検索し、名前の前にあるチェックボックスを選択して、 **「追加」** を選択します。

7. メンバー一覧が変更されていることを確認したら、 **「完了」** を選択します。

8. **[保存]** を選択します。  

9. **[eDiscovery Manager]** ロールに対して手順 3 から 8 を繰り返します。これで、Joni が将来のラボで電子情報開示データをエクスポートできるようになります。

コンプライアンス管理者に、検索結果をエクスポートし、レコード管理タスクを実行するためのアクセス許可が正常に付与されました。 ユーザーにアクセス許可が適用されるまで最大 60 分かかる場合がありますが、次のタスクに進むことができます。

### <a name="task-3--export-data-from-ediscovery-case"></a>タスク 3 - 電子情報開示ケースからのデータのエクスポート

このタスクでは、タスク 1 で見つけたデータをエクスポートする準備をして、法務部に提供できるようにします。  アクセス許可がご利用のテナントで使用可能となるまでに、最大 60 分かかる可能性があることを覚えておいてください。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインしておきます。

2. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動して、**Joni Sherman** として Microsoft 365 コンプライアンス ポータルにログインします。

3. **Microsoft 365 コンプライアンス** ポータルの左側のナビゲーション ペインで、 **[電子情報開示]** を展開し、 **[コア]** を選択します。

4. **[Mark 8 Project Case]** をクリックして、そのケースを開きます。

5. **[検索]** タブを選択し、 **[Mark 8 Project]** の検索を選択します。

**ヒント:** 電子情報開示検索にデータが含まれていない場合は、検索のパラメーターを考慮してください。  前のラボで、Megan から *Mark 8* プロジェクトに関するメールが送信されていましたか?  されていない場合は、検索のキーワードを、Megan のメールボックスにある既存のメールのいずれかの用語に変更することを検討してください。  たとえば、Megan の既存のメールには、よく "planner" という用語が出現します。  エクスポート処理の対象となるものが存在するには、検索にデータが含まれている必要があります。

6. **[Mark 8 Project]** ダイアログで、 **[アクション]** ボタンのドロップダウンを選択し、 **[結果のエクスポート]** を選択します。

7. **[結果のエクスポート]** ペインの **[出力オプション]** で、オプションを確認します。  **[エクスポート]** ボタンを選択します。

8. **[Mark 8 Project]** 検索ペインを閉じます。  

9. ケース画面の **[エクスポート]** タブを選択します。  先ほど作成されたエクスポートをダブルクリックします。

10.  [エクスポート] ペインの **[キーのエクスポート]** で、 **[クリップボードにコピー]** を選択し、 **[結果のダウンロード]** を選択します。
  
11.  プロンプトが表示されたら、電子情報開示エクスポート ツールをインストールするために、ブラウザーで **[開く]** を選択してから、 **[インストール]** を選択します。

12.  表示されるダイアログ ボックスで、前にクリップボードにコピーしたキーを貼り付けます。  ファイルをダウンロードする適切な場所を選択します。  **[スタート]** を選択します。

見つけたデータを正常にエクスポートしました。

### <a name="task-4--perform-search--purge-on-mailboxes"></a>タスク 4 - メールボックスでの検索と消去の実行

調査によって何人かのユーザーがフィシング メールを受信したことがわかり、あなたは、環境内のすべてのメールボックスでこのようなメールを削除する仕事を任せられました。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインしておきます。

2. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動して、**Joni Sherman** として Microsoft 365 コンプライアンス ポータルにログインします。

3. コンプライアンス センターの左側のナビゲーション ペインで、 **「コンテンツ検索」** を選択します。

4. [新しい検索] の **+** アイコン/ボタンを選択します。

5. **「名前と説明」** ウィンドウで、 *「フィッシング メールの削除」* と入力し、 **「次へ」** を選択します。

6. **「場所」** セクションで、 **「特定の場所」** を選択し、 **「Exchange メールボックス」** を選択して **「オン」** に切り替え、 **「次へ」** を選択します。

7. **[検索条件の定義]** ページの **[キーワード]** フィールドに、「 *From:phishingmail@outlook.com AND subject:"Password changed"* 」と入力し、 **[次へ]** を選択します。

8. **「検索の確認と作成」** ウィンドウで、 **「送信」** を選択します。 **[Done]** をクリックします。

9. 検索を作成したら、消去を開始するには、 **「セキュリティ & コンプライアンス PowerShell」** を使用する必要があります。 スタート メニューで、管理者として **Windows PowerShell** を実行することを選択します。

10. **「PowerShell」** ウィンドウで、次のコマンドレットを使用して、**MOD 管理者** としてサインインします。

    `Connect-IPPSSession`

11. **PowerShell** ウィンドウで次のコマンドを入力します。

    `New-ComplianceSearchAction -SearchName "Phishing mail removal" -Purge -PurgeType HardDelete`

12. PowerShell に「Yes」の「**Y**」を入力し、操作を確定します。

特定のメールを探すための新しいコンテンツ検索を正常に作成し、ユーザーのメールボックスからフィッシング メールを削除するために消去操作を行いました。 消去操作は、組織管理ロールのメンバーとしてのみ行うことができ、コンプライアンス管理者はこれに該当しません。

# <a name="proceed-to-lab-3---exercise-5"></a>ラボ 3 - 演習 5 に進む