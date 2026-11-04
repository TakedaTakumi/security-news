---
layout: post
title: "今日のホットニュース（2026年11月4日）"
date: 2026-11-04 09:00:00 +0900
---

## 今日のポイント

- 無印良品の公式アプリ「MUJIアプリ」で、最大約2,726万件の顧客情報（メールアドレス・生年月日・性別）が流出した可能性が報じられました。
- 【続報】Binance が事件の詳細を公表。偽の採用面接を入口に社員PCへマルウェアを仕込まれ、約63億ドルが盗まれたと説明しています。
- AI 型の攻撃ツール「ARTEX AI」による侵害（WorkOS・Chainstack）や、セキュリティ製品 cPGuard の更新経路乗っ取りなど、「信頼している仕組み」を悪用する攻撃が目立ちます。

---

## 1. 「MUJIアプリ」で最大約2,726万件の顧客情報が流出した可能性

**何が起きたか**
良品計画は、無印良品の公式アプリ「MUJIアプリ」への外部からの不正アクセスを検知し、保有する顧客情報の一部が外部へ流出した可能性があると公表しました。発表日は2026年10月30日で、専門メディアによる報道は11月4日です。

**影響範囲**
- 最大約2,726万件（退会した顧客の情報も含む）。
- 流出した可能性のある情報：メールアドレス、生年月日、性別。報道では、これ以外の情報（パスワード・カード情報等）への言及は確認できていません。

**現状と対応**
不正アクセスの対象箇所へのアクセス遮断と修正を実施済みとされています。対象顧客へは順次連絡し、開発会社・関係会社と連携して監視体制を強化するとしています。

**やさしい解説**
名簿の一部（名前ではなく、メールアドレスと誕生日・性別）が持ち出された可能性がある状況です。こうした情報は、「無印良品を名乗る偽メール」の信憑性を高めるために悪用されやすくなります。利用者の方は、メール内のリンクを開かず、アプリや公式サイトから直接確認してください。念のため、同じメールアドレスのパスワード使い回しがないかも見直しましょう。

