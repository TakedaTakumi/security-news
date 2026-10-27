# 今日のホットニュース

ウェブサービスの脆弱性・情報流出に関するニュースを、Claude Code のルーティンで毎朝 9:00（JST）に自動作成し、GitHub Pages で公開するリポジトリです。

公開サイト：https://takedatakumi.github.io/security-news/

## 構成

| パス | 役割 |
|---|---|
| `CLAUDE.md` | 毎朝のタスク手順書（ルーティンが自動で読み込む） |
| `_config.yml` | Jekyll 設定（minima 3.0 系 dark スキンを remote_theme で固定, timezone: Asia/Tokyo） |
| `index.md` | トップページ（記事一覧） |
| `_posts/` | 毎日の記事 |
| `_data/covered.yml` | 掲載済み案件の台帳（重複除外に使用） |

## 初回セットアップ

1. このファイル一式を GitHub の**公開リポジトリ**に push する
2. リポジトリの Settings → Pages で、Source を「Deploy from a branch」、Branch を `main` / `/ (root)` にする
3. Claude Code（Web）で GitHub を連携する
4. claude.ai/code/routines で「New routine」を作成する
   - リポジトリ：このリポジトリ
   - 環境：ネットワークアクセスを **Full** にした環境（Default の Trusted ではニュースサイトにアクセスできないため）
   - トリガー：Schedule → Daily 9:00
   - コネクタ：すべて外す
   - プロンプト：下記
5. 「Run now」で試験実行し、main への push と Pages への反映を確認する

## ルーティンのプロンプト

```
あなたは毎朝9時に起動される無人タスクです。確認は求めず、最後まで実行してください。

リポジトリ直下の CLAUDE.md の手順に従い、本日（日本時間）の「今日のホットニュース」を作成してください。

完了条件：
1. _posts/YYYY-MM-DD-security-news.md（日本時間の本日付）が作成されている
2. _data/covered.yml に本日掲載した案件が追記・更新されている
3. 上記2ファイルの変更が main ブランチに直接 commit & push されている

例外時：
- 本日付の記事が既に存在する場合は、何も変更せず終了する
- main への push が拒否された場合は claude/news-YYYY-MM-DD ブランチに push する
- ニュースサイトへのアクセスが 403 等で失敗した場合は、失敗したURLをセッションの最後に一覧で報告する
```
