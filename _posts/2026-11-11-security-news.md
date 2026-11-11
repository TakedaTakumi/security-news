---
layout: post
title: "今日のホットニュース（2026年11月11日）"
date: 2026-11-11 09:00:00 +0900
---

- ニトリHDが不正アクセスを公表し、最大約3,762万件の顧客情報が流出した可能性があります。パスワードとカード情報は含まれないと説明しています。
- 仮想化管理基盤「Xen Orchestra」の認証回避の脆弱性が悪用されています。Microsoft の11月月例更新は、悪用中の Outlook ゼロデイを修正しました。
- Barracuda 製品の脆弱性に悪用が確認され、CISA KEV に追加されました。Chrome のゼロデイ修正、SAP の CVSS 10.0 脆弱性4件、AI・クラウド基盤の侵害も続いています。

---

## 1. ニトリHD：不正アクセスで最大約3,762万件の顧客情報が流出した可能性

**何が起きたか**
ニトリホールディングスは2026年11月10日、第三者による不正アクセスを公表しました。11月6日に検知して通信を遮断しています。ログ解析によれば、10月中旬〜下旬から侵入されていた可能性があります。

**影響範囲**
対象は最大約3,762万件です。個人会員・購入者の会員番号、氏名、住所、電話番号、生年月日、性別、メールアドレスが含まれます。法人会員の会社名・担当者の連絡先、ニトリネットとモール内公式ショップの注文情報も対象です。パスワードとクレジットカード情報は対象外と説明されています。

**現状と対応**
侵入経路と原因は、外部専門家と調査中です。個人情報保護委員会と警察には報告・相談済みです。対象者には、メールまたは郵送で順次通知されます。ニトリは、パスワード・カード番号・暗証番号をメールや電話で尋ねることはないとしています。

**やさしい解説**
大型店の「会員名簿と配達伝票」がまとめて持ち出されたおそれがある状態です。カード番号は無事でも、名前・住所・購入履歴がそろうと「ご注文の件で」と本物らしく装う詐欺に使われます。ニトリを名乗る連絡が来ても、メールのリンクは開かないでください。公式アプリや公式サイトをブックマークから開いて確認しましょう。

