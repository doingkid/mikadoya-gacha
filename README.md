# ミカドガチャ

静岡県三島市の居酒屋「ミカドヤ」の食べ物メニューから、予算以内の組み合わせをガチャで生成する非公式ファンサイト。  
※ドリンク・お通し代は予算に含みません。

公開URL: https://doingkid.github.io/mikadoya-gacha/

## 機能

- **予算ガチャ**: 2,000円 / 3,000円 の2ボタン。タップ1つで即実行
- **フィルター**: ⚡ スピードメニュー（すぐ出る品のみ）/ 🥗 ヘルシーメニュー（300kcal以下）
- **ストーリーズシェア**: 結果を1080×1920のPNG画像にしてネイティブシェアシート経由で投稿（非対応環境はPNGダウンロード）
- **メニュー一覧**: 食べ物・ドリンク全品をkcal付きで表示（`menu.html`）

## ローカル開発

ビルド不要。任意の静的サーバで配信して開くだけ。

```bash
python3 -m http.server 8000
# → http://localhost:8000/ を開く
```

`file://` で直接開くと `fetch('./menu.json')` が CORS で動かないので、必ず HTTP サーバ経由で開くこと。

## メニュー更新

`menu.json` を編集して commit → push するだけ。  
GitHub の Web エディタ（リポジトリで `.` キーを押す or `menu.json` を開いて鉛筆アイコン）から直接編集してもOK。

### menu.json のアイテム構造

```json
{ 
  "id": "a01",
  "name": "品名",
  "category": "agemono",
  "price": 500,
  "available": true,
  "tags": [],
  "kcal": 430,
  "speed": "medium"
}
```

| フィールド | 型 | 説明 |
|---|---|---|
| `kcal` | number | カロリー概算（ドリンクも含む全品に設定） |
| `speed` | `"fast"` / `"medium"` / `"slow"` | 提供速度。食べ物のみ設定（ドリンクは不要） |
| `available` | boolean | `false` にすると非表示・ガチャ対象外 |

ドリンクは `kind: "drink"` のカテゴリに属するためガチャ対象外。`kcal` は参考表示用として保持。

## デプロイ（GitHub Pages）

初回のみ:

1. GitHub リポジトリの **Settings → Pages** を開く。
2. **Source**: `Deploy from a branch` を選択。
3. **Branch**: `main` / `/(root)` を選択して **Save**。
4. 数十秒待つと `https://doingkid.github.io/mikadoya-gacha/` で公開される。

以降は `main` への push で自動再デプロイ。

## ファイル構成

```
mikadoya-gacha/
├── index.html        # ガチャ画面（HTML + CSS + JS を1ファイルに内包）
├── menu.html         # メニュー一覧（食べ物・ドリンク全品、kcal付き）
├── menu.json         # 本番メニューデータ
├── kanban.png        # 看板画像（背景透過PNG）
└── README.md
```

## 注意事項

- HTML 内の参照はすべて相対パス（`./menu.json`）にする。`/menu.json` は GitHub Pages のサブパス配信で壊れる。
- メニュー情報は店舗の所有物。掲載前に店主の許諾を確認すること。
