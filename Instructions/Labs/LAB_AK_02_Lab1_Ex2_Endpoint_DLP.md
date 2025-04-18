---
lab:
  title: 演習 2 - エンドポイント DLP を管理する
  module: Module 2 - Implement Data Loss Prevention
---

# ラボ 2 - 演習 2 - エンドポイント DLP を管理する

あなたは Contoso Ltd. が新しく採用したコンプライアンス管理者、Joni Sherman です。データ損失防止の目的で、組織の Microsoft 365 テナントを構成する任務を負っています。 Contoso Ltd. は米国で自動車運転教習を行っている企業です。あなたには機密の顧客情報がこの組織から漏えいしないようにする役目があります。 そのため、あなたは Microsoft 365 の DLP ポリシーを実装するだけでなく、この保護を組織内のデバイスに拡張することにしました。

**タスク**:

1. デバイスのオンボードを有効にする
1. エンドポイント DLP にデバイスをオンボードする
1. エンドポイント DLP ポリシーを作成する
1. エンドポイント DLP 設定を構成する
1. Microsoft Purview 拡張機能を構成する

## タスク 1 – デバイスのオンボードを有効にする

このタスクでは、組織向けにデバイスのオンボードを有効にします。

1. **SC-400-cl1\admin** アカウントで Client 1 VM (SC-400-CL1) にログインします。

1. **Microsoft Edge** で、 **`https://purview.microsoft.com`** に移動し、**Joni Sherman** として Microsoft Purview ポータルにログインします。 `JoniS@WWLxZZZZZZ.onmicrosoft.com` としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 Joni のパスワードは、前の演習で設定しました。

1. **Microsoft Edge** で、**`https://purview.microsoft.com`** に移動し、左サイドバーから **[設定]** を選択します。

1. 左サイドバーで、**[デバイスのオンボード]** を展開し **[デバイス]** を選択します。

1. **[デバイス]** ページで、**[デバイスのオンボードを有効にする]** を選択して、テナントのソリューションを有効にします。

1. **[OK]** を選択し、**[デバイスのオンボーディングを有効にします]** ダイアログに同意します。

1. **[OK]** を選択し、**[デバイスのオンディングが有効化されます]** ダイアログに同意します。

これでデバイスのオンボーディングが有効となりました。デバイスをエンドポイント DLP ポリシーで保護するためにオンボードを開始できます。 この機能を有効にするプロセスには最大 30 分かかる場合がありますが、次のタスクはこれに依存しないため、次のタスクに進んでもかまいません。

## タスク 2 – エンドポイント DLP にデバイスをオンボードする

このタスクでは、ローカル スクリプト オプションを使って、Windows 11 デバイスをオンボードし、エンドポイント DLP ポリシーで保護できるようにします。

1. **SC-400-cl1\admin** アカウントで Client 2 VM (SC-400-CL2) にログインします。

1. Microsoft Edge を開き、**`https://purview.microsoft.com`** に移動して、**Joni Sherman** として Microsoft Purview ポータルにログインします。 `JoniS@WWLxZZZZZZ.onmicrosoft.com` としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 Joni のパスワードは、前の演習で設定しました。

1. 左側のサイドバーで **[設定]** を選択します。

1. 左サイドバーで、**[デバイスのオンボード]** を展開し **[オンボード]** を選択します。

1. **オンボーディング**ページの **[デプロイ方法]** ドロップダウン メニューで **[ローカル スクリプト (最大 10 台のマシン用)]** を選択し、**[ダウンロード パッケージ]** を選択します。

1. **[ダウンロード]** ダイアログで、ダウンロードにカーソルを合わせ、フォルダー アイコンを選択して **[フォルダーに表示]** します。

1. ZIP ファイルを SC-400-CL1 の**デスクトップ**に解凍します。 **DeviceComplianceLocalOnboardingScript.cmd** という名前のスクリプトがあるはずです。

1. デスクトップで、抽出した **DeviceComplianceLocalOnboardingScript.cmd** ファイルを右クリックし、**[その他のオプションの表示]** 選択し、**[プロパティ]** を選択します。

1. プロパティ ウィンドウの **[全般]** タブの下部にある **[セキュリティ]** セクションで、**[ブロック解除]** を選択し、**[OK]** を選択してこの設定を保存します。

