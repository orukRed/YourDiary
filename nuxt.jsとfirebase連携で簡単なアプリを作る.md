# nuxt.jsとfirebase連携で簡単なアプリを作る

## 記事の内容

* firebaseでのプロジェクト設定
* nuxtで作っているアプリとの連携(Cloud Firestore使用)
* デプロイして公開する

# firebaseプロジェクト作成

はじめに、firebaseのTopから画面の指示に従いプロジェクトを作成します。
###プロジェクト一覧.png

###アプリ選択.png
その後、</>アイコンをクリック。
htmlに貼り付けるコードが出たらOKです。

# nodejsにfirebaseをインストール

下記コマンドを実行します。

```shell
npm install --save firebase
```

package.jsonに以下が追記されていることを確認しましょう。
下記は私の環境です。

```json
  "dependencies": {
    "core-js": "^3.6.5",
    "firebase": "^8.1.1",
    "nuxt": "^2.14.6"
  },
```