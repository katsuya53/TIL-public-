# 参考URL
https://qiita.com/engineer_ikuzou/items/0a7cbead95948d0ad1cc


# API_KEYの取得
OpenWeatherMapで会員登録して、API_KEYを取得
以下参照
https://qiita.com/matsubishi5/items/fcd77eacb0ed111299e2

http://api.openweathermap.org/data/2.5/weather?q=Tokyo&appid=
末尾に取得したAPI_KEYを貼り付けて、ブラウザで実行。東京の今の天気が返ってくる
会員登録からAPI_KEYが使えるようになるまで数時間程度かかることも

# 必要なライブラリをインストール & API_KEYを格納

## Gemfile
#API_KEYを環境変数として管理する（Keyを外部流出させないための措置）
gem 'dotenv-rails'
#アプリケーション内でHTTPリクエストを投げたい場合に使うクラス
gem 'httpclient'

Gemfile記載後、bundle install

# 環境変数への設定
..env.
OPEN_WEATHER_MAP_API = 'API_KEY貼り付け'
URI = 'https://api.openweathermap.org/data/2.5/weather'

.envには、前もって取得したAPI_KEYをコピペ
export GOOGLE_MAPS_API_KEY='APIキーを貼り付け'


- 本番環境 EC2にログイン
①EC2にSSHで接続し、Vimを開く
% cd .ssh
% SSH接続のコマンド（ssh -i hoge.pem ec2-user@アプリのIPアドレス）

接続後
[ec2-user@ip-172-31-0-160 ~]$ sudo vim /etc/environment
②環境変数を記述する
内容を変更するには「i」を押して編集モードにする。
変更し終わったら「esc」を押して編集モードを終了してから「:wq」で保存して終了すること。


参考記事
https://qiita.com/4ma9147/items/1a4a20e10aec0efbb24e