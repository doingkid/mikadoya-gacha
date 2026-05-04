# ミカドヤ 食べ物ガチャ

静岡県三島市の居酒屋「ミカドヤ」の **食べ物メニュー** から、予算（2000円 / 3000円）以内に収まる組み合わせをガチャで生成する非公式ファンサイト。  
※ドリンク・お通し代は予算に含みません。

公開URL: https://doingkid.github.io/mikadoya-gacha/

## v1 スコープ

- 対象: 食べ物のみ（ドリンクは除外）
- 予算: 2000円 / 3000円 の二択

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
├── index.html          # HTML + CSS + JS を1ファイルに内包
├── menu.json           # 本番メニュー（後で差し込む）
├── menu.sample.json    # 動作確認用ダミー（menu.json がない場合の自動フォールバック）
└── README.md
```

`menu.json` が存在しない場合は自動で `menu.sample.json` を読み込みます。

## 注意事項

- HTML 内の参照はすべて相対パス（`./menu.json`）にする。`/menu.json` は GitHub Pages のサブパス配信で壊れる。
- メニュー情報は店舗の所有物。掲載前に店主の許諾を確認すること。
