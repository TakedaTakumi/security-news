---
layout: post
title: "今日のホットニュース（2026年11月12日）"
date: 2026-11-12 09:00:00 +0900
---

- 印刷通販のラクスルで、データ入稿システムの認証情報が不正に取得され、保管データに外部からアクセスできる状態になっていました。件数は集計中です。
- ConnectWise ScreenConnect を悪用した MSP（運用代行事業者）への攻撃で、6社・47組織・286台が確認されています。Cisco BroadWorks の脆弱性は悪用が確認され、CISA KEV に追加されました。
- 続報として、Notion AI のチャット記録が Fireworks AI の侵害で露出しました。N-able N-central にはホットフィックスが提供されました。

---

## 1. ラクスル：データ入稿システムの認証情報が不正取得され、保管データに外部からアクセス可能に

**何が起きたか**
ラクスルは2026年11月9日、データ入稿処理システムへの不正アクセスを発表しました。11月8日0時20分ごろに発覚しています。システムの認証情報が不正に取得され、保管データの一部に外部からアクセスできる状態でした。認証情報の取得経緯は分かっていません。

**影響範囲**
件数と期間は集計中で、公表されていません。対象は、入稿された印刷データ、請求書・Web郵便などに含まれる氏名、会社名、住所、電話番号、メールアドレスです。名刺やはがきに載った、注文者以外の第三者の個人情報も含まれる可能性があります。

**現状と対応**
ラクスルは認証情報を無効化し、アカウントを停止しました。関連サービスは一時停止後、11月9日から順次再開しています。「ラクスル パッケージ」と「ラクスル Adobe Express連携」は、発表時点で停止中です。個人情報保護委員会へは報告予定です。カード情報、ログインID、パスワードの漏えいと、二次被害は確認されていません。

**やさしい解説**
印刷会社の「入稿用の受付ボックス」の鍵が盗まれ、中身をのぞける状態になったイメージです。名刺やはがきのデータには、注文した本人以外の名前や連絡先も載っています。ラクスルを使っている方は、公式サイトの案内を確認してください。心当たりのないメールや電話には注意してください。

