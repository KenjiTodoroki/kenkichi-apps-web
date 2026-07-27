# kenkichi-apps-web

けん吉アプリ（Kenkichi Apps）の事業者情報サイト。静的ファイルのみで構成。

## ファイル構成

```
/
├── index.html          # メインページ
├── privacy.html        # プライバシーポリシー（本文は要貼り付け）
├── assets/
│   ├── style.css       # スタイルシート
│   ├── app-icon.png    # アプリアイコン（要配置）
│   ├── x-avatar.png    # X アカウントのアバター画像（要配置）
│   ├── other-avatar.png # その他アカウントのアバター画像（要配置）
│   ├── favicon.ico     # ファビコン（要配置）
│   └── favicon.svg     # SVG ファビコン（要配置）
└── README.md
```

## ローカル確認

ブラウザで直接 index.html を開くだけで確認できる。
Python が入っている場合は簡易サーバーが便利：

```bash
cd kenkichi-apps-web
python3 -m http.server 8080
# → http://localhost:8080 で確認
```

## Cloudflare Pages へのデプロイ

### A. GitHub 連携（推奨・自動デプロイ）

1. このディレクトリを GitHub リポジトリ（Private）に push する
2. [Cloudflare Dashboard](https://dash.cloudflare.com/) → Workers & Pages → **Create application** → **Pages** → **Connect to Git**
3. リポジトリを選択し、以下を設定：
   - **Framework preset**: None
   - **Build command**: （空欄）
   - **Build output directory**: `/`（ルート）
4. **Save and Deploy** → 初回デプロイ完了後、カスタムドメイン `kenkichi-apps.com` を設定

以後、main ブランチに push するたびに自動デプロイされる。

### B. wrangler CLI（コマンドライン）

```bash
# wrangler のインストール（未導入の場合）
npm install -g wrangler

# Cloudflare にログイン
wrangler login

# デプロイ（プロジェクト名は初回に設定）
wrangler pages deploy . --project-name kenkichi-apps
```

### C. ダイレクトアップロード（ブラウザ）

1. Cloudflare Dashboard → Workers & Pages → **Create application** → **Pages** → **Upload assets**
2. プロジェクト名を設定して `index.html` など必要ファイルをまとめてアップロード
3. デプロイ完了後にカスタムドメインを設定

## カスタムドメイン設定（共通）

1. Cloudflare で `kenkichi-apps.com` のゾーンを追加（DNS 管理を Cloudflare に移管）
2. Pages のプロジェクト → **Custom domains** → `kenkichi-apps.com` を追加
3. 自動で SSL/TLS 証明書が発行される