1. デスクトップに戻り、**DeviceComplianceLocalOnboardingScript.cmd** ファイルを右クリックし、**[管理者として実行]** を選択します。 **[ユーザー アカウント制御]** ダイアログで、**[はい]** を選択します。

1. **[コマンド プロンプト]** スクリーンで、**[Y]** と入力して確認し、Enter キーを押します。

1. スクリプトが完了すると、成功メッセージと、**[任意のキーを押して続行します]** プロンプトが表示されます。 任意のキーを押して、コマンド ライン ウィンドウを閉じます。 オンボーディングが完了するのに、1 分ほどかかることがあります。

1. [スタート] メニューを開き、「`Access work or school`」を検索します。 **[最も一致する検索結果]** で **[職場または学校にアクセスする]** を選択します。

1. **[職場または学校アカウントを追加する]** の **[職場または学校にアクセスする]** ウィンドウで **[接続]** を選択します。

1. **[職場または学校アカウントのセットアップ]** ダイアログで、**[このデバイスを Microsoft Entra ID に参加させる]** リンクを選択し、**Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 Joni のパスワードは、前の演習で設定しました。

1. **[これがあなたの組織であることを確認してください]** ダイアログで、テナントの URL を確認し、**[参加する]** を選択します。  

1. デバイスが接続されたら、**[すべての設定が完了しました]** で **[完了]** を選択します。 スクリーン

1. クライアント 2 VM (SC-400-CL2) を再起動します。

1. クライアント 1 VM (SC-400-CL1) に再度ログインします。

1. Microsoft Purview ウィンドウは、引き続き **[デバイス]** ページで開いているはずです。 このページを更新し、デバイスが正常にオンボードされたことを確認します。

デバイスがオンボーディングして、Microsoft Entra ID に参加し、エンドポイント DLP ポリシーで保護できるようになりました。

## タスク 3 : エンドポイント DLP ポリシーを作成する

このタスクでは、Microsoft Purview ポータルでデータ損失防止 (DLP) ポリシーを作成して、Windows 11 デバイス上の生成 AI プラットフォームと機密情報が共有されないようにします。 このポリシーは、ドライバーのライセンス番号や個人情報などの機密性の高い顧客データが誤ってまたは意図的に AI プラットフォームと共有されないようにし、組織のデータ整合性を保護するのに役立ちます。

1. Client 1 VM (SC-400-CL1) に SC-400-cl1\admin アカウントでログオンします。

1. 引き続き、Microsoft Purview ポータルの **[デバイス]** ページに、Joni Sherman としてログインしている必要があります。 画面の左上部にある **[ホーム]** ボタンを選択します。 ログインしていない場合は、`https://purview.microsoft.com` に移動し、Joni Sherman としてログインします。 Joni のパスワードは、前の演習で設定しました。

1. Microsoft Purview ポータルで、左側のサイドバーから **[ソリューション]** を選択し、**[データ損失防止]** を選択します。

1. 左側のナビゲーション パネルで、**[ポリシー]** を選択し、**[+ ポリシー管理]** を選択します。

1. **[テンプレートの利用またはカスタム ポリシーの作成]** ページで、**[カスタム]**、**[カスタム ポリシー]** の順に選択し、**[次へ]** を選択します。

1. **[DLP ポリシーの名前の設定]** ページで、以下を入力します。

    - **名前**: `Generative AI sharing DLP policy`
    - **説明**: `Prevent sharing of sensitive data with generative AI platforms.`

1. [**管理単位の割り当て**] ページで、[**次へ**] を選択します。

1. **[ポリシーを適用する場所の選択]** ページで **[デバイス]** 場所のみを選択します。 他の場所が選択されている場合は、その場所の選択が解除されていることを確認し、**[次へ]** を選択します。

1. **[ポリシー設定の定義]** ページで、**[高度な DLP ルールを作成またはカスタマイズする]** を選択し、**[次へ]** を選択します。

1. **[詳細な DLP ルールをカスタマイズする]** ページで、**[+ ルールの作成]** を選択します。

1. **[ルールの作成]** ページで、次を入力します。

    - **名前**: `Sensitive data protection rule`
    - **説明**: `Detect and restrict sharing of sensitive information with generative AI platforms.`

1. **[条件]** で、**[+ 条件の追加]** を選択し、**[次を含むコンテンツ]** を選択します。

1. 新しく開かれた **[コンテンツに含まれている]** 領域で、**[追加]** を選択し、**[機密情報の種類]** を選択します。

