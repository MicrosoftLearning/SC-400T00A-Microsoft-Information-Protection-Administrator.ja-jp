---
lab:
  title: セッション 1 - Microsoft Purview Information Protection
  module: Learning Objective - Create and manage sensitive info types
---


# デモ ラボ 1 - 機密情報の種類を管理する

## タスク 1 - カスタム機密情報の種類を作成する

この演習では、セキュリティ/コンプライアンス センター PowerShell モジュールを用い、キーワード "Employee" と "ID" に近い従業員 ID のパターンを認識するカスタム機密情報を新しく作成します。

1. 引き続き Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインしている必要があります。

1. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動し、Microsoft Purview ポータルに admin@WWLxZZZZZZ.onmicrosoft.com としてログインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 管理者のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. 左側のペインで **[データ分類]** を展開し、 **[分類子]** を選択します

1. "**データ分類とは?** " というメッセージが表示されたら、 **[閉じる]** を選択します。

1. 上部のペインから **[機密情報の種類]** を選択します。  

1. **[機密情報の種類]** タブで、 **[+ 機密情報の種類を作成]** を選択し、新しい機密情報の種類を作成するウィザードを開きます。

1. **[機密情報の種類の名前を設定]** ページで、次の情報を入力します。

    - **[名前]** : Contoso 従業員 ID
    - **[説明]** : Contoso の従業員 ID のパターン。

1. **[次へ]** を選択します。

1. **[この機密情報の種類のパターンを定義する]** ページで、**[パターンを作成する]** を選択します。

1. 右側の **[新しいパターン]** ウィンドウで、 **[+ 主要要素を追加]** を選択し、 **[正規表現]** を選択します。

1. 新しい右側の **[正規表現の追加]** ウィンドウで、次のように入力します。

    - **[ID]** : Contoso ID
    - **正規表現**: ```[A-Z]{3}[0-9]{6}```
    - *"文字列の一致"*

1. **完了** を選択します。

1. **[新しいパターン]** ポップアップ ページの **[補助要素]** で、**[+ 補助要素または要素のグループを追加]** ドロップダウン メニューを選択し、**[キーワード一覧]** を選択します。

1. 新しい右側の **[キーワード一覧の追加]** ウィンドウで、次のように入力します。

    - **ID**: 従業員 ID のキーワード
    - **大文字と小文字の区別をしない**:
        - *Employee*
        - *ID*
    - **[大文字と小文字を区別する]** フィールドで *[単語の一致]* ラジオ ボタンを選択します。

1. **完了** を選択します。

1. 新しいパターン ウィンドウで、**文字近接**値を *100* 文字に減らします。

1. **[作成]** ボタンを選択します。

1. **[この機密情報の種類のパターンを定義する]** ページに戻り、 **[次へ]** を選択します。

1. **[コンプライアンス ポリシーに表示する推奨信頼レベルの選択]** ページで、既定値を使用して **[次へ]** を選択します。

1. **[設定の確認と終了]** ページで設定を確認し、**[作成]** を選択します。 正常に作成されたら、**[完了]** を選択します。

1. ブラウザー画面は開いたままにします。

100 文字の範囲内で、3 つの大文字、6 つの数字、キーワード "Employee"、"IDs" のパターンで、従業員 ID を特定する、新しい機密情報の種類を作成しました。

## タスク 2 – EDMベースの分類情報の種類を作成する。

追加の検索パターンとして、従業員データのデータベース スキーマで完全データ一致 (EDM) ベースの分類を作成します。 データベース ソース ファイルは以下の従業員のデータ フィールドでフォーマットされます:Name、Birthdate、StreetAddress、EmployeeID。

1. 引き続き、Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **MOD 管理者**としてログインしている必要があります。

