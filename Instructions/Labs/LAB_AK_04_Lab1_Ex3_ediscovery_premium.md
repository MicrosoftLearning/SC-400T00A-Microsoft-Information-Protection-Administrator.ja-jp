---
lab:
  title: 演習 3 - 電子情報開示 (Premium) を使用したケース調査
  module: Module 4 - Monitor and investigate data and activities by using Microsoft Purview
---

# ラボ 4 - 演習 3 - 電子情報開示 (Standard) とコンテンツ検索を使用したケース調査

あなたは、Contoso Ltd のコンプライアンス管理者である Joni Sherman です。同社は現在、潜在的な知的財産の盗難に関する法的調査に関与しています。 コンプライアンス管理者として、関連するすべての電子データが保持され、法的および内部的なレビュー義務を満たすためにアクセスできることを保証する責任があります。 この演習では、電子情報開示 (Premium) を使用してケースを効果的に管理し、Contoso Ltd. が調査に必要な電子証拠を提供できるようにします。

1. 電子情報開示 (Premium) ケースを作成する
1. ケースにカストディアンを追加する
1. コレクションの見積もりを作成して実行する
1. コレクションをレビュー セットにコミットする
1. レビュー セットを確認する
1. 検索結果をエクスポートする
1. 電子情報開示 (Premium) ケースを閉じる

## タスク 1 - 電子情報開示 (Premium) ケースを作成する

まず、電子情報開示 (Premium) ケースを作成して調査を開始します。 このケースは、知的財産の盗難調査に関連するすべてのアクティビティとデータの中央リポジトリになります。

1. **SC-400-cl1\admin** アカウントで Client 1 VM (SC-400-CL1) に ログインします。

1. **Microsoft Edge** で、 **`https://purview.microsoft.com`** に移動して Microsoft Purview ポータルに **Joni Sherman** `JoniS@WWLxZZZZZZ.onmicrosoft.com` としてログインします (ZZZZZZ はラボ ホスティング プロバイダーによって提供される固有のテナント ID)。

1. 左サイド バーで、**[ソリューション]** を選択し、**[電子情報開示]** を選択します。

1. **[電子情報開示]** ページの左サイド バーで、**[Premium ケース]** を展開し、**[ケース]** を選択します。

1. **[電子情報開示 (Premium)]** ページで、**[+ ケースの作成]** を選択します。

1. 右側の **[ケースに名前を付ける]** ポップアップ パネルで、次の情報を入力します。

   - **名前**: `Contoso IP Theft Investigation`
   - **説明**: `Case for the 2024 investigation into potential intellectual property theft involving relevant emails and documents.`
   - **Docket Number**: `2024-IP-INV-001`

1. [**次へ**] を選択します。

1. **[チーム メンバーを追加して設定を構成する]** ページの **[ユーザー]** フィールドで `Joni` を検索し、**Joni Sherman** を選択します。 `Megan` を検索し、**Megan Bowen** をユーザーとして追加して、Joni で調査を行います。

1. 他の値を既定値のままにして、**[次へ]** を選択します。

1. **[ケースの確認]** ページで、**[送信]** を選択します。

1. ケースが作成されたら、**[新しいケースの準備完了]** ページで **[完了]** を選択します。

これで、電子情報開示ケースが正常に作成されました。

## タスク 2 - ケースにカストディアンを追加する

ケースが作成されたので、カストディアンを追加する必要があります。 カストディアンは、調査に関連する情報を持っている可能性のある個人です。

1. Joni のアカウントで Microsoft Purview にログインしたままである必要があります。 電子情報開示 (Premium) で **Contoso IP 盗難調査**ケースの **[概要]** ページが表示されているはずです。

   そうでない場合は、`https://purview.microsoft.com` に移動し、Joni Sherman としてログインします。 **[ソリューション]** > **[電子情報開示]** > **[Premium ケース]** > **[Contoso IP 盗難調査]** を選択します。

1. 上部のナビゲーション バーから **[データ ソース]** タブを選択し、**[データ ソースの追加]** > **[新しいカストディアンを追加]** のドロップダウンを選択します。

