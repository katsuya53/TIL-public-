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

# form
<form action="user-output.php" method="post">

# リクエストパラメータ
<input type="text" name="user">
echo 'ようこそ、', $_REQUEST['user'], 'さん。';

# チェックボックス
<input type="checkbox" name="mail">お買い得情報のメールを受け取る

# if-else文
if (isset($_REQUEST['mail'])) {
	echo 'メールをお送りさせて頂きます。';
} else {
	echo 'メールはお送りさせて頂きません。';
}

# ラジオボタン
<p><input type="radio" name="meal" value="和食" checked>和食</p>

# switch文
<?php
switch ($_REQUEST['meal']) {
case '和食':
	echo '焼き魚、煮物、味噌汁、御飯、果物';
	break;
case '洋食':
	echo 'ジュース、オムレツ、ハッシュポテト、パン、コーヒー';
	break;
case '中華':
	echo '春巻、餃子、卵スープ、炒飯、杏仁豆腐';
	break;
}
echo 'をご提供いたします。';
?>

# セレクトボックス
<select name="seat">
<option value="自由席">自由席</option>
<option value="指定席">指定席</option>
<option value="グリーン席">グリーン席</option>
</select>
<p><input type="submit" value="確定"></p>

