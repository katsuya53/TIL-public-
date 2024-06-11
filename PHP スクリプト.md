# echo
メッセージを出力
<?php
echo 'Welcome to PHP!';
?>

# print
echoの代わりにもなる。

# ヒアドキュメント構文
複数行の文字列を表現するための構文
echoやprintと合わせて複数行のメッセージを出力できる

echo <<<END
Welcome
to
PHP
END;

# echoタグ
<?= 7いらっしゃいませ' >

# メッセージをHTMLで出力する
ブラウザの設定に関わらず正しく日本語のメッセージが出力されるように、HTML形式で出力する
<meta charset="UTF-8">


# require 'ファイル名';
同じ部分の使い回し。
require '../header.php';

