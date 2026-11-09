---
layout: post
title: "今日のホットニュース（2026年11月9日）"
date: 2026-11-09 09:00:00 +0900
---

## 今日のポイント

- アイリスオーヤマの通販サイト「アイリスプラザ」で、外部クラウドサービスの不正アクセスにより、最大約770万人分の個人情報が漏えいした可能性があると発表されました。
- 【続報】OpenSSH の認証回避「SSHole」（CVE-2026-123158）が、公開から9時間未満で実際に試されていたと報告されました。Alpine Linux などは更新と侵害確認が必要です。
- Claude Desktop の「Dispatch」機能が、ブラウザ拡張機能から遠隔操作されうる問題が報告されました。報告者は、現時点でも悪用可能だと述べています。

---

## 1. アイリスオーヤマ：「アイリスプラザ」で最大約770万人分の個人情報が漏えいの可能性

**何が起きたか**
アイリスオーヤマは10月28日、外部クラウドサービス上で不審なファイルを見つけ、通販サイトと関連システムを停止しました。10月29日に警察と個人情報保護委員会へ報告し、11月5日に公表しています（報道ベース）。

**影響範囲**
- 最大約770万人分。内訳は会員約580万人、非会員約190万人と報じられています。
- 氏名・住所・電話番号・メールアドレスなど。会員データには暗号化されたパスワードや生年月日も含まれるとされます。
- クレジットカード情報は対象外とされています。
- 不正利用の報告は確認されていません。件数は「可能性のある」データ総数で、確定値ではありません。

**現状と対応**
調査は継続中です。利用者は、アイリスオーヤマを装うメール・SMS に注意し、同じパスワードを他サービスで使っていれば変更してください。

**やさしい解説**
お店そのものではなく、お店が顧客名簿を預けていた「外部の貸し倉庫」から名簿が持ち出された可能性がある、という話です。パスワードは暗号化されていますが、住所・電話番号・生年月日がそろうと、本物らしい詐欺連絡に使われやすくなります。身に覚えのない請求や「確認してください」というリンクは開かず、公式サイトから確認してください。

