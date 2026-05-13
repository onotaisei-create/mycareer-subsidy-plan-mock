# 静的HTMLをお名前.comサーバーにアップする手順

WordPress を経由せず、`https://my-career.co.jp/ai-naiseika-kun/` でアクセスできる静的ページとして公開します。

## 仕組み

WordPress の `.htaccess` には標準で以下のルールがあります:

```
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
```

「実在するファイルまたはディレクトリにはリライトを適用しない」という意味なので、ドキュメントルート直下に `ai-naiseika-kun/` フォルダを作って `index.html` を置けば、WordPress に取られず静的HTMLがそのまま配信されます。

## アップロード手順

### 1. ファイル取得

[index.html](index.html) をローカルに保存。

直接URL: https://raw.githubusercontent.com/onotaisei-create/mycareer-ai-naiseika-kun-mock/main/static/index.html

ブラウザでこのURLを開き、右クリック → 「名前を付けてページを保存」（HTML のみ）で `index.html` として保存。

### 2. お名前.com にアップロード

#### 方法A: Web Filer（ブラウザだけで完結・推奨）

1. https://www.onamae.com/navi/login.php からログイン
2. ご利用中のサービス → レンタルサーバー → コントロールパネル
3. **Web Filer**（ファイルマネージャー）を開く
4. **ドキュメントルート直下**（`public_html/` など、`index.php`（WordPressのもの）と `wp/` フォルダが並んでいる階層）に移動
5. 「新規フォルダ作成」で `ai-naiseika-kun` という名前のフォルダを作る
6. 作った `ai-naiseika-kun/` フォルダに入って、「アップロード」で `index.html` を選択

#### 方法B: FTPクライアント（Cyberduck 等）

1. お名前.com Navi でFTPアカウント情報を取得
2. Cyberduck で SFTP 接続
3. ドキュメントルートに移動 → `ai-naiseika-kun/` フォルダ作成 → `index.html` をドロップ

### 3. 動作確認

ブラウザで以下を開く:

```
https://my-career.co.jp/ai-naiseika-kun/
```

## アクセスできなかった場合

### 「404 Not Found」になる
- ファイルが置かれた場所が間違っている可能性
- Web Filer で `ai-naiseika-kun/index.html` のパスを確認
- ドキュメントルートではなく WordPress の `/wp/` の中に入れてしまっていないか確認

### WordPressのページ「お探しのページは見つかりませんでした」が出る
- `.htaccess` のリライトが効きすぎている可能性（稀）
- ドキュメントルートの `.htaccess` を確認し、WordPress標準のままなら問題なし。改変されている場合は連絡ください

### スタイルが崩れる
- 外部CDN（Google Fonts / yakuhanjp）が読めていない可能性
- お名前.comサーバーの外部接続が制限されている → 開発者ツールのNetworkタブで赤いエラーを確認

## 編集する場合

`index.html` をローカルで編集 → 再度同じ場所に上書きアップロード。フォルダ構成は変えない。
