# 講義資料作成プロンプト

## 1
全4回の学生向けのWebアプリケーション開発の講義を行なっています。
1~3回目の講義は終わっており、過去3回の講義資料は `/docs/learning-phase-1`, `/docs/learning-phase-2`, `/docs/learning-phase-3` の各ディレクトリに格納しています。
あなたにはこれから、一緒に4回目の講義資料を作成してもらいたいです。

4回目の講義は時間が6時間で、テーマは「AIを組み込んだアプリ開発」です。

進め方は以下のように考えています。
1. ベースとなるペット管理アプリのコードを配布し、その説明 (このアプリを作成するためのプロンプトは用意したので、後ほどそちらを指示して作成してもらいます)
2. ベースのアプリに対してAIを組み込めるAPI(例: Google Gemini API, Hugging Face Inference API, Cloud Vision APIなど)を使って、AI機能を追加していく
3. 演習(好きなAI APIを使って2時間程度で自由に開発をしてもらう)

上記の進め方の「2」の中でAIを組み込んで追加したい機能は以下です。
1. ペット登録時にペット画像から犬種/猫種を自動識別する機能 (Google Gemini APIを利用する想定)
2. ペットのヘルスケアケアアドバイザーチャットボット
3. 選択したペット2匹を両親とした時の子供のイメージ画像生成機能(画像生成AIのAPIを利用する想定)

ここまでの内容に関して、不明点や追加で必要な情報があれば教えてください。
もしなければ、次は用意したプロンプトでベースとなるペット管理アプリのコードを生成してもらおうと思います。

## 2
以下のプロンプトに従って、 `/apps/learning-phase-4` 配下に pet-management-appを作成してください。
```
あなたはフルスタックエンジニアAIとして、
Next.js（App Router）+ TypeScript + Tailwind CSS + shadcn-ui を使用した
「ペット管理アプリ（Pet Management App）」を実装してください。

## 🎯 アプリ概要
ユーザーがログインし、自分のペットの情報を管理できる CRUD Web アプリを作成してください。

必要な画面：
1. サインアップ
2. ログイン・ログアウト
3. ペット一覧（My Pets）
4. ペット登録（Add New Pet）
5. ペット詳細（Pet Detail）
6. ペット編集（Edit Pet）

## 🗂 機能仕様（必須）
- Supabase Auth を使用したログイン認証
- ペット情報の CRUD（Create / Read / Update / Delete）
- 画像アップロード（Supabase Storage）
- Route Handler（app/api/...）を用いた API 実装
- Prisma ORM による DB アクセス
- ログインユーザーごとにペットが紐づく
- UI は Tailwind CSS と shadcn-ui コンポーネントを使用すること

## 🐾 ペットデータモデル（Prisma）
model Pet {
  id        String   @id @default(uuid())
  ownerId   String
  name      String
  category  String
  breed     String?
  birthday  DateTime?
  gender    String?
  imageUrl  String?
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

## 📦 技術スタック（必須）
- Next.js 14（App Router）
- TypeScript
- Tailwind CSS
- shadcn-ui
- Prisma
- Supabase（DB + Auth + Storage）
- Vercel で動作可能な構成
- ESLint / Prettier セットアップ

## 🎨 UI / コンポーネント要件
- 全体のレイアウトと余白・タイポグラフィは Tailwind CSS で調整すること
- ボタン、カード、ダイアログ、フォーム、インプットなどの UI 要素は shadcn-ui コンポーネントを利用すること
  - 例: Button, Card, Input, Label, Form, Avatar など
- shadcn のセットアップ（`npx shadcn-ui@latest init` 等）と、必要コンポーネントの追加手順も明記すること

各画面の要素：
### ● ペット一覧（My Pets）
- Pet カードを shadcn-ui の Card コンポーネントで表示
- カード内に：
  - 名前
  - 種類（Cat / Dog 等）
  - アイコン画像（Avatar コンポーネントなど）
- 「Add New Pet」ボタン（Button コンポーネント）
- ログイン中ユーザーのペットのみ一覧表示

### ● 新規登録フォーム（Add New Pet）
- shadcn-ui の Form コンポーネントを使ったバリデーション付きフォーム
- 入力項目：
  - Pet Name（必須）
  - Category（Dog / Cat などのセレクトボックス）
  - Breed
  - Birthday（日付入力）
  - Gender（ラジオボタンまたはセレクト）
  - Photo Upload（画像アップロード）
- Create / Cancel ボタン（Button コンポーネント）

### ● ペット詳細（Pet Detail）
- Card コンポーネントでペットの詳細を表示
- 表示項目：
  - 名前
  - 種類
  - 性別
  - 年齢（birthday から自動計算）
  - 写真
- Edit / Delete ボタン（Button コンポーネント）
- Delete 時は shadcn-ui の AlertDialog などで確認ダイアログを表示

### ● ペット編集（Edit Pet）
- 新規登録と同じフォーム構成
- 既存値を初期値として表示
- Save ボタンで更新、Cancel で戻る

## 🔐 認証・権限
- Supabase Auth でメール＋パスワード認証
- ログインしていない場合はペット管理画面にアクセスできないようにする
- API では `ownerId` とログイン中ユーザーを照合し、他人のペットを操作できないようにする

## 🛠 実装してほしい内容
次の内容をすべて生成してください：

1. Next.js プロジェクトのディレクトリ構成
2. Tailwind CSS と shadcn-ui のセットアップ手順と設定ファイル
3. Prisma schema の定義とマイグレーション手順
4. Supabase のセットアップ手順（Auth / Storage / .env 設定）
5. ペット CRUD 用 Route Handler（app/api/pets/...）
6. ペット一覧／追加／詳細／編集ページ（app/my-pets/... など）の実装
7. サインアップ / ログイン / ログアウト UI と処理
8. 型定義、エラーハンドリング、ローディング状態の処理
9. Vercel でデプロイする際の注意点や環境変数の設定方法

## 📁 ファイル生成ポリシー
- 必要なファイルは Claude Code の「Insert」機能で、正しいディレクトリに生成してください。
- 一度にすべて生成せず、以下の順番で進めてください：
  1. ディレクトリ構成と依存パッケージ一覧
  2. Tailwind + shadcn-ui のセットアップファイル
  3. Prisma schema と設定
  4. Supabase 連携部分
  5. ペット CRUD API
  6. 各ページコンポーネント

## 🚀 出力形式
- それぞれのステップで、生成・更新すべきファイル名を明示しつつ、コードブロックで完全なコードを提示してください。
- 途中で前提が足りない場合は、必要な設定値や前提条件を質問した上で続行してください。

以上を踏まえて、まずは
「プロジェクト全体のディレクトリ構成・使用ライブラリ・インストールコマンドの提案」
から開始してください。
```

## 3 