# MPA Sample (GitHub Pages 用)

このフォルダは、埋め込み版ガイドツールの動作をMPA(複数HTML)で検証するための最小サンプルです。

## 手順（ローカル確認）

1. バンドルをビルド
   - `pnpm -C ux-canvas-extension-viewer build:vite`
   - 生成物: `ux-canvas-extension-viewer/dist/ux-canvas-viewer.iife.js`
2. バンドルを配置
   - `cp ux-canvas-extension-viewer/dist/ux-canvas-viewer.iife.js mpa-sample/assets/`
3. サーバAPIベースURLを設定（必要に応じて各HTML内の `__UXC_API_BASE__` を変更）
   - デフォルト: `http://localhost:8080`
4. ローカルHTTPサーバで配信
   - `cd mpa-sample && python3 -m http.server 8081`
   - `http://localhost:8081/index.html` へアクセス

## GitHub Pages で公開

1. 新規リポジトリ作成（例: `uxc-mpa-sample`）
2. ルートにこの `mpa-sample/` フォルダを配置し、以下を実行
   ```bash
   git init
   git add .
   git commit -m "Add MPA sample"
   git branch -M main
   git remote add origin git@github.com:<YOUR_GH_USERNAME>/uxc-mpa-sample.git
   git push -u origin main
   ```
3. GitHub リポジトリ Settings → Pages
   - Source: `Deploy from a branch`
   - Branch: `main` / `/ (root)` を選択し Save
4. 数分後、`https://<YOUR_GH_USERNAME>.github.io/uxc-mpa-sample/mpa-sample/index.html` で公開

## 注意
- API は `/user/embed-auth` に `{ "data": { "productUuid", "sessionId" } }` 形式でPOSTします。サーバ側と整合していることを確認してください。
- `YOUR_PRODUCT_UUID` を実際の UUID に置き換えてください。
- CORSでブロックされる場合は、サーバのCORS許可設定に `https://<YOUR_GH_USERNAME>.github.io` を追加してください。
