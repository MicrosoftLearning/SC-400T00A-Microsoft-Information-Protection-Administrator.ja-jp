---
lab:
  title: 演習 3 - トレーニング可能な分類器を管理する
  module: Module 1 - Implement Information Protection
---

# ラボ 1: 演習 3: トレーニング可能な分類器を管理する

Contoso Ltd. は、"Sales and Marketing" SharePoint サイトに格納されている財務ドキュメントとレポートが適切に分類されていることを確認する必要があります。 これを実現するには、これらのファイルを認識してラベル付けするためのトレーニング可能な分類子を作成する必要があります。

## タスク 1 – トレーニング可能な分類子を作成する

このタスクでは、テナントでトレーニング可能な分類子をアクティブ化して、カスタム分類子の作成を有効にします。

1. Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** で、 **`https://compliance.microsoft.com`** に移動します。

1. 左側のナビゲーション ウィンドウで **[データ分類]** を展開し、**[分類子]** を選択します。

1. **[分類子]** ページで、**[トレーニング可能な分類子]** タブが既に選択されている必要があります。

2. **[+ トレーニング可能な分類器を作成する]** を選択し、新しい分類器を作成します。

1. **[トレーニング可能な分類器の名前と説明]** ページで次の情報を入力します。

    - **名前**: `Contoso Company Data`
    - **説明**: `Trainable classifier for company data produced and stored by Contoso Ltd.`

1. [**次へ**] を選択します。

1. **[正のサンプル コンテンツのソース**] で、**[ サイトの選択**] を選択します。

1. 右側の**SharePoint サイトの追加**のポップアップ ページで、次の SharePoint サイトを選択します。

    - Mark8ProjectTeam

1. ポップアップ ページの下部にある **[追加]** を選択します。

1. **[正のサンプル コンテンツのソース**] ページに戻り **[次へ]** を選択します。

1. **[負のサンプル コンテンツの ソース]** ページで、次の SharePoint サイトを選択します。

    - HR

1. ポップアップ ページの下部にある **[追加]** を選択します。

1. **[負のサンプル コンテンツのソース**] ページに戻り **[次へ]** を選択します。

1. **[分類子をレビューして作成しサンプル コンテンツの処理を開始する]** で **[トレーニング可能な分類子の作成]** を選択します。

1. **[分類子のトレーニング中です]** ページで、**[Done]** を選択します。

選択した SharePoint サイトのドキュメントとファイルは現在分析されています。分析には最大で48 時間かかります。

<!---
## Task 3 – Publish a trainable classifier (optional lab task)

After the new trainable classifier was created and the initial analysis of the documents and files is done, the manual training process needs to be performed. In this task, Joni will start the calibration of the classifier to achieve the required accuracy for publishing.

1. You should still be logged into your Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.

1. In your browser window, you are in the Microsoft Purview portal at **Data classification** in the **Trainable classifiers** tab.

1. Select the trainable classifier with the name **Contoso Company Data** of the type **Custom** to open the detailed settings.

1. Review the **Details** tab on the right side, including the source site for the classifier, the number of processed items and the **Status**, which is in **Need test items**.

1. To add items for training the classifier, select **Add items to test** to open the right side selection pane.

1. In the **Choose sites with items to test** pane, select **+ Choose sites**.

1. Select the following SharePoint sites:

    - **Communication site**
    - **News @ Contoso**
    - **Contoso Web 1**
    - **Brand**
    - **Digital Initiative Public Relations**
    - **Work @ Contoso**
    - **Sales and Marketing**
    - **Contoso Landings**
    - **Mark 8 Project Team**
    - **HR**
    - **Operations**
    - **Retail**
    - **PointPublishing Hub Site**
    - **Team Site**
    - **Leadership Team**
    - **Community**
    - **Give @ Contoso**
    - **Benefits @ Contoso**
    - **Learn @ Contoso**
    - **Campaigns - Events**

1. Select **Add**.

1. Wait until the sites are shown in the list and select **Add**.

1. When the **Overview** section is updated, a new tab is shown in the top of the window.

1. Select **Tested items to review** from the top pane.

1. It will take between 15 to 30 minutes until first results are ready for review. Refresh the browser window if no files are shown in the list, until data is available.

1. Select the name of the first file from the list to open the preview window.

1. When the **Prediction** row is equal to **Match**, the file was identified as a match for the classifier. Below the preview window, a message **We predict this item "matched" this classifier.** is shown. Select **Match** to approve the automatic classification.

1. When the **Prediction** row is equal to **Not a match**, the file was identified not as a match for the classifier. Below the preview window, a message **We predict this item "does not match" this classifier.** is shown. Select **Not a match** to approve the automatic classification.

1. Proceed with all items in the list and approve the automatic classification. After all items have been reviewed, select **Overview** from the top pane and **Tested items to review** again, to load the next set of items for review.

1. For each 30 reviewed items an **Auto-retrain performed** window is shown. Select **OK** and proceed with the previous steps, until no items for review are left.

1. After sufficient items are reviewed, the **Publish** button in the upper right gets available. Select it as soon it is available.

1. In the **Publish classifier** window, select **Yes** to publish the classifier.

1. When the right side pane with **Your trainable classifier has been published** is displayed, the trainable classifier was successfully published.

1. Close the right side pane with the **X** in the upper right.

1. Back at the main site, the custom classifier was moved to **Published** and the **Status** has been changed to **Ready to use**.

1. Leave the browser window open.

You have successfully created, trained, and published a custom trainable classifier that matches the files stored on the existing SharePoint sites of Contoso Ltd.
