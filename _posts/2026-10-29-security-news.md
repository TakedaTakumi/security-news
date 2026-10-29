---
layout: post
title: "今日のホットニュース（2026年10月29日）"
date: 2026-10-29 09:00:00 +0900
---

## 今日のポイント

- ソニーグループのISP子会社 Sony Network Communications で、So-net／plala の会員情報約258万件が流出。メールアドレス約5.4万件はパスワードも含まれるため、変更が推奨されています。
- 【続報】Brotli の脆弱性（Node2Shell）と、PHP2Shell と連鎖して悪用される Linux カーネルの脆弱性が、CISA の「悪用確認済み」リスト（KEV）に追加されました。Adobe Commerce/Magento の脆弱性も同リストに入っています。
- Oracle E-Business Suite の重大な脆弱性に対する探索的な攻撃が観測されています。修正は10月20日に公開済みなので、未適用の組織は急ぎましょう。

---

## ニュース本文

### 1. Sony Network Communications（So-net／plala）会員情報 約258万件が流出

**何が起きたか**
Sony Network Communications が管理する会員データベースに不正アクセスがあり、10月19日に発生、10月23日頃に検知したと、10月27日に公表されたと報じられています。検知後、該当サーバーは停止され外部との通信が遮断されました。

**影響範囲**
報道によると、流出は計2,585,481件で、内訳は So-net が2,141,986件、plala（S Course）が443,495件です。plala は NTT ドコモの「ドコモ光」を提供しているため、ドコモ経由の利用者も対象に含まれます。氏名、電話番号、メールアドレス、ユーザーID、生年月日、性別、インターネット接続IDが対象で、銀行口座・クレジットカード等の決済情報は含まれないとされています。別途、複数のメールサービスのメールアドレス54,401件がパスワードとともに流出したと報じられています。

**現状と対応**
同社は個人情報保護委員会に報告し、原因と被害範囲を調査中です。10月27日時点で流出データの悪用は確認されていないとされます。NTT ドコモは顧客に通知し、d POINT CLUB や USJ を装ったフィッシングへの注意を呼びかけたと報じられています。

**やさしい解説**
住民名簿と連絡先リストが丸ごと持ち出されたようなものです。今回は「あなたの名前・電話番号・生年月日を知っている」相手からの偽メールや偽SMSが届きやすくなる点が一番の危険です。支払い情報は含まれないとされていますが、届いたメールのリンクは踏まず、公式アプリや自分で開いたブックマークから確認してください。対象のメールアドレスを使っていた方は、同じパスワードを使い回している他のサービスも含めて変更しましょう。