1. 右側の [**機密情報の種類]** ポップアップ パネルで、`U.S.` を検索し、米国に関連するすべての機密情報の種類を選択します。 ポップアップ ページの下部にある **[追加]** を選択します。

1. **[アクション]** まで下にスクロールし、**[+ アクションを追加]** ドロップダウンを選択し、**[デバイスでのアクティビティの監査または制限]** を選択します。

1. 新しく開いた **[デバイスでのアクティビティの監査または制限]** 領域の **[Service ドメインとブラウザーアクティビティ]** セクションで、**制限付きクラウド サービス ドメインへの アップロードまたは未許可のブラウザーからのアクセス**のチェック ボックスをオンにし、このオプションの下にある **[ + 機密性の高いサービス ドメインに対して異なる制限を選択する]** を選択します。

1. **[機密性の高い Service ドメインの制限]** ポップアップ パネルで、**[ + グループの追加]** を選択します。

1. **[機密性の高い Service ドメイン グループの選択]** で **[生成 AI Webs サイト]** のチェック ボックスをオンにし、ポップアップ パネルの下部にある **[追加]** を選択します。

1. **[Sensitive サービス ドメインの制限]** ページに戻り、**生成 AI Web サイト**が一覧表示されていることを確認し、ポップアップ パネルの下部にある **[保存]** を選択します。

1. **[ルールの作成]** に戻り、**サポートされているブラウザーに張り付ける**チェック ボックスをオンにし、このオプションの下で **[+ 機密性の高いサービス ドメインに対して異なる制限を選択する]** を選択します。

1. **[機密性の高い Service ドメインの制限]** ポップアップ パネルで、**[ + グループの追加]** を選択します。

1. **[機密性の高い Service ドメイン グループの選択]** で **[生成 AI Webs サイト]** のチェック ボックスをオンにし、ポップアップ パネルの下部にある **[追加]** を選択します。

1. **[ルールの作成]** に戻り、**[サービス ドメインとブラウザー アクティビティ]** セクションで、**[制限されたクラウド サービス ドメインにアップロードするか、制限されていないブラウザーからアクセスする]** および **[サポートされているブラウザーに張り付ける]** の両方に対してアクションを **[監査のみ]** から **[ブロック]** に更新します。

1. **[すべてのアプリのファイル アクティビティ]** セクションで、既定のアクション **[監査のみ]** のままにします。　

1. **[ユーザー通知]** セクションで、**[ユーザーへのお知らせに通知を使い、機密情報の適切な使用についてのユーザーの教育に役立てる]** を設定します。 **オン**に

1. **[エンドポイント デバイス]** で、**[アクティビティが制限されている場合にユーザーにポリシー ヒント通知を表示する] のチェック ボックスを選択します。これは、Windows でアクティビティに対して [ブロック] を選択するとオンになります。Windows デバイスで通知をオフにするには、制限を無効にします**。

1. **[Microsoft 365 サービス]** で、 **[ポリシーのヒントを使用して Office 365 でユーザーに通知する]** のチェックボックスを選択します。

1. ポップアップ パネルの下部にある **[保存]** を選択します。

1. **[詳細な DLP ルールをカスタマイズする]** ページに戻り、**[次へ]** を選択します。

1. **[ポリシー モード]** ページで、**[ポリシーをすぐにオンにする]** を選択し、**[次へ]** を選択します。

1. **[レビューと完了]** ページでポリシーの設定を確認し、**[送信]** を選択してポリシーを作成します。

1. ポリシーが作成されたら、**[新しいポリシーの作成]** ページで **[完了]** を選択します。

エンドポイント DLP ポリシーが正常にアクティブ化されました。 このポリシーにより、生成 AI プラットフォームとの機密情報の共有が防止され、ドライバーのライセンス番号や個人情報などの機密データが不正アクセスや漏洩から保護されます。

## タスク 4 - エンドポイント DLP ポリシーを構成する

このタスクでは、Windows 11 デバイス上のフォルダーに対して、ファイル パスの除外を構成し、作成したエンドポイント DLP ポリシーが、このフォルダーのコンテンツを監視しないようにします。

1. Client 1 VM (SC-400-CL1) には **lon-cl1\admin** アカウントでログインし、Microsoft 365 には **Joni Sherman** としてログインしておく必要があります。

