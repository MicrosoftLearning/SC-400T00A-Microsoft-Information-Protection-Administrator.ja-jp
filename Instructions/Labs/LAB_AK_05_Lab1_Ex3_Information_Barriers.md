---
lab:
  title: 演習 3 - 情報バリアを構成する
  module: Module 5 - Manage insider and privacy risk in Microsoft 365
---

# ラボ 5 - 演習 3 - 情報バリアを構成する

Contoso Ltd. のコンプライアンス管理者である Joni は、Microsoft 365 で情報バリアを構成および管理する責任を負っています。 情報バリアは、明確な境界を維持し、組織内の特定のグループまたは個人間の不正な通信を防止するうえで重要な役割を果たします。 情報バリアを実装すると、規制の準拠、機密情報の保護、利益相反の最小化を確保します。 このセットアップにより、セキュリティで保護された作業環境が作成され、データの機密性が保護され、Contoso Ltd. のコンプライアンスへのコミットメントがサポートされます。

1. Microsoft Teams で名前による検索が有効になっていることを確認する
1. 組織内のユーザーをセグメント化する
1. 情報バリア ポリシーを作成する
1. 情報バリア ポリシーを適用する

## タスク 1: Microsoft Teams で名前による検索が有効になっていることを確認する

このタスクでは、Microsoft Teams で **[名前で検索**] 機能が有効になっていることを確認します。 この機能を使用すると、ユーザーは組織内の特定の個人を簡単に検索して見つけることができます。 提供されている手順に従って、この機能を構成してアクティブ化し、コラボレーションを強化し、組織の Microsoft Teams 環境内でのコミュニケーションを効率化します。

1. Client 1 VM (SC-400-CL1) に **SC-400-cl1\admin** アカウントでログインします。

1. 今も Joni のアカウントでサインインしている場合は、このアカウントからサインアウトし、すべてのブラウザー ウィンドウを閉じてください。

1. **Microsoft Edge** で、 **`https://admin.teams.microsoft.com`** に移動し、Microsoft Purview ポータルに MOD 管理者 `admin@WWLxZZZZZZ.onmicrosoft.com` としてログインしてください (ZZZZZZ はラボ ホスティング プロバイダーから支給された一意のテナント ID です)。

1. 左側のナビゲーション ウィンドウの **[Teams]** ドロップダウンで、**[Teams の設定]** を選択します

1. **[名前で検索]** まで下にスクロールしてください。 この機能が [オフ] に設定されている場合は、この機能を **[オン]** に切り替え、 **[保存]** を選択してこの設定を保存してください。

1. **[変更が有効になるまでに時間がかかります]** ポップアップで、 **[確認]** を選択してください

    >**注:** この変更が有効になるには数時間かかる場合があります。

## タスク 2 - 組織内のユーザーをセグメント化する

このタスクでは、PowerShell を使用して Security & Compliance モジュールに接続し、**Legal** および **Marketing** 部門の組織セグメントを作成します。

1. タスク バーの Windows ボタンを右クリックして昇格された PowerShell ウィンドウを開き、**[ターミナル (管理者)]** を選択します。

1. [Terminal] ウィンドウで、Security & Compliance PowerShell に接続するコマンドレットを入力します。

    ````powershell
    Connect-IPPSSession
    ````

    **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` としてサインインします (ここで ZZZZZZ はラボ ホスティング プロバイダーから支給された一意のテナント ID です)。 Joni のパスワードは、前の演習で設定しました。

1. **UserGroupFilter** パラメーターを指定して **New-OrganizationSegment** コマンドレットを実行して **Legal** セグメントを作成してください。

    ````powershell
    New-OrganizationSegment -Name "Legal" -UserGroupFilter "Department -eq 'Legal'"
    ````

1. **New-OrganizationSegment** コマンドレットをもう一度実行して **Marketing** セグメントを作成してください。

    ````powershell
    New-OrganizationSegment -Name "Marketing" -UserGroupFilter "Department -eq 'Marketing'"
    ````

1. **Get-OrganizationSegment** コマンドレットを実行して、作成されたセグメントを表示してください。

    ````powershell
    Get-OrganizationSegment
    ````

Security & Compliance PowerShell に正常に接続し、Legal および Marketing 部門の組織セグメントを作成し、Get-OrganizationSegment コマンドレットを使用してセグメントを表示しました。

## タスク 3: 情報バリア ポリシーを作成する

このタスクでは、PowerShell を使用して情報バリア ポリシーを作成し、Legal と Marketing 部門間の通信をブロックします。

1. 管理者特権の PowerShell ウィンドウは引き続き開いているはずです。

1. **SegmentsBlocked** パラメーターを指定して **New-InformationBarrierPolicy** コマンドレットを実行し、新しい **Legal-Marketing** ポリシーを作成してください。

    ````powershell
    New-InformationBarrierPolicy -Name "Legal-Marketing" -AssignedSegment "Legal" -SegmentsBlocked "Marketing" -State Active
    ````

1. PowerShell の種類 **Y** に情報バリア ポリシーの警告に関する通知が表示されたら、**Enter** キーを押してポリシーの作成に進みます。

1. 次に、反対方向にブロックする情報バリア ポリシーを作成する必要があります。 **SegmentsBlocked** パラメーターを指定して **New-InformationBarrierPolicy** コマンドレットを実行し、新しい **Marketing-Legal** ポリシーを作成してください。

    ````powershell
    New-InformationBarrierPolicy -Name "Marketing-Legal" -AssignedSegment "Marketing" -SegmentsBlocked "Legal" -State Active
    ````

1. **Get-InformationBarrierPolicy** コマンドレットを実行して、作成されたポリシーを表示してください。

    ````powershell
    Get-InformationBarrierPolicy
    ````

    >**注:** 作成されたポリシーを確認するときに、ポリシーが **[アクティブ]** としてマークされていることを確認してください。 情報バリア ポリシーは、適用する前にアクティブにする必要があります。

PowerShell を使用して Legal-Marketing と Marketing-Legal 情報バリア ポリシーを正常に作成し、Get-InformationBarrierPolicy コマンドレットを実行して、その状態がアクティブであることを確認しました。

## タスク 4: 情報バリア ポリシーを適用する

このタスクでは、PowerShell を使用してアクティブな情報バリア ポリシーを適用し、アプリケーションの状態をチェックします。

1. 管理者特権の PowerShell ウィンドウは引き続き開いているはずです。

1. **Start-InformationBarrierPoliciesApplication** コマンドレットを実行して、アクティブな情報バリア ポリシーを適用してください。

    ````powershell
    Start-InformationBarrierPoliciesApplication
    ````

1. **Get-InformationBarrierPoliciesApplicationStatus** コマンドレットを実行して、適用されたポリシーを表示してください。

    ````powershell
    Get-InformationBarrierPoliciesApplicationStatus
    ````

    >**注:** システムがポリシーの適用を開始するには、30 分かかります。

1. ポリシーが適用されると、**状態**は **NotStarted** から **Completed** に更新されます。

正常に、Start-InformationBarrierPoliciesApplication コマンドレットを実行して情報バリア ポリシーを適用し、Get-InformationBarrierPoliciesApplicationStatus コマンドレットを使用してアプリケーションの状態を確認できました。
