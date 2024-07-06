# 単体テストコード

## gemを追加
gem 'rspec-rails', '~> 4.0.0'
% bundle install

## RSpecの設定
% rails g rspec:install

## .rspecに設定を追加
--require spec_helper
--format documentation

## Userモデルのテストファイルを生成
% rails g rspec:model user

## rails_helper レイルズ ヘルパー
RSpecでモデル、ビュー、コントローラーのテストを行うためには、rails_helper.rbというファイルを読み込む必要がある

## describe
テストコードのグループ分けを行うメソッド
describeにつづくdo~endの間に、さらにdescribeメソッドを記述することで、入れ子構造をとることもできる

## it
describeメソッド同様に、グループ分けを行うメソッド
「describeメソッドに記述した機能において、どのような状況のテストを行うか」を明記

## example
itで分けたグループのこと

## bundle exec バンドル エグゼクコマンド
Gemの依存関係を整理してくれるコマンド

## rspec アールスペック コマンド
pecディレクトリ以下に書かれたRSpecのテストコードを実行するコマンド
% bundle exec rspec spec/models/user_spec.rb 

## valid? バリッド
バリデーションを実行させて、エラーがあるかどうかを判断するメソッド
エラーがない場合はtrueを、ある場合はfalseを返す
エラーがあると判断された場合は、エラーの内容を示すエラーメッセージを生成

## expectation
検証で得られた挙動が想定通りなのかを確認する構文

## matcher
「expectの引数」と「想定した挙動」が一致しているかどうかを判断

## include
「expectの引数」に「includeの引数」が含まれていることを確認するマッチャ

## eq
「expectの引数」と「eqの引数」が等しいことを確認するマッチャ

## errors
インスタンスにエラーを示す情報がある場合、その内容を返すメソッド

## full_messages
エラーの内容から、エラーメッセージを配列として取り出すメソッド

## FactoryBot
インスタンスをまとめることができるGemです。他のファイルであらかじめ各クラスのインスタンスに定める値を設定しておき、各テストコードで使用する
gem 'factory_bot_rails'
% bundle install
FactoryBotの記述を格納するディレクトリfactoriesと、Userモデルに対するFactoryBotのファイルusers.rbを、以下のように手動で作成

## build
ActiveRecordのnewメソッドと同様の意味を持つ

## before
それぞれのテストコードを実行する前に、セットアップを行うことができる

## Faker
ランダムな値を生成するGem
gem 'faker'
% bundle install

## be_valid
valid?メソッドの返り値が、trueであることを期待するマッチャ
expectの引数に指定されたインスタンスが、バリデーションでエラーにならないものであれば、valid?の返り値はtrueとなりテストは成功

## context
特定の条件を指定してグループを分け。
使用方法はdescribeと同じだが、describeには何についてのテストなのかを指定するのに対し、contextには特定の条件を指定


# コントローラーの単体テストコード

## Request Spec
RSpecが提供している、コントローラーのテストコードを書くために特化した手法です。RSpecの導入が完了していれば使用でき流。

## ディレクトリ作成
% rails g rspec:request posts

# postsコントローラーindexアクションの単体テストコード

## create
ActiveRecordのcreateメソッドと同様の意味。
buildとほぼ同じ働きをするが、createの場合はテスト用のDBに値が保存。
注意すべき点として、1回のテストが実行され、終了する毎にテスト用のDBの内容がロールバックされる。（保存された値がすべて消去されてしまう）

## テストコードを実行
% bundle exec rspec spec/requests/posts_spec.rb

## get
it 'indexアクションにリクエストすると正常にレスポンスが返ってくる' do 
  get root_path
  binding.pry
end
以下のコマンドでテストコードを実行し、binding.pryの部分で止まることを確認

## response
リクエストに対するレスポンスそのものが含まれる
このレスポンスで取得できる情報に、想定する内容が含まれているかを確認することで、テストコードを書くことができる
binding.pryで停止しているところに、responseと入力してエンターキーを押下
ここから、「正常なレスポンスかどうか」を判断する必要がある。それを判断するためには、HTTPステータスコードで判別

## HTTPエイチティーティーピーステータスコード
ステータスコード	内容
100~	処理の継続中
200~	処理の成功
300~	リダイレクト
400~	クライアントのエラー
500~	サーバーのエラー

正常にレスポンスを得ることを確かめたいため、200というステータスコードを期待
レスポンスの中からステータスコードを確かめるためには、statusを利用

## status
response.statusと実行することによって、そのレスポンスのステータスコードを出力できる
binding.pryで停止しているところに、response.statusと入力してエンターキーを押下
200が確認できれば成功

## 完成したテストコード
it 'indexアクションにリクエストすると正常にレスポンスが返ってくる' do 
  get root_path
  expect(response.status).to eq 200
end

## bodyボディー
response.bodyと記述すると、ブラウザに表示されるHTMLの情報を抜き出すことができる

## response.bodyに@tweet.textが含まれているかどうかを確かめる
it 'indexアクションにリクエストするとレスポンスに投稿済みのツイートのテキストが存在する' do
  get root_path
  expect(response.body).to include(@tweet.text)
end

