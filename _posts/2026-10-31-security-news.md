---
layout: post
title: "今日のホットニュース（2026年10月31日）"
date: 2026-10-31 09:00:00 +0900
---

## 今日のポイント

- 【続報】Binance の暗号資産流出は約63億ドル規模と確認され、原因は DevOps エンジニアのノートPC侵害と説明されました（北朝鮮系グループの関与は分析会社の見立て）。
- GitLab（CVE-2026-97229）と Drupal Commerce Core（CVE-2026-118539）の最大級の脆弱性が、実際に悪用され始めています。更新が急務です。
- 開発者向けでは、Cursor のマーケットプレイスで Claude Code を装った悪意ある拡張機能が約11時間配布されました。

---

## 1. 【続報】Binance 暗号資産流出：約63億ドル、原因は DevOps 端末の侵害

**何が起きたか**
Binance は、2026年10月29日に調査を始めた大規模流出について、被害額が約63億ドルであること、DevOps エンジニアのノートPCが侵害され、そこから出金処理を行うサービスのコンテナに到達されたことを説明しました。単一の権限での単純な操作ではなく、より複雑な攻撃だったとしています（以上は BleepingComputer の報道による）。

**影響範囲**
- ブロックチェーン分析企業 TRM の分析では、10のチェーン上のウォレットから約63.6億ドル相当が動き、その大半は約20分間に集中。
- Tether や Circle などが約27億ドル相当を凍結済み。一方、攻撃者は凍結できない約24億ドル相当（ETH・BTC）を保有していると TRM は指摘。
- 被害額は報道により「63億」「63.6億」「64億」ドルと表記に揺れがあります。

**現状と対応**
Binance は入出金を一時停止し、影響を受けたアドレスの権限を取り消し、捜査当局などと追跡を進めています。損失は SAFUファンドと自社資金で補填し、利用者資金は安全だと表明。ウォレットの秘密鍵漏えいの証拠は見つかっていないとのことです。攻撃者は TRM が北朝鮮系の TraderTraitor（Lazarus）と分析し Chainalysis も同意していますが、Binance 自身は特定していません。

**やさしい解説**
金庫（ウォレット）そのものが破られたのではなく、金庫を開ける権限を持つ社員のパソコンが乗っ取られ、「正規の担当者のふり」をされた形です。どんなに堅い金庫でも、鍵を持つ人の端末が弱いと破られる、という教訓です。利用者として今すぐ必要な操作は公式には示されていませんが、Binance からの案内に注意し、「補償」をうたう偽メールやリンクには触れないようにしましょう。

