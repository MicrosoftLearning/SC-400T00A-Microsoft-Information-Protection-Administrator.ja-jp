---
lab:
  title: '演習 2: Microsoft Purview メッセージ暗号化を管理する'
  module: Module 1 - Implement Information Protection
---

<!--
# Lab 1 - Exercise 2 - Manage Microsoft Purview Message Encryption
-->

# 演習 3: Microsoft Purview のメッセージ暗号化を管理する

Joni Sherman がパイロット チームで構成しテストする必要がある最初の設定は、Microsoft Purview メッセージ暗号化です。 この目的のために、彼女は既定のテンプレートを変更し、パイロット ユーザーの 1 人に割り当てられる新しいブランド テンプレートを作成します。 次に、パイロット ユーザーは自分のアカウントを使用してメッセージ暗号化機能をテストします。

## タスク 1 – Azure RMS の機能を確認する

このタスクでは、Exchange Online PowerShell モジュールをインストールし、前回の演習でコンプライアンス管理者のロールが割り当てられた Joni Sherman として、自分のテナントの Azure RMS の機能が正しいことを確認します。

<!--
1. You should still be signed in to Client 1 VM (LON-CL1) as the **lon-cl1\admin** account.

1. Open an elevated PowerShell window by selecting the Windows button with the right mouse button and then select **Windows PowerShell (Admin)**.

1. Confirm the **User Account Control** window with **Yes**.
-->

1. タスク バーから管理者特権の PowerShell ウィンドウを開きます。

1. 次のコマンドレットを入力して、Exchange Online PowerShell モジュールの最新版をインストールします。

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. 信頼されていないレポジトリ セキュリティ ダイアログで、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。  この処理は、完了までに時間がかかる場合があります。

1. 次のコマンドレットを入力して実行ポリシーを変更し、**Enter** キーを押します。

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

1. [実行ポリシーの変更] で、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。

<!--
1. Close the PowerShell window.

1. Open a regular PowerShell window, without elevation, by selecting the Windows button with the right mouse button and select **Windows PowerShell**.
-->

1. 次のコマンドレットを入力して Exchange Online PowerShell モジュールを使用し、テナントに接続します。

    ```powershell
    Connect-ExchangeOnline
    ```

1. **[サインイン]** ウィンドウが表示されたら、JoniS@WWLxZZZZZZ.onmicrosoft.com としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 前のラボでリセットした Joni のパスワードを使用します。

1. 次のコマンドレットを使用して、テナントで Azure RMS および IRM がアクティブ化されていることを確認し、**Enter** キーを押します。

    ```powershell
    Get-IRMConfiguration | fl AzureRMSLicensingEnabled
    ```

1. **AzureRMSLicensingEnabled** の結果が **True** の場合、テナントに対して Azure RMS がアクティブになります。 次の手順に進みます。 

1. 次のコマンドレットを使用して、Office 365 メッセージ暗号化に使用される Azure RMS テンプレートを他のパイロット ユーザー **Megan Bowen** に対してテストし、**Enter** キーを押します。

    ```powershell
    Test-IRMConfiguration -Sender MeganB@contoso.com -Recipient MeganB@contoso.com
    ```

    ![IRM 検証スクリプトの結果。 ](../Media/IRMvalidationl.png)

1. すべてのテストが **PASS** を表示し、エラーが表示されていないことを確認します。

1. PowerShell ウィンドウは開いたままにします。

Exchange Online PowerShell モジュールがインストールされ、テナントに接続し、Azure RMS が正しく機能していることを確認しました。

## タスク 2: 既定のブランド テンプレートを修正する

組織からは Google や Facebook などの ID プロバイダーへの信頼を制限する要件が出されています。 既定では、このようなソーシャル ID はメッセージ暗号化で保護されたメッセージにアクセスするためにアクティブ化されているので、組織内のすべてのユーザーに対してソーシャル ID の利用を非アクティブ化する必要があります。

<!--
1. You should still be signed in to your Client 1 VM (LON-CL1) as the **lon-cl1\admin** account and there should still be an open PowerShell window with Exchange Online connected.
-->

1. 次のコマンドレットを実行して、既定の構成を表示します。

    ```powershell
    Get-OMEConfiguration -Identity "OME Configuration" | fl
    ```

1. 設定を確認して、**SocialIdSignIn** のパラメーターが **True** に設定されていることを確認します。

1. 次のコマンドレットを実行し、OME で保護されたテナントからのメッセージにアクセスするためのソーシャル ID の利用を制限します。

    ```powershell
    Set-OMEConfiguration -Identity "OME Configuration" -SocialIdSignIn:$false
    ```

