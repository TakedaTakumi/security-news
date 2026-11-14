---
layout: post
title: "今日のホットニュース（2026年11月14日）"
date: 2026-11-14 09:00:00 +0900
---

- 続報として、PHP2Shell が Check Point のゲートウェイへの攻撃に使われ、一部の組織では VMware ESXi のデータを消去する破壊活動にまで至ったと報じられました。Trezor は、不正な部品入りのウォレット3台を正式に確認しました。
- 通信事業者の設備を乗っ取って通話や SMS を傍受する SilentAir の報告と、PostgreSQL の52件の脆弱性修正がありました。
- 国内では、ノジマオンライン（約700万件）、ネットマイル（最大約549万人）、ブックオフ（約638万人）など、大規模な会員情報の流出が相次いで報じられています。

---

## 1. 【続報】PHP2Shell が Check Point ゲートウェイ攻撃に悪用、ESXi を破壊する攻撃も

**何が起きたか**
Check Point は、11月13日までに、同社のゲートウェイを狙った攻撃の分析を公表しました。入口には PHP2Shell（過去に掲載済みの PHP の脆弱性群、CVE-2026-109618・CVE-2026-109619）が使われたと報じられています。その後、新たに判明した権限昇格の欠陥 CVE-2026-123039（CVSS 7.8、root 権限の取得）で機器を掌握しました。同社は、この欠陥が悪用されていると述べています。

**影響範囲**
対象は、R81 から R82.20 までの各版の Check Point 製品です（ファイアウォール、管理・ログサーバー、Multi-Domain、Maestro Orchestrator）。悪用は「数十社の顧客」で確認されたとされます。10月30日にイスラエルの組織を狙う第1波、11月2日に複数国・複数業種への第2波が起きました。第1波の一部の組織では、ESXi 上のファイルを消すワイパー（破壊型マルウェア）も使われたと報じられています。

**現状と対応**
Check Point はアドバイザリ SK1000362 で修正を案内しています（修正の詳細は未確認）。攻撃者の特定は確定していません。Check Point は、過去に報じられたツール群との類似を認めつつ、偽装の可能性も含めて断定を避けています。IT 担当者は、アドバイザリの確認、該当版への修正適用、管理画面や SSH の接続元の制限、ESXi への不審なログインの調査を進めてください。

**やさしい解説**
建物の入口を守る警備機器そのものが破られ、そこから社内の別の部屋の金庫（仮想マシン）まで荒らされた、という話です。一般の方が取る操作はありません。Check Point 製品を使う組織の担当者は、至急、修正の適用状況を確認してください。