1. **[新しいカストディアン]** ポップアップ パネルの **[カストディアンの選択]** に「`Patti`」と入力し、**PattiFerandez** を選択します。 カストディアンを追加するフィールドに「`Pradeep`」と入力し、**Pradeep Gupta** を選択して別のカストディアンを追加します。

1. [**次へ**] を選択します。

1. **[保留設定]** ページで、訴訟ホールドのために Patti と Pradeep が選択されていることを確認し、**[次へ]** を選択します。

1. [**カストディアンの確認**] ページで、[**送信**] を選択します。

1. カストディアンを選択したら、**[新しいカストディアンが作成されました]** ページで **[完了]** を選択します。

1. **[ソースの状態]**、**[インデックス作成の状態]**、**[保留状態]** のすべてが正常に完了したことが示されるまで、**[データ ソース]** ページを更新します。

これで、**Contoso IP 盗難調査**ケースにカストディアンが正常に追加されました。

## タスク 3 - コレクションの見積もりを作成して実行する

カストディアンが追加されたので、コレクションの見積もりを実行して、データ ボリュームと関連性の概要を取得できるようになりました。

1. Joni のアカウントで Microsoft Purview にログインしたままである必要があります。 電子情報開示 (Premium) の **Contoso IP 盗難調査**ケースの **データ ソース** ページに表示されている必要があります。  

   そうでない場合は、`https://purview.microsoft.com` に移動し、Joni Sherman としてログインします。 **[ソリューション]** > **[電子情報開示]** > **[Premium ケース]** > **[Contoso IP 盗難調査]** を選択します。

1. 上部のナビゲーション バーから **[コレクション]** タブを選択し、**[+ 新しいコレクション]** を選択します。

1. **[名前と説明]** ページの **[新しいコレクション]** 構成で、次のように入力します。

   - **名前**: `IP Theft Data Collection`
   - **説明**: `Collecting emails and documents relevant to the 2024 investigation into potential intellectual property theft at Contoso Ltd.`

1. [**次へ**] を選択します。

1. **[カストディアンのデータ ソースの選択]** で、**[+ カストディアンの選択]** を選択します。

1. **[カストディアンの選択]** ポップアップ パネルで、**Pradeep Gupta** と **Patti Ferandez** のチェックボックスを選択し、パネルの下部にある **[追加]** を選択します。

1. **[カストディアンのデータ ソースの選択]** ページに戻り、**[次へ]** を選択します。

1. **[非カストディアンのデータ ソースの選択]** で、**[次へ]** を選択します。

1. **[追加の場所]** で、次の場所の状態を **[オン]** に設定します。

   - Exchange メールボックス
   - Exchange パブリック フォルダー

1. [**次へ**] を選択します。

1. **[検索クエリの定義]** ページで、**[KQL エディター]** を使用するオプションを選択します。 KQL エディター ボックスに、次のように入力します。

   `(Subject:"confidential" OR Subject:"intellectual property" OR ConversationBody:"confidential" OR ConversationBody:"intellectual property" OR ConversationBody:"trade secret" OR Subject:"trade secret") AND (From:"@contoso.com" OR To:"@contoso.com")`

1. [**次へ**] を選択します。

1. **[コレクションの確認と作成]** ページで、**[送信]** を選択します。

1. コレクションの見積もりが作成されたら、**[新しいコレクションが作成されました]** ページで、**[完了]** を選択します。

1. **[コレクション]** ページに戻り、コレクションの見積もりの進行状況を確認します。 **[更新]** ボタンを使用してページを更新し、コレクションの見積もりの状態を確認します。 見積もりの状態が **[見積もり済み]** に更新され、**[プレビュー] 状態**が **[成功]** に更新されると、コレクションの見積もりが完了します。

    >**ヒント**: コレクションの見積もりが完了したら、さまざまなクエリを作成するか、KQL エディターを使用してより高度な検索を試してみてください。 これを行うには、コレクションの見積もりの左側にあるチェックボックスを選択し、**[コレクションの編集]** を選択します。 これにより、**[検索クエリの定義]** ページに直接移動します。 クエリを変更し、新しいコレクションの見積もりを送信して、クエリによってコレクションの見積もりがどのように変更されるかを確認することができます。

