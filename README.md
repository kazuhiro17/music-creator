# Music Creator

AIを使用して音楽を生成・管理するWebアプリケーションです。React、TypeScript、Viteを使用して構築されています。

## 機能

- 🎵 AIによる音楽生成
- 🎨 モダンなUIデザイン（Tailwind CSS）
- 💾 生成した音楽の保存機能
- 🎧 音楽プレビュー機能
- 📱 レスポンシブデザイン

## 技術スタック

- **React 19** - UIライブラリ
- **TypeScript** - 型安全性
- **Vite** - ビルドツール
- **Tailwind CSS** - スタイリング
- **shadcn/ui** - UIコンポーネントライブラリ（Radix UIベース）
- **React Router** - ルーティング
- **Axios** - HTTPクライアント
- **Radix UI** - アクセシブルなUIプリミティブ（shadcn/uiの基盤）
- **Lucide React** - アイコンライブラリ

## セットアップ

### 必要な環境

- Node.js 18以上
- npm または yarn

### インストール

1. リポジトリをクローンします：

```bash
git clone <repository-url>
cd music-creator
```

2. 依存関係をインストールします：

```bash
npm install
```

3. 環境変数を設定します：

プロジェクトのルートに `.env` ファイルを作成し、以下の環境変数を設定してください：

```env
VITE_LOUDLY_API_KEY=your_api_key_here
```

4. 開発サーバーを起動します：

```bash
npm run dev
```

ブラウザで `http://localhost:5173` を開いてアプリケーションを確認できます。

## スクリプト

- `npm run dev` - 開発サーバーを起動
- `npm run build` - 本番用ビルドを作成
- `npm run preview` - ビルドしたアプリケーションをプレビュー
- `npm run lint` - ESLintでコードをチェック

## プロジェクト構造

```
music-creator/
├── src/
│   ├── components/     # 再利用可能なコンポーネント
│   │   └── ui/         # shadcn/uiコンポーネント
│   ├── App.tsx         # メインアプリケーション
│   ├── CreatePage.tsx  # 音楽生成ページ
│   └── main.tsx        # エントリーポイント
├── public/             # 静的ファイル
├── components.json     # shadcn/ui設定ファイル
├── .env               # 環境変数（.gitignoreに含まれています）
└── package.json       # 依存関係とスクリプト
```

## shadcn/uiについて

このプロジェクトでは[shadcn/ui](https://ui.shadcn.com/)を使用してUIコンポーネントを構築しています。shadcn/uiは以下の特徴があります：

- **コピー&ペースト方式**: コンポーネントがプロジェクトに直接コピーされるため、完全にカスタマイズ可能
- **Radix UIベース**: アクセシビリティに優れたプリミティブコンポーネントを使用
- **Tailwind CSS**: ユーティリティファーストのCSSフレームワークでスタイリング
- **TypeScript**: 完全な型安全性を提供

### 使用しているshadcn/uiコンポーネント

- `Button` - ボタンコンポーネント
- `Card` - カードコンポーネント
- `Input` - 入力フィールド
- `Textarea` - テキストエリア
- `Label` - ラベルコンポーネント
- `Select` - セレクトボックス

### 新しいコンポーネントを追加する場合

shadcn/uiのCLIを使用して新しいコンポーネントを追加できます：

```bash
npx shadcn@latest add [component-name]
```

例：
```bash
npx shadcn@latest add dialog
npx shadcn@latest add toast
```

詳細は[shadcn/ui公式ドキュメント](https://ui.shadcn.com/docs)を参照してください。

## 使用方法

1. **音楽を生成する**
   - 「Generate Music」ページに移動
   - 楽曲タイトル、ジャンル、音楽の説明を入力
   - 「Generate Music」ボタンをクリック
   - 生成が完了するまで待機（数秒かかる場合があります）

2. **音楽を保存する**
   - 生成された音楽をプレビュー
   - 「Save to Collection」ボタンをクリック
   - 保存された音楽はホームページで確認できます

## React Compiler

このテンプレートでは、開発とビルドのパフォーマンスへの影響を考慮して、React Compilerは有効化されていません。有効化する場合は、[公式ドキュメント](https://react.dev/learn/react-compiler/installation)を参照してください。

## ESLint設定の拡張

本番アプリケーションを開発する場合は、型を意識したlintルールを有効にするために設定を更新することをお勧めします：

```js
export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // 他の設定...

      // tseslint.configs.recommendedを削除し、以下に置き換え
      tseslint.configs.recommendedTypeChecked,
      // または、より厳格なルールを使用する場合
      tseslint.configs.strictTypeChecked,
      // オプション：スタイルルールを追加する場合
      tseslint.configs.stylisticTypeChecked,

      // 他の設定...
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // その他のオプション...
    },
  },
])
```

React固有のlintルールについては、[eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) と [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) をインストールすることもできます：

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // 他の設定...
      // React用のlintルールを有効化
      reactX.configs['recommended-typescript'],
      // React DOM用のlintルールを有効化
      reactDom.configs.recommended,
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // その他のオプション...
    },
  },
])
```

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。
