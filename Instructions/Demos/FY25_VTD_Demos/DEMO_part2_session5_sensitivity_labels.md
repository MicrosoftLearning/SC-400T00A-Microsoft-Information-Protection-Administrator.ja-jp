---
lab:
  title: 'セッション 5 : Microsoft Purview Information Protection'
  module: Learning Objective - Implement and manage information protection
---

# パート 2 デモ 5: 秘密度ラベルを作成する

Microsoft 365 Copilot の導入に伴い、Contoso Ltd.の人事部は、自動的に生成されるドキュメント内の機密従業員データの保護を懸念しています。 データ セキュリティを確保するために、Microsoft Purview に秘密度ラベルを適用しています。 これらのラベルは、AI によって作成されたものを含む機密性の高い人事ドキュメントを暗号化し、アクセス制御を適用し、機密情報を保護します。

## タスク 1 – 秘密度ラベルを作成する

このタスクでは、内部ドキュメントを保護するための秘密度ラベルと、HR 従業員データ専用のサブラベルを作成します。 これらのラベルは、承認されたユーザーのみがアクセスできるようにすることで、Contoso Ltd. が従業員レコードなどの機密情報をセキュリティで保護するのに役立ちます。

1. 引き続き Client 1 VM (LON-CL1) に **SC-400-cl1\admin** アカウントでログインしている必要があります。

1. **Microsoft Edge** を開き、 **`https://purview.microsoft.com`** に移動します。 Microsoft Purview に **MOD 管理者**`admin@WWLxZZZZZZ.onmicrosoft.com`としてサインインします (ここで ZZZZZZ はラボ ホスティング プロバイダーから支給された一意のテナント ID です)。

1. Microsoft Purview ポータルの左サイドバーで、**[ソリューション]** を選択してから、**[情報の保護]** を選択します。

1. **[Microsoft Information Protection]** ページの左サイドバーで、**[秘密度ラベル]** を選択します。

1. **[秘密度ラベル]** ページで **[+ ラベルの作成]** を選択します。

1. **[新しい秘密度ラベル]** 構成が起動します。 **[このラベルの基本的な詳細を指定します]** で、次のように入力します。

    - **名前**: `Internal`
    - **表示名**: `Internal`
    - **ユーザー向けの説明**: `Internal sensitivity label.`
    - **管理者向けの説明**: `Internal sensitivity label for Contoso.`

1. [**次へ**] を選択します。

1. **[このラベルのスコープを定義]** ページで、**[アイテム]** を選択し、**[ファイル]** と **[メール]** を選択します。 **[会議]** のチェック ボックスがオンになっている場合は、選択が解除されていることを確認します。

1. [**次へ**] を選択します。

1. **[ラベル付きのアイテムの保護設定を選択する]** ページで、 **[次へ]** を選択します。

1. **[ファイルと電子メールの自動ラベル付け]** ページで、**[次へ]** をクリックします。

1. **[グループとサイトの保護設定を選択]** ページで、**[次へ]** をクリックします。

1. **[Auto-labeling for schematized data assets (preview)] (スキーマ化されたデータ アセットの自動ラベル付け (プレビュー))** ページで、**[次へ]** を選択します。

1. **[設定の確認と終了]** ページで、**[ラベルの作成]** を選択します。

