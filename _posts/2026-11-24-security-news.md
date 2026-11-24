---
layout: post
title: "今日のホットニュース（2026年11月24日）"
date: 2026-11-24 09:00:00 +0900
---

- Microsoft の Azure API Management（旧来型）の欠陥を悪用し、ノルウェーのエネルギー企業などで秘密情報が狙われました。保管中のキー類は「漏えいした」前提で入れ替えが推奨されています。
- ルーター等の GL.iNet 製品のクラウド管理サービス「GoodCloud」が悪用され、一部の機器にマルウェアが仕込まれました。クラウド側の修正だけでは感染機器は直りません。
- 古い ASP.NET 向けライブラリ Idunno.AntiCsrf（CVE-2026-131914）の悪用が確認されましたが、公式の修正はなく、使用中止が必要です。

---

## 1. Azure API Management（旧来型）の欠陥でノルウェーのエネルギー企業などが標的に

**何が起きたか**
Equinor（11月17日に攻撃を公表）と Skagerak Energi（11月18日に公表）で起きたインシデントの背景に、Microsoft の Azure API Management（APIM）の欠陥があるとみられると報じられました。正体不明の攻撃者が、APIM に保管されたトークン・シークレット・「名前付き値」を狙ったとされます。Microsoft は11月18日に問題を把握し、翌19日にアクセス経路を塞いだとされています。

**影響範囲**
- Microsoft によれば、影響を受けたのは APIM の Classic（旧来型）インスタンスのうち、同社の公開ガイダンスに沿っていないものです。v2 系の階層は影響なしとされています。
- 露出しうる情報：名前付き値、ID プロバイダのクライアントシークレット、サブスクリプションキー、管理 API 用トークン。
- ノルウェー国家安全保障局（NSM）は、国内外の複数の組織・業種に影響があるとしています。悪用の広がりは不明です。両社とも、データの窃取や改ざんの証拠はなく、運用への影響もないとしています。
- CVE 番号は確認できません。Microsoft の通知の全文は、顧客が共有した投稿でしか確認できておらず、公式文書による裏付けは未確認です。

**現状と対応**
- Microsoft 側でアクセス経路は閉じられています。
- NSM は、APIM 内のシークレットや名前付き値を侵害されたものとして再発行すること、インスタンスが更新済みか確認すること、サービス経由で到達できるデータを洗い出すことを勧めています。

**やさしい解説**
ビルの管理室に、建物じゅうの合鍵を保管した金庫があり、その金庫の裏口が一時的に開いていた、というイメージです。盗まれた合鍵は、別の建物（外部サービス）の扉も開けられるかもしれません。一般の利用者が直接できることは多くありませんが、Azure を使う組織の担当者は、APIM に保存しているキーの入れ替えと、Classic 版を使っていないかの確認を急いでください。

**ソース**
- ノルウェー国家安全保障局（NSM）：<https://nsm.no/aktuelt/nsm-deler-tiltak-mot-sarbarhet-i-azure-api-management>
- SecurityWeek：<https://www.securityweek.com/azure-flaw-exploited-to-target-secrets-at-norwegian-energy-firms/>
- 専門家の分析（Anders Kristiansen）：<https://anderskristiansen.com/post/2026/apim-legacy-access/>

## 2. GL.iNet の遠隔管理サービス「GoodCloud」が悪用され、ルーターや KVM にマルウェア

**何が起きたか**
攻撃者が GL.iNet のクラウド遠隔管理サービス GoodCloud の欠陥を悪用し、一部の顧客のルーターと KVM（遠隔操作用機器）にマルウェアを仕込みました。ベンダーは脆弱性を修正し、攻撃者のアクセスを遮断したとしています（ベンダー通知は11月20日付、報道は11月23日）。

**影響範囲**
- 影響台数、攻撃の開始時期、クラウド側の侵害方法は公表されていません。CVE 番号も確認できません。
- 感染報告のある例：ルーター GL-AXT1800（ファームウェア 4.8.3、GoodCloud 有効）、KVM の GL-RM1。一覧にない機種が安全とは限らないとされています。
- 研究者の分析（ベンダーによる確認は未了）では、クライアントがクラウドからの値を十分に検証せず、管理者権限で実行していたとされます。