**ソース**
- [アイリスオーヤマ お知らせ（2026年11月5日）](https://www.irisohyama.co.jp/news/2026/?date=1105)
- [BleepingComputer：Iris Ohyama data cloud breach exposes info of 7.7 million customers](https://www.bleepingcomputer.com/news/security/iris-ohyama-data-cloud-breach-exposes-info-of-77-million-customers/)
- [innovaTopia：アイリスプラザ約770万人分に漏えいの可能性（解説）](https://innovatopia.jp/cyber-security/cyber-security-news/119744/)

---

## 2. 【続報】OpenSSH「SSHole」：公開から9時間未満で攻撃の試行

**新しい事実**
既報の OpenSSH の認証回避（CVE-2026-123158、CVSS 8.1）について、セキュリティ企業 Previdian が、CVE 公開から9時間未満で最初の攻撃試行を観測したと報告しました。Alpine Linux を動かすおとりサーバー（ハニーポット）では root 権限での侵入も確認されています。日本の IP アドレスと推定される1か所から8回の試行があり、`id`・`uname`・`hostname` など環境確認のコマンドが実行されたとのことです。
※記事の日付は11月6日で、直近48時間よりやや前ですが、既出案件の新事実として取り上げました。

**影響範囲（既報の再確認）**
musl C ライブラリ上で OpenSSH を使い、PAM を使わない Linux（Alpine Linux の標準設定を含む）。glibc 系ディストリビューション、Dropbear、PAM で認証する環境は対象外とされています。

**現状と対応**
OpenSSH 10.6p2 または各ディストリビューションの修正パッケージへ更新し、sshd を再起動します。Alpine は、本来パスワードでログインしないはずのアカウント（root・key-only ユーザーなど）について、ログの「Accepted password for」を確認するよう案内しています。侵害を否定できなければ、そのマシンは侵害されたものとして扱うよう勧めています。

**やさしい解説**
鍵のかかっていない扉に、長すぎる合言葉を言うと「開いた」と誤解して通してしまう欠陥です。修正の公開直後から試す人がいたため、「後で更新する」では間に合わない可能性があります。Alpine 系のサーバーを使っている方は、更新に加えて、不審なログインや新しいユーザー・鍵がないかも確認してください。

**ソース**
- [The Hacker News：Hackers Target OpenSSH SSHole Flaw Within Hours of Disclosure, Gain Root on Honeypot](https://thehackernews.com/2026/11/hackers-exploited-openssh-sshole-flaw.html)

---

## 3. Claude Desktop「Dispatch」：ブラウザ拡張機能から遠隔操作されうる問題

**何が起きたか**
Forever Security の研究者が、Claude Desktop の Dispatch（スマホから PC 上の Claude へ作業を送る機能）が、通常のログイン済み claude.ai セッションからの指示も受け付けると報告しました。claude.ai 上でスクリプトを実行できるブラウザ拡張機能があれば、利用者が入力したかのように Claude Desktop へ命令できます。検証では、Claude に npm パッケージを導入させ、電卓アプリを起動させたとのことです。

**影響範囲**
- Dispatch を有効にした Claude Desktop と、claude.ai にログインした環境。
- 実際の攻撃は報告されていません。
- Claude Code Remote Control や Cowork も同様の可能性があるとされますが、検証されていません。

**現状と対応**
報告は5月14日に Anthropic へ行われ、重複報告として閉じられました。Anthropic は10月に Dispatch を廃止予定と伝えたとされ、現在は新規利用者の受付を終了しています（報道ベース）。研究者は、問題は今も悪用可能だと述べています。Anthropic 側の公式見解は確認できていません。

**やさしい解説**
自宅の「スマホからの遠隔操作ボタン」が、同じ家の別の出入口（ブラウザの拡張機能）からも押せてしまう状態です。利用者は、①Dispatch が不要なら端末をまたぐ機能を切る、②入れているブラウザ拡張機能の権限を見直す、③AI エージェントが勝手にパッケージを入れていないか確認する、を実施してください。

**ソース**
- [The Hacker News：Malicious Browser Extensions Could Use Claude Dispatch to Run Code on Users' Computers](https://thehackernews.com/2026/11/malicious-browser-extensions-could-use.html)

---

## 今日やること

**一般利用者向け**
- アイリスプラザの会員は、アイリスオーヤマを装う連絡のリンクを開かず、パスワードの使い回しがあれば変更する。
- Claude Desktop の Dispatch を使っていない人は、端末をまたぐ機能を切り、不要なブラウザ拡張機能を削除する。

**IT 担当者向け**
- Alpine Linux など musl 系の SSH サーバーを OpenSSH 10.6p2 以降へ更新し、「Accepted password for」のログを確認する。
- SonicWall の SonicOS は、11月6日付の更新を適用する（SSL-VPN の SAML 認証回避は悪用の報告あり）。
- 外部クラウドサービスに顧客データを置く場合は、アクセスキーや権限、不審なファイルの有無を点検する。

## 留意点

- アイリスオーヤマの件は、同社の公式ページと BleepingComputer 本体が取得できず（403）、件数・経緯は検索結果の要約と二次報道に基づきます。原因・侵入経路は未確認です。
- Dispatch の件は研究者側の主張が中心で、Anthropic 側の見解は確認できていません。
- SonicWall は SecurityNEXT（11月9日付）で、同じアドバイザリで計7件の脆弱性が公表され、悪用報告を調査中とされています。既出の CVE-2026-19868 以外の詳細は確認できず、新規掲載は見送りました。
- OpenSSH の記事（11月6日付）と Dispatch の記事（同日付）は、直近48時間よりやや前ですが、新事実または台帳未掲載のため取り上げました。
- 見送った案件：OpenAI GPT-6 Cyber（脆弱性検出の話題で、特定の被害・脆弱性ではない）、偽のセキュリティツールを使う GitHub 攻撃（BleepingComputer が403で内容確認不可）、WorkOS（既出案件で新事実を確認できず）、ヤクルト・ノジマ・WatchGuard・Apache OFBiz（詳細確認が不十分）。
