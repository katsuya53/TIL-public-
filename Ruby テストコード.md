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







