---
layout: post
title: "今日のホットニュース（2026年11月13日）"
date: 2026-11-13 09:00:00 +0900
---

- 乗っ取られた GitHub アカウント4,837件を使い、CI（自動ビルド）のシークレットを盗むキャンペーンが報じられました。少なくとも1,835の対象で窃取が確認されています。
- 続報として、N-able N-central は修正版（HF2）を適用した環境でも悪用が報告されています。Apache HTTP Server の HTTP/2 や NetScaler、Windows の未修正ゼロデイ SignDrop など、重大な脆弱性が相次ぎました。
- 国内では日本商工会議所のネット試験で最大約98万人分の情報が流出した可能性があります。Apify の侵害や、Operation Endgame、Binance の続報もあります。

---

## 1. GitHub アカウント4,837件を乗っ取った CI シークレット窃取キャンペーン

**何が起きたか**
攻撃者「wfx-loot」が、乗っ取った4,837件の GitHub アカウントを使い、61,764のリポジトリへの書き込み権限を探りました。書き込めた場合は、GitHub Actions のシークレットやクラウドの認証情報を盗む仕掛けを置いたとされます。11月10日12:45 UTC ごろに始まり、11月12日に報じられました。発見したのはセキュリティ企業 Aikido で、2025年の GhostAction と重なる点があるとされています。アカウントの乗っ取りの経路は分かっていません。

**影響範囲**
BleepingComputer は、少なくとも1,835の対象で窃取が確認されたと報じています。The Hacker News の見出しは「1,806以上」で、数字が割れています。被害に挙がった組織として、Fortune 100 企業、米 GSA、フランス政府、Nextcloud、WebdriverIO が報じられていますが、各組織の公式な確認はありません。約50のアカウントは npm や PyPI などへの公開権限も持っていました。Packagist のパッケージと Go モジュール2版には、ペイロードの混入が報じられています。

**現状と対応**
手口は、「docs: dependency audit notes」という PR で書き込み可否を探り、ワークフローの改変などで情報を盗むものです。その後、変更を元に戻し、実行ログを削除したとされます。狙われたのは、GitHub トークン、クラウド・SSH・コンテナ・パッケージ公開・Vault/Terraform の資格情報、AI サービスの API キーです。確認する点は次のとおりです。
- 「wfx-docs」というブランチがないか。
- 上記タイトルの PR がないか。
- ワークフローの実行番号に欠番がないか。

実行が見つかった場合は、そのワークフローが使えるすべてのシークレットとクラウドのロールを、侵害済みとして更新してください。

**やさしい解説**
合鍵を手に入れた泥棒が、多くの家の郵便受けをこっそり開け、中の鍵束を写して元に戻していくようなものです。開けた跡も消されるため、気づきにくくなっています。GitHub を使う方は、見覚えのない PR やブランチがないか確認してください。2要素認証の設定も見直しましょう。

