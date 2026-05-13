# お名前.com レンタルサーバー へのアップロード手順

`page-subsidy-plan.php` を テーマフォルダ にアップロードする手順です。

## アップロード先パス（共通）

```
/wp/wp-content/themes/mycareer_2023/page-subsidy-plan.php
```

WordPressのインストール位置がドキュメントルート直下の `wp/` 配下になっているので、サーバー側では以下のような実パスになるはずです（プランにより前部分は異なる）:

```
/<contractID>/<domain>/public_html/wp/wp-content/themes/mycareer_2023/
または
/home/<account>/<domain>/wp/wp-content/themes/mycareer_2023/
```

---

## 方法A: Web Filer（ブラウザから・推奨）

サーバーにFTPツールなしでアップロードできる、お名前.comの管理画面内蔵ファイルマネージャー。

1. https://www.onamae.com/navi/login.php からログイン
2. 上部メニュー「ご利用中のサービス確認」→「レンタルサーバー」を選択
3. 該当サーバーの「コントロールパネル」へ
4. メニューから「**Web Filer**」（または「ファイルマネージャー」）を開く
5. ディレクトリを `wp/wp-content/themes/mycareer_2023/` まで降りる
6. 「**アップロード**」ボタン → page-subsidy-plan.php を選択
7. アップロード完了を確認

ファイル本体取得:
- https://raw.githubusercontent.com/onotaisei-create/mycareer-subsidy-plan-mock/main/wordpress/page-subsidy-plan.php

ブラウザでこのURLを開いて「右クリック → 名前を付けて保存」で `page-subsidy-plan.php` として保存してから Web Filer にアップロード。

---

## 方法B: FTPクライアント（FileZilla / Cyberduck）

Macなら **Cyberduck**（無料）が楽です。

### 1. FTPアカウント情報を取得

1. お名前.com Navi → レンタルサーバー → コントロールパネル
2. 「FTPアカウント」または「FTP/SFTPアカウント」メニュー
3. 既存アカウントの情報、または新規作成
   - **FTPサーバー名**: `ftp.<契約ID>.gmoserver.jp` 等
   - **FTPユーザー名**
   - **FTPパスワード**

### 2. Cyberduckで接続（Mac）

1. https://cyberduck.io/ からダウンロード・インストール
2. 起動 → 「新規接続」
3. プロトコル: **SFTP**（推奨）または FTP
4. 上記の接続情報を入力
5. 接続

### 3. アップロード

1. 接続後、`wp/wp-content/themes/mycareer_2023/` に移動
2. ローカルから `page-subsidy-plan.php` をドラッグ＆ドロップ

---

## アップロード後のWP設定

1. WP管理画面 → 固定ページ → 既存の「助成金活用プラン」ページを編集
2. **本文は空に**（テンプレート側で全部出力するので）
3. 右サイド「ページ属性」→「テンプレート」のドロップダウンを開く
4. 「**助成金活用プラン**」が表示されているはず → 選択
5. 「更新」
6. プレビュー or ページを表示で確認

---

## トラブルシューティング

### テンプレートのドロップダウンに「助成金活用プラン」が出てこない
- アップロード先パスが間違っている可能性 → `wp/wp-content/themes/mycareer_2023/` 直下を確認
- ブラウザキャッシュ → 管理画面を一度ログアウト→再ログイン
- ファイル名が正確か（`page-subsidy-plan.php`、拡張子間違いなし）

### アップロード後、ページが真っ白
- PHPの構文エラーの可能性 → サーバーのエラーログ確認
- Web Filerでファイルが0バイトになっていないか確認 → 再アップロード

### お問い合わせのURLが違う
- ファイル末尾 `home_url( '/contact/' )` の `/contact/` を実際のURLに変更してから再アップロード

---

## 注意

- `get_header()` / `get_footer()` でテーマのヘッダー・フッター・CSSは自動で読み込まれます
- ページ独自のCSSは全クラスに `.sp-` プレフィックスを付けてあるのでテーマCSSと干渉しないはずです
- もし崩れが発生したらブラウザの検証ツール（右クリック→検証）で該当箇所のスクショを送ってください