**現状と対応**
- クラウド側の修正は済んでいますが、すでに感染した機器からはマルウェアは消えません。機種ごとの修正版ファームウェアが出ています（例：GL-AXT1800 は 4.8.4）。
- 感染が疑われる場合の扱いについて、ベンダーは「設定を保持したままの更新で除去できる」、研究者は「設定を保持せず初期状態から入れ直す」ことを勧めており、見解が分かれています。
- 感染が疑われる機器は、VPN 鍵・Wi-Fi／管理者パスワード・クラウド認証情報などを漏えいしたものとして入れ替えるのが安全です。確認方法の詳細はベンダー通知と研究者の資料を参照してください。

**やさしい解説**
家の合鍵を預かる管理会社の仕組みが破られ、留守中に勝手に「不審な荷物」を置かれたような状態です。管理会社が裏口をふさいでも、すでに置かれた荷物は自分で片づけなければなりません。対象機器を使っている方は、遠隔管理機能（GoodCloud）を使っているか確認し、最新ファームウェアへの更新と、パスワード類の変更を検討してください。

**ソース**
- GL.iNet セキュリティ通知：<https://forum.gl-inet.com/t/2026-11-20-gl-inet-security-notice-goodcloud-kvm-routers/73056>
- 研究者の調査資料：<https://github.com/RemoteToHome-io/gl-security-incident-2026>
- The Hacker News：<https://thehackernews.com/2026/11/hackers-exploited-glinet-cloud-flaw-to.html>
- SecurityWeek：<https://www.securityweek.com/gl-inet-routers-kvms-compromised-via-remote-management-service-flaw/>

## 3. 放置された ASP.NET 向けライブラリ Idunno.AntiCsrf に重大な欠陥、悪用も（CVE-2026-131914）

**何が起きたか**
2008年を最後に更新されていない ASP.NET WebForms 向けの CSRF（なりすましリクエスト）対策ライブラリ Idunno.AntiCsrf に、外部から任意のコードを実行できる欠陥が見つかりました。Mandiant は実際の悪用を観測したとしています（報道は11月23日）。

**影響範囲**
- 対象：Idunno.AntiCsrf 0.9.1.0 および 0.9.1 Beta（CVSS 9.3）。
- 認証や正当なトークンなしの1回のHTTPリクエストで、IIS のワーカープロセス上でコードが実行され、サーバ全体の乗っ取りにつながりうるとされています。
- 公式の修正はありません（プロジェクトは開発終了）。

**現状と対応**
- ライブラリの使用をやめ、System.Web.Helpers.AntiForgery、MAC 検証付き ViewState、ASP.NET Core の IAntiforgery などへ移行する。
- Web.config や bin ディレクトリに Idunno.AntiCsrf／AntiCsrfModule の参照がないか点検する。
- 侵害が疑われる場合は、machineKey やDB認証情報などを入れ替え、Web公開領域に不審なファイルがないか確認する。

**やさしい解説**
何年も前に作者が手を引いた「防犯カメラ」の部品が、実は誰でも開けられる裏口になっていた、という話です。サポートが終わった部品は修理されないため、取り替えるしかありません。一般の利用者がすることはありません。古い業務システムや社内Webを管理する担当者が、使っていないか棚卸ししてください。

**ソース**
- Mandiant アドバイザリ（MNDT-2026-0048）：<https://github.com/mandiant/Vulnerability-Disclosures/blob/master/2026/MNDT-2026-0048.md>
- The Hacker News：<https://thehackernews.com/2026/11/hackers-exploit-critical-aspnet-anti.html>

## 4. 【続報】N-able Mail Assure の侵害調査中に重大な欠陥（CVE-2026-134624）が判明

**何が起きたか**
11月20日に掲載した Mail Assure／SpamExperts クラウドサーバの侵害の続報です。調査の過程で、認証済みの API 利用者が内部のホスト・ポートへ接続させられる SSRF の欠陥（CVE-2026-134624、CVSS 4.0 で9.3）が公表されました（11月22日ごろ）。

