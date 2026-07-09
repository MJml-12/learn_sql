# ⚽ SQL Practice Playground — Football League Edition

ブラウザだけで動くSQL学習サイトを自作しました。サーバー・インストール不要、`index.html` を開くだけでSQLiteデータベース（架空のサッカーリーグ）に対してSQLを実行できます。

An interactive SQL practice playground that runs entirely in the browser — no server, no installation. Open `index.html` and run real SQL queries against a fictional football league database (SQLite via WebAssembly).

**🔗 Demo:** GitHub Pages を有効にすると `https://<username>.github.io/<repo>/` でそのまま動きます

## 特徴 / Features

- **完全にブラウザ内で動作** — [sql.js](https://github.com/sql-js/sql.js)（SQLite の WebAssembly 版）を使用。データベースはページ読み込み時に JavaScript でシード生成（8クラブ・104選手・56試合）
- **14日間のカリキュラム** — 基礎の SELECT から Window 関数まで、データアナリストの実務・コーディングテストを想定した構成
- **サッカーがテーマ** — 得点ランキング、順位表の作成、スタジアム稼働率などの実践的な題材
- **各問題に模範解答つき**（折りたたみ表示）
- エディタは Ctrl+Enter で実行可能

## カリキュラム / Curriculum

| 日 | テーマ |
|---|---|
| 1 | SELECT, WHERE, ORDER BY |
| 2 | 集計 (COUNT / SUM / AVG / GROUP BY / HAVING) |
| 3 | INNER JOIN |
| 4 | 複数 JOIN・自己結合・LEFT JOIN |
| 5 | サブクエリ |
| 6 | CTE (WITH句) — 順位表の作成 |
| 7 | 週次レビュー・ミニテスト |
| 8 | ROW_NUMBER / RANK / DENSE_RANK |
| 9 | LAG / LEAD |
| 10 | 累積合計・移動平均 |
| 11 | CASE / COALESCE / 日付関数 |
| 12 | グループごとの Top-N（頻出パターン） |
| 13 | KPI設計クエリ（スタジアム稼働率・月次トレンド等） |
| 14 | 模擬テスト（60分） |

## データベーススキーマ / Schema

```
teams   (team_id, name, city, stadium_capacity)
players (player_id, team_id, name, position, birth_year, nationality)
matches (match_id, match_date, home_team_id, away_team_id,
         home_goals, away_goals, attendance)
goals   (goal_id, match_id, player_id, minute, is_penalty)
```

## 使い方 / How to use

1. このリポジトリをクローンまたはダウンロード
2. `index.html` をブラウザで開く（初回のみ sql.js の読み込みにインターネット接続が必要）
3. 画面下のエディタにSQLを書いて「▶ 実行」

```sql
-- まずはこれから
SELECT * FROM teams;

-- 得点ランキング
SELECT p.name, COUNT(*) AS goals
FROM goals g JOIN players p ON p.player_id = g.player_id
GROUP BY p.player_id
ORDER BY goals DESC LIMIT 10;
```

## 技術スタック / Tech stack

- HTML / CSS / Vanilla JavaScript（フレームワークなし・1ファイル完結）
- [sql.js 1.8.0](https://sql.js.org/) — SQLite compiled to WebAssembly
- シード付き擬似乱数（mulberry32）による再現可能なデータ生成

## 作成の背景 / Background

データアナリスト職の就職活動に向けて、SQL（特に Window 関数と KPI 設計クエリ）を
体系的に練習するために作成しました。問題文はインドネシア語（母語）で書いています。

Built as part of my preparation for data analyst positions in Japan.
Exercise descriptions are written in Indonesian (my native language).

## License

MIT © 2026 Muhamad Jamal Alhafizt
