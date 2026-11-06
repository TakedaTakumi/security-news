---
layout: post
title: "今日のホットニュース（2026年11月6日）"
date: 2026-11-06 09:00:00 +0900
---

## 今日のポイント

- Zyxel GS1900 シリーズのスイッチで、既存の修正では防げない別の未修正脆弱性が悪用され、48か国の約1,000台が侵害されました。修正ファームウェアは10月22日に公開済みです。
- DigiCert（顧客の身分証類を含む可能性）と DreamHost（FTP認証情報等）で、サービス事業者側の情報流出が相次いで公表されました。
- Debian/Ubuntu の APT、Ruby on Rails の Active Storage、Alpine 等の OpenSSH と、広く使われる基盤ソフトの深刻な脆弱性に修正版が出ています。国内ではデニーズ・資さんうどんが情報流出の可能性を公表しました。

---

## 1. Zyxel GS1900 スイッチのゼロデイ（CVE-2026-107441）：約1,000台が侵害

**何が起きたか**
Zyxel 製 GS1900 シリーズ（管理画面付きスイッチ）の Web 管理画面に、認証なしで OS コマンドを実行できる脆弱性（CVE-2026-107441）があり、悪用されていました。当初は6月に修正済みの別の脆弱性（CVE-2026-7273）と見られていましたが、Binarly の調査で、実際には別の未修正の欠陥だったと判明したと報じられています。

**影響範囲**
- GS1900 シリーズの10機種。
- GreyNoise の観測では、侵害は996台・48か国。8月中旬ごろから悪用が始まり、設定情報や管理者の認証情報（ハッシュ）が持ち出されたとされます。

**現状と対応**
Zyxel は10月22日に修正ファームウェアを公開し、11月3日に公式アドバイザリを出しました。対象バージョン番号は公式アドバイザリで確認してください。攻撃者が既存の修正を意図的に回避したのかは、報道上も不明です。

**やさしい解説**
オフィスの「ネットワークの交通整理装置」の、鍵のかかっていない裏口が見つかった状態です。しかも一度「鍵を直した」と案内された後に別の裏口が残っていました。装置の管理画面をインターネットから見える状態にしていると狙われます。IT担当者は、管理画面を外部に公開していないか確認し、ファームウェアを更新してください。侵害が疑われる場合は管理者パスワードの変更も必要です。一般利用者が直接できることは特にありません。

