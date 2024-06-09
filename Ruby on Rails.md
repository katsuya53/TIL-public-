# Ruby on Rails
通称Rails（レイルズ）と呼ばれる。
Railsは、Rubyで作られたフレームワークの中で、最も利用されている有名なもの

# 新規Railsアプリケーションの作成
# Railsアプリケーションを作成
% rails new アプリケーション名

# データベース管理システムにmysqlを指定
% rails new アプリケーション名 -d mysql

# ホームディレクトリへ移動
% cd

# projectsディレクトリに移動
% cd ~/projects

# Railsのバージョン7.0.0を用いて、FirstAppを作成
% rails _7.0.0_ new first_app -d mysql

# 「first_app」ディレクトリに移動
% cd first_app

# 現在のディレクトリのパスを表示
% pwd

# データベースを作成する
% rails db:create

# ローカルサーバーを起動
% rails s

# 設定されているルーティングを確認
% rails routes

# コントローラーを作成
% rails g controller コントローラー名

# postsコントローラーを作成
% rails g controller posts

# rails gコマンドで生成したファイル一式を、rails dコマンドで削除
% rails d ファイルの種類 削除するファイル名

# postモデルを作成
% rails g model post

# マイグレーションを実行
% rails db:migrate

# rails db:rollbackレイルズ ディービー ロールバックコマンド
% rails db:rollback
マイグレーション実行による変更を差し戻すためのコマンド

# マイグレーションファイルの状況を確認
% rails db:migrate:status

# コンソールを起動
% rails c

# saveセーブメソッド
モデルのインスタンス.save

# ActiveRecordアクティブレコードメソッド
モデルがテーブル操作に関して使用できるメソッドの総称
all	  テーブルのすべてのデータを取得する
find	引数にレコードのidを指定し、対応するレコードを取得する
new	  クラスのインスタンス（レコード）を生成する
save	クラスのインスタンス（レコード）を保存する

# findファインドメソッド
モデル名.find(レコードのid)

# ヘルパーメソッド
form_with	投稿ページなどにおけるフォームの実装
link_to	リンクの実装

# form_withフォームウィズメソッド
<%= form_with url: "/posts", method: :post, local: true do |form| %>
urlオプション	フォームの情報を送るリクエストのパスを指定
methodオプション	フォームの情報を送るリクエストのHTTPメソッドを指定。オプションの初期値は:postなので、
                 postメソッドを指定する場合は省略することが可能
localオプション	リモート送信を無効にするかどうかを指定。trueにすると無効になる

text_field	1行のテキストボックス
password_field	パスワード入力ボックス（入力したテキストがアスタリスクなどに置き換えて表示される）
check_box	チェックボックス（複数選択可能）
radio_button	ラジオボタン（複数の中から1つしか選択できない）
submit	送信ボタン

# link_toリンクトゥーメソッド
リンク先をURLで指定する場合
  <%= link_to 'リンクに表示する文字', 'リンク先のURL' %>
リンク先をパスで指定する場合
  <%= link_to 'リンクに表示する文字', 'パス', method: :HTTPメソッド %>

# params
送られてきたパラメーターをハッシュのような構造で格納したもの。
フォームで送信されたデータもparamsの中に格納されてコントローラーで受け取られる。

text_fieldの後に記載されたキーでparamsに格納されている。
フォームで入力された情報の値は、params[:キー名]として取り出すことができる。

# createクリエイトメソッド
モデルが使用できるActiveRecordメソッドのひとつ。
保存のために、new→情報を記述→saveとしていたところが、createメソッドの引数を記述して実行するだけで保存できる。
モデル.create(カラム名: 値)
  Post.create(content: params[:content])

# redirect_to
特定のURLへ移動

# pictweetのディレクトリで実行するため、別ディレクトリにいる場合は移動
% cd ~/projects/pictweet

# Gemfileを元にGemをインストールし、Gemfile.lockを更新する
% bundle install

# コントローラーを削除
% rails d controller コントローラー名

# gem devise
gem 'devise'
% bundle install
% rails s

# deviseの設定ファイルを作成
% rails g devise:install

# deviseコマンドでUserモデルを作成
% rails g devise user

# rails g devise:viewsレイルズ ジー デバイス ビューズコマンド
% rails g devise:views

# rails g migrationレイルズ ジー マイグレーションコマンド
rails g migration Addカラム名To追加先テーブル名 追加するカラム名:型とすることで、テーブルにカラムを追加する際に必要なコードが記述された状態で、マイグレーションが生成

# usersテーブルにnicknameカラムをstring型で追加するマイグレーションファイルを作成
% rails g migration AddNicknameToUsers nickname:string

# paramsのpermitメソッド
params.require(:モデル名).permit(:許可するキー)

# devise_parameter_sanitizerのpermitメソッド
devise_parameter_sanitizer.permit(:deviseの処理名, keys: [:許可するキー])
処理名	         役割
:sign_in	      サインイン（ログイン）の処理を行うとき
:sign_up	      サインアップ（新規登録）の処理を行うとき
:account_update	アカウント情報更新の処理を行うとき

# 不要なカラムを削除
% rails g migration Removeカラム名From削除元テーブル名 削除するカラム名：型
# マイグレーションの作成
% rails g migration RemoveNameFromTweets name:string
# マイグレーションの実行
% rails db:migrate


# 環境変数を表示する
 printenv

# 直接環境変数を設定する
export GMAIL_USER_NAME=your_gmail_username
export GMAIL_PASSWORD=your_gmail_password
環境変数の値にスペースが含まれる場合は、値をクォーテーションで囲むことで解決できる

# 特定の環境変数を探す
grep -r "GMAIL_PASSWORD" ~/.bash* /etc/*

# ブラウザのタブに好きなアイコン(favicon)を設定する
favicon.icoを、railsのimageフォルダに保存
application.html.erbの<header>内に、以下のコードを追加
<%= favicon_link_tag 'favicon.ico' %>

# スマホのホーム画面のアイコンを設定する
画像をファイル名「apple-touch-icon.png」で保存
アイコン画像データをRailsアプリのassets > imagesディレクトリ配下へ設置。
  <link href="<%= image_path("apple-touch-icon.png") %>" rel="apple-touch-icon" sizes="180x180" type="image/png" />
  <link href="<%= image_path("android-touch-icon.png") %>" rel="icon" sizes="192x192" type="image/png" />

# フォーマット内の改行を反映する simple format
simple_formatは、Ruby on Railsのビューで使用されるヘルパーメソッドの1つ。
このメソッドは、テキスト内の改行をHTMLの段落タグ (<p>) および改行タグ (<br>) に変換する。
これにより、テキストがHTMLとして適切にフォーマットされ、改行が反映されるようになる