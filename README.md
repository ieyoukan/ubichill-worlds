# Ubichill Worlds

Ubichillで遊べるワールドを、アプリ本体やmodのリリース周期から分離して公開するリポジトリです。

## ちるわ

ペンで自由に描きながら、みんなで動画や音楽を楽しむためのチルワールドです。

- World: [`worlds/chillwa.yaml`](./worlds/chillwa.yaml)
- Integrity lock: [`worlds/chillwa.lock.json`](./worlds/chillwa.lock.json)
- Video Player: `3.0.1`（Ubichill mod protocol v3対応Hostが必要）
- Video backend: `https://videoplayer.youkan.uk`

各dependencyの`source.url`に公開元を記録しているため、このリポジトリ単体でlockを再生成できます。
`--base-url`や本体リポジトリの`mods/`は必要ありません。YAMLではmod更新の意図を`latest`で表し、
実行時に使うversion・worker hash・capabilityは兄弟のlock fileで固定しています。`latest`が実行のたびに変わることはありません。

公開後は次のURLをUbichillへ入力して参加できます。

```text
https://ieyoukan.github.io/ubichill-worlds/worlds/chillwa.yaml
```

動画はワールドに同梱せず、自動再生もしません。再生するコンテンツの利用条件や権利は、URLを追加するユーザーが確認してください。

## GitHub Pagesへの公開

公開ページは <https://ieyoukan.github.io/ubichill-worlds/> です。
`main`へのpush、またはActionsの「Publish worlds to GitHub Pages」の手動実行で公開します。
GitHubのSettings → Pages → Sourceは **GitHub Actions** に設定します。

ubichill `2.4.0`の`ci create`で生成した文字列を、Repository Secret `UBICHILL_CREDENTIALS`に登録します。
この認証情報にはサーバー・作者アカウント・トークン・署名用秘密鍵・公開環境IDが含まれるため、
別の鍵Secretは不要です。秘密鍵はリポジトリや公開ファイルに保存しません。

```bash
npx ubichill ci create --server=https://ubichill.com --name="GitHub Actions: ieyoukan/ubichill-worlds"
```

Actionsでは`npm ci`後に`npm run build:pages`を実行し、`dist/worlds/`にYAML・lock・`.sig.json`を
書き出してGitHub Pagesへ配置します。`publish --no-install`でコミット済みのlockをそのまま署名するため、
公開時に`latest`を再解決しません。modを更新する場合は、下記の手順でlockを更新してコミットしてください。
署名にはCIで承認した作者アカウントが入り、Ubichillは登録済み公開鍵で作者を確認します。
元のraw GitHub URLにはCIで生成した署名がないため、参加にはPagesのURLを使ってください。

## ロックの更新

`*.lock.json` は、利用するmodのversion・worker hash・capability上限・取得元を固定するセキュリティ境界です。
modを更新するときは、対応するUbichill CLIで再生成し、YAMLと一緒にレビュー・コミットします。

Node.js 22以上を用意し、最初に依存関係をインストールしてください。

```bash
npm ci
```

lockを現在公開されているmodから再生成するには、次を実行します。

```bash
npm run lock
```

ファイルを書き換えず、コミット済みのlockが最新の解決結果と一致するか確認するには、次を実行します。

```bash
npm run lock:check
```
