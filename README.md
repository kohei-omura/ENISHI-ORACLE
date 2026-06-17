# 企業縁占 — ENISHI ORACLE

占術15種 × 現実キャリアで、企業と個人の相性を 0〜100 点で鑑定する PWA。
総合相性が **85点以上** になると、その企業向けの転職戦略が解放される。

## 構成
```
enishi/
├─ index.html      … アプリ本体（バニラJS・ビルド不要）
├─ manifest.json   … PWA設定
├─ sw.js           … オフライン用 Service Worker
├─ icons/          … アイコン一式（縁の御朱印）
└─ README.md
```

## GitHub へアップロード → GitHub Pages で公開

### A. ブラウザだけで（一番簡単）
1. GitHub で新規リポジトリ作成（例：`enishi-oracle`、Public）。
2. このフォルダの中身（`index.html`・`manifest.json`・`sw.js`・`icons/`）をドラッグ＆ドロップでアップロード → Commit。
3. リポジトリの **Settings → Pages** へ。
4. **Source** を `Deploy from a branch`、**Branch** を `main` / `/(root)` にして Save。
5. 1〜2分後、`https://<ユーザー名>.github.io/enishi-oracle/` で公開。

### B. コマンドで
```bash
cd enishi
git init
git add .
git commit -m "企業縁占 PWA"
git branch -M main
git remote add origin https://github.com/<ユーザー名>/enishi-oracle.git
git push -u origin main
# その後、Settings → Pages で main / root を有効化
```

## APIキー（必須）
このアプリは Anthropic の API を直接呼びます。初回に **設定（⚙︎）** でキーを入力してください。
- 取得：https://console.anthropic.com → API Keys
- 保存先：**この端末のブラウザ内（localStorage）のみ**。サーバーには保存されません。
- 送信先は `api.anthropic.com` のみ。
- 注意：GitHub のコードに直接キーを書かないこと（公開リポジトリでは漏洩します）。アプリの設定欄に入れる方式なので、コードに書く必要はありません。

> モデルは既定で `claude-sonnet-4-6`。設定欄で変更可。

## iPhone でホーム画面に追加（PWA化）
1. Safari で公開URLを開く。
2. 共有ボタン → **「ホーム画面に追加」**。
3. ホームの「企業縁占」アイコンから、全画面のアプリとして起動。

## 仕組み（概要）
- 企業情報：Anthropic API の **web_search** ツールで最新情報を取得。
- 占術相性：西洋占星術〜血液型まで15手法を統合して採点（手法別内訳つき）。
- 現実相性：候補者の経歴（Apple販売8年・IT転職検討 等）に対する業界成長性／スキル適合／年収余地／キャリアパス／安定性。
- 総合 = 占術 × 0.4 ＋ 現実 × 0.6（四捨五入）。
- 鑑定履歴は端末内に最大12件保存。

占術はエンタメ、現実相性は判断材料としてご活用ください。