**ソース**
- [BleepingComputer: Hackers compromise 4,800 GitHub accounts to steal cloud credentials](https://www.bleepingcomputer.com/news/security/hackers-compromise-4-800-github-accounts-to-steal-cloud-credentials/)
- [The Hacker News](https://thehackernews.com/2026/11/4837-hijacked-github-accounts-ran-ci.html)（見出しのみ確認）
- [SecurityWeek](https://www.securityweek.com/attacker-targets-60000-github-repositories-in-credential-theft-campaign/)（見出しのみ確認）
- Aikido の一次レポートは未確認

## 2. 【続報】N-able N-central：修正版（HF2）適用済みでも悪用、新たな攻撃チェーン

**何が起きたか**
11月12日の新しい事実です。研究者の Sean Bales が、2つの攻撃チェーンの PoC を公開しました。
- **4EverAble2Shell**：Legacy API が有効な N-central で、認証なしに root 権限でコマンドを実行できます。Apache Axis の CVE-2026-90436 と、別の権限昇格を連鎖させるものです。
- **Agent2Shell**：管理下の Windows 端末で、SYSTEM 権限のコマンド実行ができると主張されています。

PoC は、11月10日の HF2（2026.4.1.26 HF2）にも有効だと報告されています。

**影響範囲**
Previdian のハニーポット（おとり環境）で、11月12日 08:30 UTC ごろに試行が確認されました。Huntback は、少なくとも21台の本番サーバーの侵害を確認しています。うち19台は HF2 適用済みでした。暗号資産マイナー XMRig が設置されています。場所は米国、カナダ、南アフリカ、英国、ドイツ、フランス、スウェーデンです。侵害の痕跡の例は、予期しない xvd.service や、/tmp/.xvd・/var/tmp/.xvd 配下のファイルです。

**現状と対応**
N-able は11月12日のアドバイザリで、一部機能を制限し、Intune 連携を予防的に無効化しました。オンプレミスの顧客には、Legacy API が無効（既定）であることの確認を求めています。ホスト環境は保護済みで、新たな欠陥による侵害の兆候は見ていないとしており、研究者側の報告と食い違っています。恒久的な修正は示されていません。

**やさしい解説**
中央管制室の鍵を付け替えたのに、別の窓から入られた状態です。一般の方に必要な操作はありません。N-central を運用する IT 担当者は、Legacy API が無効かを確認し、上記の痕跡を調べてください。

**ソース**
- [BleepingComputer: New N-able 4EverAble2Shell zero-day exploited hours after PoC released](https://www.bleepingcomputer.com/news/security/new-n-able-4everable2shell-zero-day-exploited-hours-after-poc-released/)
- [The Hacker News](https://thehackernews.com/2026/11/new-n-central-exploits-work-against.html)（見出しのみ確認）
- [SecurityWeek](https://www.securityweek.com/hackers-target-n-central-zero-days-as-n-able-rushes-patches/)（見出しのみ確認）
- N-able の公式情報は未確認

## 3. Apache HTTP Server の HTTP/2 に重大な脆弱性

**何が起きたか**
mod_http2 の競合状態によるメモリ破壊 CVE-2026-119618 が修正されました。Red Hat は CVSS 9.8 と評価しています。11月11日に 2.4.71 が公開され、11月12日に報じられました。Anthropic の OSS スキャナー（10月26日報告）と、Google Cloud の研究者2名（11月3日）が、それぞれ独立に報告したとされます。

**影響範囲**
対象は、HTTP/2 を有効にした 2.4.55 から 2.4.70 のサーバーです。HTTP/1.1 のみなら影響はありません。2.4.71 は、CVE-2026-106023（クラッシュ、important）と CVE-2026-109163（低）も修正しています。

**現状と対応**
Wiz は11月11日時点で、悪用の報告はないとしています。公開されている PoC はクラッシュの再現で、リモートコード実行の実証ではありません。一方、Red Hat は信頼できる悪用が研究で示されたとしていますが、根拠は特定できず、情報が割れています。2.4.71 へ更新してください。できない場合は HTTP/2 を無効化してください。

**やさしい解説**
Web サーバーの「窓口の同時対応」の部分に、順番の取り違えで壊れる欠陥がありました。一般の方に必要な操作はありません。サイトを運営する方は、Apache のバージョンと HTTP/2 の設定を確認してください。

**ソース**
- [SecurityWeek: Apache patches critical HTTP Server RCE found by Anthropic, Google](https://www.securityweek.com/apache-patches-critical-http-server-rce-found-by-anthropic-google/)
- [BleepingComputer](https://www.bleepingcomputer.com/news/security/apache-http-server-patches-critical-http-2-remote-code-execution-flaw/)（見出しのみ確認）
- [The Hacker News](https://thehackernews.com/2026/11/critical-apache-http2-flaw-could-let.html)（見出しのみ確認）
- Apache の公式情報は未確認

## 4. NetScaler ADC / Gateway に複数のクリティカルな脆弱性

**何が起きたか**
Cloud Software Group が11月12日（現地時間）にアドバイザリを公開し、Security NEXT が11月13日に報じました。総数は28件とされています。
- **CVE-2026-107412**：CVSS v4 で 9.5。ゲートウェイまたは AAA 仮想サーバー構成でのメモリ溢れです。
- **CVE-2026-120868**：9.3。パケット処理時のメモリ溢れです。9.3 の脆弱性は8件あります。
- **CVE-2026-120864**：ICA プロキシ関連です。
- **CVE-2026-111344**：エンドポイント分析関連です。この2件は深刻度の記載がありません。
- **CVE-2026-120869**：NetScaler Console（旧 ADM）の脆弱性で、別のアドバイザリでクリティカルとされています。

**影響範囲**
The Hacker News は「NetScaler と Secure Access Client の12件」と見出しで報じており、件数が食い違っています（見出しのみ確認）。影響バージョン、修正版の番号、悪用の有無は未確認です。

**現状と対応**
修正版への更新が必要です。NetScaler の脆弱性は過去にも繰り返し悪用されてきたため、早めの更新が望ましいといえます。

**やさしい解説**
会社の出入口にある「受付ゲート」の部品に、多数の欠陥が見つかった状態です。一般の方に必要な操作はありません。NetScaler を使う IT 担当者は、アドバイザリで自社の版が対象かを確認してください。

**ソース**
- [Citrix アドバイザリ CTX697305](https://support.citrix.com/support-home/kbsearch/article?articleNumber=CTX697305)（本文は取得できず）
- CTX697320（Console 向け、未確認）
- [Security NEXT](https://www.security-next.com/192789)

## 5. Windows CLFS の未修正ゼロデイ「SignDrop」の PoC が公開

**何が起きたか**
11月12日に報じられました。Nightmare Eclipse の名で活動する研究者が公開したものです。CLFS（Windows のログ基盤）が認証用ファイルを作る処理に論理的な欠陥があり、特権プロセスにログファイルを開かせると、SYSTEM 権限へ昇格できます。2025年10月の CLFS の緩和策に由来するとされています。

**影響範囲**
研究者は、Windows 11 26H2 と Windows Server 2025 の試験版で検証しています。「約80%の環境が影響」やタンパー保護の無効化は、研究者の主張で、未検証です。

**現状と対応**
PoC は GitHub にあります。実際の攻撃での悪用は、報じられていません。CVE はなく、公式パッチも、実質的な回避策もありません。Microsoft の公式声明は未確認です。月例更新を待ちつつ、EDR で不審な権限昇格を監視してください。

**やさしい解説**
すでに建物に入った人が、管理人の権限を手に入れてしまう欠陥です。入り込まれないことが最初の防御になります。利用者は、不審なファイルを開かないようにしてください。

**ソース**
- [BleepingComputer: New Windows SignDrop zero-day gives hackers SYSTEM privileges](https://www.bleepingcomputer.com/news/security/new-windows-signdrop-zero-day-gives-hackers-system-privileges/)
- [The Hacker News](https://thehackernews.com/2026/11/new-signdrop-zero-day-exploit-turns.html)（見出しのみ確認）
- Microsoft の公式情報は未確認

## 6. 日本商工会議所「ネット試験」の管理システムに不正アクセス、最大約98万人

**何が起きたか**
外部サーバー上の試験管理システムに、不正なプログラムが設置されました。11月4日にシステム管理会社の報告で発覚し、不正ファイルの削除とパッチ適用を行っています。11月9日に個人情報保護委員会へ報告しました。公表は11月10日付と報じられています（推定で、公式ページは未確認）。Security NEXT が11月12日に報じました。設置日を11月1日とする報道がありますが、日付の整合は未確認です。

**影響範囲**
2022年4月1日から2026年11月4日にネット試験を受けた、最大約98万人が対象です。対象の試験は、簿記、リテールマーケティング（販売士）、日商PC、電子会計実務、キータッチ2000、ビジネスキーボード、日商プログラミング、日商ビジネス英語です。情報は、氏名、生年月日、性別、合否、得点、任意入力の住所・電話番号・メールアドレスです。決済情報は含まれません。

**現状と対応**
不正利用は確認されていません。試験は通常どおり受験できます。

**やさしい解説**
試験の「受験者名簿」を置いていた倉庫に、不審な装置が仕掛けられていた状態です。過去に受験した方は、日本商工会議所の案内を確認してください。心当たりのないメールや電話には注意してください。

**ソース**
- 日本商工会議所の公式サイト（https://www.jcci.or.jp/ 、該当のお知らせは未確認）
- [Security NEXT](https://www.security-next.com/192652)
- [Impress Watch](https://www.watch.impress.co.jp/docs/news/2155307.html)（検索結果の要約のみ確認）

## 7. 【続報】ScreenConnect を悪用した MSP 攻撃：ツールキット「SCKit」と侵入経路

**何が起きたか**
11月12日の新しい事実です。「SCKit」は、16のスクリプトなどからなるツールキットです。不正なクライアントを入れ、顧客端末から技術者の端末への拡散を試みます。中核の RelayTrap は、ScreenConnect のファイル転送の欠陥 CVE-2026-84869（26.6.5 で修正）を突こうとします。コードは LLM が生成した可能性が高いとされています。技術者の端末ではセッション Cookie を盗み、パスワードや MFA なしでセッションの乗っ取りを狙います。

**影響範囲**
少なくとも288台、48組織です。全端末が90分以内に標的になったとされます。

**現状と対応**
初期侵入について、Huntress はサードパーティ拡張「RMM+」の 1.0.31 と 1.0.32 が原因とみています。アクセスキーが未設定だと、認証なしでコマンドを実行できます。ConnectWise は、関連の可能性がある5つの拡張を、約400のパートナー環境で無効化しました。拡張があるだけで侵害とは限らないとしています。ワーム的な拡散の成功例は、Huntress と Blackpoint は確認していません。Blackpoint は、最新のクライアントがエクスプロイトを阻止したと報告しています。ScreenConnect を 26.6.5 以降に更新し、RMM+ などの拡張の有無とアクセスキーの設定を確認してください。

**やさしい解説**
マスターキーの管理会社の入口に弱い扉があり、そこから入った者が、各テナントへ偽の鍵を配ろうとした状況です。一般の方に必要な操作はありません。MSP に IT 管理を任せている組織は、委託先に対応状況を確認してください。

**ソース**
- [BleepingComputer: New worm-like SCKit malware targets MSPs in ScreenConnect attacks](https://www.bleepingcomputer.com/news/security/new-worm-like-sckit-malware-targets-msps-in-screenconnect-attacks/)
- [The Record](https://therecord.media/connectwise-screenconnect-breaches-third-party-tool)（見出しのみ確認）
- [The Hacker News](https://thehackernews.com/2026/11/sckit-malware-targets-screenconnect.html)（見出しのみ確認）
- Huntress と ConnectWise の一次情報は未確認

## 8. Red Hat Quay に CVSS 9.8・9.9 の脆弱性

**何が起きたか**
11月12日に報じられました。
- **CVE-2026-123710（9.8）**：攻撃者が自前の署名鍵を信頼鍵に追加でき、任意のリポジトリのトークンを偽造できます。プライベートイメージの読み書きなどが可能になります。匿名アクセスが有効だと認証なしで悪用できます。無効化だけでは完全には防げません。
- **CVE-2026-110697（9.9）**：名前空間を作れるユーザーが、他テナントのロボットアカウントのトークンを盗めます。

**影響範囲**
Quay 3 と 5 の全バージョンが対象です（スタンドアロン、Quay Operator、mirror registry for OpenShift）。Quay.io は修正済みです。悪用や PoC の報告はありません。

**現状と対応**
修正状況は情報が割れています。8つの Quay 3 ブランチに修正版があるとする一方、記事自身が、CVE ページは未修正のままだと指摘しています。CVE-2026-110697 の修正状況は不明です。暫定策は次のとおりです。
- /keys エンドポイントをプロキシなどで遮断する。
- 鍵の追加・削除イベントを監査する。
- 不明なサービス鍵を削除する。
- ロボットトークンを更新する。
- アンダースコアを含む名前空間の作成権限を制限する。

**やさしい解説**
荷物を預かる倉庫で、偽の身分証を登録され、他人の荷物を出し入れされるおそれがある状態です。一般の方に必要な操作はありません。Quay を運用する方は、暫定策を実施し、Red Hat の情報を確認してください。

**ソース**
- [The Hacker News](https://thehackernews.com/2026/11/critical-red-hat-quay-flaw-lets.html)
- [SecurityWeek](https://www.securityweek.com/critical-red-hat-quay-vulnerability-could-expose-private-container-images/)（見出しのみ確認）
- Red Hat の公式情報は未確認

## 9. Apify：内部システムへの不正アクセスで API トークンを一斉更新

**何が起きたか**
Apify が11月12日に公表しました。11月9日から10日にかけて内部システムの一部へ侵入され、翌日に検知して遮断しました。2段階認証コードが露出した可能性があります。

**影響範囲**
影響を受けた顧客の数と、侵入経路は不明です。パスワードは影響なし、アカウントデータへの影響の兆候もないとされています。

**現状と対応**
Apify は次の対応を行いました。
- 内部の認証情報の無効化。
- API トークンと Apify Proxy のパスワードの更新。
- セッションのリセット。
- GitHub などの外部 OAuth 連携の一部取り消し（再接続は後日メールで案内）。

利用者は、2段階認証の再設定、自分のコードや連携先に保存した旧トークンの差し替え、OAuth 連携の再接続を行ってください。

**やさしい解説**
施設の合鍵をすべて交換する、という対応です。古い鍵を持ったままだと、入れなくなります。Apify の利用者は、使っているプログラムや連携サービスの鍵（トークン）を新しいものに入れ替えてください。

**ソース**
- [BleepingComputer: Apify rotates API tokens, prompts 2FA resets after breach](https://www.bleepingcomputer.com/news/security/apify-rotates-api-tokens-prompts-2fa-resets-after-breach/)
- Apify の公式声明は未確認

## 10. その他の脆弱性：MongoDB Server と PTC Windchill / FlexPLM

**何が起きたか**
- **MongoDB Server（CVE-2026-118383、CVSS v4 9.5）**：レプリカセットのメンバーに use-after-free があります。認証不要の特定のコマンドで、選出時に遅れたメンバーがクラッシュします。リモートコード実行の可能性は示唆されていますが、未実証です。
- **PTC Windchill / FlexPLM（CVE-2026-126325、CVSS v4 9.2）**：信頼できないデータのデシリアライズによる、リモートコード実行です。

**影響範囲**
- MongoDB：系列ごとの対象版はアドバイザリで確認してください。8.2 系は7月31日に EOL を迎え、一覧に含まれません。
- PTC：Windchill 11.0 M030、11.1 M020、11.2.1.0、12.0.2.0、12.1.2.0、13.0.2.0、13.1.0.0〜13.1.4.0、FlexPLM 13.1.0.0〜13.1.3.0 です。

**現状と対応**
- MongoDB：修正版が公開されています（報道では 8.0.37 など）。公開 PoC があります。悪用の試みは把握されていません。Atlas は保守時に適用されます。自社で運用する場合は、全メンバーを更新し、DB へのネットワークを制限してください。
- PTC：PTC のホスト環境は修正済みです。自社で運用する場合は、パッチの適用が必要です。それまでは、ネットワークの制限と Web シェルの監視を行ってください。悪用は報じられていません。同じ製品の別の脆弱性は7月に悪用されたと報じられています。

**やさしい解説**
どちらも企業が自社で動かす基盤ソフトの欠陥で、「施錠の甘い裏口」にあたります。一般の方に必要な操作はありません。該当製品を運用する担当者は、版を確認して更新してください。

**ソース**
- MongoDB：[The Hacker News](https://thehackernews.com/2026/11/critical-pre-auth-mongodb-flaw-cve-2026.html)、[Security NEXT](https://www.security-next.com/192699)
- PTC：[The Hacker News](https://thehackernews.com/2026/11/ptc-patches-critical-windchill-and.html)
- 各ベンダーの一次情報は未確認

## 11. 摘発・押収：Operation Endgame と Binance 流出資金

**何が起きたか**
- **Operation Endgame（新規）**：11月12日、Europol 主導で、Gootloader、CastleRAT、StealC のインフラが摘発されました。9か国が参加し、257のドメインと235台のサーバーを押収しました。約640万件の被害者データ（認証情報は600万件超）が確認され、Have I Been Pwned などで通知される見込みです。
- **【続報】Binance**：11月12日の報道です。米司法省が、盗まれた資産のうち12億ドル超の差押えと凍結の裁判所承認を得ました。被害総額は約63億ドルと報じられています（64.3億ドルとする報道もあり、割れています）。複数のプラットフォームで、計約27億ドルが凍結されています。Binance と FBI は北朝鮮の TraderTraitor によるものとしていますが、北朝鮮は否定しています。同時に、FBI と司法省は「FaceStealer」のインフラを妨害しました。偽の Zoom/Teams 会議の招待で、18か月に4億ドル超を盗んだとされています。

**影響範囲**
Endgame は、押収したデータに含まれる約640万件が対象です。Binance は上記の金額のとおりです。

**現状と対応**
Endgame の被害者は通知される見込みです。Binance の資金の凍結と押収は、続いています。

**やさしい解説**
Endgame は、泥棒が盗んだ鍵束ごと警察が押さえた、というイメージです。自分のメールアドレスが含まれていないか、Have I Been Pwned で確認してください。含まれていたら、パスワードを変更し、2段階認証を有効にしましょう。偽の会議招待のリンクは、開かないようにしてください。

**ソース**
- Endgame：[BleepingComputer: Police dismantles Gootloader, CastleRAT, StealC malware infrastructure](https://www.bleepingcomputer.com/news/security/police-dismantles-gootloader-castlerat-stealc-malware-infrastructure/)、[The Record](https://therecord.media/european-authorities-take-down-stealic-malware-second-time)（見出しのみ確認）
- Binance：[The Record](https://therecord.media/stolen-binance-crypto-recovered-doj-facestealer-disrupted)、[The Hacker News](https://thehackernews.com/2026/11/threatsday-59-linux-kernel-bugs-falcon.html)
- 米司法省の発表は未確認

---

## 今日やること

**一般利用者向け**
- 日商のネット試験を受けたことがある方は、日本商工会議所の案内を確認してください。心当たりのないメールや電話には注意しましょう。
- Have I Been Pwned で、自分のメールアドレスが漏えいしていないか確認してください。
- Apify を使っている方は、2段階認証を再設定してください。
- GitHub を使っている方は、見覚えのない PR やブランチがないか確認してください。
- 不審なファイルや、偽の会議招待のリンクは開かないでください。

**IT担当者向け**
- GitHub の組織は、「wfx-docs」ブランチ、「docs: dependency audit notes」の PR、ワークフロー実行番号の欠番を確認してください。見つかった場合は、シークレットとクラウドのロールを更新してください。
- N-central は、Legacy API が無効かを確認し、xvd.service などの痕跡を調べてください。
- Apache HTTP Server を 2.4.71 へ更新してください。できなければ HTTP/2 を無効化してください。
- NetScaler と NetScaler Console は、アドバイザリで対象版を確認し、更新してください。
- ScreenConnect を 26.6.5 以降に更新し、RMM+ などの拡張とアクセスキーを確認してください。
- Red Hat Quay は、暫定策（/keys の遮断、鍵の監査、ロボットトークンの更新など）を実施してください。
- MongoDB は全メンバーを更新し、PTC Windchill / FlexPLM はパッチを適用してください。
- Apify のトークンと OAuth 連携を差し替えてください。
- SignDrop は、EDR で不審な権限昇格を監視し、月例更新を待ってください。

## 留意点

- 今回は一次ソース（各ベンダー・企業の公式発表）を直接確認できたものはほぼなく、多くを報道に頼っています。CISA KEV は、11月11日〜12日の新規追加をページ上で確認できませんでした（11月10日の追加分は既出です）。
- 報道で数字が割れているものがあります。GitHub 攻撃の件数（1,835件／1,806件）、Binance の被害額（約63億ドル／64.3億ドル）、NetScaler の件数（28件／12件）です。
- N-central の侵害件数は研究者側の報告です。N-able は、新たな欠陥による侵害の兆候はないとしています。
- 日商ネット試験は、公表が11月10日で48時間の境界付近です。報道が11月12日のため掲載しました。
- 期間外として見送ったもの：Microsoft 365 の大規模障害（11月12日、サイバー攻撃ではなく可用性障害のため本編では扱いません）、ポーランドの政府基盤 ePUAP のサイバー攻撃による停止（11月11日、詳細不明）。
- 一次発表が期間外のため見送ったもの（報道は期間内）：NTTデータ受託の住友生命 Vitality 関連サービス（約8万人、11月9日発表）、良品計画 第四報（11月9日）、資生堂 肌測定システム（2,515件）、ブックオフ（第3報11月6日）、ノジマオンライン（約700万件、11月2日）、Maru-Jan（約186万人、11月7日）、ApplyNow（11月4日）、丸井グループ（11月2日）、九州電力送配電（11月5日）、Baker Tilly（9月に把握、10月28日に精査完了）。
- 続報が確認できず見送ったもの：ラクスル、ニトリHD、Maersk、Notion/Fireworks、Xen Orchestra。ARARA は、重複除外後の合計約8,133万件が報じられましたが、前回までに言及済みで新事実といえず、見送りました。
- 見出しのみで未確認のため見送ったもの：Node.js の16件の修正、Chrome・Firefox の更新、Google Cloud による AMD CPU の欠陥の警告、Microsoft が報告した Linux カーネルの59件。