**ソース**
- ニトリHD 公式発表（PDF）：https://www.nitorihd.co.jp/news/items/2b702dbe4d438f7fef74945d68e5bd27_3.pdf（取得時に HTTP 503 で閲覧できず、内容は下記報道で確認）
- [Security NEXT（2026年11月10日）](https://www.security-next.com/192572)
- [BleepingComputer: Japanese furniture giant Nitori says hackers stole 37.6M customer records](https://www.bleepingcomputer.com/news/security/japanese-furniture-giant-nitori-says-hackers-stole-376m-customer-records/)

## 2. Xen Orchestra：認証回避の脆弱性が悪用され、仮想基盤が乗っ取られるおそれ

**何が起きたか**
仮想化管理ツール「Xen Orchestra」で、認証クッキーの扱いの不備により、ログインなしで管理者として操作できる脆弱性が見つかりました（Vates のアドバイザリ VSA-2026-062）。ベンダーは実際の悪用を確認しています。悪用されると、管理下の XCP-ng ホストが root 権限で乗っ取られるおそれがあります。

**影響範囲**
Xen Orchestra と、アプライアンス版の XOA が対象です。報道時点で CVE 番号は付与されておらず、影響を受けるバージョンの下限も明らかになっていません。

**現状と対応**
修正版は Xen Orchestra 6.9.1（安定版）と 6.10.0（最新版）です。すぐ更新できない場合は、管理画面への接続元を絞ってください。侵害が疑われる場合は、仮想基盤で使うパスワードとシークレットを変更してください。この攻撃は通常のログに痕跡が残りにくいため、報道では HTTP 通信の監視と、ベンダーが示す侵害指標の確認が勧められています。

**やさしい解説**
多数のサーバーをまとめて動かす「マスターキー付きの管理室」の扉が、合言葉なしで開いてしまう状態です。一般の方に必要な操作はありません。サーバー管理者は、すぐに更新してください。

**ソース**
- [BleepingComputer: Critical Xen Orchestra auth bypass flaw exploited to hijack VM servers](https://www.bleepingcomputer.com/news/security/critical-xen-orchestra-auth-bypass-flaw-exploited-to-hijack-vm-servers/)（Vates の公式アドバイザリは今回直接確認できず）

## 3. Microsoft 11月の月例更新：悪用中の Outlook ゼロデイを修正

**何が起きたか**
Microsoft は2026年11月10日（米国時間）に月例のセキュリティ更新を公開しました。悪用が確認されたゼロデイは、Outlook のなりすましの脆弱性 CVE-2026-124194 の1件です。細工されたメッセージを扱うと、Windows のログイン認証に使う情報（NTLM ハッシュ）が攻撃者側に送られてしまいます。CISA も同日、悪用が確認された脆弱性の一覧（KEV）に追加しました。

**影響範囲**
報道によると、緊急（Critical）は66件です。Active Directory ドメインサービス（CVE-2026-118146）、Defender（CVE-2026-122194）、Exchange Server（CVE-2026-118207）、Office（CVE-2026-120003）のリモートコード実行が含まれます。修正の総数は約1,235件と報じられていますが、数え方（Edge を含むか、月初の修正分を含むか）は確認できていません。

**現状と対応**
Windows Update と Microsoft 365（Office）の更新を適用してください。組織では、Outlook と Exchange Server を優先して更新してください。

**やさしい解説**
Outlook のゼロデイは、届いたメールが「勝手に外部へ社員証のコピーを見せに行く」ような問題です。パソコンの更新通知が来たら、後回しにせず再起動まで済ませましょう。

**ソース**
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [BleepingComputer: Microsoft November 2026 Patch Tuesday fixes 1,235 flaws, Outlook zero-day](https://www.bleepingcomputer.com/news/microsoft/microsoft-november-2026-patch-tuesday-fixes-1-235-flaws-outlook-zero-day/)

## 4. 【続報】Barracuda 製品：root 権限取得の脆弱性で悪用を確認

**何が起きたか**
11月4日に紹介した Barracuda 製品の脆弱性2件について、新しい事実がありました。Barracuda は11月9日にアドバイザリを更新し、「少数の組織」に対する悪用を認めました。CISA も11月10日付で、2件を KEV に追加しました。

**影響範囲**
対象は CVE-2026-116606（Email Security Gateway の認証の弱さ）と CVE-2026-111560（認証不要の OS コマンド実行）です。2件を組み合わせると root 権限を取られます。CVE-2026-111560 は、ESG のほか Load Balancer ADC、Message Archiver、WAF、WAF Control Center、Web Security Gateway にも影響します。悪用には管理画面に届くことが条件です。

**現状と対応**
修正パッチは約1週間前から提供されています。未適用の場合は、すぐに適用してください。あわせて、管理画面は信頼できる社内ネットワークからだけ開けるようにしてください。

**やさしい解説**
「修理キットは配られていたのに、付け忘れた家が狙われ始めた」段階です。IT 担当者は、パッチを適用済みかを今日中に確認してください。

**ソース**
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [BleepingComputer: Hackers exploit Barracuda Email Security Gateway flaws to get root access](https://www.bleepingcomputer.com/news/security/hackers-exploit-barracuda-email-security-gateway-flaws-to-get-root-access/)

## 5. Chrome：悪用が確認されたゼロデイ CVE-2026-125350 を修正

**何が起きたか**
Google は2026年11月10日、Chrome の XML 処理部分にある use-after-free（解放済みメモリの再利用）の脆弱性 CVE-2026-125350 を修正しました。Google は、この脆弱性の悪用コードが出回っていると認めています。CISA も同日、KEV に追加しました。

**影響範囲**
対象は、Windows・macOS・Linux 版の Chrome です。修正版は 157.0.8103.50（macOS は .50/.51）です。報道では今年8件目の悪用ゼロデイとされていますが、同じ記事に載っている一覧は7件で、数は一致しません。

**現状と対応**
Chrome の「設定 → Chrome について」を開いて更新し、再起動してください。Chromium ベースの他のブラウザ（Edge など）も、提供され次第更新してください。

**やさしい解説**
Web ページを見るだけで攻撃されるおそれがある種類の欠陥です。ブラウザの右上に「更新」が出ていたら、すぐに押して再起動しましょう。

**ソース**
- [BleepingComputer: Google patches eighth Chrome zero-day exploited in attacks this year](https://www.bleepingcomputer.com/news/security/google-patches-eighth-chrome-zero-day-exploited-in-attacks-this-year/)
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)

## 6. AI・クラウド基盤の侵害が相次ぐ：Railway、Fireworks AI、Qubole

**何が起きたか**
2026年11月10日、AI やクラウドの開発基盤に関わる侵害が、3件まとめて報じられました。
- **Railway**：10月の侵害について、詳しい報告書を公開しました。ビルド基盤の未知の脆弱性から内部資格情報を奪われ、顧客の環境変数（AI サービスの API キーなど）を復号できる状態になっていました。盗まれたキーによる AI の不正利用は約74万ドルにのぼります。
- **Fireworks AI**：委託先のクラウド事業者が侵害された後、開発マシンで不正な処理が実行されたと公表しました。請求情報や一部顧客のモデル重み・データセットにアクセスされました。
- **Qubole**：データ分析基盤 Qubole の IAM ユーザー2件が悪用されました。顧客の AWS 環境で Qubole を信頼する設定が使われ、シークレットや S3 上のデータが盗まれました。数十社が被害を受けたと報じられています。

**影響範囲**
Railway で影響を受けうるのは、最大でワークスペース全体の約1.85%（約10万）です。これは上限で、実際に盗まれた数ではありません。1,852 ユーザーの連携トークン（GitHub OAuth など）も露出しました。Qubole の件の被害期間は10月14〜26日です。Qubole 本体はまだ公式に発表していません（未確認）。

**現状と対応**
Railway は脆弱性を修正し、露出したトークンをリセットしました。不正利用分は、AI 事業者と返金を調整し、残りを自社で負担するとしています。Qubole を使っている、または使っていた組織には、10月1日以降の CloudTrail の確認と資格情報の更新が勧められています。あわせて、不要なクロスアカウントロールの削除も勧められています。

**やさしい解説**
開発者が預けていた「AI サービスの合鍵」が狙われ、他人の財布で AI を使われるという被害です。クラウド上に API キーを置いている方は、キーの再発行と、利用額アラートの設定を検討してください。

**ソース**
- [BleepingComputer: Railway breach leads to $740,000 in fraudulent AI charges](https://www.bleepingcomputer.com/news/apple/railway-breach-leads-to-740-000-in-fraudulent-ai-charges/)（Railway のインシデント報告を引用。報告本体は未参照）
- [BleepingComputer: Fireworks AI discloses new breach after cloud provider hack](https://www.bleepingcomputer.com/news/security/fireworks-ai-discloses-new-breach-after-cloud-provider-hack/)
- [BleepingComputer: Hackers exploit trusted AWS access to breach multiple cloud environments](https://www.bleepingcomputer.com/news/security/hackers-exploit-trusted-aws-access-to-breach-multiple-cloud-environments/)

## 7. SAP：CVSS 10.0 の脆弱性4件を含む11月の更新

**何が起きたか**
SAP は11月の月例更新で35件の脆弱性を修正しました。うち4件は、認証なしで遠隔からシステムを掌握されうる最も深刻な評価（CVSS 10.0）です。

**影響範囲**
最も深刻な4件は次のとおりです。
- NetWeaver AS ABAP の ICM（CVE-2026-76964）
- SAP Web Dispatcher（CVE-2026-89126）（上の1件と合わせて「ICM2SHELL」と呼ばれる）
- NetWeaver AS ABAP の SAML2 Service Provider（CVE-2026-120017）
- SAP Gateway（CVE-2026-89103、通称「PROXYGATE」）

報道時点で、悪用の報告はありません。

**現状と対応**
SAP のセキュリティノートを確認し、パッチを適用してください。影響バージョンとノート番号は、今回は一次ソースで確認できていません。

**やさしい解説**
企業の会計・人事・物流をつかさどる「基幹システム」の欠陥です。一般の方に必要な操作はありません。SAP を運用する企業は、計画を前倒しして適用してください。

**ソース**
- [BleepingComputer: SAP patches four maximum severity security vulnerabilities](https://www.bleepingcomputer.com/news/security/sap-patches-four-maximum-severity-security-vulnerabilities/)

---

## 今日やること

**一般利用者向け**
- ニトリを名乗るメール・SMS・電話には注意してください。リンクは開かず、公式アプリやブックマークから確認しましょう。
- Windows Update、Office、Chrome を更新し、再起動まで済ませてください。
- iPhone の更新（11月9日公開の iOS 27.2.1 など）が届いていれば適用してください。

**IT担当者向け**
- Microsoft の11月更新を適用してください（Outlook と Exchange Server を優先）。
- Xen Orchestra を 6.9.1 または 6.10.0 に更新し、管理画面への接続元を制限してください。
- Barracuda 製品のパッチの適用状況を確認し、管理画面を内部ネットワークに限定してください。
- SAP のセキュリティノートを確認し、CVSS 10.0 の4件を優先してください。
- クラウドに置いた API キーとクロスアカウントロールを棚卸しし、Qubole 連携があれば CloudTrail を確認してください。
- Zoom Workplace for Windows の Critical 脆弱性（CVE-2026-108186、CVSS 9.6）も公表されています。最新版へ更新してください（[Security NEXT](https://www.security-next.com/192629)）。

## 留意点

- 今回は一次ソース（ニトリの公式PDF、Vates・Microsoft・SAP・Barracuda の公式アドバイザリ）を直接確認できず、多くを報道に頼っています。CISA KEV の掲載は一覧で確認しました。
- ニトリの件数は「最大」の値で、実際の流出件数は確定していません。日本語の報道は Security NEXT のみで確認しています。
- Microsoft の修正総数（約1,235件）は報道の数字です。集計方法は未確認です。
- 掲載済み案件の N-able N-central と ARARA（SEGA）は、昨日の記事以降に新しい事実が確認できなかったため、掲載を見送りました。
- 期間外として見送ったもの：Crédit Mutuel Arkéa の不正送金（11月4日公表）、OpenAM の脆弱性（10月22日公開）。
- 年の確認や一次ソースの確認ができなかったため、全国鍼灸マッサージ協会オンラインストアのカード情報流出の可能性は見送りました。
