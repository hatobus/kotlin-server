# kotlin-server

kotlinでAPIサーバーを書く

- 認証周り ... JWT
- DB ... mysql
- CRUDで情報を操作できるもの

図書館アプリのAPIを作る

本の登録、検索、更新、削除、貸し出しができるようなAPIを作成する。

# API
## CRUD
- POST ... /title
  - 新しいタイトルの本を追加する
  - jsonで詳細情報をbodyに含めてあげる
- GET ... /title
  - そのタイトルの本を取得する
  - なかったら404が返る
- PUT ... /title
  - そのタイトルの本を更新する
  - bodyに入っている情報の通りに更新される
- DELETE ... /title
  - そのタイトルの本を削除する
    
## その他API
- POST /user
  - sign up用API
  - user IDとpasswordを保存する
  - 管理者ユーザーはここで指定する
- POST /user/login
  - login用API
  - パスワードとIDが入ってくる
- GET /search
  - クエリパラメータで指定した検索をする
  - タイトルや著者名で検索ができるようにする
  - asc, descで並べ替えが可能にする

## ユーザー
- 管理者ユーザー
  - すべてのAPIを利用可能
  - DBで`admin`フラグを設定して`true`の場合に管理者ユーザーになれる
- 通常ユーザー
  - 検索、取得、ログインのみ
  - `admin`フラグが`false`のときには通常ユーザーになる
- パスワードなどの制約
  - IDは3文字以上32文字以下である必要がある
  - passwordは8文字以上64文字以下、英数字+記号で入れる必要がある
  