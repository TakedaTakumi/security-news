---
layout: post
title: "今日のホットニュース（2026年11月2日）"
date: 2026-11-02 09:00:00 +0900
---

## 今日のポイント

- 【続報】Binance の約63億ドル流出について、FBI が北朝鮮系 TraderTraitor の犯行と断定し、関連アドレスの取引遮断を要請しました。
- Canonical の LXD / MicroCloud に CVSS 10.0 の認証回避の脆弱性が見つかりました。悪用は確認されていませんが、更新が必要です。
- 【続報】GitLab の重大脆弱性を狙った攻撃が Alpine Linux で発生。Android の通信を妨害する「SMS of Death」の検証コードも公開されました。

---

## 1. 【続報】Binance 大規模流出：FBI が北朝鮮系 TraderTraitor の犯行と断定

**何が起きたか（新しい事実）**
FBI は2026年10月31日（土）付の注意喚起で、Binance からの60億ドル超の暗号資産窃取は北朝鮮の犯行（TraderTraitor／Lazarus 等として知られるグループ）だと発表しました。窃取は10月29日ごろに発生し、大半が約20分で移動したと報じられています。Binance は、侵害された DevOps 担当者の PC を起点に不正な出金が行われたと説明しています（報道による）。

**影響範囲**
報道では約63億6千万ドル、10のブロックチェーンにまたがる規模です。FBI・シークレットサービス・IRS 犯罪捜査部は、取引所などに対し628件のアドレス（Ethereum 608、Bitcoin 19、Solana 1）に関する取引の遮断を要請しました。

**現状と対応**
資金は主に ETH へ換えられ、DeFi や即時スワップ経由で洗浄される見込みとされています。Binance は11月1日に出金を段階的に再開する予定で、損失の約95%を補填済み、残りも調達中、損失は利用者に転嫁しないと表明しています（Binance の発表を報じたもので、当方では未確認）。

**やさしい解説**
銀行の金庫そのものが破られたというより、「金庫番の社員の鍵（業務用PC）」を奪われて正規の手順で引き出された、というイメージです。利用者として今すぐ必要な操作は特にありませんが、取引所からの公式案内以外のメールやリンクは「補償」などを装った詐欺に注意してください。

