# Master System (Backend)

`br-master` は、Buckshot Roulette システムの中核となるバックエンドサーバーです。Python と FastAPI で構築されており、ゲームの進行管理、クライアントへの状態提供、ハードウェアとの通信を担います。

## ディレクトリ構成

```
br-master/
├── core/                # ゲームロジックの中核
│   ├── game.py          # Gameクラス（1ゲームの状態管理）
│   ├── game_manager.py  # GameManagerクラス（複数ゲームの管理）
│   ├── player.py        # Playerクラス
│   ├── shotgun.py       # Shotgunクラス（弾薬管理）
│   ├── items.py         # アイテムの効果定義
│   └── logic.py         # 補助ロジック
├── hardware/            # ハードウェア通信
│   ├── interface.py     # ハードウェアインターフェース（抽象化層）
│   └── comms.py         # 通信実装（TCP/Serial等）
├── static/              # 静的ファイル（管理画面用CSS/JS）
├── templates/           # HTMLテンプレート（管理画面用）
├── web_server.py        # FastAPIサーバーエントリーポイント
├── config.json          # ゲーム設定
└── requirements.txt     # 依存ライブラリ
```

## セットアップと実行

推奨環境: Python 3.10+ (uv 推奨)

```bash
# 依存関係のインストール
uv pip install -r requirements.txt

# サーバーの起動
uv run python web_server.py
```

サーバーは `http://localhost:8000` で起動します。

## 主な機能

### 1. ゲーム管理 (Game Manager)
`core/game_manager.py` で実装されています。
- 複数のゲームセッションを `game_id` で管理。
- ゲームの作成、取得、削除を行います。

### 2. ゲームロジック (Game Core)
`core/game.py` が中心となります。
- **ラウンド進行**: 弾の装填、ターン管理、勝敗判定。
- **アイテム処理**: アイテムの使用と効果の適用。
- **状態管理**: ライフ、弾数、アイテム所持状況。

### 3. ハードウェア連携
`hardware/interface.py` を通じて物理デバイスと通信します。
- 現在は開発用にモック（シミュレーション）動作が含まれています。
- 本番環境では TCP または Serial 通信を用いて ESP32 とデータをやり取りします。

## 設定 (config.json)

ゲームバランスは `config.json` で調整可能です。

- `game_rules`: 初期ライフ、最大ライフなど。
- `shell_counts_by_round`: ラウンドごとの実弾・空砲の数。
- `item_distribution`: アイテムの出現確率。