**ソース**
- ラクスルの公式お知らせ（URLは特定できず、https://corp.raksul.com/ は未確認）
- [Impress Watch](https://www.watch.impress.co.jp/docs/news/2154881.html)
- [Security NEXT](https://www.security-next.com/192575)

## 2. ConnectWise ScreenConnect を悪用した MSP 侵害：顧客端末に不正なクライアントを配布

**何が起きたか**
セキュリティ企業 Huntress が観測した攻撃が、2026年11月11日に報じられました。侵害されたクラウド版 ScreenConnect の「Run Command」機能を使い、MSP の顧客端末に不正な ScreenConnect クライアントが配布されました。初期侵入の方法は特定されていません。認証情報の侵害やサポートセッションの乗っ取りが示唆されていますが、脆弱性が原因かどうかは不明です。

**影響範囲**
Huntress の集計で、MSP 6社、47組織、286台が確認されています。数は増加中です。まだ見つかっていない過去の侵害がある可能性もあります。

**現状と対応**
ConnectWise は調査中です。CVE 番号や修正版の記載はありません。報道で示された推奨対応は次のとおりです。
- 侵害が疑われる端末とは、対話セッションを開かない。
- 調査は別系統のツールで行う。
- アカウントの活動を確認し、セッションを失効させる。
- 信頼できる端末から資格情報をリセットし、MFA（多要素認証）を確認する。
- ConnectWise Trust Center を参照する。

**やさしい解説**
ビルの管理会社が持つ「全フロアのマスターキー」が悪用され、各テナントの部屋に偽の鍵を置かれたような状況です。一般の方に必要な操作はありません。MSP に IT 管理を任せている組織は、委託先に状況を確認してください。

**ソース**
- [BleepingComputer: Active ScreenConnect attacks breach MSPs, impact dozens of organizations](https://www.bleepingcomputer.com/news/security/active-screenconnect-attacks-breach-msps-impact-dozens-of-organizations/)（Huntress と ConnectWise の一次ソースは未確認）

## 3. Cisco BroadWorks・Openwave の脆弱性が悪用され、CISA KEV に追加

**何が起きたか**
CISA は2026年11月10日、悪用が確認された脆弱性の一覧（KEV）に、Cisco BroadWorks と Openwave Webtop Media Transcoder の脆弱性を追加しました。対応期限は11月24日です。
- **Cisco BroadWorks（CVE-2026-20320）**：OCI-P サービスの XXE（外部データの読み込みの不備）です。未認証で、設定情報などの機密ファイルを読み取れます。Cisco は8月19日の公表時点で、悪用は確認していないとしていました。その後、Malbear Labs が11月8日、欧州の通信事業者への攻撃を報告しました。同社は、中国語話者の攻撃者が AI の自律侵入ツールを使ったと評価しています。少なくとも13組織が標的になった可能性があります。
- **Openwave Webtop Media Transcoder（CVE-2026-111793）**：ファイル種別の制限が効かず、認証済みの攻撃者が細工したファイルで機密情報を取得できます。CVSS は4.3です。

**影響範囲**
BroadWorks は、Application Delivery Platform、Application Server、Profile Server、Xtended Services Platform が対象で、RI.2026.07 より前のバージョンです。Openwave は 1.1.22.0 より前のバージョンです。

**現状と対応**
BroadWorks は RI.2026.07 で修正されています。回避策はありません。Openwave は 1.1.22.0 以降に更新するか、Media Server 2.0 に移行してください。

**やさしい解説**
通信事業者が電話サービスの裏側で使う装置の、「書類棚の鍵が開いたままになっていた」状態です。一般の方に必要な操作はありません。これらの製品を運用する事業者は、バージョンを確認して更新してください。

**ソース**
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- Cisco アドバイザリ cisco-sa-bworks-xxe-uwUd7CEt（本文は未確認）
- [SecurityWeek: Threat actors exploit Openwave, Cisco BroadWorks vulnerabilities](https://www.securityweek.com/threat-actors-exploit-openwave-cisco-broadworks-vulnerabilities/)
- [BleepingComputer: CISA flags Cisco BroadWorks flaw as actively exploited in attacks](https://www.bleepingcomputer.com/news/security/cisa-flags-cisco-broadworks-flaw-as-actively-exploited-in-attacks/)（見出しのみ確認）

## 4. Maersk：LF Logistics のレガシーシステムから情報流出、WhiteArmor が500万ドルを要求

**何が起きたか**
2026年11月11日に報じられました。Maersk は、2022年に買収した LF Logistics のレガシーシステムへの侵入と、データの窃取を認めました。攻撃者グループ WhiteArmor は、約100GB を盗んだと主張しています。30日以内に500万ドル（ビットコイン）を支払うよう要求しています。

**影響範囲**
以下は攻撃者の主張で、検証されていません。
- ドライバー記録約3万件
- 平文のパスワード
- 管理者アカウント33件
- 配送受領書
- 端末ログ27,842件（電話番号、メールアドレス、IMEI を含む）

Maersk は、機微データの開示は確認されていないと説明しています。他のシステムや、顧客との連携（API・EDI）への影響はなく、業務の中断も見込まないとしています。侵入の時期などは公表されていません。

**現状と対応**
Maersk の説明の範囲では、利用者や取引先に必要な操作は示されていません。

**やさしい解説**
大手物流会社が買収した会社の「古い倉庫の台帳」に泥棒が入り、「返してほしければ金を払え」と脅されている状況です。盗まれた内容は犯人の言い分だけで、事実とは限りません。Maersk の発表と続報を待ちましょう。

**ソース**
- [BleepingComputer: Maersk confirms data breach as WhiteArmor ransomware demands $5 million](https://www.bleepingcomputer.com/news/security/maersk-confirms-data-breach-as-whitearmor-ransomware-demands-5-million/)（Maersk の公式声明は未確認）

## 5. 【続報】Fireworks AI の侵害で、Notion AI のチャット記録が露出

**何が起きたか**
11月11日の新しい事実です。Notion は、Fireworks AI の侵害により、Notion AI のチャット記録が露出したと公表しました。対象は、ワークスペース管理者向けの「Insights」機能のデータです。Notion は11月2日に Fireworks から警告を受けました。11月8日には、Fireworks が顧客データへのアクセスを確認しました。なお Fireworks 側は、10月23日に第三者のクラウド経由で開発環境が侵害されたとしています。The Record は、顧客データと課金情報が盗まれたと報じています。

**影響範囲**
影響を受けたのは、全ユーザーの1%未満にあたる少数のワークスペースです。多くの記録は、作成者やワークスペースを特定できません。

**現状と対応**
Notion は、Fireworks への通信を遮断し、先方にデータの削除を求め、Insights を無効化しました。影響を受けたワークスペースのオーナーは、「Security incident review」で確認できます。チャットに入力した資格情報（パスワードや API キーなど）は、変更が必要です。

**やさしい解説**
Notion が AI の処理を頼んでいた外部業者が侵害され、AI とのやり取りの記録が見られた状態です。AI のチャットにパスワードや API キーを貼り付けたことがある方は、念のため再発行してください。

**ソース**
- [BleepingComputer: Notion says Fireworks breach exposed customer AI chat transcripts](https://www.bleepingcomputer.com/news/security/notion-says-fireworks-breach-exposed-customer-ai-chat-transcripts/)（Notion の公式発表は未確認）
- [The Record: AI company Fireworks says hackers stole data in Oct. attacks](https://therecord.media/ai-company-fireworks-says-hackers-stole-data-in-oct-attacks)（見出しのみ確認）

## 6. 【続報】N-able N-central：ホットフィックスの提供と CVE の公開

**何が起きたか**
11月10日に紹介した N-central の脆弱性について、11月11日に新しい事実がありました。N-able は、N-central 2026.4 HF2 を提供しました。あわせて、7件の CVE が公開されています。
- CVE-2026-125883（XXE）
- CVE-2026-125878（OGNL インジェクション）
- CVE-2026-125879（ローカル権限昇格）
- CVE-2026-125880（格納型 XSS）
- CVE-2026-125881（SSRF）
- CVE-2026-125882（パストラバーサルによるリモートコード実行）
- CVE-2026-91000（ローカル権限昇格）

**影響範囲**
ホスト型（NCOD）は、全サーバーの更新が完了しました。オンプレミス版は、一時的にオフラインにしたうえで、早めの更新が強く推奨されています。Shadowserver が観測したインターネット露出のサーバーは、1,338台から約148台に減りました。Defused は11月11日、攻撃者による探索（未認証アクセスの試みなど）を観測したと報告しています。N-able は、悪用を確認したとはしていません。HF2 がすべての脆弱性を修正したかどうかは、不明です。

**現状と対応**
オンプレミス版の N-central を運用している場合は、HF2 を適用してください。

**やさしい解説**
IT 管理会社が顧客の端末をまとめて管理するための「中央管制室」の鍵穴に、修理の部品が届きました。まだ付けていない管制室は、探りを入れられています。一般の方に必要な操作はありません。N-central を使う IT 担当者は、早めに更新してください。

**ソース**
- [BleepingComputer: N-able releases security hotfixes for zero-day vulnerabilities](https://www.bleepingcomputer.com/news/security/n-able-releases-security-hotfixes-for-zero-day-vulnerabilities/)（N-able の公式情報は未確認）

## 7. AhsayCBS：2件のゼロデイが連鎖して悪用

**何が起きたか**
バックアップ製品 AhsayCBS の脆弱性2件が、2026年11月10日に The Hacker News で報じられました。2件を組み合わせると、認証を回避したうえで任意のコマンドを実行できます。Huntress の観測は10月初旬で、Ahsay は10月9日から顧客の報告を受けていました。侵入後には、Web シェル、暗号資産マイナー、Python 製のバックドアが設置されました。正規の遠隔操作ソフトで居座り、Veeam サーバーに保存された資格情報の取得も試みられています。

**影響範囲**
CVE は CVE-2026-105133 と CVE-2026-105134 です。対象は AhsayCBS 9 と 10ですが、正確なバージョンの範囲は不明です。CISA KEV には掲載されていません。

**現状と対応**
ホットフィックスは、v9が10月10日、v10が10月12日に提供されています。パッチは10月中旬に出ており、悪用の詳細が公表されたのが11月10日です。侵害された場合は、ホストを再構築し、最新版を導入して、侵入前のバックアップから復元してください。

**やさしい解説**
会社のデータの「予備の金庫」が壊され、その中に置いていた他の金庫の鍵まで探られた状態です。一般の方に必要な操作はありません。AhsayCBS の管理者は、修正版を適用してください。侵入の形跡がないかも確認してください。

**ソース**
- [The Hacker News（2026年11月10日）](https://thehackernews.com/2026/11/attackers-exploit-ahsaycbs-flaws-to.html)（Huntress と Ahsay の一次ソースは未確認）

## 8. NEAR AI：SGLang の RCE 脆弱性を悪用され、社内へ横展開

**何が起きたか**
NEAR AI は2026年11月10日、侵害を公表しました。オープンソースの推論エンジン SGLang のリモートコード実行の脆弱性を悪用され、推論サーバーでコードが実行されました。その後、社内に横展開されています。同社は、TEE（保護された実行環境）では、内部ソフトの脆弱性までは防げなかったと説明しています。

**影響範囲**
- 廃止済みの Private Chat の約100ユーザーについて、アカウント情報（メールアドレス、名前、一部のプランや残高）。会話内容にアクセスされた形跡はありません。
- 旧 NEAR AI Agents の18エージェントのデータ（チャット履歴、設定、ログ）。
- 顧客2社の API キーがログに露出しました。すでに失効済みです。

**現状と対応**
NEAR AI は、セッションと管理者の資格情報を失効させ、トークンを更新しました。Private Chat は停止し、全推論サーバーに SGLang の修正を適用しています。SGLang にも報告済みです。SGLang 側の CVE 番号と修正版は、不明です。

**やさしい解説**
AI を動かす「エンジン部品」に欠陥があり、そこから会社の中に入られたという話です。強固な保管庫を使っていても、部品の欠陥までは防げなかった、という説明です。SGLang を自社で使っている方は、最新の情報を確認してください。

**ソース**
- [The Hacker News: SGLang RCE exploit breaches NEAR AI](https://thehackernews.com/2026/11/sglang-rce-exploit-breaches-near-ai.html)（NEAR AI の公式発表は未確認）

## 9. 11月の各社月例更新：Ivanti・Fortinet・Adobe・Citrix（悪用の報告なし）

**何が起きたか**
2026年11月10日に、4社が月例のセキュリティ更新を公開しました。11月11日に報じられています。いずれも、悪用の報告や証拠は示されていません。

**影響範囲**
- **Ivanti（13件）**：EPM の SQL インジェクション CVE-2026-121653（CVSS 9.8、EPM 2024 SU8 で修正）、CSA の認証欠如 CVE-2026-121683（CVSS 9.4、CSA 5.0.8.1 で修正）、Sentry/EPMM のリモートコード実行 CVE-2026-105425（High）が含まれます。
- **Citrix XenServer（6件）**：CVE-2026-102705（High）は、Pool Secret を推測されると、ホストが侵害されるおそれがあります。アドバイザリは CTX697316 です。
- **Fortinet**：89件のアドバイザリ（約100件の脆弱性）で、Critical は約17件です。FortiMail が最多で、FortiAuthenticator、FortiOS、FortiManager、FortiAnalyzer、FortiSASE、FortiClient も含まれます。CVE 番号は未確認です。
- **Adobe**：9製品で約110件です。Adobe Connect に CVSS 10 が6件あり、AEM にも Critical があります。悪用は把握されていません。CVE 番号は未確認です。

**現状と対応**
各社の修正版を適用してください。Ivanti、Fortinet の Critical と、Adobe Connect の CVSS 10 の6件を優先してください。

**やさしい解説**
各社が定期的に配る「修理キット」です。今のところ、これらを狙った攻撃は報じられていません。ただ、早めに適用しておくと安心です。一般の方は、Adobe 製品や FortiClient を使っていれば、更新通知に従ってください。

**ソース**
- [SecurityWeek: Citrix, Ivanti patch critical and high-severity vulnerabilities](https://www.securityweek.com/citrix-ivanti-patch-critical-and-high-severity-vulnerabilities/)
- [SecurityWeek: Fortinet patches nearly 100 vulnerabilities](https://www.securityweek.com/fortinet-patches-nearly-100-vulnerabilities/)
- [SecurityWeek: Adobe patches 110 vulnerabilities across 9 products](https://www.securityweek.com/adobe-patches-110-vulnerabilities-across-9-products/)
- いずれもベンダーの一次ソースは未確認

---

## 今日やること

**一般利用者向け**
- ラクスルを利用したことがある方は、公式サイトの案内を確認してください。心当たりのないメールや電話には注意しましょう。
- AI のチャットにパスワードや API キーを入力したことがあれば、再発行してください（Notion AI の件）。
- Adobe 製品などの更新通知が届いたら、適用してください。

**IT担当者向け**
- ScreenConnect を使う MSP と、MSP に委託している組織は、不審なクライアントの有無、アカウント活動、セッション、MFA を確認してください。
- Cisco BroadWorks を RI.2026.07 以降に、Openwave Webtop Media Transcoder を 1.1.22.0 以降に更新してください。KEV の対応期限は11月24日です。
- N-central（オンプレミス版）に HF2 を適用してください。
- AhsayCBS 9・10 の修正版適用と、侵害の有無の確認を行ってください。
- SGLang を使っている場合は、修正版の有無と、推論サーバーの権限・ログへの資格情報の露出を確認してください。
- Ivanti、Citrix XenServer、Fortinet、Adobe の更新を適用してください。Ivanti EPM と CSA、Fortinet の Critical、Adobe Connect を優先してください。

## 留意点

- 今回は一次ソース（ラクスルの公式お知らせ、Cisco、ConnectWise、Huntress、Ahsay、N-able、Notion、Maersk、各ベンダー）を直接確認できず、多くを報道に頼っています。CISA KEV の掲載は一覧で確認しました。
- Maersk の窃取データの内容は、攻撃者の主張のみで、検証されていません。
- ラクスルの発表は11月9日で、48時間の境界付近です。Security NEXT の報道が11月11日付のため、掲載しました。
- AhsayCBS はパッチが10月中旬に出ており、悪用の詳細が公表されたのが11月10日です。
- ARARA について、NHK が11月6日に、合計約8,133万件（アドレス件数）と報じています。前回の掲載時点との差分が確認できず、続報としては見送りました。
- Microsoft 11月月例の修正総数は、報道で割れています（BleepingComputer 1,235件、SecurityWeek 1,094件、The Hacker News 1,259件）。前回の記事の数字は、確定的ではありません。
- 続報が確認できず見送ったもの：ニトリHD、Xen Orchestra、SAP、Zoom、Chrome ゼロデイ。
- 期間外、または公表日が不明で見送ったもの：阪急阪神百貨店・H2O（約126万件、公表日不明）、花キューピット（約424万件、10月28日から通知）、ドトール オンラインショップ（24,762件、公表日不明で境界付近）、JNSA 理解度チェック（11月9日以前）、ロート製薬・ネットマイル（11月9日付）、eMudhra（初報10月）、Baker Tilly（10月28日に通知開始）、11月9日の KEV 追加4件（IBM Aspera Faspex など）。