1. **[秘密度ラベルが作成されました]** ページ上で、**[Don't create a policy yet]** を選択し、**[完了]** を選択します。

1. **[秘密度ラベル]** ページで、新しく作成した**内部**秘密度ラベルを見つけます。 横にある縦の省略記号 (**...**) を選択し、ドロップダウン メニューから **[+ サブラベルの作成]** を選択します。

    ![秘密度ラベルのサブラベルを作成するための [アクション] メニューを示すスクリーンショット。](/Instructions/Media/create-sublabel-button.png)

1. **[新しい秘密度ラベル]** 構成が起動します。 **[このラベルの基本的な詳細を指定します]** で、次のように入力します。

   - **名前**: `Employee data (HR)`
   - **表示名**: `Employee data (HR)`
   - **ユーザー向けの説明**: `This HR label is the default label for all specified documents in the HR Department.`
   - **管理者向けの説明**: `This label is created in consultation with Ms. Jones (Head of HR department). Contact her if changes to this label are needed.`

1. [**次へ**] を選択します。

1. **[このラベルのスコープを定義]** ページで、**[アイテム]** を選択し、**[ファイル]** と **[メール]** を選択します。 **[会議]** のチェック ボックスがオンになっている場合は、選択が解除されていることを確認します。

1. [**次へ**] を選択します。

1. [**ラベル付きのアイテムの保護設定を選択する**] ページで、[**制御アクセス権**] オプションを選択し、**[次へ]** を選択します。

1. **[アクセスの制御]** ページで **[Configure access control settings] (アクセス制御設定を構成)** を選択します。

1. 次のオプションを使用して暗号化設定を構成します。

   - **アクセス許可を今すぐ割り当てますか、それともユーザーが決定するようにしますか?** :アクセス許可を今すぐ割り当てる
   - **コンテンツに対するユーザーのアクセス許可の期限**:まったくない
   - **オフライン アクセスを許可する**:数日のみ
   - **ユーザーがコンテンツへオフラインでアクセスできる日数**:15
   - **[アクセス許可の割り当て]** リンクを選択します。 **[アクセス許可の割り当て]** ポップアップ ページで、**[+ 任意の認証済みユーザーを追加]** を選択し、**[保存]** を選択してこの設定を適用します。

1. **[アクセスの制御]** ページで、**[次へ]** を選択します。

1. **[ファイルと電子メールの自動ラベル付け]** ページで、**[次へ]** をクリックします。

1. **[グループとサイトの保護設定を選択]** ページで、**[次へ]** をクリックします。

1. **[Auto-labeling for schematized data assets (preview)] (スキーマ化されたデータ アセットの自動ラベル付け (プレビュー))** ページで、**[次へ]** を選択します。

1. **[設定の確認と終了]** ページで、**[ラベルの作成]** を選択します。

1. **[秘密度ラベルが作成されました]** ページ上で、**[Don't create a policy yet]** を選択し、**[完了]** を選択します。

内部ドキュメントの秘密度ラベルと、HR 従業員データ専用のサブラベルが正常に作成されました。

## タスク 2 : 秘密度ラベルを発行する

秘密度ラベルを作成したので、Contoso Ltd の人事スタッフが使用できるように公開します。

1. Client 1 VM (SC-400-CL1) には **SC-400-cl1\admin** アカウントでログインし、Microsoft Purview には **MOD 管理者**としてログインしておく必要があります。

1. **Microsoft Edge** で、Microsoft Purview ポータルのタブがまだ開かれているはずです。 そうでない場合は、**`https://purview.microsoft.com`** > **[ソリューション]** > **[情報保護]** > **[秘密度ラベル]** に移動します。

1. **[秘密度ラベル]** ページで **[ラベルを発行]** を選択します。

1. 秘密度ラベルの発行構成が起動します。

1. **[発行する秘密度ラベルの選択]** ページで、**[発行する秘密度ラベルの選択]** リンクを選択します。

1. **[発行する秘密度ラベル]** ポップアップ パネルで、**[社内]** と **[内部/従業員データ (HR)]** チェックボックスをオンにし、ポップアップ パネルの下部にある **[追加]** を選択します。

1. **[発行する秘密度ラベルの選択]** ページに戻り、**[次へ]** を選択します。

1. [**管理単位の割り当て**] ページで、[**次へ**] を選択します。

1. **[ユーザーとグループに発行]** ページで **[次へ]** を選択します。

1. **[ポリシー設定]** ページで **[次へ]** を選択します。

1. **[Default settings for documents] (ドキュメントの既定の設定)** で、 **[次へ]** を選択します。

1. **[Default settings for emails] (電子メールの既定の設定)** で、 **[次へ]** を選択します。

1. **[会議とカレンダー イベントの既定の設定]** で、 **[次へ]** を選択します。

1. **[Default settings for Power BI Content] (Power BI コンテンツの既定の設定)** で、 **[次へ]** を選択します。

1. **[ポリシーの名前の設定] ページ**で、以下を入力します。

   - **名前**: `Internal HR employee data`
   - **秘密度ラベル ポリシーの説明を入力してください**: `This HR label is to be applied to internal HR employee data.`

1. [**次へ**] を選択します。

1. **[確認と完了]** ページで、**[送信]** を選択します。

1. **[新しいポリシーが作成されました]** で、 **[完了]** を選択して、ラベル ポリシーの発行を完了します。

1. MOD 管理者アカウントからサインアウトします。

これで秘密度ラベルが公開され、人事チームがドキュメントで使用できるようになります。

## タスク 3 : 秘密度ラベルを適用する

このタスクでは、新しく作成した秘密度ラベルを Word のドキュメントと Outlook のメールに適用し、機密人事データが適切に保護されるようにします。

1. 引き続き Client 1 VM (LON-CL1) に **SC-400-cl1\admin** アカウントでログインしている必要があります。

1. https://www.office.com/ に移動し、**Joni Sherman**`jonis@WWLxZZZZZZ.onmicrosoft.com` として**サインイン**します (ここで ZZZZZZ はラボ ホスティング プロバイダーから支給された一意のテナント ID です)。 Joni のパスワードはデモのセットアップで設定されました。

1. **Microsoft 365 にようこそ**ページで、ページの中央にある **[新規作成]** を選択します。

1. **[ドキュメント]** を選択して、新しいドキュメントを作成します。

1. **[プライバシー オプション]** ダイアログで、**[閉じる]** を選択します。

1. 新しい空白のドキュメントに次のテキストを入力します。

   `Important HR employee document.`

1. ナビゲーション リボンから **[秘密度]** を選択し、**[社内]** > 、**[従業員データ (HR)]** の順に選択して、新しく作成した秘密度ラベルをこのドキュメントに適用します。

    ![Word に秘密度ラベル ボタンが表示されているスクリーンショット。](/Instructions//Media/word_label.png)

    >**注:** 新しく発行された秘密度ラベルがアプリケーションで使用できるようになるまで、24 から 48 時間かかる可能性があります。 新しく作成した秘密度ラベルを使用できない場合は、この演習では **[機密]** - **[全従業員]** を使用できます。

1. ドキュメントの左上にある **[ドキュメント]** を選択し、このファイルの名前を **`HR Document`** に変更します。 Enter キーを押して、この名前の変更を適用します。

    ![Web の Word でファイルの名前を変更する場所を示すスクリーンショット。](/Instructions//Media/rename-web-word-file.png)

1. タブを閉じて、[Word Online] タブに戻ります。左上のミートボール メニューを選択し、**[Outlook]** を選択して、Web で Outlook を開きます。

1. Outlook on the web で、**[新しいメール]** を選択します。

1. **"宛先"** フィールドに名前 **`Allan`** を入力し、ドロップダウン リストから **[Allan Deyoung]** を選択します。

1. 件名の行に「**`Employee data for HR`**」と入力します。

1. メールの本文に、次の内容を入力します。

    ``` text
    Dear Mr. Deyoung, 

    Please find attached the important HR employee document. 

    Kind regards,

    Joni Sherman
    ```

1. 上部のナビゲーション リボンからクリップのシンボルを選択して、添付ファイルを追加します。 **[提案されたファイル]** で **HR Document.docx** を選択します。

1. **[送信]** を選択して、ドキュメントが添付された電子メールのメッセージを送信します。

1. Joni のアカウントからサインアウトします。

従業員データ (HR) 秘密度ラベルがドキュメントと電子メールの両方に正常に適用されました。

## タスク 4 : 自動ラベル付けを構成する

このタスクでは、Microsoft 365 Copilot によって生成された場合でも、人事関連の機密性の高い従業員情報を含むドキュメントと電子メールに自動ラベルを付け、それらが自動的に保護されるようにする秘密度ラベルを作成します。

1. 引き続き Client 1 VM (LON-CL1) に **SC-400-cl1\admin** アカウントでログインしている必要があります。

1. **Microsoft Edge** で、**`https://purview.microsoft.com`** に移動して、**MOD 管理者**として Microsoft Purview ポータルにログインしてください。

1. Microsoft Purview ポータルで、左側のサイド バーから **[ソリューション]** を選択し、**[情報保護]** を選択します。 **[秘密度ラベル]** を選択します。

1. **[秘密度ラベル]** ページで、新しく作成した**内部**秘密度ラベルを見つけます。 横にある縦の省略記号 (**...**) を選択し、ドロップダウン メニューから **[+ サブラベルの作成]** を選択します。

1. **[新しい秘密度ラベル]** 構成が起動します。 **[このラベルの基本的な詳細を指定します]** で、次のように入力します。

   - **名前**: `Payroll data`
   - **表示名**: `Payroll data`
   - **ユーザー向けの説明**: `This label is for documents and emails containing payroll information.`
   - **管理者向けの説明**: `Automatically applies to any content containing payroll data.`

1. [**次へ**] を選択します。

1. **[このラベルのスコープを定義]** ページで、すべての既定の場所を選択したままにし、**[次へ]** を選択します。

1. **[ラベル付きのアイテムの保護設定を選択する]** ページで、 **[次へ]** を選択します。

1. **[ファイルと電子メールの自動ラベル付け]** ページで、**[ファイルと電子メールの自動ラベル付け]** を有効に設定します。

1. **[これらの条件に一致するコンテンツを検出する]** セクションで、**[+条件の追加]** >  を選択し、**[コンテンツに含まれている]** を選択します。

1. **[コンテンツに含まれている]** セクションで、**[追加]** > **[トレーニング可能な分類器]** を選択します。

1. **[機密情報の種類]** ポップアップ パネルで、`paystub` を検索して、**Paystub** トレーニング可能な分類子を表示します。

1. **Paystub** のチェック ボックスをオンにし、パネルの下部にある **[追加]** を選択して、この分類子を追加します。

1. [**ファイルと電子メールの自動ラベル付け**] ページで、[**次へ**] をクリックします。

1. **[グループとサイトの保護設定を選択]** ページで、**[次へ]** をクリックします。

1. **[Auto-labeling for schematized data assets (preview)] (スキーマ化されたデータ アセットの自動ラベル付け (プレビュー))** ページで、**[次へ]** を選択します。

1. **[設定の確認と終了]** ページで、**[ラベルの作成]** を選択します。

1. **[秘密度ラベルが作成されました]** ページ上で、**[Don't create a policy yet]** を選択し、**[完了]** を選択します。

1. **[秘密度ラベル]** ページに戻り、**内部**秘密度ラベルを展開し、新しく作成した **Payroll データ**サブラベルを展開します。

1. 右側の **[Payroll データ]** ポップアップ パネルで、**[自動ラベル付けポリシーの作成]** を選択します。

1. 自動ラベル付けポリシーの構成で、 **[自動ラベル付けポリシーの名前を設定]** ページに、次のように入力します。

   - **名前**: `Payroll data auto-labeling policy`
   - **説明**: `Automatically applies the Payroll Data label to sensitive payroll documents and emails.`

1. [**次へ**] を選択します。

1. [**管理単位の割り当て**] ページで、[**次へ**] を選択します。

1. **[ラベルを適用する場所を選択する]** ページで、既定値を選択したまま **[次へ]** を選択します。

1. **[共通または高度なルールの設定]** ページで **[次へ]** を選択します。

1. **[すべての場所のコンテンツのルールを定義する]** ページで、鉛筆アイコンを選択してルールを編集します。

1. 右側の **[新しいルール]** ポップアップ パネルの **[条件]** セクションの **[コンテンツに含まれている] ** [追加]** > **[トレーニング可能な分類子]**** を選択し、**Paystub**トレーニング可能な分類子をもう一度追加します。

   **なぜこれを行うのですか?** これが行われた以前は、ファイルと電子メールに自動的にラベルを付ける条件を設定していました。 これにより、SharePoint と OneDrive のファイルに自動的にラベルを付ける追加の手順が実行されます。

1. **[新しいルール]** の下部にある **[保存]** を選択します。

1. **[すべての場所のコンテンツのルールを定義する]** ページに戻り、**[次へ]** を選択します。

1. **[自動適用するラベルを選択します]** ページで、**内部/給与データ**が表示されていることを確認し、**[次へ]** を選択します。

1. [ポリシーを今すぐテストするか後でテストするかを決定する] ページで、**[シミュレーション モードでポリシーを実行する]** を選択し、**[7 日間変更されていない場合は、ポリシーを自動的にオンにする]** オプションを選択します。

1. **[次へ]** を選択して、**[作成]** を選択します。

1. **[自動ラベル付けポリシーが作成されました]** ページで、**[完了]** を選択します。

従業員の機密情報を含むドキュメントに給与データ ラベルを自動的に適用するように自動ラベル付けポリシーを構成しました。