# GitHub Personal Access Token (PAT) 設定ガイド

## Personal Access Tokenとは？

Personal Access Token（PAT）は、GitHub APIやGitコマンドで認証するために使うパスワードのようなものです。アプリやサービスがあなたの代わりにGitHubにアクセスする際に使用します。

## なぜ必要？

- パスワードの代わりに使う安全な認証方法
- 特定の権限だけを付与できる（セキュリティが高い）
- 不要になったら削除できる
- 有効期限を設定できる

## 作成手順（詳細）

### 1. GitHubにログイン
https://github.com にログインしてください。

### 2. 設定ページにアクセス
以下のいずれかの方法でアクセス：
- 右上のプロフィール画像をクリック → **Settings**
- 直接URL: https://github.com/settings/profile

### 3. Developer settings に移動
左側のメニューから、一番下の **Developer settings** をクリック

### 4. Personal access tokens を選択
- **Tokens (classic)** をクリック
- または直接URL: https://github.com/settings/tokens

### 5. 新しいトークンを生成
- **Generate new token** ボタンをクリック
- **Generate new token (classic)** を選択

### 6. トークンの設定

#### Note（メモ）
トークンの用途を書く（例：`Google AI Studio 画像アップロード`）

#### Expiration（有効期限）
- **30 days**（30日間）
- **60 days**（60日間）
- **90 days**（90日間）
- **Custom**（カスタム日数）
- **No expiration**（無期限）⚠️ セキュリティ上、推奨されない

#### Select scopes（権限の選択）
必要な権限にチェックを入れる：

**このプロジェクトに必要な権限：**
- ✅ **`repo`** （すべてのリポジトリへのフルアクセス）
  - 公開リポジトリのみの場合は **`public_repo`** でOK
  - プライベートリポジトリも使う場合は **`repo`** が必要

**その他のよく使う権限：**
- `workflow` - GitHub Actionsのワークフローを管理
- `write:packages` - GitHub Packagesにアップロード
- `read:org` - 組織情報の読み取り

### 7. トークンを生成
- ページ下部の **Generate token** ボタンをクリック

### 8. ⚠️ 重要：トークンをコピー
**この画面を離れると、もう一度トークンを確認できません！**

表示されたトークン（`ghp_` で始まる文字列）をコピーして、安全な場所に保存してください。

例：
```
ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## このプロジェクト（manga_sozai）の場合

### 必要な権限
- **`repo`** または **`public_repo`**
  - リポジトリが公開（Public）なら `public_repo` でOK
  - プライベート（Private）なら `repo` が必要

### 使用目的
- `output/` フォルダーに画像をアップロード
- 自動コミット・プッシュ

## セキュリティのベストプラクティス

### ✅ 推奨事項
1. **最小限の権限を付与** - 必要な権限だけを選ぶ
2. **有効期限を設定** - 長期間使わないなら期限を短く
3. **定期的に確認** - 不要なトークンは削除
4. **トークンは秘密に** - 他人と共有しない、Gitにコミットしない

### ❌ やってはいけないこと
- トークンをGitリポジトリにコミットする
- トークンを公開の場所に貼り付ける
- 無期限のトークンを作りっぱなしにする
- 必要以上の権限を付与する

## トークンの確認・管理

### トークン一覧の確認
https://github.com/settings/tokens で確認できます

### トークンの削除
- 一覧から該当トークンを探す
- **Revoke** ボタンをクリック

### トークンの再生成
- 古いトークンを削除
- 新しいトークンを生成
- 使用しているサービスで更新

## トラブルシューティング

### エラー: "Bad credentials"
- トークンが正しくコピーされていない
- トークンの有効期限が切れている
- 必要な権限が付与されていない

### エラー: "Resource not accessible by integration"
- 権限が不足している
- `repo` 権限が必要なのに `public_repo` しか付与していない

### エラー: "Token has expired"
- トークンの有効期限が切れた
- 新しいトークンを生成して更新

## まとめ

1. **GitHub Settings** → **Developer settings** → **Tokens (classic)**
2. **Generate new token (classic)**
3. **Note**: 用途を記入（例：`Google AI Studio 画像アップロード`）
4. **Expiration**: 適切な期限を設定
5. **Select scopes**: ✅ `repo` または `public_repo` にチェック
6. **Generate token** をクリック
7. **トークンをコピー**（`ghp_` で始まる文字列）
8. Google AI Studioなどのサービスに貼り付ける

## 参考リンク

- GitHub公式ドキュメント: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
- トークン管理ページ: https://github.com/settings/tokens

