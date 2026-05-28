# hit-sbv2-to-aivm-webui

[hit-sbv2-to-aivm-api](https://github.com/Glue-th/hit-sbv2-to-aivm-api) と連携する WebUI です。  
ブラウザから SBV2 モデルを選択・メタデータを入力して `.aivmx` ファイルに変換できます。

## 概要

- ダークテーマの SPA（単一 HTML ファイル）
- モデル一覧をリアルタイム検索・フィルタリング
- 話者・スタイルのカスタム設定
- API キーはブラウザの `localStorage` に保存（サーバーには保存しない）
- nginx で静的ファイルを配信

## 必要環境

- Docker + Docker Compose
- 別途 [hit-sbv2-to-aivm-api](https://github.com/Glue-th/hit-sbv2-to-aivm-api) が起動済みであること

## セットアップ & 起動

```bash
git clone git@github.com:Glue-th/mm-sbv2-to-aivm-webui.git
cd mm-sbv2-to-aivm-webui
bash run.sh
```

メニューから `2`（起動）を選択。

## run.sh メニュー

| 番号 | 操作 |
|------|------|
| 1 | 更新 & 再起動（`git pull` → `restart`） |
| 2 | 起動（`up -d`） |
| 3 | 再起動 |
| 4 | 停止 |
| 5 | ログ表示 |
| 6 | 状態確認 |

> `index.html` はボリュームマウントのため、`git pull` 後に `restart` するだけで反映されます（再ビルド不要）。

## 初回設定

1. ブラウザでアクセス（デフォルト: `http://localhost:8081`）
2. 自動的に「API 接続設定」モーダルが開く
3. **API URL** と **API キー** を入力して「保存して接続」

設定はブラウザの `localStorage` に保存され、次回以降は自動で読み込まれます。

> **注意：** `localStorage` はドメイン・ポートごとに独立しています。  
> 別のドメインからアクセスした場合は再設定が必要です。

## 使い方

1. **モデルを選択** — 検索ボックスにキーワードを入力してフィルタリング
2. **メタデータを入力** — モデル名・説明・制作者・アーキテクチャを設定
3. **話者・スタイルを設定** — 自動入力される話者・スタイルを必要に応じて編集
4. **「変換する」ボタンを押す** — 変換完了後に `.aivmx` ダウンロードボタンが表示される

## ポート

| ポート | 用途 |
|--------|------|
| `8081` | WebUI（nginx） |