1. **[IP 盗難データ コレクション]** を選択し、コレクションの見積もりを確認します。

   - **[概要] タブ**: 取得された項目、ヒットがある場所、ファイルの種類など、コレクションの統計情報の概要を示します。
   - **[データ ソース] タブ**: コレクションに含まれるカストディアン データ ソースと非カストディアン データ ソースに関する情報が表示されます。
   - **[統計の検索] タブ**: 項目数やデータ量など、前回のコレクションの見積もりからの詳細な統計情報が表示されます。
   - **[コレクション オプション] タブ**: クラウドの添付ファイルや会話スレッドなど、コレクションを構成するときに使用できるさまざまなオプションを一覧表示し、説明します。

これで、**IP 盗難データ コレクション**の見積もりが正常に作成され、確認されました。

## タスク 4 – コレクションをレビュー セットにコミットします。

コレクションに問題がなければ、詳細な分析のためにレビュー セットにコミットします。

1. 引き続き、**Contoso IP 盗難調査**ケースの **[コレクション]** ページに表示されている必要があります。

   そうでない場合は、`https://purview.microsoft.com` に移動し、Joni Sherman としてログインします。 **[ソリューション]** > **[電子情報開示]** > **[Premium ケース]** > **[Contoso IP 盗難調査]** > **[コレクション]** を選択します。

1. **[IP 盗難データ コレクション]** コレクションを選択します。

1. 右側の **[IP 盗難データ コレクション]** ポップアップ パネルで、**[コレクションのコミット]** を選択します。

1. **[レビュー セットへのアイテムのコミット]** ページで、**[新しいレビュー セットに追加する]** オプションが選択されていることを確認し、`Case2024 Data Breach Review` と名前を付けます。

1. 他の既定値を選択したまま、**[コミット]** を選択して、コレクションをレビュー セットにコミットします。

コレクションがレビュー セットに正常にコミットされました。

## タスク 5 – レビュー セットを確認する

コレクションをレビュー セットにコミットした後、レビュー セットを調べて、集めたアイテムで何ができるかを確認します。

1. 引き続き、**Contoso IP 盗難調査**ケースの **[コレクション]** ページに表示されている必要があります。

   そうでない場合は、`https://purview.microsoft.com` に移動し、Joni Sherman としてログインします。 **[ソリューション]** > **[電子情報開示]** > **[Premium ケース]** > **[Contoso IP 盗難調査]** > **[コレクション]** を選択します。

1. 上部のナビゲーション バーから **[レビュー セット]** タブを選択し、新しく作成した **[Case2024 データ侵害レビュー]** レビュー セットを選択します。

1. 右側の **Case2024 データ侵害レビュー** ポップアップ パネルで、ページの下部にある **[レビュー セットを開く]** を選択します。

1. レビュー セット内のアイテムでできることについて確認します。

   - **フィルター**: 条件を適用して、レビュー セットに表示される項目を絞り込みます。
   - **タグ**: 特定のタグを使用して、ドキュメントにラベルを付けて、より適切な整理と識別を行うことができます。
   - **グループ**: 家族や会話などの関連アイテムごとにレビュー セットのコンテンツを整理できます。
   - **ソースの表示**: 選択したドキュメントを元の形式で表示し、豊富なビューを提供します。
   - **プレーンテキストの表示**: 埋め込まれた画像と書式設定を無視して、ドキュメントの抽出されたテキストを表示します。
   - **注釈**: ユーザーが文書にマークアップ、編集、その他の注釈を適用できるようにします。
   - **メタデータの表示**: 選択したドキュメントに関連付けられているさまざまなメタデータを表示して、詳細な分析情報を得ることができます。

1. レビュー セットを調べ終えたら、項目をエクスポートして詳細な分析を行うことができます。

