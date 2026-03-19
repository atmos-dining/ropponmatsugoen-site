# 六本松ごえん サイト作業メモ

## プロジェクト概要
- サイト: https://ropponmatsu-goen.com
- ホスティング: Netlify
- リポジトリ: `atmos-dining/ropponmatsugoen-site`（GitHub）
- ブランチ: main

## ブログの仕組み
- ブログデータは `blog/posts.json` 一本で管理
- 記事一覧: `blog/index.html`（posts.json を fetch して表示）
- 記事詳細: `blog/posts/post.html?slug=xxx`
- 画像: `images/` フォルダ

## CMS の状況（作業中）

### 目標
Decap CMS（`/admin`）でブログ記事を管理できるようにする。
更新者：オーナー＋スタッフ複数名。全員 GitHub アカウントが必要。

### 現在の問題
- Decap CMS の GitHub PKCE 認証でログインできない
- 原因: GitHub OAuth App のコールバック URL がおそらく間違っている

### 修正すべきこと

**Step 1: GitHub OAuth App の URL を修正**
- GitHub → Settings → Developer settings → OAuth Apps
- Client ID: `Ov23liCY31EnaQCgwLx9` のアプリを開く
- 以下に修正する：
  - Homepage URL: `https://ropponmatsu-goen.com`
  - Authorization callback URL: `https://ropponmatsu-goen.com/admin/`

**Step 2: スタッフを GitHub リポジトリに招待**
- リポジトリ → Settings → Collaborators → Add people
- ブログ更新するスタッフ全員を Collaborator として招待

### admin/ の構成
- `admin/index.html`: Decap CMS 本体（PKCE 設定済み）
- `admin/config.yml`: CMS 設定（こちらは参考用、index.html の JS 設定が優先）
