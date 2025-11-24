# Shotgun System (Hardware)

`br-shotgun` は、ESP32 マイコンを使用した物理的なショットガンデバイスのファームウェアです。PlatformIO で開発されています。

## ハードウェア構成

- **マイコン**: Seeed XIAO ESP32C3
- **通信**: Wi-Fi (TCP Client/Server)
- **センサー/アクチュエータ**:
    - **トリガー**: マイクロスイッチ
    - **IMU (9軸センサー)**: 銃口の向き検知 (MPU9250等)
    - **フィードバック**: 振動モーター、スピーカー、LED

## ディレクトリ構成

```
br-shotgun/
├── src/
│   └── main.cpp         # ファームウェアのメインロジック
├── include/
│   └── config.h         # Wi-Fi設定 (要作成)
├── lib/                 # ライブラリ
├── platformio.ini       # PlatformIO設定
└── README.md            # セットアップガイド
```

## セットアップ

1. **PlatformIO のインストール**: VSCode 拡張機能を使用します。
2. **設定**: `include/config.h` を作成し、Wi-Fi SSID とパスワードを設定します。
3. **書き込み**: USB で ESP32 を接続し、Upload します。

## 通信プロトコル

ESP32 は TCP サーバー (Port 8080) として動作し、Master からのコマンドを待ち受けます。
また、トリガーやセンサーのイベントを Master に送信します。

### 受信コマンド (Master -> Shotgun)

- `FIRE:<shellType>`: 発砲指示。
    - `LIVE`: 実弾のエフェクト（音、振動、LED赤）
    - `BLANK`: 空砲のエフェクト（音、振動小、LED青）
    - 例: `FIRE:LIVE`

### 送信データ (Shotgun -> Master)

(現状の実装予定)
- トリガー検知: `TRIGGER`
- 向き検知: `AIM:<TARGET>`
