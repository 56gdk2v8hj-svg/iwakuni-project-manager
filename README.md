# 岩国シティFC 案件管理Webアプリ

## できること
- 案件（プロジェクト）の追加・編集
- グループとタスクの追加・編集・削除
- 担当者（福井・上田・山本・川上）の割り当て
- ステータス・期限・区分の管理
- 案件別の進捗率表示、担当者フィルター、タスク検索
- Supabaseによる4人共有・リアルタイム同期
- スマートフォン／PC対応

## 共有版を公開する手順

### 1. Supabaseを用意
1. https://supabase.com/ でアカウントを作成し、New project。
2. Dashboard の SQL Editor を開き、`supabase/schema.sql` の内容を貼り付けて実行。
3. Authentication > Settings で新規ユーザー登録（Allow new users to sign up）を無効にする。
4. Authentication > Users から福井・上田・山本・川上の4人をメールアドレスで招待する。
5. Project Settings > API から Project URL と anon / publishable key を確認する。

※招待する4人のメールアドレスは管理者が確認して入力してください。サービスロールキーは絶対にブラウザへ設定しないでください。

### 2. 環境変数を設定
`.env.example` を `.env` にコピーし、次を設定：
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

### 3. ローカルで確認
Node.js 20以上を用意し、プロジェクトフォルダで実行：
```bash
npm install
npm run dev
```

### 4. Web公開
1. GitHubにこのプロジェクトを新規リポジトリとしてアップロード。
2. https://vercel.com/ でGitHubリポジトリをImport。
3. VercelのEnvironment Variablesに `.env` と同じ2項目を設定。
4. Deploy。発行されたURLを4人に共有。
5. Supabase Authentication > URL Configuration の Site URL と Redirect URLs に公開URLを登録。

## 注意
- `.env` はGitHubへアップロードしないでください（`.gitignore` 推奨）。
- 共有データはSupabaseに保存されます。ローカルプレビュー時のデータは共有されません。
- このスターターでは「招待済みの認証ユーザー全員」が同じワークスペースを編集できます。4人以外を招待しない運用にしてください。
- 現状のメンバー名はタスク担当欄で選択します。ログインユーザー表示はメールアドレスまたはSupabaseのユーザーメタデータ名です。
