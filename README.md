# 三角コーナー web チャット＆大喜利

`index.html` はビルド不要の静的アプリです。チャット、返信・いいね、大喜利のお題作成、回答、投票、結果表示に対応しています。

## ローカルで試す

`index.html` をブラウザーで開くと、データはそのブラウザーの `localStorage` に保存されます。画面上部に「ローカル保存」と表示されている間は、別の端末や利用者とは同期されません。

## Firebase でリアルタイム同期する

Firebase コンソールで Web アプリを作成し、Authentication の匿名ログインと Cloud Firestore を有効にしてください。Firebase の Web 設定を `window.FIREBASE_CONFIG` に設定してから、アプリの ES module スクリプトが実行されるようにします。例えば、`index.html` のアプリ用 `<script type="module">` より前に次を置きます。

```html
<script>
  window.FIREBASE_CONFIG = {
    apiKey: "Firebase の Web API key",
    authDomain: "プロジェクトID.firebaseapp.com",
    projectId: "プロジェクトID"
  };
</script>
```

Firebase Web 設定はクライアントに公開される情報です。Firestore の Security Rules で匿名認証済みユーザーに必要な読み書きだけを許可してください。このアプリが使うコレクションは `artifacts/{appId}/public/data/chat_messages` と `artifacts/{appId}/public/data/ogiri_topics` です。公開読み書きルールを無条件に設定しないでください。

Firebase 設定がない、または Firebase 接続に失敗した場合もアプリはローカル保存モードで起動し、画面上部に同期されないことを表示します。

## GitHub Pages

GitHub リポジトリの **Settings → Pages** で公開元を設定してください。公開後、Firebase 同期を利用する場合は上記の Web 設定をページで読み込めるように設定します。Pages の公開設定がない場合、リポジトリに push してもサイトは公開されません。