**ソース**
- [Zyxel セキュリティアドバイザリ（GS1900 の範囲外書き込み脆弱性）](https://www.zyxel.com/global/en/support/security-advisories/zyxel-security-advisory-for-out-of-bounds-write-vulnerability-in-gs1900-series-switches-11-03-2026)
- [BleepingComputer：Zyxel fixes zero-day exploited to hack nearly 1,000 network switches](https://www.bleepingcomputer.com/news/security/zyxel-fixes-zero-day-exploited-to-hack-nearly-1-000-network-switches/)
- [The Hacker News：Zyxel GS1900 Patch Fails to Block Zero-Day Exploit…](https://thehackernews.com/2026/11/zyxel-gs1900-patch-fails-to-block-zero.html)（本文は未確認）

---

## 2. DigiCert：アーカイブされた顧客情報・身分証類が閲覧された

**何が起きたか**
認証局の DigiCert が、2025年2月のサーバー移行ミスで社内の業務システムがインターネットに公開状態となり、外部が作成したアカウントから過去の顧客データが読み取られたと説明しています。2026年6月27日〜7月2日にアクセスがあり、10月19日の追加調査で確認されました。

**影響範囲**
- 「ごく一部」の顧客の氏名、業務用メール、電話番号、住所。一部は運転免許証・パスポート・公共料金明細などの身分証類を含みます。
- 影響人数は未公表です。
- DigiCert は、認証局サービス、CertCentral、DigiCert ONE は侵害されておらず、証明書の発行や変更はできなかったと説明しています。

**現状と対応**
アクセス制限、自己登録機能の無効化、権限管理の追加を実施し、通知を開始したとされます。

**やさしい解説**
倉庫の引っ越しの際に、本来は社員しか入れない書庫の入口が一時的に表通りに面してしまい、古い書類が見られたイメージです。DigiCert の利用者は、同社からの通知を待ち、身分証類が含まれていた場合は、なりすまし申込みなどに注意してください。通知を装った偽メールにも注意が必要です。

**ソース**
- [DigiCert のインシデント報告（Mozilla Bugzilla）](https://bugzilla.mozilla.org/show_bug.cgi?id=2084460#c2)
- [BleepingComputer：DigiCert data breach exposes customer information, identity documents](https://www.bleepingcomputer.com/news/security/digicert-data-breach-exposes-customer-information-identity-documents/)

---

## 3. DreamHost：ファイルマネージャ経由でFTP認証情報等が漏えい

**何が起きたか**
レンタルサーバー事業者 DreamHost の Web ファイルマネージャ（files.dreamhost.com）が、ソフトウェアの脆弱性を突かれて侵害されました。2026年8月ごろから10月23日の発覚まで続いたとされます。

**影響範囲**
- ファイルマネージャにログインした利用者の FTP/SFTP のユーザー名・パスワード。一部の利用者についてはウェブメールのセッション情報も含まれる可能性。
- 管理パネルのログイン情報と決済情報は対象外と説明。影響件数は未公表です。

**現状と対応**
攻撃者のアクセス遮断、脆弱性の修正、セッション終了とパスワード無効化を実施。Equifax 経由で1年間のクレジット監視を提供するとしています。

**やさしい解説**
ホームページ用の「倉庫の鍵」が盗まれた可能性があります。利用者は、サイト内のファイルに身に覚えのない変更がないか、ウェブメールの転送設定や振り分けルールに不審なものがないか確認し、同じパスワードを他で使い回していれば変更してください。

**ソース**
- [DreamHost の通知書面（カリフォルニア州司法長官サイト掲載）](https://oag.ca.gov/system/files/DreamHost%20-%20Data%20Security%20Breach%20Notice%20Letter%20%28USA%20other%20than%20MA%29%20261102.1.pdf)
- [BleepingComputer：DreamHost confirms data breach exposed FTP logins and webmail sessions](https://www.bleepingcomputer.com/news/security/dreamhost-confirms-data-breach-exposed-ftp-logins-and-webmail-sessions/)

---

## 4. Debian/Ubuntu の APT に脆弱性（CVE-2026-109518）

**何が起きたか**
パッケージ管理ツール APT に、通信経路を改ざんできる攻撃者が、検証済みパッケージを別のものにすり替え、root 権限でコードを実行させられる脆弱性が見つかりました。APT 開発者は「クリティカル」、Ubuntu は CVSS 4.0 で7.7（High）と評価しています。

**影響範囲**
- 条件：攻撃者が APT とパッケージサーバー間の通信を操作できること（悪意あるミラーやプロキシ等）、かつダウンロード再試行が有効なこと。再試行は Debian 12 / Ubuntu 22.04 以降で既定有効です。Debian 11 / Ubuntu 20.04 は既定では対象外ですが、設定次第で影響します。
- 悪用の報告は、参照した情報の範囲では確認できていません。

**現状と対応**
Debian と Ubuntu が修正版を公開中です（Ubuntu 24.04 LTS は 2.8.4ubuntu0.1、22.04 LTS は 2.4.15ubuntu0.1 など）。回避策は示されていません。

**やさしい解説**
宅配便の中身を、配達の途中で別物にすり替えられるような問題です。ただし、荷物の経路に割り込める必要があるため、信頼できるミラーを使い、アップデートを早めに適用すれば大きく下げられます。サーバー管理者は `apt update && apt upgrade` で APT 自体を更新してください。

**ソース**
- [Debian セキュリティ告知](https://lists.debian.org/debian-security-announce/2026/msg00526.html)
- [Ubuntu CVE-2026-109518](https://ubuntu.com/security/CVE-2026-109518)
- [APT 開発者のアドバイザリ](https://lists.debian.org/deity/2026/11/msg00005.html)
- [The Hacker News：Debian and Ubuntu APT Flaw Lets MitM Attackers…](https://thehackernews.com/2026/11/debian-and-ubuntu-apt-flaw-lets-mitm.html)

---

## 5. Ruby on Rails Active Storage の重大な脆弱性（GHSA-f3w6-w445-fwh9、CVSS 9.8）

**何が起きたか**
Rails の Active Storage で、ImageMagick を使った画像処理を行うアプリに対し、細工したアップロードにより認証なしでサーバー上にファイルを書き込める脆弱性が公表されました。CVE は未付与と報じられています。

**影響範囲**
- 8.0.5.2 未満の Active Storage、および 8.1.4.1 未満の 8.1 系。
- 次の3条件がすべて当てはまる場合：画像処理に ImageMagick（mini_magick）を使う／ImageMagick のセキュリティポリシーが関連コーダーを制限していない（Debian/Ubuntu の既定は制限しないと説明）／信頼できない利用者のアップロードを受け付ける。
- 同じリリースで、別の脆弱性 GHSA-v924-7rp8-4mxh（CVSS 8.8）も修正。

**現状と対応**
8.1.4.1 と 8.0.5.2 で修正済み。8.0 系の修正提供は11月7日までとされ、それ以前の系統は修正されません。

**やさしい解説**
「写真を受け取って自動で加工する窓口」に、悪意あるファイルが紛れ込むと、加工機が意図しない動きをする問題です。会員がプロフィール画像などをアップロードできる Rails サービスを運営している担当者は、バージョンの確認と更新を優先してください。

**ソース**
- [Rails セキュリティアドバイザリ GHSA-f3w6-w445-fwh9](https://github.com/rails/rails/security/advisories/GHSA-f3w6-w445-fwh9)
- [GHSA-v924-7rp8-4mxh](https://github.com/rails/rails/security/advisories/GHSA-v924-7rp8-4mxh)
- [The Hacker News：Critical Rails Flaw Lets Attackers Write Server Files…](https://thehackernews.com/2026/11/critical-rails-flaw-lets-attackers.html)

---

## 6. OpenSSH（musl 系 Linux）：パスワード無効化アカウントにログインされる問題

**何が起きたか**
研究者が「*sshole」と名付けた問題で、musl libc を使う Linux（Alpine、OpenWrt、Buildroot、Yocto）上の OpenSSH で、極端に長いパスワードにより、パスワード無効化済み（ハッシュが `*`）のアカウントにログインできる場合があるとされます。CVE 番号は報道では示されていません。

**影響範囲**
- 条件：musl 系 OS、PAM 認証が無効（Alpine の既定）、SSH のパスワード認証が有効、`*` のアカウントと有効なハッシュのアカウントが両方ある。
- Alpine の公式 AWS/Azure イメージの既定アカウント「alpine」が該当し得ると報じられています。glibc 系（Debian、Ubuntu、Fedora）は対象外とされます。

**現状と対応**
OpenSSH 10.6p2 に更新（Alpine は `apk upgrade openssh`）。当面の緩和策は `PasswordAuthentication no` です。

**やさしい解説**
「この扉は使用禁止」の札が付いた扉が、特殊な方法で開いてしまう問題です。鍵（公開鍵）認証だけを使い、パスワードでのログインを切っておけば防げます。

**ソース**
- [研究者の公開ページ sshhole.com](https://sshhole.com/)
- [BleepingComputer：OpenSSH flaw lets attackers log into password-disabled Linux accounts](https://www.bleepingcomputer.com/news/security/openssh-flaw-lets-attackers-log-into-password-disabled-linux-accounts/)
- [The Hacker News：OpenSSH Issues Emergency Fix…](https://thehackernews.com/2026/11/openssh-issues-emergency-fix-for-flaw.html)（本文は未確認）

---

## 7. デニーズ：アプリ移行処理の不備で、一部顧客の情報が流出した可能性

**何が起きたか**
デニーズジャパンが、旧アプリから新アプリへの移行処理の不備により、第三者が認証情報を不正に作成し、一部顧客のアカウントにアクセスできる状態だったと公表したと報じられています（10月30日判明）。

**影響範囲**
旧アプリ利用者の一部について、メールアドレス、生年月日、性別、居住都道府県、アプリ会員コード等。件数は報道に記載がありません。情報取得の処理履歴はあるものの、本人の操作か第三者かは区別できないとされます。

**現状と対応**
報道には具体的な再発防止策や通知方法の記載がありません。

**やさしい解説**
アプリの引っ越しの手続きに穴があり、他人が「なりすまし」で会員情報を見られた可能性がある、という話です。カード番号などは挙がっていませんが、メールアドレスと生年月日が知られると、偽メールで信用させる詐欺に使われやすくなります。デニーズを名乗るメールのリンクは開かず、公式アプリから確認してください。

**ソース**
- [Security NEXT：デニーズ、アプリ移行処理の不備で認証情報を不正作成された可能性](https://www.security-next.com/192388)（一次ソースは直接確認できていません）

---

## 8. 資さんうどん：委託先サーバー設定不備で従業員情報が閲覧可能だった可能性

**何が起きたか**
資さんうどんの運営会社が、サーバー運用の委託先カホエンタープライズの設定不備により、従業員・退職者の個人情報が外部から閲覧できた可能性があると公表したと報じられています。

**影響範囲**
2021年10月〜2026年10月に在籍した従業員・退職者の、氏名、電話番号、生年月日、性別、賃金履歴、勤怠記録等。一部は退職理由や社会保険加入履歴を含みます。件数は報道に記載がありません。顧客情報には触れられていません。

**現状と対応**
設定を修正し、個人情報保護委員会へ報告済み。対象者へ順次連絡予定とされます。

**やさしい解説**
社員名簿をしまった棚のドアが、委託先の施錠ミスで開いていた可能性があるという話です。対象の方は、会社を名乗る不審な電話・メッセージに注意してください。IT担当者は、委託先のクラウド設定の公開範囲を定期的に点検しましょう。

**ソース**
- [Security NEXT：資さんうどん、サーバ設定の不備により従業員情報が流出した可能性](https://www.security-next.com/192260)（一次ソースは直接確認できていません）

---

## 今日やること

**一般利用者向け**
- 利用中のサービスから「情報流出」の連絡が来ても、メール内リンクは開かず、公式アプリ・ブックマークから確認する。
- 同じパスワードを複数サービスで使い回していないか見直す（特にホスティング、アプリ会員）。
- デニーズ・DigiCert などの通知を装った偽メール・偽電話に注意する。

**IT担当者向け**
- Zyxel GS1900 を使っている場合は、ファームウェアを更新し、管理画面の公開有無を確認する。
- Debian/Ubuntu のサーバーで APT を更新する。信頼できるミラー以外を使っていないか確認する。
- Rails の Active Storage で ImageMagick を使っている場合は 8.1.4.1 / 8.0.5.2 以上に更新する。8.0 系は11月7日で修正提供が終わる。
- Alpine 等の musl 系 Linux で SSH のパスワード認証が有効なら、OpenSSH 10.6p2 に更新するか無効化する。
- DreamHost 利用者は FTP/SFTP パスワードの変更と、サイト内ファイル・メール転送設定の確認を行う。

---

## 留意点

- デニーズ・資さんうどんは、Security NEXT の記事で確認したもので、各社の公式発表は直接確認できていません。件数も未公表です。
- Zyxel の機種名・対象ファームウェアのバージョンは、公式アドバイザリで確認してください。「別の欠陥を突いた」という点は Binarly の分析に基づく報道であり、攻撃者の意図は不明です。
- *sshole は CVE が確認できていません。DigiCert・DreamHost は影響人数が未公表です。
- 期間内の他の案件（Linux カーネルの IPv4 TCP 脆弱性、Xen の脆弱性、Apple 脆弱性悪用に関する CISA の注意喚起、Apache OFBiz のRCE、HPE ネットワーク管理製品、SolarWinds Dameware、Ruby on Rails 本体更新の21件、各種自治体の紛失事案など）は、本稿では詳細を確認できておらず見送りました。
