# Ubichill Worlds

Ubichillで遊べるワールドを、アプリ本体やmodのリリース周期から分離して公開するリポジトリです。

## ちるわ

ペンで自由に描きながら、みんなで動画や音楽を楽しむためのチルワールドです。

- World: [`worlds/chillwa.yaml`](./worlds/chillwa.yaml)
- Integrity lock: [`worlds/chillwa.lock.json`](./worlds/chillwa.lock.json)
- Video Player: `3.0.0`（Ubichill mod protocol v3対応Hostが必要）
- Video backend: `https://videoplayer.youkan.uk`

YAMLではmod更新の意図を`latest`で表し、実行時に使うversion・worker hash・capabilityは兄弟のlock fileで固定しています。`latest`が実行のたびに変わることはありません。

公開後は次のURLをUbichillへ入力して参加できます。

```text
https://raw.githubusercontent.com/ieyoukan/ubichill-worlds/main/worlds/chillwa.yaml
```

動画はワールドに同梱せず、自動再生もしません。再生するコンテンツの利用条件や権利は、URLを追加するユーザーが確認してください。

## ロックの更新

`*.lock.json` は、利用するmodのversion・worker hash・capability上限を固定するセキュリティ境界です。modを更新するときは、対応するUbichill CLIで再生成し、YAMLと一緒にレビュー・コミットします。

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