1. **Microsoft Edge** では、データ損失防止のために Microsoft Purview ポータル タブが引き続き **[ポリシー]** ページに開かれているはずです。 左側のサイドバーで **[設定]** を選択します。

1. 設定ページで、左側のサイドバーから **[データ損失防止]** を選択します。

1. **[データ損失の防止の設定]** ページが、**[エンドポイント DLP 設定]** に開くはずです。

1. **[エンドポイント DLP 設定]** ページで、**[Windows のファイル パスの除外]** を展開し、**[+ ファイル パスの除外の追加]** を選択します。

1. **[ファイル パスの除外]** フィールドの **[Exclude these file paths from Windows devices] (Windows デバイスからこれらのファイル パスを除外する)** ポップアップ ページで、「`C:\FilePathExclusionTest`」と入力し、右側の **+** ボタンを選択します。 **[保存]** を選択して、この入力を保存します。

1. **[エンドポイント DLP 設定]** ページに戻り、**[機密データに対するブラウザーとドメインの制限]** を展開し、**[+ 許可されていないブラウザーの追加または編集]** を選択します。

1. **[許可されていないブラウザーの追加]** ポップアップ ページで、**[Google Chrome]** の左側にあるチェック ボックスをオンにし、**[保存]** を選択します。

1. **[エンドポイント DLP 設定]** ページに戻り、**[サービス ドメイン]** のドロップダウンを選択して **[オフ]** から **[ブロック]** に変更します。

1. **[クラウド アプリのモードの更新]** ダイアログで **[はい]** を選択して、ブロック モードをアクティブにします。

1. **[サービス ドメイン]** で、**[+ クラウド サービス ドメインの追加]** を選択します。

1. **[クラウド サービス ドメインの追加]** ポップアップ ページの **[ドメイン]** フィールドに「`dropbox.com`」と入力し、右側にある **+** を選択します。 **[保存]** を選択して設定を保存します。

1. ブラウザー ウィンドウを閉じます。

これで、エンドポイント DLP ポリシーのカスタム設定が構成されました。 作成するすべてのポリシーで、構成したフォルダー内のコンテンツが無視されるようになり、Google Chrome ブラウザーが、機密データの処理を許可されていないブラウザーとして追加されました。

## タスク 5 : Microsoft Purview 拡張機能を構成する

コンプライアンス管理者であるあなたは、機密データを操作するために、Chrome ブラウザーを複数のユーザーにロールアウトするための新しいビジネス要件を評価する必要があります。 このテストでは、Google Chrome ブラウザーをクライアント 01 にインストールし、**Google 用 Microsoft Purview 拡張機能**を Google Web ストアから手動で追加します。

1. タスク バーから Edge ブラウザーを開きます。

1. Google Chrome のダウンロード場所 ( **`https://chrome.google.com`** ) に移動します。

1. **[Chrome をダウンロード]** を選択し、**[ダウンロード]** の通知から **[ChromeSetup.exe]** の **[ファイルを開く]** を選択します。

1. **[ユーザー アカウント制御]** で **[はい]** を選択して、Chrome ブラウザーをインストールします。

1. インストールが完了したら、**[Chrome にサインイン]** ページで **[サインインしない]** を選択します。

1. **[既定のブラウザーの設定]** ページで **[スキップ]** を選択します。

1. 新しくインストールされた Chrome ブラウザー ウィンドウが開いたら、Chrome Web ストアの次の場所にある Microsoft Purview 拡張機能に移動します。

   `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`

1. **[Microsoft Purview 拡張機能]** 拡張機能ページ上にいることを確認し、 **[Chrome に追加]** を選択します。

1. **[Microsoft Purview 拡張機能を追加しますか?]**  ウィンドウで **[拡張機能の追加]** を選択します。

1. Chrome に追加されている拡張機能の通知を閉じ、**`chrome://extensions`** に移動します。

1. **[Microsoft Purview 拡張機能]** が表示され、アクティブ化されていることを確認します。

1. Chrome ブラウザー ウィンドウを閉じます。

正常に Chrome ブラウザーがインストールされ、Microsoft Purview 拡張機能がクライアントに追加されました。 これで、Chrome ブラウザーを Edge ブラウザーと同様に使用して、機密データを操作できるようになり、Chrome ブラウザーを使用するときにも、以前に構成したエンドポイント DLP ポリシーが適用されるようになりました。