**ソース**
- [Binance links $6.3 billion crypto theft to compromised DevOps laptop（BleepingComputer）](https://www.bleepingcomputer.com/news/security/binance-links-63-billion-crypto-theft-to-compromised-devops-laptop/)
- [Binance probes potential $5.8 billion crypto-theft hack（BleepingComputer、前報）](https://www.bleepingcomputer.com/news/security/binance-probes-potential-58-billion-crypto-theft-hack/)

---

## 2. GitLab に最大深刻度の脆弱性（CVE-2026-97229）：悪用確認、CISA が KEV に追加

**何が起きたか**
GitLab の CI/CD 設定で使われる正規表現処理の整数オーバーフローにより、細工された設定を使って認証なしで遠隔からコード実行される恐れがあります。CISA は2026年10月29日に実際の悪用を確認し、KEV に追加しました。

**影響範囲**
GitLab Community Edition / Enterprise Edition（セルフマネージド環境）。影響を受ける範囲の詳細は報道では明記されていません。Shadowserver は、インターネットに公開された GitLab CE を約2,800件確認しています。

**現状と対応**
修正版は 19.4.2 / 19.3.5 / 19.2.8。GitLab は管理者に直ちの適用を求め、セルフマネージド向けの検知ルールも公開しています。

**やさしい解説**
社内の「ソースコード置き場兼自動ビルド工場」に、外から入り込める裏口が見つかった状態です。しかも実際に侵入が始まっています。自社で GitLab を運用している場合は、更新を最優先にしてください。クラウド版（GitLab.com）を使うだけの利用者は、特別な操作は不要とみられます（※報道に明記はなく、公式アドバイザリで確認してください）。

**ソース**
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [CISA says max severity GitLab flaw now exploited in the wild（BleepingComputer）](https://www.bleepingcomputer.com/news/security/hackers-now-exploiting-max-severity-gitlab-flaw-in-attacks/)

---

## 3. Drupal Commerce Core に重大な脆弱性（CVE-2026-118539）：悪用確認

**何が起きたか**
Drupal の EC 向けモジュール Commerce Core で、認可チェックの欠落により、認証なしでアクセス制御を回避できる問題が見つかり、実際の攻撃で悪用されていると Drupal が公表しました。金銭的被害につながるおそれがあるとされています。

**影響範囲**
Commerce Core 0.0.0〜2.41、および 3.0.0〜3.3.13。42,000以上のサイトで利用されているとのことです。

**現状と対応**
3.x 系は 3.3.13、それ以前は 8.x-2.41 へ更新。あわせて注文データに不整合がないか監査することが求められています。

**やさしい解説**
ネットショップのレジ周りの「本人確認」が抜けていて、他人が勝手に注文や金額を操作できてしまう可能性がある、というイメージです。ショップ運営者は更新と注文履歴の確認を。買い物をする側は、利用明細に身に覚えのない請求がないかを確認しましょう。

**ソース**
- [Drupal warns of critical Commerce Core flaw exploited in attacks（BleepingComputer）](https://www.bleepingcomputer.com/news/security/drupal-warns-of-critical-commerce-core-flaw-exploited-in-attacks/)

---

## 4. Cursor のマーケットプレイスで「Claude Code」を装った拡張機能が SSH バックドアを設置

**何が起きたか**
2026年10月29日、Anthropic の Claude Code の拡張機能を装った悪意あるバージョン（2.1.313）が、Cursor の拡張機能マーケットプレイスで約11時間配布されました。読み込み時に自動実行され、永続的な SSH バックドアの設置を試みます。Anthropic はこの拡張機能を開発しておらず、攻撃者がどう公開できたかは不明です（報道時点）。

**影響範囲**
最大約5,000人の開発者が入手した可能性。Phorion の分析では、SSH 有効化処理の不具合で遠隔アクセスが成立しなかった端末も多いとされますが、SSH 鍵の設置や端末情報の送信は行われた可能性があります。当初報じられた npm / Open VSX / VS Code Marketplace への影響は、後に否定されています。

**現状と対応**
Cursor は拡張機能を削除し、マーケットプレイスを一時停止して他の拡張機能を監査、アクセスキーを更新、攻撃者のサーバーを停止させました。該当期間に導入した人は、`svc-telemetry` という名前の SSH 鍵がないか確認し、あれば端末を隔離して秘密情報の更新を行うよう推奨されています。

**やさしい解説**
「公式っぽい名前のアプリ」を入れたら、中身が合鍵屋だった、という話です。拡張機能は便利な反面、パソコン内の情報に広く触れられます。開発者は、入れる拡張機能の発行元を確認し、不要なものは入れないことが基本です。

**ソース**
- [Malicious Claude Code extension on Cursor planted SSH backdoors（BleepingComputer）](https://www.bleepingcomputer.com/news/security/malicious-claude-code-extension-on-cursor-planted-ssh-backdoors/)

---

## 5. Trezor「Safe 5」に暗号資産窃取用の部品が仕込まれた疑い（未確認）

**何が起きたか**
Trezor は、東南アジアの販売代理店 CryptoBilis 経由で売られた「Trezor Safe 5」に、窃取目的とみられる不正な部品が見つかった疑いがあると警告しました。インドネシアの購入者が、基板と画面の間に携帯通信モジュール付きの余分な基板があると報告したものですが、Trezor はまだ実機を検証できておらず、**現時点では未確認**です。

**影響範囲・対応**
2026年3月以降に CryptoBilis 経由で購入した端末が対象。Trezor は使用・セットアップを控えるよう推奨し、すでに使った場合は新しいリカバリーフレーズで作った新規ウォレットへ資産を移すよう案内しています。購入証明があれば交換などに応じるとのことです。サプライチェーン攻撃による流出は把握していないとしています。

**やさしい解説**
「安全な金庫」を買ったら、中に盗聴器が入っていたかもしれない、という話です。ハードウェアウォレットは正規の販売店から購入することが重要です。

**ソース**
- [Trezor warns of suspected crypto-theft implant in hardware wallet（BleepingComputer）](https://www.bleepingcomputer.com/news/security/trezor-warns-of-suspected-crypto-theft-implant-in-hardware-wallet/)

---

## 今日やること

**一般利用者向け**
- 暗号資産取引所や関連サービスからの「補償」「再認証」を名乗るメール・SMS のリンクは開かない。
- 利用中サービスから漏えいの連絡が来たら、同じパスワードを使い回していないか確認し、変更する。
- ハードウェアウォレットなどの機器は、公式または正規販売店で購入する。

**IT担当者向け**
- GitLab セルフマネージド版を 19.4.2 / 19.3.5 / 19.2.8 のいずれか該当版へ更新（CVE-2026-97229）。
- Drupal Commerce Core を 3.3.13 または 8.x-2.41 へ更新し、注文データを監査（CVE-2026-118539）。
- 開発端末で Cursor を使用している場合、`svc-telemetry` という SSH 鍵の有無を確認。拡張機能の導入ルールも見直す。
- 特権的な操作ができる管理者・開発者端末の防御（EDR、権限の最小化）を点検する。

## 留意点

- Binance の被害額は報道で表記に揺れがあり、攻撃者の特定は分析企業の見立てで、Binance 公式の見解ではありません。
- Trezor の件は、メーカーが実機未検証の段階で、報告内容は未確認です。
- CISA KEV には2026年10月30日に Ivanti Connect Secure の CVE-2026-111357 / CVE-2026-118527 が追加されたことを確認しましたが、検索では詳細な裏付けを取れなかったため、本日は掲載を見送りました。IT担当者は [CISA KEV](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) と Ivanti の公式アドバイザリを直接確認してください。同日に KEV 追加された VMware ESX（CVE-2026-41709、10月28日追加）も未掲載です。
- 期間外として見送った国内案件（いずれも ScanNetSecurity が10月29〜30日に報じたが、事業者の公表は48時間より前）：ショップサーブ（約2,335万6,000人、最終報は10月16日）、阪急阪神百貨店予約サイト（H2O ID 約126万件、10月19日公表）、ニフティ（最大54万2,513件、10月19日確認）。詳細は [ScanNetSecurity 10月の記事一覧](https://scan.netsecurity.ne.jp/article/2026/10/) を参照してください。