**影響範囲・新しい事実**
- 対象：ビルド 20261121.1943 より前。このビルドで修正されています。高権限の API アクセスが前提で、コード実行は主張されていません。
- N-able は、この欠陥が侵入経路だったかどうかを明らかにしていません。
- 侵害は1台のホスト型クラウドサーバで、N-able はサーバの隔離、内部認証情報の更新、顧客の API トークン失効などを実施しました。顧客データ（メールボックス含む）が侵害された証拠はなく、ダッシュボードと API は土曜深夜に復旧したとのことです。メール配信とフィルタリング自体は継続していたとされます。
- 外部のフォレンジック（DFIR）チームが関与し、正式な原因分析は更新から2週間以内に出る予定です。
- 11月9日の N-central 停止（別件）とは無関係とされています。

**現状と対応**
- 顧客のマシン上で動かす SpamExperts Local Cloud の運用者は、ビルド 20261121.1943 以降か確認してください。

**やさしい解説**
金庫室の扉が破られた事件の調査中に、別の「壁の弱い所」も見つかったので補修した、という段階です。それが侵入口だったかは調査待ちです。Mail Assure を使っている組織は、N-able の更新情報を確認し、API トークンの再発行を求められた場合は早めに対応してください。

**ソース**
- N-able セキュリティアドバイザリ：<https://me.n-able.com/s/security-advisory/aArVy0000002mrlKAA/cve2026134624-mailassure-ldap-sync-connection-check-ssrf>
- N-able インシデント更新：<https://www.n-able.com/blog/mail-assure-incident-update>
- The Hacker News：<https://thehackernews.com/2026/11/n-able-discloses-critical-mail-assure.html>
- SecurityWeek：<https://www.securityweek.com/n-able-patches-critical-flaw-disclosed-after-mail-assure-cyberattack/>

## 5. FBI の全国犯罪情報データベース（NCIC）に不正アクセスか（未確認）

**何が起きたか**
FBI が、法執行機関が使う全国犯罪情報データベース NCIC への不正アクセスの疑いを調べていると、AP通信が関係者の話として報じました（米国時間11月21日。最初に報じたのは CNN）。FBI はコメントを控えています。

**確認できていないこと**
- 実際に侵害があったのか、範囲、攻撃者は、いずれも不明です。
- 最近の他のシステム障害との関連を示す兆候は、現時点ではないとされています。
- FBI や政府の公式発表は確認できておらず、匿名の関係者に基づく報道です。

**やさしい解説**
全国の警察が共通で参照する「指名手配・盗難品・行方不明者の台帳」に、何か異常があった可能性がある、という段階です。事実関係はまだ固まっていません。私たちが今すぐ取る行動はなく、公式発表を待つのが適切です。

**ソース**
- SecurityWeek（AP通信配信）：<https://www.securityweek.com/fbi-investigating-apparent-hack-of-its-key-national-criminal-justice-database-ap-source-says/>

## 今日やること

**一般利用者向け**
- GL.iNet のルーターや KVM を使っている場合は、ファームウェアを更新し、パスワード類の変更を検討する。
- 業務で Azure や N-able 製品を使っている場合は、担当部署の案内に従う。

**IT担当者向け**
- Azure API Management Classic を使っていれば、保存しているシークレット・名前付き値・サブスクリプションキーを再発行し、更新状況を確認する。
- 社内の ASP.NET WebForms アプリで Idunno.AntiCsrf を使っていないか棚卸しし、使っていれば移行する。IISログの不審な POST（.aspx への 302／500）も確認する。
- GL.iNet 機器の有無を確認し、感染確認（再起動前に実施）と修正版への更新を行う。
- Mail Assure／SpamExperts Local Cloud はビルド 20261121.1943 以降かを確認する。

## 留意点

- Azure API Management の件は CVE が付与されておらず、Microsoft の通知は顧客共有の投稿経由でしか確認できていません。GL.iNet の根本原因は研究者の分析で、ベンダー確認は未了です。NCIC の件は匿名関係者の報道に基づきます。
- 期間外として見送った案件：SBC Medical Group の200万人超の情報流出（SEC提出資料。報道は11月20日）。
- 台帳掲載済みで新しい事実を確認できなかったため見送った案件：VMware vCenter、PHP/phpAfterShell、Java4Shell、NGINX、SAP、Cisco Expressway、ScreenConnect、OpenRouter、Ghostscript など。
- 今回アクセスできなかったサイト：BleepingComputer（HTTP 403）。
