# Markdown 手順書テンプレート

Markdown と [Markdown Preview Enhanced](https://shd101wyy.github.io/markdown-preview-enhanced/)（MPE）を使い、標準化された作業手順書（SOP）を効率的に作成・PDF 出力するためのテンプレート一式です。

## ファイル構成

| ファイル | 説明 |
| :--- | :--- |
| `標準手順書テンプレート.md` | 手順書の Markdown テンプレート（コピーして実手順書として利用） |
| `style.less.sample` | MPE 用スタイル定義のサンプル（プレビュー・PDF 共通） |
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

### 2. 手順書の作成

1. `標準手順書テンプレート.md` をコピーし、作業名に合わせてファイル名を変更する
2. Frontmatter の `status` を `draft` から `active` に変更する
3. 本文のプレースホルダ（〇〇、YYYY-MM-DD など）を実際の内容に置き換える

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
- **目次:** 手動では書かず、MPE の自動目次生成（`<!-- @import "[TOC]" ... -->`）を利用する
- **改ページ:** `<div class="page-break"></div>` は PDF 用マーカー。削除・移動しない

## PDF / HTML の出力

1. `標準手順書テンプレート.md`（またはコピーした手順書）を MPE で開く
2. コマンドパレットから **Markdown Preview Enhanced: Open Preview** でプレビューを確認する
3. プレビュー上で右クリック → **Chrome (Puppeteer) / PDF** を選択して PDF を出力する
4. HTML が必要な場合は **Chrome (Puppeteer) / HTML** を利用する

`style.less` が正しく配置されていれば、本リポジトリに含まれる `標準手順書テンプレート.pdf` および `標準手順書テンプレート.html` と同様の体裁で出力されます。

## スタイルの主な特徴

`style.less.sample` は手順書向けに次の点を調整しています。

- 日本語フォント（Meiryo / Yu Gothic UI など）と 11pt ベースの読みやすい行間
- 見出し・表・コードブロック・引用の視認性
- A4 縦・余白・改ページ制御（`@media print`）
- `<div class="page-break"></div>` による手動改ページ
- 印刷時の要素分割防止（表・コード・リスト・Mermaid 図など）

## Frontmatter リファレンス

```yaml
---
tags: [SOP, template]
date: 2026-07-06
status: draft    # draft | active
related: [[関連ノート名]]
print_background: true
---
```

## ライセンス

社内・個人の手順書作成に自由に利用・改変してください。
