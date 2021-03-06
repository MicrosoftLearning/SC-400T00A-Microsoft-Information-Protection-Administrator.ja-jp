---
ms.openlocfilehash: 316829a7c3ad1a9aa61b13121c1df0dbc4836590
ms.sourcegitcommit: 2e9e5dd78a50682b1afef130c7c566b7d929f854
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2022
ms.locfileid: "137899423"
---
# <a name="lab-3---exercise-3---configure-service-based-retention"></a>ラボ 3 - 演習 3 - サービスベースの保持を構成する

Contoso Ltd. のシステム管理者である Joni Sherman のロールを実行します。法務部からは、不満を持った従業員が企業データを削除しないよう、サポートしてほしいと求められています。

### <a name="task-1--configure-mailbox-holds"></a>タスク 1 – メールボックスのホールドを構成する

このタスクでは、メールボックスのホールドをアクティブ化して、従業員のメールボックスからいかなるコンテンツも削除できないようにします。

1. Client 1 仮想マシン (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

2. **Microsoft Edge** で、 **https://outlook.office.com/ecp** に移動して、**Joni Sherman** として Exchange 管理センターにログインします。

3. **Exchange 管理センター** では、左側のナビゲーション ウィンドウで、 **「受信者**」、さらに **「メールボックス」** を選択します。

4. **Alex Wilber** のメールボックスを選択したら、鉛筆のアイコンを選択して、メールボックスを編集します。

5. **ユーザーメールボックスの編集** ウィンドウで、 **「メールボックスの機能」** を選択します。

6. **[訴訟ホールド:無効]** で、 **[有効にする]** を選択します。

7. **「訴訟ホールド」** ページで、次の情報を入力します。

    - **訴訟ホールドの期間 (日数)** :90
    - **注**:メールボックスはこれから 90 日間ホールドされます。 いかなるメッセージも削除することはできません。

8. **「保存」** を 2 回選択します。 **注:**  **"The hold setting may takes up to 240 minutes to take effect" (保留設定が有効になるまでに最大 240 分かかる場合があります)** という警告メッセージが表示されます。そのメッセージで **[OK]** をクリックします。

これで環境内のメールボックスでメールボックスのホールドをアクティブ化し、全員に対してメールボックス内のいかなるコンテンツも永久に削除することができないようにしました。 ホールドの適用には最大で 4 時間かかります。  直ぐに次のタスクに進むことができます。

### <a name="task-2--recover-sharepoint-documents"></a>タスク 1 – SharePoint のドキュメントを復元する

このタスクでは、ドキュメントを削除した後、削除したドキュメントを復元し、メールボックスに対して設置された訴訟ホールドについて通知を受けた従業員がドキュメントを削除しても復元できることを確認します。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。

2. **Microsoft Edge** で、 **https://www.office.com** に移動して、**Joni Sherman** として Microsoft 365 にログインします。

3. Microsoft Office 365 のランディング ページで、左上の角にあるアプリ ランチャー アイコン（9つのドット）を選択し、サブメニューから **SharePoint** を選択します。

4. SharePoint が開いたら、SharePoint サイト **Benefits @ Contoso** を選択します。

5. 左側のナビゲーション ウィンドウで **「ドキュメント」** を選択します。

6. **Vacation Policies.pptx** の前にあるチェックボックスを選択して、このファイルを強調表示にします。

7. アクション バーで、 **「削除」** を選択します。

8. **「削除しますか?」** ダイアログで **「削除する」** を選択します。

9. 左側のナビゲーション ウィンドウで **「ごみ箱」** を選択し、**Vacation Policies.pptx** の前にあるチェックボックスを選択して、このファイルを強調表示にします。

10. 上部のアクション バーで、 **「復元」** を選択します。

11. 左側のナビゲーション ウィンドウで **「ドキュメント」** を選択し、このファイルが復元されたか確認します。

SharePoint サイトの削除したドキュメントを復元することができました。

# <a name="proceed-to-lab-3---exercise-4"></a>ラボ 3 - 演習 4 に進む
