# Client System (Frontend)

`br-client` は、プレイヤーがゲーム状況を確認するための Web アプリケーションです。React と TypeScript で構築されており、Vite を使用してビルドされます。

## 技術スタック

- **フレームワーク**: React
- **言語**: TypeScript
- **ビルドツール**: Vite
- **通信**: Axios (HTTP Polling)
- **スタイル**: CSS Modules / Vanilla CSS

## ディレクトリ構成

```
br-client/
├── src/
│   ├── components/      # UIコンポーネント (PlayerCard, GameStatus等)
│   ├── hooks/           # カスタムフック (useGameState等)
│   ├── api.ts           # API通信ロジック
│   ├── App.tsx          # メインアプリケーション
│   └── main.tsx         # エントリーポイント
├── public/              # 静的アセット
├── index.html           # HTMLエントリーポイント
└── vite.config.ts       # Vite設定
```

## セットアップと実行

推奨環境: Node.js 18+

```bash
# 依存関係のインストール
pnpm install

# 開発サーバーの起動
pnpm dev
```

ブラウザで `http://localhost:5173` にアクセスします。
特定のゲームに参加する場合は、クエリパラメータを使用します: `http://localhost:5173/?game_id=<GAME_ID>`

## 通信仕様

クライアントは定期的に Master サーバーの API (`/api/game/{game_id}/state`) をポーリングし、最新のゲーム状態を取得して画面を更新します。
リアルタイム通信（WebSocket）ではなく、ポーリング方式を採用しています（現状の実装）。

## 主なコンポーネント

- **App.tsx**: ルーティングと全体レイアウト。
- **GameStatus**: 現在のラウンド、ターン、弾数（既知の場合）の表示。
- **PlayerCard**: 各プレイヤーのライフ、アイテム、ステータスの表示。
