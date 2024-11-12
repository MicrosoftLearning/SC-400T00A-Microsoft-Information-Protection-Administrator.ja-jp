---
lab:
  title: '演習 4: サービスベースの保持を構成する'
  module: Module 3 - Implement Data Lifecycle and Records Management
---

# ラボ 3: 演習 4: サービスベースの保持を構成する

Contoso Ltd. は最近、社内でいくつかの課題に直面しており、不満を持つ可能性のある従業員が重要な会社のデータの削除を試みるのではないかという懸念を抱えています。 あなたは Contoso Ltd. のコンプライアンス管理者、Joni Sherman として、機密情報をセキュリティで保護し、重要なレコードの損失を防止する必要があります。 法務部門はデータが危険にさらされる可能性がある具体的な領域を特定しており、あなたの役割は、特にメール通信と SharePoint ドキュメントに焦点を当てて、データ損失を防ぐための対策を講じることです。

**タスク:**

1. メールボックス ホールドを構成する
1. SharePoint ドキュメントを復元する

## タスク 1: メールボックス ホールドを構成する

データ損失を防ぐために、Alex Wilber のアカウントにメールボックス ホールドを適用します。

1. **SC-400-cl1\admin** アカウントで Client 1 仮想マシン (SC-400-CL1) にログインします。

1. **Microsoft Edge** で、 **`https://admin.exchange.microsoft.com`** に移動して、**Joni Sherman** として Exchange 管理センターにログインします。 `JoniS@WWLxZZZZZZ.onmicrosoft.com` としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。

1. 表示されている場合は、すべてのヒント ウィンドウを閉じます。

1. Exchange 管理センターの左側のサイド バーで、**[受信者]** を展開し、**[メールボックス]** を選択します。

1. メールボックスの一覧から **[Alex Wilber]** を選択すると、右側に Alex のメールボックス設定を表示するポップアップ パネルが表示されます。

1. **Alex Wilber** のポップアップ ページで、**[その他]** タブを選択します。

1. **[訴訟ホールド]** で、 **[Manage litigation hold] (訴訟ホールドの管理)** を選択します。

1. **[訴訟ホールドの管理]** ページで、**[訴訟ホールド]** 設定を **[オフ]** から **[オン]** に切り替えて、訴訟ホールド設定を表示します。

1. Alex のメールボックスの訴訟ホールドを構成するには、次の値を使用します。

    - **ホールド期間 (日数)**: `90`
    - **注 (ユーザーに表示する)**: `Your mailbox has been put on hold for the next 90 days. You will not be able to delete any messages.`

1. パネルの下部にある**保存**を選択します。 パネルに、**訴訟ホールドが更新された**ことを示すメッセージが表示されます。

これで環境内のメールボックスでメールボックスのホールドをアクティブ化し、全員に対してメールボックス内のいかなるコンテンツも永久に削除することができないようにしました。 ホールドの適用には最大 60 分かかる場合があります。

## タスク 2: SharePoint ドキュメントを復元する

このタスクで、あなたはドキュメントを削除し、削除したドキュメントを復元します。このタスクを通じて、メールボックスに対して訴訟ホールドが適用されたと通知を受けた従業員がドキュメントを削除しても、そのドキュメントを復元できることを確認します。

1. **SC-400-cl1\admin** アカウントで Client 1 VM (SC-400-CL1) にログインします。

1. **Microsoft Edge** で、 **`https://www.office.com`** に移動して、**Joni Sherman** として Microsoft 365 にログインします。

1. Microsoft Office 365 ランディング ページで、左上隅にあるミートボール メニューを選択し、サブメニューから **[SharePoint]** を選択します。

   ![アクション メニューを表示するための省略記号がある場所を示すスクリーンショット。](../Media/show-more-actions-sharepoint.png)

1. SharePoint ランディング ページで、「`Benefits`」を検索し、検索結果から **Benefits @ Contoso** を選択します。

1. 左側のサイド バーで **[ドキュメント]** を選択します。

1. **[ドキュメント]** ページで、**Vacation Policies.pptx** の左側にあるチェック ボックスをオンにし、操作バーから **[削除]** を選択します。

1. **[削除しますか?]** ダイアログで **[削除する]** を選択します。

1. 左側のサイド バーで **[ごみ箱]** を選択します。

1. **[ごみ箱]** ページで、**Vacation Policies.pptx** を右クリックし、**[復元]** を選択します。

1. 左側のサイド バーで **[ドキュメント]** を選択し、ファイルが復元されたことを確認します。

SharePoint サイトの削除したドキュメントを復元することができました。