## レスポンスに投稿済みの画像URLが含まれていることを確認
it 'indexアクションにリクエストするとレスポンスに投稿済みのツイートの画像URLが存在する' do 
  get root_path
  expect(response.body).to include(@tweet.image)
end

## 検索フォームの「投稿を検索する」という文言がレスポンスに含まれているかどうかを確認
it 'indexアクションにリクエストするとレスポンスに投稿検索フォームが存在する' do 
  get root_path
  expect(response.body).to include('投稿を検索する')
end


# 結合テスト

## System Spec
結合テストコードを記述するための仕組みのこと。大枠の記述はこれまでのRSpecと変わらない。
System Specを記述するためには、CapybaraというGemを用いる。
すでにデフォルトでRuby on Railsに搭載されてい流。

## Capybara
System Specを記述するために必要なGem
gem 'capybara', '>= 2.15'

## 結合テストコードを書くためのファイルを生成
% rails g rspec:system users

## visit
visit 〇〇_pathのように記述すると、〇〇のページへ遷移することを表現。
RequestSpecで学んだgetと似ているが、getはあくまでリクエストを送るだけのことを意味し、visitはそのページへ実際に遷移することを意味

## page
visitで訪れた先のページの見える分だけの情報が格納

## have_content
expect(page).to have_content('X')と記述すると、visitで訪れたpageの中に、Xという文字列があるかどうかを判断するマッチャ

## fill_in
fill_in 'フォームの名前', with: '入力する文字列'のように記述することで、フォームへの入力を行うことができる

## find().click
find('クリックしたい要素').clickと記述することで、実際にクリックができる

## change
expect{ 何かしらの動作 }.to change { モデル名.count }.by(1)と記述することによって、モデルのレコードの数がいくつ変動するのかを確認できる
changeマッチャでモデルのカウントをする場合のみ、expect()ではなくexpect{}となる

## have_current_path
expect(page).to have_current_path('X')と記述すると、visitで訪れたpageのURLがXであるかどうかを判断

## hover
find('ブラウザ上の要素').hoverとすることで、特定の要素にカーソルをあわせたときの動作を再現

## have_no_content
文字列が存在しないことを確かめるマッチャ

## 実装コード例
spec/system/users_spec.rb

it '正しい情報を入力すればユーザー新規登録ができてトップページに移動する' do
  # トップページに移動する
  visit root_path
  # トップページにサインアップページへ遷移するボタンがあることを確認する
  expect(page).to have_content('新規登録')
  # 新規登録ページへ移動する
  visit new_user_registration_path
  # ユーザー情報を入力する
  fill_in 'Nickname', with: @user.nickname
  fill_in 'Email', with: @user.email
  fill_in 'Password', with: @user.password
  fill_in 'Password confirmation', with: @user.password_confirmation
  # サインアップボタンを押すとユーザーモデルのカウントが1上がることを確認する
  expect{
    find('input[name="commit"]').click
    sleep 1
  }.to change { User.count }.by(1)
  # トップページへ遷移することを確認する
  expect(page).to have_current_path(root_path)
  # カーソルを合わせるとログアウトボタンが表示されることを確認する
  expect(
    find('.user_nav').find('span').hover
  ).to have_content('ログアウト')
  # サインアップページへ遷移するボタンや、ログインページへ遷移するボタンが表示されていないことを確認する
  expect(page).to have_no_content('新規登録')
  expect(page).to have_no_content('ログイン')
end

## テストコードを実行
% bundle exec rspec spec/system/users_spec.rb


## 投稿のテストコード

## have_selector
指定したセレクタが存在するかどうかを判断するマッチャ
投稿した画像が表示されているか確認は
have_selector ".content_post[style='background-image: url(#{@tweet_image});']"という形で記述

## テストコードを実行
% bundle exec rspec spec/system/tweets_spec.rb

## have_link
expect('要素').to have_link 'ボタンの文字列', href: 'リンク先のパス'と記述することで、要素の中に当てはまるリンクがあることを確認

## have_no_link
expect('要素').to have_no_link 'ボタンの文字列', href: 'リンク先のパス'と記述することで、要素の中に当てはまるリンクがないことを確認

## all
all('クラス名')でpageに存在する同名のクラスを持つ要素をまとめて取得できます。そしてall('クラス名')[0]のように添字を加えることで「◯番目のmoreクラス」を取得

## have_field
have_field('tweet_image')と記述することで、「tweet_image」というidを持ったフォームが存在するかを確認
なお、CSSにおいてidを表すために「#」が必要だが、have_fileldで引数を指定する際は不要。
have_field('#tweet_image')ではなく、have_field('tweet_image')と記述することに注意
また、あるフォームが存在し、そのフォームにある入力がされていることを確認するには「with」を使用し、have_field('tweet_image', with: "イメージ")のように記述


## ツイート削除の結合テスト

## find_link().click
find_link('リンクの文字列', href: 'URL').clickといった形で使う。
find().clickと似ているが、find_link().clickはa要素のみに対して用いることができる


# テストコードをまとめる
サポートモジュール
RSpecに用意されている、メソッド等をまとめる機能

specディレクトリ配下にsupportディレクトリを作成し、その配下にsign_in_support.rbを作成