**ソース**
- [Sony ISP subsidiary data breach exposes 2.5 million customer records（BleepingComputer・報道。同社の一次発表は本稿作成時点で未確認）](https://www.bleepingcomputer.com/news/security/sony-isp-subsidiary-data-breach-exposes-25-million-customer-records/)

### 2. 【続報】Brotli の脆弱性（Node2Shell）、CISA が悪用を確認しKEVに追加

**何が起きたか**
Googleの圧縮ライブラリ Brotli のデコーダの脆弱性 CVE-2026-111497（Node2Shell／HTTP2Shell とも呼ばれる）が、10月27日に CISA の KEV に追加されました。実際の悪用が確認されたことを意味します（初出は10月26日の記事）。

**影響範囲**
細工した圧縮データによりクラッシュやメモリ情報の漏えい、条件次第でリモートコード実行につながるとされます。Node.js をはじめ、脆弱な Brotli 実装を使うサーバー・クライアントが対象になり得ます。BleepingComputer は、Microsoft が .NET 向けに緊急更新を出したと報じています。

**現状と対応**
米連邦機関の対応期限は11月10日です。パッチ適用後はプロセスの再起動、コンテナイメージの再ビルドと再デプロイが必要とされています。すぐに更新できない場合の暫定策として、プロキシ等で Brotli 圧縮リクエストを遮断する、デコード機能を無効化する、といった案が報じられています。

**やさしい解説**
荷物（圧縮データ）を開梱する機械に欠陥があり、細工した荷物を送るだけで機械が壊れたり乗っ取られたりする状態です。利用者側でできることはほとんどなく、サービス運営者の更新を待つことになります。開発・運用の担当者は、自社が使うランタイムやコンテナに更新が入っているかを確認してください。

**ソース**
- [CISA KEV カタログ（一次）](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [CISA warns of hackers now exploiting critical Node2Shell flaw（BleepingComputer）](https://www.bleepingcomputer.com/news/security/cisa-warns-of-hackers-now-exploiting-critical-node2shell-flaw/)

### 3. 【続報】PHP2Shell：連鎖して悪用される Linux カーネルの脆弱性 CVE-2026-46300 がKEVに追加

**何が起きたか**
CISA は10月28日、Linux カーネルの脆弱性 CVE-2026-46300 を KEV に追加しました。KEV の説明では、PHP2Shell の2件（CVE-2026-109618、CVE-2026-109619）と組み合わせると、PHP のウェブシェルを仕込み root 権限でコマンドを実行できるとされています。

**影響範囲**
ソケットバッファの結合処理での変数初期化漏れにより、ESP（IPsec）入力処理が共有メモリ領域をその場で復号し、ページキャッシュ上のデータが意図せず書き換わり得る、と説明されています。対象のカーネルバージョンは本稿作成時点で未確認です。

**現状と対応**
修正はカーネルのstableツリーに公開されています（KEVの参照先に記載）。対応期限は10月31日と短く設定され、フォレンジック（調査）の実施対象とされています。PHPの更新に加え、ディストリビューションのカーネル更新も確認が必要です。

**やさしい解説**
玄関（PHP）の鍵が壊れていた件に加え、建物の中の「万能の合鍵」（Linuxカーネルの欠陥）まで見つかり、組み合わせると侵入者が建物全体の管理者になれる、という話です。自分でサーバーを運用していない方がすることは特にありません。運用している方は、PHPとOSの両方を更新してください。

**ソース**
- [CISA KEV カタログ（一次）](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [NVD: CVE-2026-46300（一次）](https://nvd.nist.gov/vuln/detail/CVE-2026-46300)

### 4. Adobe Commerce／Magento の脆弱性 CVE-2026-48356 がKEVに追加

**何が起きたか**
Adobe Commerce と Magento の「危険な種類のファイルのアップロードを許してしまう」脆弱性 CVE-2026-48356 が、10月27日に KEV に追加されました。Adobe の公報（7月14日公開）では深刻度 Critical（CVSS 9.6）で、公報公開時点では悪用を把握していないとされていました。

**影響範囲**
Adobe Commerce 2.4.9、2.4.8-p5以前、2.4.7-p10以前、2.4.6-p15以前、2.4.5-p17以前、2.4.4-p18以前が対象です。

**現状と対応**
Adobe は各系統の「2026-jul」パッチ（例：2.4.8-2026-jul）を公開済みです。対応期限は11月10日です。

**やさしい解説**
ネットショップの裏側で使われる基盤ソフトに、悪意あるファイルを置けてしまう穴があった、というものです。買い物をする利用者側の対処は不要ですが、自分でECサイトを運営している場合は、パッチ適用の有無をすぐに確認してください。

**ソース**
- [Adobe セキュリティ公報 APSB26-73（一次）](https://www.adobe.com/trust/security/products/commerce/apsb26-73.html)
- [CISA KEV カタログ（一次）](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)

### 5. Oracle E-Business Suite の重大な脆弱性 CVE-2026-101767 を狙う探索的な攻撃

**何が起きたか**
認証なしでHTTP経由から攻撃できるとされる脆弱性 CVE-2026-101767 について、脅威インテリジェンス企業 Defused が、10月27日に自社のおとりシステムで探索的な攻撃を観測したと報じられました。Oracle はこの CVE を「悪用確認済み」とはまだ表示していません。

**影響範囲**
Oracle E-Business Suite の Application Object Library が対象です。Defused によれば、Thin Client Framework サーブレットの SQL インジェクションからリモートコード実行につながるとされています。Shadowserver は、インターネットに公開された EBS を670件以上追跡しています。

**現状と対応**
Oracle は10月20日の Critical Security Patch Update で修正を公開しており、攻撃が成功した例にはパッチ未適用の顧客が含まれると説明しているとのことです。

**やさしい解説**
会社の基幹業務（会計・購買など）を動かす大型ソフトの玄関に穴があり、世界中の攻撃者が「鍵の掛け忘れ」を探して回っている段階です。実害が確認されたわけではありませんが、パッチが出ている以上、IT担当者は優先的に適用してください。EBS を使っていない一般の利用者は何もする必要はありません。

**ソース**
- [Hackers now scanning systems for recently-patched Oracle flaw（BleepingComputer・Oracleの10月CPUに言及）](https://www.bleepingcomputer.com/news/security/hackers-now-scanning-systems-for-recently-patched-oracle-flaw/)

### 6. ブラジルの決済基盤 Convertr のアクセス解析スクリプト改ざん、カード情報が窃取

**何が起きたか**
Convertr が運用するアクセス解析ツール（Plausible）のトラッカーが改ざんされ、同社を利用する店舗のチェックアウトページでカード情報が盗まれたと報じられています。10月24日に攻撃が特定されました。

**影響範囲**
カード番号、有効期限、CVV、名義人、ブラジルの納税者番号（CPF）が対象です。ブラジルのファッションブランド数十社が影響を受けるとされ、10月24日以降にチェックアウトページのアドレスに「checkout.convertr」を含む店舗でカード決済した利用者に注意が呼びかけられています。侵入経路は古い Plausible の脆弱性（CVE-2026-8467）が疑われていますが、未確認です。

**現状と対応**
Convertr は不正スクリプトを削除し、Plausible を更新したとされます。影響を受けた店舗と決済事業者への通知を進めており、ブラウザのキャッシュにより最大24時間は不正スクリプトが動作し得るとされています。報道時点でConvertrからの公式回答は得られていません。

**やさしい解説**
レジの横に、こっそりカード読み取り装置を付けられたようなものです。店自体は無事でも、店が使う「部品」を乗っ取られると被害が出ます。対象の店舗で最近カード決済した方は、カード会社に連絡して利用明細を確認し、必要なら再発行を依頼してください。

**ソース**
- [Hackers hijack Convertr analytics script to steal payment card data（BleepingComputer）](https://www.bleepingcomputer.com/news/security/hackers-hijack-convertr-analytics-script-to-steal-payment-card-data/)

### 7. 中国系 Volt Typhoon の中継インフラ「Silent Train」、管理基盤の脆弱性を悪用

**何が起きたか**
Lumen の Black Lotus Labs が、中国国家支援とされる Volt Typhoon の攻撃基盤「Silent Train」に関する報告を公開したと報じられています（10月28日付）。侵害したルーターなどを中継点として連鎖させ、攻撃元を隠すとされます。

**影響範囲**
通信、政府、防衛、重要インフラなどが標的とされています。悪用された製品として、VeloCloud Orchestrator（CVE-2026-16812）、Cisco Catalyst SD-WAN（CVE-2026-20127）、N-able N-central、Versa Director、Quest KACE（ゼロデイの疑い）などが挙げられています。

**現状と対応**
報告では、集中管理システムの強化、管理画面へのインターネットからのアクセス制限、迅速なパッチ適用、ログの長期保存が推奨されています。

**やさしい解説**
泥棒が他人の家を何軒も経由して足跡を消しながら目的の家に入る、という手口です。一般の方がすることは特にありませんが、ネットワーク機器や運用管理ツールを扱う担当者は、管理画面を外部に公開していないかを点検してください。

**ソース**
- [Volt Typhoon hides zero-day attacks using 'Silent Train' framework（BleepingComputer・Black Lotus Labsの報告を報道）](https://www.bleepingcomputer.com/news/security/volt-typhoon-hides-zero-day-attacks-using-silent-train-framework/)

---

## 今日やること

**一般利用者向け**
- So-net／plala／ドコモ光のメールアドレスを使っている方は、公式の案内を確認し、メールのパスワードを変更する。
- 身に覚えのないメール・SMSのリンクは開かず、公式アプリやブックマークから確認する。
- ブラジルのネットショップでカード決済した方は、利用明細を確認する。

**IT担当者向け**
- Brotli（CVE-2026-111497）、PHP（CVE-2026-109618／109619）、Linux カーネル（CVE-2026-46300）、Adobe Commerce（CVE-2026-48356）の更新状況を確認する。コンテナは再ビルドが必要。
- Oracle E-Business Suite の10月 CPU を適用する。
- ネットワーク機器・管理基盤（SD-WAN、リモート管理ツール等）の管理画面が外部に公開されていないか点検する。

## 留意点

- Sony Network Communications の件は、報道（BleepingComputer）に基づく内容です。同社の一次発表は確認できていません。
- Oracle EBS の件は探索的な攻撃の観測で、実害や悪用確認は報じられていません。
- Linux カーネルの影響バージョンは未確認です。
- 同じ10月28日に KEV に追加された Broadcom VMware ESX の CVE-2026-41709（管理者権限での操作がログに残らない問題）は、詳細未確認のため見送りました。
- GMO の件は、新しい事実を確認できなかったため見送りました。