これで、レビュー セットが正常に開いてレビューされました。

## タスク 6: 検索結果をエクスポートする

作業内容を保存して詳細な分析を有効にするには、検索結果をエクスポートします。

1. 引き続き、電子情報開示 (Premium) の **Case2024 データ侵害レビュー** レビュー セットに含まれている必要があります。

   そうでない場合は、`https://purview.microsoft.com` に移動し、Joni Sherman としてログインします。  **[ソリューション]** > **[電子情報開示]** > **[Premium ケース]** > **[Contoso IP 盗難調査]** > **[レビュー セット]** > **[Case2024 データ侵害レビュー]** > **[オープン レビュー セット]** を選択します。

1. **[Actions]** (![Actions アイコン](../Media/ediscovery-premium-action-icon.png)) のドロップダウンを選択し、**[エクスポート]** を選択します。

1. 右側の **[エクスポート オプション]** ポップアップ パネルで、次のように入力します。

   - **エクスポート名**: `Case2024_DataBreach_Export`
   - **説明**: `Export of collected emails and documents for the 2024 data breach investigation case.`
   - **これらのドキュメントをエクスポートする**: レビュー セット内のすべてのドキュメント
   - **出力オプション**: 圧縮されたディレクトリ構造

1. ポップアップ ページの下部にある **[エクスポート]** ボタンを選択します。

1. レビュー セットをエクスポートするために、**ジョブが作成された**という通知が表示されます。 この通知上の **[OK]** を選択します。

1. ジョブの状態を確認するには、左側のサイドバーから **[Premium ケース]** を展開し、**[ケース]** を選択します。 上部のナビゲーションから **[Contoso IP 盗難調査]** ケースを選択し、**[ジョブ]** タブを選択します。

   ここでは、**[Contoso IP 盗難調査]** ケースで実行されるすべてのジョブの一覧が表示されます。

1. ジョブの状態 **[エクスポートの準備]** が **[成功]** に更新されるとエクスポートが完了します。

1. エクスポートしたレビュー セットにアクセスするには、上部のナビゲーションから **[エクスポート]** タブを選択します。

1. **[Case2024_DataBreach_Export]** エクスポートを選択します。

1. 右側の **[Case2024_DataBreach_Export]** ポップアップ パネルで、エクスポートされた各ファイルの左側にあるチェック ボックスをオンにし、**[ダウンロード]** を選択します。 これにより、エクスポートされたアイテムの .csv の概要と zip ファイルがダウンロードされます。

    >**ヒント**: エクスポートされたファイルを正常にダウンロードするには、ポップアップ ブロックを無効にする必要がある場合があります。

検索結果が正常にエクスポートされ、レビューが行われます。

## タスク 7 – 電子情報開示 (Premium) ケースを閉じる

この最後のタスクでは、知的財産盗難調査の電子情報開示ケースを閉じます。 この手順では、必要なすべてのデータ収集およびレビュー タスクが完了していることを示します。

1. Microsoft Purview で、引き続き Joni Sherman としてログインする必要があります。

1. 左側のサイドバーから **[Premium ケース]** を選択し、**[ケース]** を選択します。

1. **[Contoso IP 盗難調査]** のフィールドで縦の省略記号を選択し、**[ケースを閉じる]** を選択します。

   ![電子情報開示 (Premium) でケースを閉じるためのクリック パスを示すスクリーンショット](../Media/ediscovery-premium-close-case.png)

1. ケースを閉じるとすべての保留が解除され、データが失われる可能性があることを通知する **[警告]** ダイアログを確認します。

1. 警告メッセージで **[はい]** を選択します。

1. ケースの状態は、**[クローズ]** になるまで **[クローズ中]** に更新されます。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 右上にある Joni Sherman のプロファイル画像を選択し、Joni のアカウントからサイン アウトします。 **[サインアウト]** を選択し、ブラウザー ウィンドウを閉じます。

**[Contoso IP 盗難調査]** ケースが正常に閉じられ、すべての電子情報開示タスクが完了し、ケースは次の手順に対応できるようになります。