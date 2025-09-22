# Laravel Lesson レビュー①

## Todo一覧機能

### Todoモデルのallメソッドで実行しているSQLは何か
SELECT * FROM todos;

### Todoモデルのallメソッドの返り値は何か
Collectionオブジェクト

### 配列の代わりにCollectionクラスを使用するメリットは
- オブジェクトなので、メソッドチェーンを使用できる
- 可読性・保守性が高い

### view関数の第1・第2引数の指定と何をしているか
- 第1引数に表示したいbladeファイル
- 第2引数に渡したいデータを連想配列で指定できる

### index.blade.phpの$todos・$todoに代入されているものは何か
- $todos -> Todoモデルのレコードを複数まとめたCollectionオブジェクト
- $todo -> Todoモデルインスタンス
- $todosと$todoの違いは$todoはTodoクラスに定義されているtodosテーブルからインスタンス化したtodo一件のデータが代入されていて、$todosはインスタンス化された$todoをallメソッドで全件取得した返り値としてCollectionオブジェクトが代入されています

## Todo作成機能

### Requestクラスのallメソッドは何をしているか
HTTPリクエストに含まれるすべての入力値を連想配列にして返す

### fillメソッドは何をしているか
連想配列で取得した値をTodoインスタンスに一括で代入している

### $fillableは何のために設定しているか
定義することによって代入できる項目に制限をかけている

### saveメソッドで実行しているSQLは何か
INSERT INTO todos(content, created_at, updated_at) VALUES ('フォームから送られた値', '作成された日時', 更新された日時);

### redirect()->route()は何をしているか
一覧画面に遷移するよう、リダイレクト処理が記述されている
*今回はroutingで指定しているtodo.indexに遷移するように指定している

## その他

### テーブル構成をマイグレーションファイルで管理するメリット
Gitで共有することで、開発者全員が同じテーブルを作成することができる

### マイグレーションファイルのup()、down()は何のコマンドを実行した時に呼び出されるのか
- up()メソッドは"php artisan migrate"を実行した時
- down()メソッドは"php artisan migrate:rollback"を実行した時

### Seederクラスの役割は何か
DBにテスト用データを投入することができる

### route関数の引数・返り値・使用するメリット
- 引数 : 第1引数URLパス、第2引数に呼び出すControllerメソッド
- 返り値 : Routeオブジェクト
- メリット : ルートの変更がしやすく、可読性が高い

### @extends・@section・@yieldの関係性とbladeを分割するメリット
- 関係性 : 
@extendsを使用しbladeファイルを継承している。
@section() ~ @endsectionでカッコった部分を継承したbladeファイルの@yield()に挿入する。
- bladeを分割するメリット : 
一覧画面と新規作成画面など同じ記述が複数回登場する場合、修正する際に必要な場所をすべて変更する必要があり、保守性が低い状態になってしまうため、分割することにより、可読性・保守性が向上する。

### @csrfは何のための記述か
CSRF対策ための記述で、記述することによってフォームにCSRFトークンが自動で埋め込まれます

### {{ }}とは何の省略系か
bladeテンプレートにおけるecho(PHP)構文
例えば{{ $todo->content }}の場合省略しない場合は以下になる
<?pho echo e ($todo->content); ?>