**ソース**
- [The Hacker News: Hackers Exploit PHP2Shell Flaws in Check Point Gateways to Deploy TSGA Backdoor and Wipe ESXi Files](https://thehackernews.com/2026/11/hackers-exploit-php2shell-flaws-in.html)
- [SecurityWeek: PHP2Shell Exploited in Destructive Check Point Gateway Attacks](https://www.securityweek.com/php2shell-exploited-in-destructive-check-point-gateway-attacks/)（見出しのみ確認）
- [BleepingComputer: Check Point warns of zero-day flaw exploited for root access](https://www.bleepingcomputer.com/news/security/check-point-patches-zero-day-that-lets-hackers-get-root-access/)（アクセス不可、見出しのみ確認）
- Check Point の一次アドバイザリ（SK1000362）は未確認

## 2. 【続報】Trezor が不正な部品入りウォレット3台を確認

**何が起きたか**
10月30日に疑いとして掲載した件で、Trezor が11月13日に確認を公表しました。販売店 CryptoBilis 経由で買われた Trezor Safe 5 の3台に、リカバリーフレーズ（資産を復元する合言葉）を盗んで携帯回線で送る追加基板が入っていたとされます。1台は同社の研究所で調べ、残る2台は持ち主が撮った写真から判断したとのことです。

**影響範囲**
確認されたのは3台で、購入時期は8月20日〜9月23日です。同社への問い合わせは48件で、確認作業は続いています。資金の被害報告は受けていないとされます。今のところ、他の販売店や他の機種では見つかっていません。誰が、供給網のどこで仕込んだかは不明です。

**現状と対応**
ファームウェア 2.13.1 で、既知の部品による情報の取得を止められるとされます。ただし、すでに盗まれた情報は守れません。Trezor は、CryptoBilis で買った人に、新しいウォレットと新しいリカバリーフレーズで資金を移すよう案内しています。

**やさしい解説**
金庫の中に、暗証番号をこっそり撮影するカメラが仕込まれていたようなものです。後から鍵を替えても、すでに撮られた番号は役に立ちません。CryptoBilis など正規でない販売店で買った方は、新しいウォレットを作り直して資金を移してください。

**ソース**
- [The Hacker News: Trezor Confirms Hidden Implants in CryptoBilis-Sold Wallets That Can Steal Recovery Phrases](https://thehackernews.com/2026/11/trezor-confirms-hidden-hardware.html)
- [BleepingComputer: Trezor confirms crypto-stealing implants in three wallets, releases fix](https://www.bleepingcomputer.com/news/cryptocurrency/trezor-confirms-crypto-stealing-implants-in-three-wallets-releases-fix/)（アクセス不可、見出しのみ確認）
- Trezor の公式発表は未確認

## 3. 国内で大規模な会員情報の流出が相次いで報じられる

ScanNetSecurity が11月12〜13日に報じた案件です。各社の発表はそれより前で、日付を併記します。原因の詳細は多くが公表されていません。

**何が起きたか・影響範囲**
- **ノジマオンライン**：11月1日に検知し、2日に発表。会員情報約700万件（退会者を除く）。氏名、生年月日、住所、電話番号、メールアドレス、ログイン ID と暗号化されたパスワードなど。クレジットカード情報は挙がっていません。
- **ネットマイル（ウィルズ）**：11月2日に発表。退会者を含む最大約549万人分の会員情報が漏れた可能性。氏名やメールアドレスなどが含まれ得ます。
- **ブックオフ（子会社の会員管理システム）**：10月9日に初報、11月6日に第3報。約638万人分で、氏名、生年月日、住所、メールアドレス、パスワードのハッシュ値などが含まれます。アクセス制御の欠陥を突かれたとされます。
- **NTTデータ（住友生命 Vitality 関連）**：11月9日に発表。約8万人分で、氏名、住所、電話番号、生年月日、メールアドレス、一部を伏せたクレジットカード番号が含まれます。
- そのほか、ヤクルト本社の公式サイト（約4万件、10月30日発表）、丸井グループの委託先 Securitize Japan（最大9,086人、11月2日発表）の件も報じられています。

**現状と対応**
ノジマオンラインとネットマイルは、サイトを一時停止しています。ブックオフは、対象者へ個別に通知済みです。他の案件も、各社が対象者への通知や調査を進めているとされます。

**やさしい解説**
会員名簿が丸ごと持ち出された状態です。名簿の情報を使った「なりすましメール」や、同じパスワードを使い回しているサービスへの不正ログインが心配です。該当するサービスの会員だった方は、次の対応をしてください。
- 同じパスワードを使っている他のサービスを、すべて変更する。
- 各社の名をかたるメールや SMS のリンクを開かない。
- クレジットカード番号が含まれた案件の対象者は、明細を確認する。

**ソース**
- [ScanNetSecurity: 「ノジマオンライン」に不正アクセス、約700万件の会員情報が漏えい](https://scan.netsecurity.ne.jp/article/2026/11/13/56774.html)
- [ScanNetSecurity: 「ネットマイル」に不正アクセス、最大約549万人の会員情報等が漏えいした可能性](https://scan.netsecurity.ne.jp/article/2026/11/13/56773.html)
- [ScanNetSecurity: ブックオフグループホールディングス子会社の会員管理システムに不正アクセス、638万3,279人の会員情報が漏えい](https://scan.netsecurity.ne.jp/article/2026/11/13/56778.html)
- [ScanNetSecurity: NTTデータが住友生命から受託した「住友生命Vitality体験版・企業型」等に不正アクセス](https://scan.netsecurity.ne.jp/article/2026/11/12/56761.html)
- [ScanNetSecurity: ヤクルト本社ホームページに不正アクセス、約4万件の個人情報が漏えい](https://scan.netsecurity.ne.jp/article/2026/11/12/56756.html)
- [ScanNetSecurity: 丸井グループの業務委託先 Securitize Japan に不正アクセス](https://scan.netsecurity.ne.jp/article/2026/11/13/56775.html)
- 各社の一次発表は未確認

## 4. PostgreSQL が52件の脆弱性を修正、古い拡張機能の再ビルドも必要

**何が起きたか**
PostgreSQL プロジェクトが、11月の定期更新で52件の脆弱性を修正しました。注目は CVE-2026-6460（CVSS 8.8）で、オブジェクトを作れるデータベース利用者が、サーバーの OS 権限でコードを実行できる可能性があります。報道では、攻撃の報告はないとされます。

**影響範囲**
修正版は 18.7、17.12、16.16、15.20、14.25 です。PostgreSQL 14 は今回で保守が終了しました。古い主要版も影響を受けますが、更新は出ていません。C 言語で作られた拡張機能は、再ビルドしないと守られない場合があります。pg_restore や psql などのクライアントにも修正があります。

**現状と対応**
CVE-2026-116322 は、ログインなしでの PostgreSQL 18 の再起動につながる欠陥とされます。回避策はないため、更新が必要です。更新後は、拡張機能の再ビルドと、リリース告知にある再インデックス手順の確認も必要です。AWS、Azure、Google などのマネージドサービスは事前に通知を受けていますが、各社の適用状況は未確認です。

**やさしい解説**
建物の鍵（データベース）の仕様に不具合が見つかり、合鍵の作り方（拡張機能）まで直す必要がある、という話です。一般の方の操作はありません。PostgreSQL を使う担当者は、バージョンを確認し、更新と拡張機能の再ビルドを計画してください。

**ソース**
- [The Hacker News: PostgreSQL Patches 52 Flaws, Including 22-Year-Old Bug Enabling Authenticated RCE](https://thehackernews.com/2026/11/postgresql-patches-52-flaws-including.html)
- PostgreSQL プロジェクトの一次発表は未確認

## 5. SilentAir：通信事業者の設備から通話・SMS を傍受

**何が起きたか**
セキュリティ企業 Enea が、国家規模の新しい攻撃グループ「SilentAir」を報告しました。侵害した通信事業者の設備を使い、狙った相手の通話や SMS を経由させて盗み見るとされます。主な標的は台湾で、政治家や政府関係者も含まれていました。

**影響範囲**
少なくとも6か国のアジアの事業者の設備が使われたとされます。ほかにも十数の国・地域が狙われました。中国に関係する活動との一致が指摘されていますが、確度は低いと説明されています。

**現状と対応**
Enea は2025年初めから追跡しており、2026年第1四半期からは、関連するバックドアを顧客の事業者で複数回ブロックしたとしています。報道に、利用者向けの対策は書かれていません。

**やさしい解説**
手紙の仕分け所が乗っ取られ、特定の人宛ての手紙だけが一度寄り道させられるようなものです。SMS で届く認証コードが盗み見られる恐れがあります。重要なサービスでは、SMS 以外の認証（アプリや認証キー）への切り替えを検討してください。

**ソース**
- [SecurityWeek: SilentAir Hackers Intercept Calls, SMS From Inside Mobile Networks](https://www.securityweek.com/silentair-hackers-intercept-calls-sms-from-inside-mobile-networks/)
- [The Hacker News: SilentAir Hijacks Asian Telecom Networks to Intercept SMS 2FA Codes and Spy on Taiwanese Users](https://thehackernews.com/2026/11/silentair-hijacks-asian-telecom.html)（見出しのみ確認）
- Enea の一次レポートは未確認

## 今日やること

**一般利用者向け**
- ノジマ、ネットマイル、ブックオフなどの会員だった方は、同じパスワードを使う他のサービスも変更する。
- 各社を装うメールや SMS のリンクは開かない。
- 暗号資産ウォレットを正規でない販売店で買った方は、新しいウォレットに資金を移す。
- 重要なサービスの2要素認証は、SMS 以外の方式に切り替える。

**IT 担当者向け**
- Check Point 製品の修正適用状況を確認し、ESXi への不審なログインを調べる。
- PostgreSQL を更新し、C 言語の拡張機能を再ビルドする。PostgreSQL 14 は保守終了の扱いを確認する。
- 前日までに掲載した N-central の Legacy API の無効化確認、GitHub のシークレット更新も、引き続き確認する。

## 留意点

- BleepingComputer の記事ページは、本日の取得で 403 となり、本文を確認できませんでした。見出しと一覧の要約のみで判断しています。
- 国内の流出案件は、各社の一次発表を確認できていません。ScanNetSecurity の記事の範囲です。発表日が48時間より前のものは、報道が11月12〜13日だったため掲載しました。
- 期間外または確認不足で見送った案件：ドイツの Quantum Systems のサイバー攻撃（軍用ドローン運用への影響、詳細未確認）、AMD SEV-SNP への実験室での攻撃（Mior・Skyfall、ホスト制御が前提）、Microsoft 365 の障害（攻撃の証拠なしと報じられています）、FAA の運航停止（原因は未公表）、Chrome・Firefox の更新。
