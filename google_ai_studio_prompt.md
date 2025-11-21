# Google AI Studio プロンプト案

## パターン1: 画像生成 + GitHubアップロード指示（推奨）

```
以下の条件で漫画の画像を生成してください：

1. 画像生成の要件：
   [ここに具体的な画像生成の指示を書く]
   例：「教室のシーンで、教師と生徒が対話している場面を白黒の漫画スタイルで描いてください」

2. 生成後の処理：
   生成した画像を以下のGitHubリポジトリのoutputフォルダーに自動でアップロードしてください。
   
   - リポジトリURL: https://github.com/zawasasa/manga_sozai.git
   - ブランチ: master
   - 保存先フォルダー: output/
   - ファイル名: manga-[タイムスタンプ].png（例: manga-20241121-112700.png）
   
3. アップロード方法：
   生成した画像をbase64エンコードで返し、以下の情報も一緒に提供してください：
   - 画像データ（base64）
   - ファイル名
   - コミットメッセージ
   
   その後、GitHub APIまたはGitコマンドを使用してリポジトリにアップロードしてください。
```

## パターン2: シンプルな指示（画像生成のみ）

```
漫画の画像を生成してください。
生成した画像は、以下のGitHubリポジトリのoutputフォルダーに保存してください：

リポジトリ: https://github.com/zawasasa/manga_sozai
フォルダー: output/
ファイル名: 自動生成（タイムスタンプ付き）

生成後、画像データとファイル名を返してください。
```

## パターン3: 詳細な技術仕様付き

```
【画像生成タスク】

1. 画像生成：
   [具体的な画像生成の指示]

2. GitHubアップロード仕様：
   - リポジトリ: zawasasa/manga_sozai
   - ブランチ: master
   - パス: output/manga-[YYYYMMDD-HHMMSS].png
   - コミットメッセージ: "Add manga output: [ファイル名]"

3. 出力形式：
   以下のJSON形式で返してください：
   {
     "image_base64": "[base64エンコードされた画像データ]",
     "filename": "manga-20241121-112700.png",
     "commit_message": "Add manga output: manga-20241121-112700.png",
     "repository_url": "https://github.com/zawasasa/manga_sozai.git"
   }

4. アップロード処理：
   返されたデータを使用して、GitHub API（PUT /repos/{owner}/{repo}/contents/{path}）で
   ファイルをアップロードしてください。
   認証にはPersonal Access Tokenが必要です。
```

## パターン4: 実用的な統合プロンプト

```
画像を生成し、GitHubリポジトリに自動アップロードするワークフローを実行してください。

【ステップ1: 画像生成】
[ここに画像生成の具体的な指示]

【ステップ2: GitHubアップロード】
生成した画像を以下の設定でGitHubにアップロード：

- リポジトリ: https://github.com/zawasasa/manga_sozai
- ブランチ: master  
- 保存先: output/manga-[現在の日時].png
- コミットメッセージ: "Add manga output: [ファイル名]"

【必要な情報】
- GitHub Personal Access Token（repo権限が必要）
- または、ローカルでGitコマンドを実行する場合は、リポジトリのクローンが必要

【出力】
1. 生成した画像のプレビュー
2. アップロード先のGitHub URL
3. エラーがあればエラーメッセージ
```

## 注意事項

⚠️ **重要**: Google AI Studio自体はGitHubに直接アップロードする機能を持っていない可能性があります。

**推奨される実装方法：**

1. **方法A: スクリプトで自動化**
   - Google AI Studioで画像を生成
   - 生成した画像をbase64で取得
   - ローカルのoutputフォルダーに保存
   - Gitコマンドで自動コミット・プッシュ

2. **方法B: GitHub APIを使用**
   - 生成した画像をbase64で取得
   - GitHub API（Contents API）で直接アップロード
   - Personal Access Tokenが必要

3. **方法C: 統合スクリプト**
   - Pythonスクリプトなどで、Google AI Studio API + GitHub APIを統合
   - 画像生成 → 自動アップロードのワークフローを構築

## 実際に使用する場合の例

```
教室のシーンで、教師と生徒が対話している場面を白黒の漫画スタイルで描いてください。
生成した画像は、https://github.com/zawasasa/manga_sozai の output フォルダーに
「manga-[現在の日時].png」という名前で保存してください。
画像データはbase64エンコードで返し、GitHub APIを使用してアップロードしてください。
```

