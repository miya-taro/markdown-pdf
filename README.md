# Markdown 手順書テンプレート

Markdown と [Markdown Preview Enhanced](https://shd101wyy.github.io/markdown-preview-enhanced/)（MPE）を使い、標準化された作業手順書（SOP）を効率的に作成・PDF 出力するためのテンプレート一式です。

本テンプレートは **Linux サーバー上の CLI 作業** を主に想定しています。GUI 操作が中心の手順は「6. 作業手順」を画面操作ベースに差し替えてください。

## ファイル構成

| ファイル / フォルダ | 説明 |
| :--- | :--- |
| `標準手順書テンプレート.md` | 手順書の Markdown テンプレート（コピーして実手順書として利用） |
| `style.less.sample` | MPE 用スタイル定義のサンプル（プレビュー・PDF 共通） |
| `images/` | 挿絵・スクリーンショット用フォルダ |
| `標準手順書テンプレート.html` | テンプレートから出力した HTML の記録 |
| `標準手順書テンプレート.pdf` | テンプレートから出力した PDF の記録 |

## 前提環境

- **エディタ:** Visual Studio Code / Cursor
- **拡張機能:** [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)
- **PDF 出力:** MPE の「Chrome (Puppeteer) / PDF」（Chromium が必要）

## セットアップ

### 1. スタイルの適用

`style.less.sample` を MPE のグローバルスタイルとして配置します。

```text
~/.crossnote/style.less
```

Windows の場合の例:

```text
C:\Users\<ユーザー名>\.crossnote\style.less
```

`style.less.sample` の内容をコピーするか、リポジトリから直接コピーしてください。プレビューと PDF の両方に同じスタイルが適用されます。

**重要:** 図番号は使わず、図タイトルは図の下、表タイトルは表の上に置きます。更新後は MPE プレビューを開き直してください。

### 2. 手順書の作成

1. `標準手順書テンプレート.md` をコピーし、作業名に合わせてファイル名を変更する
2. Frontmatter の `status` を `draft` から `active` に変更する
3. 先頭の「運用ルール」ブロックを削除する（PDF 配布物には含めない）
4. 本文のプレースホルダ（〇〇、YYYY-MM-DD など）を実際の内容に置き換える

### 3. 画像・図タイトルの挿入

画像は `images/` フォルダに配置し、図タイトルは `図：[名称]` の形式で記載します。

#### 画像の例

```html
<img src="images/サンプル.png" alt="説明" width="80%">
<p class="fig-caption">図：キャプション文</p>
```

表示例: **図：キャプション文**（図の下）

#### Mermaid フロー図の例

```html
```mermaid
graph TD
    A --> B
```

<p class="fig-caption">図：作業全体フロー</p>
```

### 4. 表タイトルの付け方

Markdown の表の直前に `<p class="table-caption">` を置き、`表：[名称]` の形式で記載します。

```markdown
<p class="table-caption">表：固定情報（GUI等）</p>

| 項目 | 値 |
| :--- | :--- |
| 対象システム | 本番環境 |
```

表示例: **表：固定情報（GUI等）**

## テンプレートの構成

手順書は次の 10 セクションで構成されています。

1. 目的と対象者
2. 前提条件
3. 準備するもの
4. 変数・固定情報
5. 全体フロー（Mermaid 図）
6. 作業手順（フェーズ別・ロールバック含む）
7. トラブルシューティング
8. 問い合わせ先・エスカレーション
9. 関連資料
10. 変更履歴

## 運用ルール

テンプレート先頭の運用ルールに従ってください。要点は次のとおりです。

- **日付の同期:** Frontmatter の `date`、本文の「最終更新日」、「10. 変更履歴」を更新時に必ず揃える
- **ステータス:** 実運用開始時は Frontmatter の `status` を `active` に変更する
- **運用ルールの削除:** 実手順書として配布する前に、先頭の運用ルール blockquote を削除する
- **目次:** 手動では書かず、MPE の自動目次生成（`<!-- @import "[TOC]" ... -->`）を利用する
- **目次の自動生成ブロック:** `<!-- code_chunk_output -->` は MPE が自動挿入する。手編集不要。プレビュー時に差分が出ても問題ない
- **改ページ:** `<div class="page-break"></div>` は PDF 用マーカー。削除・移動しない
- **警告の書き方:** MPE 互換のため `<blockquote class="alert-warning">` を使う（テンプレート 6.2 に例あり）
- **リンク:** PDF 共有が主目的の場合は `[[wikiリンク]]` ではなく通常の Markdown リンク `[表示名](URL)` を使う

## PDF / HTML の出力

1. `標準手順書テンプレート.md`（またはコピーした手順書）を MPE で開く
2. コマンドパレットから **Markdown Preview Enhanced: Open Preview** でプレビューを確認する
3. プレビュー上で右クリック → **Chrome (Puppeteer) / PDF** を選択して PDF を出力する
4. HTML が必要な場合は **Chrome (Puppeteer) / HTML** を利用する

`style.less` が正しく配置されていれば、本リポジトリに含まれる `標準手順書テンプレート.pdf` および `標準手順書テンプレート.html` と同様の体裁で出力されます。

`style.less` を更新した場合は、プレビューを開き直してから PDF を再出力してください。

## スタイルの主な特徴

`style.less.sample` は手順書向けに次の点を調整しています。

- 日本語フォント（Meiryo / Yu Gothic UI など）と 11pt ベースの読みやすい行間
- 見出し・表・コードブロック・引用の視認性
- 挿絵・スクリーンショットのサイズ指定（`<img ... width="80%">`）
- 図タイトル・表タイトル（`図：[名称]` / `表：[名称]`）
- 警告ブロック（`.alert-warning`）の赤系スタイル
- A4 縦・余白・改ページ制御（`@media print`）
- `<div class="page-break"></div>` による手動改ページ
- 印刷時の要素分割防止（表・コード・画像・Mermaid 図など）

## Frontmatter リファレンス

```yaml
---
tags: [SOP, template]
date: 2026-07-06
status: draft    # draft | active
related: "関連ドキュメント名"
print_background: true   # PDF 出力時に背景色・枠線を印刷する（false にすると省インク）
---
```

## ライセンス

社内・個人の手順書作成に自由に利用・改変してください。