**ソース**
- [良品計画 お知らせ（一次。本日の実行時にはアクセス制限で内容を直接確認できませんでした）](https://www.ryohin-keikaku.jp/news/articles/2026_1030_01)
- [「MUJIアプリ」で最大 約2,726万件の顧客情報が流出した可能性（ScanNetSecurity）](https://scan.netsecurity.ne.jp/article/2026/11/04/56662.html)

---

## 2. 【続報】Binance、偽の採用面接から約63億ドルの流出に至った経緯を公表

**何が起きたか（新しい事実）**
Binance は11月3日、事件の報告書を公表しました。同社の説明によると、求職サイトを通じて偽の企業を名乗る人物がソフトウェアエンジニアに接触し、偽の面接を経て「コーディング課題」を取得させ、そこに仕込まれたマルウェアでエンジニアのPCが侵害されました。その後、社内のAIツールも使って別の従業員2人の認証情報などを入手し、10月29日にウォレットの署名サービスへ到達して資金を移動したとしています。

**影響範囲**
- 流出額は同社の説明で約63.4億ドル。11月3日時点で約28.5億ドルを凍結または阻止。
- 10月31日時点で、影響を受けたトークン資産の98%は補填済みと説明されています。
- 攻撃者は、出金停止後も Ethereum の仕組み（EIP-7702）を悪用して盗み続けたとされます。

**現状と対応**
影響を受けたシステムの再構築、侵害された端末の交換、認証情報の失効を実施済みで、外部の専門企業による検証を含め調査は継続中です。

**未確認・留意**
北朝鮮の国家支援グループ「TraderTraitor（Lazarus等）」による犯行とのFBIの見立ては以前の報道によるもので、今回の同社報告書で特定の攻撃キャンペーンとの関連は示されていません。最終的な損失額も確定していません。

**やさしい解説**
鍵のかかった金庫をこじ開けたのではなく、「金庫番の社員に、仕事の誘いを装って合鍵のコピー機を持ち込ませた」ような攻撃です。転職活動中の方は、面接官から送られた課題ファイルを会社支給や普段使いのPCで実行しないでください。IT担当者は、開発者端末と本番の権限を分離することが重要です。

**ソース**
- [Binance says fake job interview led to $6.3 billion crypto heist（BleepingComputer）](https://www.bleepingcomputer.com/news/security/binance-says-fake-job-interview-led-to-63-billion-crypto-heist/)
- [Binance Reveals How Fake Job Interviews and AI Tool Abuse Led to $6.43 Billion Theft（The Hacker News）](https://thehackernews.com/2026/11/binance-reveals-how-fake-job-interviews.html)

---

## 3. セキュリティ製品 cPGuard の更新経路が乗っ取られ、サーバー約2,946台が影響

**何が起きたか**
Linux Web サーバー向けセキュリティ製品「cPGuard」（開発元 OpsShield）の更新基盤が、盗まれた認証情報で侵害され、バックドアと情報窃取スクリプトが配布されました。2026年11月2日 02:06 UTC に開始し、同社は約12時間以内に検知して配布を止めたとしています。侵入に使われた認証情報の入手経路は不明です。

**影響範囲**
- 対象バージョン：5.88.12〜5.88.19。
- 影響を受けたサーバーは同社の説明で2,946台。請求システムのデータベースも複製されたとされます。
- 窃取対象：Linux のパスワードハッシュ、データベースの管理者設定、root のシェル履歴、SSH 関連ファイルなど。

**現状と対応**
5.88.25 以降へ更新するとバックドアなどは除去されます。ただし、すでに盗まれた情報は戻らないため、パスワード・DB認証情報・クラウドの秘密情報・SSH鍵の再発行が必要です。

**やさしい解説**
防犯システムの「定期点検業者」が偽物にすり替えられ、点検のたびに家の鍵の情報を持ち出されたような事態です。cPGuard を使っている方（主にホスティング管理者）は、更新だけで終わらせず、鍵とパスワードを全て取り替えてください。

**ソース**
- [Hackers hijack cPGuard autoupdate to deploy backdoor, steal data（BleepingComputer）](https://www.bleepingcomputer.com/news/security/hackers-hijack-cpguard-autoupdate-to-deploy-backdoor-steal-data/)
- [cPGuard Update Channel Hijacked to Backdoor Linux Servers and Collect Password Hashes（The Hacker News）](https://thehackernews.com/2026/11/cpguard-update-channel-hijacked-to.html)

---

## 4. AI 型攻撃ツール「ARTEX AI」で WorkOS・Chainstack が侵害

**何が起きたか**
開発者向け基盤を提供する WorkOS は、10月30日に営業チーム用の社内アプリへの不正アクセスを確認したと公表しました。攻撃には、AI で偵察・侵入を自動化するオープンソース由来のツール「ARTEX AI」が使われたと説明しています。ブロックチェーン基盤の Chainstack も、10月26日に開発環境へ侵入され、本番環境の一部まで権限を広げられたと公表しています（10月31日に検知・遮断）。

**影響範囲**
- WorkOS：CRM の取引先担当者情報（氏名・メール・役職・会社）、顧客アカウントの利用履歴、営業・サポートでのやり取りの要約など。同社は、製品の本番サービスやアプリのデータへの影響はないとしています。
- Chainstack：顧客アカウントのデータベース（組織名・担当者名・メール）、パスワードのハッシュ、ノード認証情報（読み取られた証拠はないが、漏えい扱い）。顧客数は未公表。
- 関連して、Chainalysis など同じ攻撃との関連が報じられた事例が複数あります（Chainalysis は既報）。Chainstack は、中国系グループによる ARTEX 利用の可能性を示唆していますが、攻撃の詳細は公表していません。

**現状と対応**
WorkOS は外部アクセスの遮断と調査会社の起用を、Chainstack は経路の遮断と、顧客へのノード認証情報・API キー・パスワードの再発行を案内しています。

**やさしい解説**
AI が「侵入できる扉を24時間休まず探して回る」ようになり、守る側の対応が追いつきにくくなっています。利用者としては、該当サービスから通知が届いたら案内どおりに鍵（APIキー・パスワード）を取り替え、営業やサポートを装った不審な連絡に注意してください。

**ソース**
- [WorkOS says attacker used ARTEX AI to breach internal sales app（BleepingComputer）](https://www.bleepingcomputer.com/news/security/workos-says-attacker-used-artex-ai-to-breach-internal-sales-app/)
- [Chainstack Reports Production Systems Breach Exposing Customer Data and Password Hashes（The Hacker News）](https://thehackernews.com/2026/11/chainstack-reports-production-systems.html)

---

## 5. Barracuda 製品に root 権限につながる重大な脆弱性（修正版あり）

**何が起きたか**
Barracuda は、複数製品に影響する脆弱性 CVE-2026-116606（Email Security Gateway の認証の不備で、全体設定を変更される恐れ）と CVE-2026-111560（管理者権限を持つ利用者が root 権限で OS コマンドを実行できる）を公表しました。2つを組み合わせると、権限の制限を回避して root 権限を得られる可能性があるとされています。

**影響範囲**
- Email Security Gateway は両方、Load Balancer ADC・Message Archiver・WAF・WAF Control Center・Web Security Gateway は CVE-2026-111560 の対象。
- 悪用の確認は報じられていません。攻撃には管理画面へのアクセスが必要とされます。

**現状と対応**
製品ごとにパッチが提供されています（例：Email Security Gateway は BNSF-40425／BNSF-40430）。最新ファームウェアと全パッチの適用、管理画面を信頼できる内部ネットワークに限定することが推奨されています。

**やさしい解説**
建物の「管理人室」に入れる人が、そこから建物全体のマスターキーまで手に入れられてしまう欠陥です。管理画面がインターネットから見える状態になっていないかを、まず確認してください。

**ソース**
- [Barracuda warns of critical flaws allowing root access to devices（BleepingComputer）](https://www.bleepingcomputer.com/news/security/barracuda-warns-of-critical-flaws-allowing-root-access-to-devices/)
- [Barracuda Flaws Could Be Chained to Bypass Authorization and Gain Root Access（The Hacker News）](https://thehackernews.com/2026/11/barracuda-flaws-could-be-chained-to.html)

---

## 6. 外務省の外部接続ネットワークに不正アクセス、約3,600件の個人情報が漏えいした可能性

**何が起きたか**
外務省は2026年10月30日、外部とのやり取りが可能なネットワークへの不正アクセスを7月27日に検知していたと公表しました（専門メディアの報道は11月4日）。

**影響範囲**
- メールアドレス・氏名など約3,600件が漏えいした可能性があり、うち外務省職員以外の個人情報は約900件。
- 機密性の高い情報を扱う閉域ネットワークは影響を受けていないとされます。

**現状と対応**
不正アクセスの遮断と認証情報の無効化を実施済みです。今後、対象者を特定して個別に連絡し、アクセス制御・認証方法の見直しなどを進める方針です。

**やさしい解説**
役所の「受付窓口」にある書類の一部が見られた可能性があるものの、「金庫室」は無事だったという状況です。外務省とやり取りした覚えのある方は、省を名乗る不審なメールに注意してください。

**ソース**
- [外務省「不正アクセスによる個人情報の漏えいの可能性について」（一次）](https://www.mofa.go.jp/mofaj/press/release/pressit_000001_04395.html)
- [外務省のネットワークに不正アクセス、7月27日に検知（ScanNetSecurity）](https://scan.netsecurity.ne.jp/article/2026/11/04/56663.html)

---

## 今日やること

**一般利用者向け**
- 無印良品・MUJIアプリの利用者は、「MUJI」を名乗るメール・SMS のリンクを開かず、公式アプリから確認する。
- 転職活動中に、面接官から「課題ファイル」を渡された場合は、実行せず内容を第三者に確認する。
- 各サービスからの通知メールは、メール内のリンクではなく公式サイトから確認する。

**IT担当者向け**
- cPGuard を使っている場合は 5.88.25 以降へ更新し、パスワード・DB認証情報・SSH鍵・クラウドの秘密情報を全て再発行する。
- Barracuda 製品の該当パッチを適用し、管理画面の公開範囲を確認する。
- 開発者端末と本番環境の権限を分離し、開発者端末へのマルウェア感染が本番に直結しない構成にする。
- WorkOS・Chainstack を利用している場合は、各社の通知に従って API キー・ノード認証情報を再発行する。

## 留意点

- MUJIアプリの件は、良品計画の一次ソースが本日アクセス制限（HTTP 429）で直接確認できず、ScanNetSecurity の報道内容に基づいています。
- Binance の経緯は同社自身の説明に基づきます。北朝鮮関与は FBI による見立てとして以前報じられたもので、今回の報告書では特定されていません。
- 本日の期間外・既出のため見送った案件：松屋フーズ・チャリロトの関連報道（既出で新しい事実を確認できず）、WordPress 本体の脆弱性（既出）、Harvard 大学の情報流出（851,000アカウント、詳細未確認）、mSecure・Siemens IoT2050 等（詳細未確認）。