1. Microsoft Purview ポータル (https://compliance.microsoft.com ) に移動します。

1. **[データの分類]** を展開し、 **[分類子]** を選択して、上部のペインから **[EDM 分類子]** タブを選択します。

   >**注:** 完全データ一致 (EDM) ベースの機密情報の種類 (SIT) を作成して使用できるようにするのは、マルチフェーズのプロセスです。 既存のクラシック エクスペリエンスで新しいエクスペリエンスを使用できます。 このラボでは、クラシック エクスペリエンスを使用して EDM ベースの SIT を作成する手順について説明します。 新しいエクスペリエンスで EDM ベースの SIT を作成する方法の詳細については、次を参照してください:[完全データ一致の機密情報の種類のワークフローの新しいエクスペリエンスを作成する](https://learn.microsoft.com/en-us/microsoft-365/compliance/sit-create-edm-sit-unified-ux-workflow?view=o365-worldwide)

1. クラシック エクスペリエンスの場合は、 **[New EDM Experience] (新しい EDM エクスペリエンス)** のスイッチが **[オフ]** になっていることを確認します。

      ![クラシック EDM エクスペリエンスを続行するオプションのスクリーンショット。](../Media/ClassicEDMExperience.png)

1. **[EDM スキーマを作成する]** を選択します。

1. **[New EDM schema] (新しい EDM スキーマ)** ページで、次のように入力します。
    - **名前**: employeedb
    - **説明**: 従業員データベース スキーマ

1. **[すべてのスキーマ フィールドで区切り記号と句読点を無視する]** をオンにします。

1. **[すべてのスキーマ フィールドで区切り記号と句読点を無視する]** のドロップダウンをクリックし、 *[ハイフン]* 、 *[ピリオド]* 、 *[スペース]* 、 *[開きかっこ]* 、 *[閉じかっこ]* を選択します。

1. 最初の **[スキーマ フィールド名]** に「*Name*」と入力し、**[フィールドは検索可能]** ボックスにマークを付けます。

1. 下端から **[+ スキーマ データ フィールドを追加]** を選択します。

1. **[スキーマ フィールド No. 2]** で、**[スキーマ フィールド名]** に「*Birthdate*」と入力します。

1. もう一度、下端から **[+ スキーマ データ フィールドを追加]** を選択します。

1. **[スキーマ フィールド No. 3]** で、**[スキーマ フィールド名]** に「*StreetAddress*」と入力します。

1. 最後にもう一度、下端から **[+ スキーマ データ フィールドを追加]** を選択します。

1. **[スキーマ フィールド No. 4]** で、**[スキーマ フィールド名]** に「*EmployeeID*」と入力します。

1. **[フィールドは検索可能]** を選択します。

1. **[保存]** を選択します。

1. 左のウィンドウから **[EDM 機密情報の種類]** を選択します。

1. **[+ EDM 機密情報の種類を作成する]** を選択すると、**EDM ルール パッケージ** ウィザードが開きます。  

1. **[データ ストア スキーマを定義する]** ページで、**[既存の EDM スキーマを選択する]** を選択します。

1. **[employeedb]** を選択し、**[追加]** を選択します。

1. データ ストア スキーマを確認してから、**[次へ]** を選択します。

1. **[この EDM 機密情報の種類のパターンを定義する]** ページで、**[パターンを作成する]** を選択します。

1. 右側の **[新しいパターン]** ペインの [Primary element](プライマリ要素) フィールドで、*[EmployeeID]* を選択します。

1. **[主要要素の機密情報の種類]** で、 **[+ 機密情報の種類を選択する]** を選択します。

1. **検索**バーで、「*Contoso*」と入力し、Enter キーを押します。

1. **[Contoso 従業員 ID]** を選択し、**[完了]** を選択します。

1. **[新しいパターン]** ページで **[完了]** を選択します。

1. **[Define patterns for this EDM sensitive info type](この EDM 機密情報の種類のパターンを定義する)** 画面で、**[次へ]** を選択します。

1. **[推奨される信頼水準と文字の近接性を選択する]** で、既定値を維持し、**[次へ]** を選択します。

1. **[名前と EDM 機密情報の種類の説明]** ページに、次のように入力します。
    - **名前**: Contoso 従業員 EDM
    - **管理者向けの説明**: 従業員の個人情報の、EDM ベースの機密情報の種類

1. **[次へ]** を選択して、設定を確認し、**[送信]** を選択します。

1. **[EDM 機密情報の種類が作成されました]** ページで、**[完了]** を選択します。

1. Microsoft Purview ポータルのブラウザーは開いたままにします。

データベース ファイル ソースから従業員データを特定するための、EDM ベースの分類による機密情報の種類を作成しました。

## タスク 3 – キーワード辞書を作成する

個人情報漏えいの違反の中には、同僚が病欠を報告した後に、ユーザーがメールを送信した際に発生しています。  発生時には、理由に病気または疾病が送信されています。それが起こらないようにしたいのです。

1. 引き続き、Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **MOD 管理者**としてログインしている必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. 左側のペインで **[データ分類]** を展開し、**[分類子]** を選択します。 上部のペインから **[機密情報の種類]** タブを選択します。

1. **[情報の種類を作成]** を選択し、新しい機密情報の種類を作成するウィザードを開きます。

1. **[機密情報の種類の名前を設定]** ページで、次のように入力します。

    - **[名前]** : Contoso 病名の一覧
    - **[説明]** : 従業員の考えられる病名の一覧。

1. **[次へ]** を選択します。

1. **[この機密情報の種類のパターンを定義する]** ページで、**[パターンを作成する]** を選択します。

1. **[新しいパターン]** ページで **[プライマリ要素]** の下のドロップダウン フィールドを選択し、**[キーワード辞書]** を選択します。

1. **[キーワード辞書の追加]** ページで、次のように入力します。

   - **名前**: 病名の辞書
   - **キーワード**:
      - flu
      - influenza
      - cold (寒い)
      - bronchitis
      - otitis  

1. **[完了]** を選択します。

1. **[補助要素]** の下で、 **[補助要素または要素のグループを追加]** ドロップダウンを選択し、 **[キーワード リスト]** を選択して、キーワード辞書のサポートを追加します。

1. **[キーワード一覧の追加]** ページで、次のように入力します。

   - **ID**: 従業員の不在
   - **大文字と小文字の区別をしない**:
     - employee
     - absence
     - reason

1. **[完了]** を選択します。

1. **[新しいパターン]** ページで、構成を確認し、 **[作成]** を選択します。

1. **[この機密情報の種類のパターンを定義する]** で、 **[次へ]** を選択します。

1. **[コンプライアンス ポリシーに表示する推奨信頼レベルの選択]** で、既定値そのまま使用して **[次へ]** を選択します。

1. **[設定の確認と終了]** ページで、設定を確認し、 **[作成]** を選択します。  処理が完了したら、**[完了]** を選択します。

1. Microsoft Purview ポータルのブラウザー ウィンドウは開いたままにします。

キーワード辞書に基づいて新しい機密情報の種類を作成し、さらにキーワードを追加して、誤検知率を下げることができました。 次のタスクに進みます。

## タスク 5 - カスタム機密情報の種類で作業する

カスタム機密情報の種類はポリシーで利用する前に必ずテストする必要があります。テストをしなかった場合、カスタム検索のパターンが動作せず、データの損失や漏えいが発生する可能性があります。

1. 引き続き、Client 1 VM (LON-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **MOD 管理者**としてログインしている必要があります。

1. 左下の Windows シンボルを選択して、スタート メニューを開き、**[Notepad]** と入力して、スタート メニューから **[メモ帳]** を選択します。

1. メモ帳のウィンドウに次のテキストを入力します。

    ``` text
    Employee Joni Sherman EMP123456 is absent because of the flu/influenza.
    ```

1. **[ファイル]**、**[名前を付けて保存]** の順に選択します。

1. 左側のウィンドウで [ドキュメント] を選択します。

1. **[ファイル名]** フィールドに *[SickTestData]* と入力し、**[保存]** を選択します

1. メモ帳ウィンドウを閉じます。

1. **Microsoft Edge** に、Microsoft Purview ポータルのタブがまだ開かれているはずです。 その場合は、それを選択して次の手順に進みます。 閉じた場合は、新しいタブで **https://compliance.microsoft.com** に移動します。

1. 左側のナビゲーション ウィンドウで **[データ分類]** を展開し、**[分類子]** を選択します。 **[機密情報の種類]** タブを選択します。

1. 右上の **[検索]** ボックスに、「*Contoso*」と入力し、Enter キーを押します。

1. **[Contoso 従業員 ID]** を選択します。

1. **[Test]** を選択します。

1. **[テストの対象ファイルのアップロード]** ページで、**[ファイルのアップロード]** を選択します。

1. 左側のウィンドウで **[ドキュメント]** を選択し、*SickTestData* という名前のファイルを選択し、**[開く]** を選択します。

1. **[テスト]** を選択して、分析を開始します。

1. **[一致する検索結果]** のページで、見つかった一致する検索結果を確認します。

1. **[完了]** を選択してテストを終了します。

1. 上部バーのナビゲーションを使用して、 **[機密情報の種類]** に戻ります。

1. *Contoso* を検索し、 **[Contoso 病名の一覧]** という名前の機密情報の種類を選択します。

1. **[Test]** を選択します。

1. **[テストの対象ファイルのアップロード]** ペインで、 **[ファイルのアップロード]** を選択します。

1. 左側のウィンドウで **[ドキュメント]** を選択し、*SickTestData* という名前のファイルを選択し、**[開く]** を選択します。

1. **[テスト]** を選択して、分析を開始します。

1. **[一致する検索結果]** のページで、見つかった一致する検索結果を確認します。 確認が完了したら、**[完了]** を選択します。

2 つの秘密情報の種類をテストし、検索パターンが目標とするパターンを認識することを検証しました。 機密情報の種類の作成が終了しました。次の演習に進めます。