**ソース**
- [FBI 注意喚起（一次）](http://www.fbi.gov/investigate/cyber/alerts/2026/north-korea-responsible-for-6-billion-binance-attack)
- [BleepingComputer](https://www.bleepingcomputer.com/news/security/fbi-links-63-billion-binance-crypto-heist-to-north-korean-hackers/)
- [The Hacker News](https://thehackernews.com/2026/11/fbi-links-north-koreas-tradertraitor-to.html)

## 2. Canonical LXD / MicroCloud に CVSS 10.0 の認証回避（CVE-2026-112816）

**何が起きたか**
コンテナ／仮想マシン管理基盤 LXD と MicroCloud に、秘密鍵なしで「信頼済みクライアント」になりすませる脆弱性が見つかりました。サーバーが証明書チェーン内の証明書を信頼リストと照合する一方、実際に鍵を持っているかの確認が葉証明書に限られていたことが原因と報じられています。コミュニティ派生の Incus が報告しました。

**影響範囲**
- 対象：LXD 4.0 / 5.0 / 5.21 / 6.x 系の修正前版、および MicroCloud。HTTPS API にネットワークから到達できる環境が対象です（標準では API はローカルソケットのみで、`core.https_address` を設定した場合に露出）。
- 権限の高いクライアントになりすませるとホストの root 相当の操作につながる可能性があります。

**現状と対応**
- 修正版：LXD 6.10.1 / 5.21.9 / 5.0.11 / 4.0.15、MicroCloud 3.4.1 / 2.1.5、Incus 7.6.0。
- 一時的な回避策はなく、更新までは API への接続元を制限します。Canonical は修正版が候補チャンネルから安定版へ移行中だったと説明しており、更新後にバージョン確認が必要です。
- 悪用の報告はなく、CISA の評価（10月30日付）でも悪用は確認されていないとされています（報道による）。

**やさしい解説**
合鍵の「コピー（公開情報）」だけで入口を通してしまうような欠陥です。LXD を管理画面（API）経由でネットワークに公開している IT 担当者は、まず公開範囲を絞り、`snap refresh` で更新してバージョンを確認してください。公開していない一般の利用者への影響は小さいと考えられます。

**ソース**
- [Canonical 公式アドバイザリ（一次）](https://discourse.ubuntu.com/t/security-advisory-critical-vulnerability-found-in-canonical-lxd-and-microcloud/90557)
- [Ubuntu CVE ページ](https://ubuntu.com/security/CVE-2026-112816)
- [Incus アドバイザリ（GHSA-xg75-xf37-cph9）](https://github.com/lxc/incus/security/advisories/GHSA-xg75-xf37-cph9)
- [The Hacker News](https://thehackernews.com/2026/11/critical-lxd-and-microcloud-flaw-cvss.html)

## 3. 【続報】GitLab の重大脆弱性：Alpine Linux が攻撃を受けサーバーを再構築

**何が起きたか（新しい事実）**
Alpine Linux は、CVE-2026-97229（GitLab が内部で使う Ruby の正規表現エンジン Onigmo の整数オーバーフロー）を狙った攻撃が10月20〜21日に自社の GitLab に対して行われたと公表しました。攻撃は GitLab のプロセスを繰り返し異常終了させ、攻撃者は GitLab のコンテナイメージも取得していたとのことです。

**影響範囲・現状**
10月27日までの調査では、コード実行やパッケージ改ざんの証拠は見つかっていません。ただし、ログや外部通信記録が不足し侵害を完全には否定できないため、同社はサーバーを一から再構築し、全パスワードをリセットしました。署名鍵は当該サーバーに置かれておらず影響しないとしています。GitLab 19.3.5 が必要なところ 19.3.4 を導入し、その後 19.3.6 へ上げても、同社独自イメージに Ruby 側の修正が入っておらず穴が塞がらなかった点が教訓です。

**対応**
Alpine の GitLab 利用者はパスワードを変更してください。自前で GitLab を運用する場合は、GitLab 本体の更新だけでなく Ruby 側の修正が含まれているかを確認してください（独自イメージの場合は特に）。

**やさしい解説**
「家の鍵（本体）を新しくしたのに、ドア枠（部品）が古いままで開いてしまった」ような事故です。更新の「完了」は、バージョン番号だけでなく、実際に脆弱性が塞がっているかまで確かめて初めて言えます。

**ソース**
- [Alpine Linux インシデント報告（一次）](https://alpinelinux.org/posts/GitLab-security-incident-CVE-2026-97229.html)
- [NVD: CVE-2026-97229](https://nvd.nist.gov/vuln/detail/cve-2026-97229)
- [BleepingComputer](https://www.bleepingcomputer.com/news/security/alpine-linux-rebuilds-gitlab-after-attempted-rce-attack/)

## 4. Android「SMS of Death」（CVE-2026-58882）：細工した SMS で端末の通信が停止

**何が起きたか**
研究者が、細工した SMS だけで Android の電話機能プロセスを異常終了させられる脆弱性（CVE-2026-58882）の検証コードを公開しました。受信者の操作は不要で、通信が切れ、通話（緊急通話を含む）が中断され得ます。報道では、Android 12 の端末で連続受信により再起動の繰り返しが起き、初期化が必要になった例が示されています。なお、攻撃に使うデータの詳細は本記事では扱いません。

**影響範囲・現状**
Android 12 / 13 は修正が提供されず脆弱なままとされ、Android 14〜17 向けには2026年10月の更新で修正が入ったと報じられています。ただし Google の10月分セキュリティ情報には掲載がないとの指摘もあり、この点は未確認です。

**対応**
最新のセキュリティ更新を適用し、必要なら再起動してください。更新が提供されない古い端末は、買い替えの検討や、キャリア・メーカーの案内の確認が現実的です。

**やさしい解説**
知らない人から届いた1通のメッセージで、スマホの「電話の部分」が止まってしまう問題です。開く・返信するといった操作に関係なく起きる点が厄介です。端末のOS更新を済ませ、サポートが終わった古いAndroidを使い続けないことが対策になります。

**ソース**
- [BleepingComputer](https://www.bleepingcomputer.com/news/security/new-android-sms-of-death-exploit-can-remotely-crash-unpatched-phones/)（同記事が引用する研究者の解説、Google の修正コミット、Android セキュリティ情報も参照）

## 5. 【続報】Polymarket：DebugBear 経由のスクリプト改ざん、原因と返金状況

**新しい事実**
- 10月29日（UTC）、Polymarket のサイトが読み込んでいた外部の性能監視スクリプト（DebugBear）が悪意あるコードに差し替えられ、ログイン中の利用者の権限を悪用して資産が移されました。
- DebugBear は、レジストラ経由で DNS 設定が乗っ取られたと説明し、狙われたのは1顧客のサイトとみられ、自社システムへの侵入の兆候は見つかっていないが調査中としています。同社は利用者に埋め込みコードの削除を案内しています。
- Polymarket は約270万ドルを726ウォレットへ返金（10月30日時点で689件完了と報道）し、取引停止中の損失などで約5,500ウォレットに119万ドルも支払うとしています。

**対応**
サイト運営者は、決済・署名を伴う画面で外部スクリプトを読み込まない、可能ならバージョン固定と SRI（改ざん検知）・CSP を使う、といった対策が有効です。DebugBear の利用者は同社の案内に従ってください。

**やさしい解説**
お店が「外部業者の看板（スクリプト）」を店内に掲げていたところ、業者の住所録が書き換えられて偽の看板が掲げられた、という構図です。利用者は、想定外の署名・承認要求は拒否するのが基本です。

**ソース**
- [Polymarket ステータス履歴（一次）](https://status.polymarket.com/history)
- [The Hacker News](https://thehackernews.com/2026/11/hackers-steal-about-27-million-from.html)

---

## 今日やること

**一般利用者向け**
- スマホ（特に Android）のセキュリティ更新を確認する。
- 取引所・暗号資産サービスを名乗る「補償」「再開」の連絡は、公式アプリ・公式サイト経由で確認する。想定外の署名要求は承認しない。

**IT担当者向け**
- LXD / MicroCloud を `snap refresh` で修正版へ更新し、API の公開範囲を絞る。
- 自前の GitLab は、本体と Ruby 側の修正の双方が適用済みか確認する（CVE-2026-97229）。
- 決済や署名を伴うページで読み込む外部スクリプトを棚卸しし、SRI・CSP・バージョン固定を検討する。

## 留意点

- Binance の補填割合・出金再開は Binance 側の発表を報道経由で確認したもので、独自には検証していません。
- Android の CVE-2026-58882 は、修正の提供範囲が Google の10月分情報に掲載されていないとの指摘があり、未確認です。
- Alpine の件は侵害の確証はなく、「否定できないための再構築」である点に留意してください。
- 期間外または既出で見送った案件：Ivanti Connect Secure の悪用注意喚起（米当局、11/2 Security NEXT 報道。11/1 掲載分から新しい事実を確認できず）、Chainalysis・Northflank（既出）、ChatGPT 共有リンクの問題（修正済みで影響限定的のため見送り）。
- 検索エンジンでは11月の日本国内の漏えい公表を確認できませんでした。
