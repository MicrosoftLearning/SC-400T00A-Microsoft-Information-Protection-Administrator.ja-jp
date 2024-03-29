---
lab:
  title: 演習 1 - コンプライアンス ロールを管理する
  module: Module 1 - Implement Information Protection
---
# 演習 1 - コンプライアンス ロールを管理する

最近採用された Contoso Ltd. のコンプライアンス管理者として Joni Sherman の役割を果たす場合、コンプライアンス要件を満たすように組織の新しい Microsoft 365 テナントを構成する責任があります。 Contoso Ltd. は、米国に本社を置く会社であり、欧州連合には新しい子会社があります。また、組織にとっては、新しい Microsoft 365 テナントが、さまざまな国の法的要件や業界内のさまざまな規制基準に確実に準拠するようにすることが不可欠です。

## 演習 1 - コンプライアンス ロールを割り当てる

この演習では、最小限の特権の原則に従い、既定のグローバル管理者を使って、コンプライアンス管理者の役割を、このラボで記述された操作を行うことが求められている Joni Sherman に割り振ります。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインします。 パスワードは、ラボ ホスティング プロバイダーから支給されます。

1. **Microsoft Edge** を開いて、アドレス バーを選び、**https://admin.microsoft.com** に移動して、Microsoft 365 管理センターに **MOD 管理者**admin@WWLxZZZZZZ.onmicrosoft.com としてログインします。 管理者のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. [**移動済みアイテム**] ダイアログボックスで、ダイアログ ボックスが閉じるまで [**次へ**] を選択します。

1. 左側のナビゲーション ウィンドウで **[ユーザー]** を展開し、 **[アクティブ ユーザー]** を選びます。

1. **[アクティブ ユーザー]** の一覧で、 **[Joni Sherman]** を選びます。 これにより、Joni のユーザー設定が表示されたポップアップ ページが右側に開きます。

1. Joni のユーザー設定ページで、 **[アカウント]** タブの下の **[ロール]** までスクロールし、 **[ロールの管理]** を選びます。

      ![[ロールの管理] オプションのスクリーンショット](../Media/ManageRoles.png)

1. **[管理者ロールの管理]** ポップアップ ページで、 **[管理センター アクセス]** を選び、下にスクロールして **[すべてをカテゴリ別に表示]** を選びます。 **[Security & Compliance]** カテゴリのカテゴリ表示で、 **[コンプライアンス管理者]** を選びます。

1. **[変更を保存]** を選択して、ロールに適用します。 **[管理者ロールが更新されました]** のメッセージがウィンドウの上部に表示されたら、左側を指している矢印を選択して、Joni のユーザー設定に戻ります。

1. Joni Sherman のアカウントが表示されているポップアップ ページを、右上にある **[X]** で閉じ、 **[アクティブ ユーザー]** リストに戻ります。

1. Joni Sherman に切り替える前に、MOD 管理者のグローバル管理者特権を使用して https://compliance.microsoft.com/auditlogsearch に移動し、監査ログをアクティブにします。

1. **[監査]** ページで、 **[ユーザーと管理者のアクティビティの記録を開始する]** を選択して、監査ログをアクティブにします。

1. 右上の **MA** の丸を選択し、**[サインアウト]** を選択します。

1. **Microsoft Edge** のブラウザーの画面を開いたままにします。

このラボの様々な演習の実施が求められてい Joni Sherman　に、コンプライアンス管理者ロールが割り当てられました。 次のタスクに進みます。

## タスク 2 – Microsoft Purview ポータルについて調べる

このタスクでは、全体管理者アカウントからサインアウトし、Joni Sherman としてもう一度サインインします。 コンプライアンス管理者の役割が割り当てられたばかりの Joni Sherman のアカウントを使えば、このラボの演習のほとんどを行うことができます。

1. Client 1 VM (LON-CL1) に **lon-cl1\admin** アカウントでログインしておきます。

1. **Microsoft Edge** で、 **https://compliance.microsoft.com** に移動します。

1. **[アカウントを選択]** ウィンドウが表示されたら、**[別のアカウントを使用]** を選択します。

1. [**サインイン**] ウィンドウが表示されたら、JoniS@WWLxZZZZZZ.onmicrosoft.com としてサインインします。 Joni のパスワードは、ラボ ホスティング プロバイダーから支給されます。

1. **[Microsoft Purview コンプライアンス ポータルへようこそ]** ページが表示されます。 ダッシュボード タイルと左側のナビゲーション ペインを調べます。

1. 様々な設定をよく理解しましょう。 終了したら、ブラウザーの画面を開いたままにしておきます。

Joni Sherman のアカウントへの切り替えが完了し、ラボを開始する準備ができました。
