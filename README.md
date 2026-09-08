# Ubichill Worlds

Ubichillで遊べるワールドを、アプリ本体やmodのリリース周期から分離して公開するリポジトリです。

## ちるわ

ペンで自由に描きながら、みんなで動画や音楽を楽しむためのチルワールドです。

- World: [`worlds/chillwa.yaml`](./worlds/chillwa.yaml)
- Integrity lock: [`worlds/chillwa.lock.json`](./worlds/chillwa.lock.json)
- Video Player: `3.0.0`（Ubichill mod protocol v3対応Hostが必要）
- Video backend: `https://videoplayer.youkan.uk`

公開後は次のURLをUbichillへ入力して参加できます。

```text
https://raw.githubusercontent.com/ieyoukan/ubichill-worlds/main/worlds/chillwa.yaml
```

動画はワールドに同梱せず、自動再生もしません。再生するコンテンツの利用条件や権利は、URLを追加するユーザーが確認してください。

## ロックの更新

`*.lock.json` は、利用するmodのversion・worker hash・capability上限を固定するセキュリティ境界です。modを更新するときは、対応するUbichill CLIで再生成し、YAMLと一緒にレビュー・コミットします。
