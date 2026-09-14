# 金沢30km挑戦会 2026-2027

月例30kmイベント用の記録・達成バッジ・シェアアプリです。

## 本番構成
- GitHub Pages
- Firebase Authentication
- Firebase Realtime Database
- Firebase UIDごとに記録を分離
- 8ペース: 3'50 / 4'00 / 4'15 / 4'30 / 5'00 / 5'30 / 6'00 / 6'30 per km
- 達成バッジ7種類

## Firebase Authentication
本番版は画面上では「ランナー名＋パスワード」ですが、内部ではランナー名から専用のFirebaseログインIDを生成し、Firebase Email/Password Authenticationを使います。

Firebase Console > Authentication > ログイン方法 で **メール/パスワード** を有効にしてください。匿名認証は有効のままでも問題ありませんが、本番版では使用しません。

## Realtime Database Rules
```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "auth != null && $uid === auth.uid",
        ".write": "auth != null && $uid === auth.uid"
      }
    }
  }
}
```

## ファイル
- `index.html` アプリ本体
- `firebase-config.js` Firebase Web設定
- `images/badge-1.png` 〜 `badge-7.png` 達成バッジ

## デモ
- 名前: 田中 太郎
- パスワード: pass1234

初回にこの組み合わせでログインするとFirebase上にデモユーザーが作成され、5か月分のデモ記録が投入されます。