1. 既定のテンプレートをカスタマイズすることに関する警告メッセージを、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。

1. 既定の構成をもう一度確認し、SocialIdSignIn のパラーメーターが [False] に設定されていることを確認します。

    ```powershell
    Get-OMEConfiguration -Identity "OME Configuration" | fl
    ```

1. **SocialIDSignIn** が **False** に設定されていることが結果に示されていることに注意してください。 PowerShell ウィンドウとクライアントは開いたままにします。

Office 365 Message Encryption での Google、Facebook などの海外の ID プロバイダーの利用を非アクティブ化しました。

## タスク 3: 既定のブランド テンプレートをテストする

テナントのユーザーから Office 365 Message Encryption で保護されたメッセージを受信するときに、ソーシャル ID ダイアログが外部の受信者に対して表示されていないことを確認する必要があります。暗号化されたコンテンツにアクセスするときはいつでも OTP を使用する必要があります。

1. 他の VM である Client 2 VM (LON-CL2) に **lon-cl2\admin** アカウントでサインインします。

<!--
1. Make sure all available Windows Updates are installed and the client does not require a restart to finish update installation.

[//]: <> (Installing the latest OS updates will also update the Edge browser to the new chromium version required to do this labs.)

1. Open **Microsoft Edge** from the taskbar and when a **Welcome to Microsoft Edge** windows is displayed, select **Start without your data**, select **Continue without this data** again and select **Confirm and start browsing**.

1. If the welcome message is missing, navigate to https://microsoft.com/edge, select **DOWNLOAD for Windows** and **Windows 10**. Select **Accept and download** and **Run** to install the latest version of the Edge browser. Once this is complete perform the previous step.
-->

1. **Microsoft Edge** を開き、https://outlook.office.com に移動します。

1. [Outlook on the web] に LynneR@WWLxZZZZZZ.onmicrosoft.com としてサインインします (ZZZZZZ はラボ ホスティング プロバイダーから支給された固有のテナント ID)。 

    >コースの開始時に、Joni Sherman と同時に Lynne のパスワードをリセットします。

1. **[サインインの状態を維持しますか?]** ダイアログボックスで、**[今後このメッセージを表示しない]** チェックボックスを選択し、**[いいえ]** を選択します。

1. **[パスワードを保存]** ダイアログで、**[保存]** を選択し、ブラウザーにパイロット ユーザーのパスワードを保存します。

1. **[翻訳元の言語]** ウィンドウが表示されたら、下向きの矢印を選択し、**[...からは翻訳しない]** を選択します。

1. Outlook の左上隅から **[新しいメール]** を選択します。

1. **[To]** フィールドに、テナント ドメインには存在しない、個人用またはその他サード パーティのメール アドレスを入力します。 

1. **[件名を追加]** フィールドに「**秘密のメッセージ**」と入力します。

1. 本文に「**私の超秘密のメッセージ**」と入力します。

1. 上部のバーで、**[オプション]** タブを選択し、**[暗号化]** (ロック アイコン) を選択したあと、ドロップダウン リストから **[暗号化]** を選択します。 

    >**[送信]** の上のメッセージ ペインの上部に、"このメッセージは暗号化されています。 受信者は暗号化を削除できません" のような通知が表示されるはずです。

    ![暗号化設定のスクリーンショット](../Media/OptionsEncrypt.png)

1. **[送信]** を選択してメッセージを送信します。

1. 個人用のメール アカウントにサインインし、Lynne Robbins からのメッセージを開きます。 

1. Microsoft アカウント (@outlook.com など) にこのメールを送った場合、暗号化は追加の手順なしに自動的に処理され、メッセージが表示されます。

    >**注:** **[私の超秘密のメッセージ]** が表示された場合、 このタスクは完了しました。 それ以外の場合は、次の手順に進みます。

1. メールを他のメール サービス (@gmail.com など) に送信した場合、暗号化を処理し、メッセージを読むために、次の手順を踏む必要がある場合があります。

    >**注:** 迷惑メール フォルダーに Lynne Robbins からのメッセージがあるかどうかを確認する必要があるかもしれません。

1. **[メッセージを読む]** を選択します。

1. ソーシャル ID をアクティブ化しなければ、Google アカウントで認証するボタンはありません。

1. **[ワンタイム パスコードを使用してサインイン]** を選択して、制限時間付きパスコードを受け取ります。

1. 個人用のメール ポータルを開き、**"メッセージを表示するためのワンタイム パスコード"** という件名のメッセージを開きます。

1. パスコードをコピーして、OME ポータルに貼り付け、 **[続行]** を選択します。

1. 暗号されたメッセージを確認します。

<!--
1. Leave Client 1 VM (LON-CL1) open as it is.
-->

修正された、既定の OME テンプレートを非アクティブ化したソーシャル ID でテストしました。

## タスク 4 – カスタム ブランド テンプレートを作成する

組織の財務部が送信する、保護されたメッセージには、カスタマイズした導入や本文、フッターの免責事項のリンクなど、特別なブランド化が必要です。 財務のメッセージはまた、7 日経過した後期限切れとします。 このタスクでは、OME 構成を新しくカスタマイズし、財務部が送信するすべてのメールに対しその OME 構成を適用する転送ルールを作成します。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでサインインし直します。また、Exchange Online が接続された状態の PowerShell ウィンドウを開いたままにしておく必要があります。

1. 次のコマンドレットを実行して、新しい構成を作成します。

    ```powershell
    New-OMEConfiguration -Identity "Finance Department" -ExternalMailExpiryInDays 7
    ```

1. テンプレートのカスタマイズに関する警告メッセージを、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。 

1. 導入のテキストメッセージを次のコマンドレットで変更します。

    ```powershell
    Set-OMEConfiguration -Identity "Finance Department" -IntroductionText " from Contoso Ltd. finance department has sent you a secure message."
    ```

1. テンプレートのカスタマイズに関する警告メッセージを、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。

1. メッセージの本文メールテキストを次のコマンドレットで変更します。

    ```powershell
    Set-OMEConfiguration -Identity "Finance Department" -EmailText "Encrypted message sent from Contoso Ltd. finance department. Handle the content responsibly."
    ```

1. テンプレートのカスタマイズに関する警告メッセージを、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。

1. 免責事項 URL を変更し、Contoso のプライバシーに関する声明のサイトを指し示すようにします。

    ```powershell
    Set-OMEConfiguration -Identity "Finance Department" -PrivacyStatementURL "https://contoso.com/privacystatement.html"
    ```

1. テンプレートのカスタマイズに関する警告メッセージを、[はい] を示す **[Y]** を選択して確定し、**Enter** キーを押します。

1. 次のコマンドレットを使用し、メール フロー ルールを作成します。このメール フロー ルールはカスタム OME テンプレートを財務チームが送信するメッセージすべてに適用します。  この処理は、完了するまでに数秒かかる場合があります。

    ```powershell
    New-TransportRule -Name "Encrypt all mails from Finance team" -FromScope InOrganization -FromMemberOf "Finance Team" -ApplyRightsProtectionCustomizationTemplate "Finance Department" -ApplyRightsProtectionTemplate Encrypt
    ```

1. 次のコマンドレットを入力して変更を確認します。

    ```powershell
    Get-OMEConfiguration -Identity "Finance Department" | Format-List
    ```

1. PowerShell ウィンドウは開いたままにします。

財務部のメンバーが外部の受信者にメッセージを送信する際に、カスタム ブランド テンプレートが自動的に適用される新たなトランスポート ルールが正常に作成されました。

## タスク 5 – カスタム ブランド テンプレートをテストする

新しいカスタム構成を検証するため、財務チームのメンバーである Lynne Robbins のアカウントをもう一度使用する必要があります。

1. Client 2 VM (LON-CL2) に **lon-cl2\admin** アカウントでサインインし直します。

1. [Outlook on the web] タブはまだ開いており、**Lynne Robbins** としてサインインしているはずです。

1. Outlook の左上隅から **[新しいメール]** を選択します。

1. **[To]** フィールドに、テナント ドメインには存在しない、個人用またはその他サード パーティのメール アドレスを入力します。 

1. **[件名を追加]** フィールドに「**財務レポート**」と入力します。

1. 本文に「**秘密の財務情報**」と入力します。

1. **[Send]** を選択します。

1. 個人用のメール アカウントにサインインし、**Lynne Robbins** からのメッセージを開きます。 以下の画像のようになります。 **[メッセージを読む]** を選択します。

    ![Lynne Robbins からの暗号化されたメールの例 ](../Media/EncryptedEmail.png)

1. 両方のオプションが利用可能となり、カスタマイズした構成でソーシャル ID がアクティブになりました。 **[ワンタイム パスコードを使用してサインイン]** を選択して、制限時間付きパスコードを受け取ります。

1. 個人用のメールに戻り、**"メッセージを表示するためのワンタイム パスコード"** という件名のメッセージを開きます。

1. パスコードをコピーしてポータルに貼り付け、**[続行]** を選択します。

1. カスタム ブランドの暗号化されたメッセージを確認します。

新しくカスタマイズされたテンプレートが正常にテストされました。
