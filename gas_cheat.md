# 一覧

- [使い方](#使い方)
- [基本](#基本)
  - [Log出力](#Log出力)
  - [変数宣言](#変数宣言)
  - [定数宣言](#定数宣言)
  - [配列](#配列)
  - [多次元配列](#多次元配列)
  - [辞書](#辞書)
  - [四則演算](#四則演算)
  - [改行](#改行)
  - [文字連結](#文字連結)
  - [文字列置換](#文字列置換)
  - [現在日時取得](#現在日時取得)
  - [関数呼び出し](#関数呼び出し)
  - [戻り値取得](#戻り値取得)
  - [条件分岐](#条件分岐)
  - [複数条件](#複数条件)
  - [繰り返し(for)](#繰り返し(for))
  - [繰り返し(while)](#繰り返し(while))
  - [メッセージボックス表示](#メッセージボックス表示)
- [スプレッドシート操作全般](#スプレッドシート操作全般)
  - [スプレッドシートを開く](#スプレッドシートを開く)
  - [AppScriptに紐付くスプレッドシートを取得する](#AppScriptに紐付くスプレッドシートを取得する)
  - [シートを開く](#シートを開く)
  - [セルの値を取得する](#セルの値を取得する)
  - [セルの値を変更する](#セルの値を変更する)
  - [ブランク判定](#ブランク判定)
  - [最終行取得](#最終行取得)
  - [最終列取得](#最終列取得)
  - [行挿入](#行挿入)
  - [行削除](#行削除)
  - [最終行に値追加](#最終行に値追加)
  - [シートを別スプレッドシートにコピーする](#シートを別スプレッドシートにコピーする)
  - [シート名取得](#シート名取得)
  - [シート名変更](#シート名変更)
  - [ソート](#ソート)
- [ドライブ操作全般](#ドライブ操作全般)
  - [フォルダを開く](#フォルダを開く)
  - [フォルダ内のフォルダ、ファイル一覧化](#フォルダ内のフォルダ、ファイル一覧化)
  - [フォルダ一覧全てに対して処理](#フォルダ一覧全てに対して処理)
  - [ファイル一覧全てに対して処理](#ファイル一覧全てに対して処理)
  - [フォルダ作成](#フォルダ作成)
- [フォーム操作全般](#フォーム操作全般)
  - [フォームを開く](#フォームを開く)
  - [フォーム名変更](#フォーム名変更)
  - [フォームの回答用URLを取得](#フォームの回答用URLを取得)
- [スライド操作全般](#スライド操作全般)
  - [スライドを開く](#スライドを開く)
  - [全スライドを配列で取得](#全スライドを配列で取得)
  - [スライド内のエレメントを配列で取得](#スライド内のエレメントを配列で取得)
- [メール操作全般](#メール操作全般)
  - [メール下書き作成](#メール下書き作成)
  - [メール送信](#メール送信)
- [その他参考記事](#その他参考記事)
  - [フォルダごとコピー](#フォルダごとコピー)

# 使い方
そもそも、GASをスプレッドシートから作るものと勘違いしている場合が多いようだが、そうではなく単体でも機能する。

[https://script.google.com/](https://script.google.com/)

ここから「新規スクリプト」で新たに作成する。

「トリガー」をプロジェクト毎に設定すれば、ある日付毎、時間毎に自動で実行させることができる。

[Google Apps Script 入門](https://qiita.com/t_imagawa/items/47fc130a419b9be0b447)

ここが詳しい。

# 基本

## Log出力
```js
function log_test(){
  Logger.log('ログ出力'); //'ログ出力' //実行後、Ctrl+Enterでログを確認することが出来る
}
```
コーディング中の実行結果確認に使う。

プログラムを書き終えて、定期的に実行させる結果ログを残す場合は、ログ用スプレッドシートに直接書き込む等したほうが良い。

## 変数宣言
```js
function var_test() {
  var hensu;
  hensu = 'helllo';
  Logger.log(hensu); //'hello' //「var」で宣言した変数の値は、名前で呼び出すことが出来る
  hensu = 100
  Logger.log(hensu); //100.0 //再び値を指定すると中身が変わる
}
```

## 定数宣言
```js
function const_test() {
  const teisu = 0;
  teisu = 1;
  Logger.log(teisu); //0.0 //「const」で宣言した定数の値は、変更することが出来ない
}
```
定数は変数と違い、宣言時に入れた値を上書きすることができない。

変わることが無い値は、誤ってプログラムの中で何度も宣言、代入を行って書き換えが起こらないように定数で宣言することが望ましい。

## 配列
```js
function array_test(){
  var hairetsu = ['Apple','Banana','Strawberry'];
  Logger.log(hairetsu); //['Apple','Banana','Strawberry']
  hairetsu.push('Orange');
  Logger.log(hairetsu); //['Apple','Banana','Strawberry','Orange']
  Logger.log(hairetsu[0]); //'Apple' //「配列名[数字]」で値を取り出すことが出来る(数字は0開始)
  Logger.log(hairetsu.length); //4 //配列に仕舞われている値の数
}
```
配列は複数の値を仕舞うことができる。

## 多次元配列
```js
function multi_array_test(){
  const hairetsu_1 = ['Red','Blue','Yellow'];
  const hairetsu_2 = ['Phone','Book','Car','Bag'];
  const multi_hairetsu = [hairetsu_1,hairetsu_2];
  Logger.log(multi_hairetsu) //[[Red, Blue, Yellow], [Phone, Book, Car, Bag]] //配列の中に配列を作ることも出来る。更にその中に..も出来る
	Logger.log(multi_hairetsu[0][2]); //'Yellow'
}
```
配列の中に配列を作ることも可能。

それは2次元配列と呼ばれ、更に増える度に3次元、4次元..と増えていく。

他にも例えば、あまり推奨できない手段だが、[[1,2,3],'test']といった風に1つの配列の中に異なる型の値を入れることも一応可能。

## 辞書
```js
function dict_test(){
  var jisho = {};
  jisho.Number = 1;
  jisho.Sex = 'Man';
  jisho.Age = 30;
	jisho.Mail = 'test@sample.com';
  Logger.log(jisho); //{Number=1, Sex='Man', Age=30, Mail='test@sample.com'}
  Logger.log(jisho.Sex); //'Man'

	var food = {};
	food.tomato = {};
  food.tomato.genre = 'vegetable',
    food.tomato.size = '80',
      food.tomato.color = 'red';
  Logger.log(food.tomato); //{size=80, color=red, genre=vegetable}
	Logger.log(food.tomato.color); //'red'
}
```
辞書のように、キー(項目名)を与えると値(その中身)を返す変数。

```js
var food = {};
food.tomato = {};
food.tomato.genre = 'vegetable',
  food.tomato.size = '80',
    food.tomato.color = 'red';
Logger.log(food.tomato); //{size=80, color=red, genre=vegetable}
Logger.log(food.tomato.color); //'red'
```
辞書の中に辞書、辞書の中に配列、配列の中に辞書、このように何度もネストして使うこともある。

## 四則演算
```js
function calc_test(){
  const origin = 10;
  var add = origin + 9;
  Logger.log(add); //19.0 //加算->「+」
  var sub = origin - 6;
  Logger.log(sub); //4.0 //減産->「-」
  var multi = origin * 3;
  Logger.log(multi); //30.0 //乗算->「*」
  var divide = origin / 2;
  Logger.log(divide); //5.0 //除算->「/」
}
```
基本的な計算。

```js
var sample = 4 * 120
```
変数に対してだけではなく、値通しを掛け合わせることも出来る。

```js
var sample = 480 //4 * 120
```
が、コード上で不要な計算はなるべく避けてこのようにしたい。

## 改行
```js
function newline_test(){
  const txt = 'うえと\nした' //改行は文字列で「\n」
  Logger.log(txt)
  //うえと
  //した
}
```
結果を改行で表したい時は、「\n」を文字列の間に入れる。

これは「エスケープ文字」と呼ばれるもので、他にも色々ある。

## 文字連結
```js
function txt_link(){
  txt_1 = 'hogehoge';
  txt_2 = 'hugahuga';
  link = txt_1 + txt_2;
  Logger.log(link) //'hogehogehugahuga' 文字の連結は間に「+」
}
```
文字列を連結する時は、間に「+」を入れる。

他にも色々やり方はある。

## 文字列置換
```js
function replace_test(){
  const txt = '私は君が大好き';
  var chikan = txt.replace('君','金');
  Logger.log(chikan) //'私は金が大好き'
}
```

## 現在日時取得
```js
function datetime_test(){
  const year = Utilities.formatDate(new Date(), "JST", "yyyy");
  Logger.log(year); //2019
  const month = Utilities.formatDate(new Date(), "JST", "M");
  Logger.log(month); //9
  const day = Utilities.formatDate(new Date(), "JST", "d");
  Logger.log(day); //26
  const hour = Utilities.formatDate(new Date(), "JST", "HH");
  Logger.log(hour); //18
  const minute = Utilities.formatDate(new Date(), "JST", "mm");
  Logger.log(minute); //29
  const yyyymmdd = Utilities.formatDate(new Date(), "JST", "yyyy/MM/dd");
  Logger.log(yyyymmdd); //2019/09/26
  const hhmm = Utilities.formatDate(new Date(), "JST", "HH:mm");
  Logger.log(hhmm); //18:29
}
```
現在日時をテキストで表したい時に使う。

ルールに則っていれば、ケースに合わせた記法が出来る。

## 関数呼び出し
```js
function func_test_1(){
  var txt = '呼び出し！';
  func_test_2(txt); //「func_test_2」で他関数を呼び出している。「()」内で値を渡す(「引数」という)ことが出来る
}
function func_test_2(txt){ //「()」内で値を受け取っている
  Logger.log(txt); //'呼び出し！' //受け取った値はそのまま使用出来る
}
```
別の関数を呼び出して使う。

ここで言う「関数」は、例えばエクセルで言われる「関数」と意味は同じ。

何かしらの値(引数)を与えると、関数毎に決められた計算を行い結果(戻り値)を返すもの。(結果が返らなくても良い。上記サンプルは返らない場合)

エクセルの「SUM(A1:B5)」であれば、「SUM」が"関数名"、「A1:B5」が"引数"で、A1～B5の中の数字を足した答えが"結果"として画面に表示されている。

## 戻り値取得
```js
function return_test_1(){
  var i = 3;
  var x100 = return_test_2(i); //変数「i」を関数「return_test_2」に渡して、戻り値を変数「x100」に
  Logger.log(x100) //300.0
}
function return_test_2(i){
  var x100 = i * 100; //変数「i」を100倍
  return x100 //「return」の後に値を入力すると、呼び出し元にその値を返す
}
```
「関数呼び出し」の、"戻り値"があるもの。

## 条件分岐
```js
function if_test(){
  const txt = 'Neko';
  if (txt == 'Neko'){ //変数「txt」が'Neko'なら
    Logger.log('Nyaa!'); //'Nyaa!'
  }
  const i = 120;
  if (i>=108){ //変数「i」が100以上なら
    Logger.log('むらむら'); //'むらむら'
  }else{ //条件に一致しなければ
    Logger.log('ひえひえ'); //'ひえひえ'
  }
  const hour = 13;
  if (hour<12){ //変数「hour」が12未満なら
    Logger.log('AM'); //'AM'
  }else if(hour>12){ //変数「hour」が12超過なら
    Logger.log('PM'); //'PM'
  }else{ //条件に一致しなければ
    Logger.log('Noon'); //'Noon'
  }
}
```
「if」の後に「()」内に記載した条件に一致する場合は、その後の「{}」で囲まれたコードを実行する。

```js
if (i>=108){ //変数「i」が100以上なら
  Logger.log('むらむら'); //'むらむら'
}else{ //条件に一致しなければ
  Logger.log('ひえひえ'); //'ひえひえ'
}
const hour = 13;
if (hour<12){ //変数「hour」が12未満なら
  Logger.log('AM'); //'AM'
}else if(hour>12){ //変数「hour」が12超過なら
  Logger.log('PM'); //'PM'
}else{ //条件に一致しなければ
  Logger.log('Noon'); //'Noon'
}
```
「else」や「else if」をその後に入力することで、一致しなかった場合の処理も書くことが出来る。

## 複数条件
```js
function ifs_test(){
  const ifs_a = 10;
  const ifs_b = 20;
  if (ifs_a == 10 && ifs_b == 15){ //AND
    var ifs_txt = '両方一致';
  } else if (ifs_a == 10 || ifs_b == 15){ //OR
    var ifs_txt = '片方一致';
  } else {
    var ifs_txt = '両方不一致';
  }
  Logger.log(ifs_txt); //'片方一致'
}
```
式を'&&'で繋ぐとAND条件に、'||'で繋ぐとOR条件になる。

## 繰り返し(for)
```js
function for_test(){
  const max = 5; // 最大値指定
  for(var i=0;i<=max;i++){ //変数「i」を値「0」で宣言、「i」が「max」以下な間処理を繰り返し、実行後に「i」に+1する(「インクリメント」という)
    Logger.log(i) //1.0,2.0,3.0,4.0,5.0
  }
}
```
少しややこしいが、上記例の場合だと「"0"から開始して、1度の実行毎に"1"を足す。"5"を超えたとき終了("5"は実行される)」と見れれば良い。

「i=0」の"0"や「max=5」の"5"を変えれば、始点終点を任意の数に変更できる。

ちょっとした編集を行うスクリプトなら大体これで解決できると思われる。

## 繰り返し(while)
```js
function while_test(){
  var txt = '';
  while (txt.length <= 7){ //「()」内の条件に一致する間繰り返し処理 //変数「txt」の文字数が7以下な間は繰り返す
    txt = txt + 'abc';
    Logger.log(txt); //'abc','abcabc','abcabcabc'
  }
}
```
「while」の後に「()」内に記載した条件に一致する間は、その後の「{}」で囲まれたコードを実行する。

「{}」内のコード中にインクリメント等を入れて、比較条件内の結果に変化が起こることが期待されるような作りにしないと、無限ループの原因となる。

## メッセージボックス表示
```js
//通常表示
function message_test(){
  Browser.msgBox('メッセージ');
}
//OK、キャンセル選択
function okcansel_test(){
  var okcansel = Browser.msgBox('OKかキャンセルを選んでください', Browser.Buttons.OK_CANCEL);
  if (okcansel == 'ok'){
    //'OK'の処理
  } else if(okcansel == 'cansel') {
    //'キャンセルの処理'
  }
}
//テキスト入力
function inputtext_test(){
  var inputtext = Browser.inputBox("あいさつを入力してください");
  if (inputtext == 'おはよう'){
    Browser.msgBox('Good morning');
  } else if(inputtext == 'こんにちは') {
    Browser.msgBox('Hello');
  } else if(inputtext == 'こんばんは') {
    Browser.msgBox('Good evening');
  } else {
    Browser.msgBox('入力が無効です');
  }
}
```
単純に画面に文字を表示させたいだけなら'msgBox'で可能。
押下したボタンで分岐させたい場合は、引数に'Browser.Buttons.OK_CANCEL'を追加。
画面で押下したボタンが'ok','cansel'で返ってくるので、それを元に分岐が可能。
ユーザーに入力を求め、それを値として使う場合は'inputBox'を使う。
何も入力せずにOKを押した場合、空のテキストが返る。

# スプレッドシート操作全般
```js
function spreadsheet_test(){
  //スプレッドシートを開く
  const wbid = 'sample12345678'; //ファイルIDを宣言
  var wb = SpreadsheetApp.openById(wbid); //ファイルIDからスプレッドシートを開く
  const wbname = 'テストシート'; //ファイル名を宣言
  var wb = SpreadsheetApp.openByName(wbname); //ファイル名からスプレッドシートを開く

  //AppScriptに紐付くスプレッドシートを取得する
  const wb_wct = SpreadsheetApp.getActive(); //開いているスプレッドシート(スプレッドシートに紐付いたスクリプトの場合)

  //シートを開く
  const wsname = 'シート1'; //シート名を宣言
  var ws = wb.getSheetByName(wsname); //シート名からシートを開く

  //セルの値を取得する
  var row = 2, //行2
      col = 3, //列3(C列)
      numrow = 5, //~5行
      numcol = 2; //~2列
  var cell_val = ws.getRange(row,col).getValue(); //C2の値を取得
  Logger.log(cell_val) //'C2の値'
  var cell_vals = ws.getRange(row,col,numrow,numcol).getValue(); //C2:D6の値を取得
  Logger.log(cell_val) //'C2:D6の値(配列)'

  //セルの値を変更する
  var row = 2, //行2
      col = 3; //列4(D列)
  ws.getRange(row,col).setValue(cell_val); //D2の値を変数「cell_val」(C3の値)に変更

  //ブランク判定
  var row = 2, //行2
      col = 1; //列1(A列)
  var isblank_range = ws.getRange(row,col);
  if (isblank_range.isBlank()==true){ //「isBlank」を関数に対して使用すると、「true」「false」でブランクかそうでないかを返す
    Looger.log('行'+row+'はブランクです');
  }else{
    Looger.log('行'+row+'はブランクではありません');
  }

  //最終行取得
  var maxrow = ws.getMaxRows(); //シートに存在する最後の行を取得
  Logger.log(maxrow) //1000
  var lastrow = ws.getLastRows(); //セルに入力のある最後の行を取得
  Logger.log(lastrow) //120

  //最終列取得
  var maxcol = ws.getMaxColumns(); //シートに存在する最後の列を取得
  Logger.log(maxcol) //26
  var lastcol = ws.getLastColumns(); //セルに入力のある最後の列を取得
  Logger.log(lastcol); //8

  //行挿入
  ws.insertRowAfter(2); //行2の後(行3)に行を追加
  ws.insertRowBefore(7); //行7の前(行7)に行を追加
  ws.insertRowsAfter(10,2); //行10の後(行11)に2行を追加
  ws.insertRowsBefore(20,4); //行20の前(行20)に4行を追加

  //行削除
  ws.deleteRow(15); //行15を削除
  ws.deleteRows(20,6); //行20~25を削除

  //最終行に値追加
  const append_val = ['10','佐藤','太郎','男性','30','東京'];
  ws.appendRow(append_val); //シートの最終行に「'10'」「'佐藤'」「'太郎'」「'男性'」「'30'」「'東京'」を追記

  //シートを別スプレッドシートにコピーする
  var wb_bk = SpreadsheetApp.openByName('wb_bk'); //スプレッドシート「wb_bk」を開く
  ws.copyTo(wb_bk); //「wb_bk」に「ws」をコピー

  //シートID取得
  wsid = ws.getSheetId();
  Logger.log(wsid) //'sample12345678'

  //シート名取得
  wsname = ws.getName(); //「ws」のシート名を取得
  Logger.log(wsname); //'シート1'

  //シート名変更
  wb_bk.getSheetByName(wsname+' のコピー').setName(wsname); //「wb_bk」の「*** のコピー」を「***」に変更

  //ソート
  ws.sort(1,true); //列1(A列)昇順で並び替え
  ws.sort(26,false); //列26(Z列)降順で並び替え
}
```

## スプレッドシートを開く
```js
const wbid = 'sample12345678'; //ファイルIDを宣言
var wb = SpreadsheetApp.openById(wbid); //ファイルIDからスプレッドシートを開く
const wbname = 'テストシート'; //ファイル名を宣言
var wb = SpreadsheetApp.openByName(wbname); //ファイル名からスプレッドシートを開く
```
ファイル名は被る可能性があり、その場合一致したファイル全てを配列として返す。

基本的には一意のファイルに対して処理を行いたい場合が殆どだと思われるので、IDで指定するのが安全。

## AppScriptに紐付くスプレッドシートを取得する
```js
const wb_wct = SpreadsheetApp.getActive(); //開いているスプレッドシート(スプレッドシートに紐付いたスクリプトの場合)
```

##シートを開く
```js
const wsname = 'シート1'; //シート名を宣言
var ws = wb.getSheetByName(wsname); //シート名からシートを開く
```
シートIDから指定することも可能だが、使うケースが特別考えられないのでここでは割愛する。

## セルの値を取得する
```js
var row = 2, //行2
    col = 3, //列3(C列)
    numrow = 5, //~5行
    numcol = 2; //~2列
var cell_val = ws.getRange(row,col).getValue(); //C2の値を取得
Logger.log(cell_val) //'C2の値'
var cell_vals = ws.getRange(row,col,numrow,numcol).getValue(); //C2:D6の値を取得
Logger.log(cell_val) //'C2:D6の値(配列)'
```

## セルの値を変更する
```js
var row = 2, //行2
    col = 3; //列4(D列)
ws.getRange(row,col).setValue(cell_val); //D2の値を変数「cell_val」(C3の値)に変更
```

## ブランク判定
```js
var row = 2, //行2
    col = 1; //列1(A列)
var isblank_range = ws.getRange(row,col);
if (isblank_range.isBlank()==true){ //「isBlank」を関数に対して使用すると、「true」「false」でブランクかそうでないかを返す
  Looger.log('行'+row+'はブランクです');
}else{
  Looger.log('行'+row+'はブランクではありません');
}
```

## 最終行取得
```js
var maxrow = ws.getMaxRows(); //シートに存在する最後の行を取得
Logger.log(maxrow) //1000
var lastrow = ws.getLastRows(); //セルに入力のある最後の行を取得
Logger.log(lastrow) //120
```
基本的に使われるのは「lastrow」の方。

「maxrow」は、画面上でスクロール出来る限界の行位置を示す。

スプレッドシートのデフォルトは1000。

## 最終列取得
```js
var maxcol = ws.getMaxColumns(); //シートに存在する最後の列を取得
Logger.log(maxcol) //26
var lastcol = ws.getLastColumns(); //セルに入力のある最後の列を取得
Logger.log(lastcol); //8
```
基本的に使われるのは「lastcol」の方。

「maxcol」は、画面上でスクロール出来る限界の行位置を示す。

スプレッドシートのデフォルトは26(Z列)。

## 行挿入
```js
ws.insertRowAfter(2); //行2の後(行3)に行を追加
ws.insertRowBefore(7); //行7の前(行7)に行を追加
ws.insertRowsAfter(10,2); //行10の後(行11)に2行を追加
ws.insertRowsBefore(20,4); //行20の前(行20)に4行を追加
```

## 行削除
```js
ws.deleteRow(15); //行15を削除
ws.deleteRows(20,6); //行20~25を削除
```

## 最終行に値追加
```js
const append_val = ['10','佐藤','太郎','男性','30','東京'];
ws.appendRow(append_val); //シートの最終行に「'10'」「'佐藤'」「'太郎'」「'男性'」「'30'」「'東京'」を追記
```
スプレッドシートをデータベース代わりに使う場合に、定期実行しているスクリプトの実行結果等を追記する時に使われる。

## シートを別スプレッドシートにコピーする
```js
var wb_bk = SpreadsheetApp.openByName('wb_bk'); //スプレッドシート「wb_bk」を開く
ws.copyTo(wb_bk); //「wb_bk」に「ws」をコピー
```

## シート名取得
```js
wsname = ws.getName(); //「ws」のシート名を取得
Logger.log(wsname); //'シート1'
```

## シート名変更
```js
wb_bk.getSheetByName(wsname+' のコピー').setName(wsname); //「wb_bk」の「*** のコピー」を「***」に変更
```

## ソート
```js
ws.sort(1,true); //列1(A列)昇順で並び替え
ws.sort(26,false); //列26(Z列)降順で並び替え
```
「true」で、指定した行を昇順で並び替え。

「false」で、指定した列を降順で並び替え。

# ドライブ操作全般
```js
function drive_test(){
  //フォルダを開く
  const fdid = 'sample12345678'; //フォルダIDを宣言
  var fd = DriveApp.getFolderById(fdid); //フォルダIDからフォルダを開く

  //フォルダ内のフォルダ、ファイル一覧化
  var fds = fd.getFolders(); //変数「fd」内のフォルダを配列で取得
  var files = fd.getFiles(); //変数「fd」内のファイルを配列で取得

  //フォルダ一覧全てに対して処理
  while (fds.hasNext()){
    var fd = fd.next();
    var fdname = fd.getName(); //フォルダ名を取得
    Logger.log(fdname); //フォルダ名
  }

  //ファイル一覧全てに対して処理
  while (files.hasNext()){
    var file = files.next();
    var filename = file.getName(); //ファイル名を取得
    Logger.log(filename); //ファイル名
  }

  //フォルダ作成
  fd.createFolder('ナイショのフォルダ'); //変数「fd」フォルダ内にフォルダ作成、「()」内で名前指定
}
```

## フォルダを開く
```js
const fdid = 'sample12345678'; //フォルダIDを宣言
var fd = DriveApp.getFolderById(fdid); //フォルダIDからフォルダを開く
```

## フォルダ内のフォルダ、ファイル一覧化
```js
var fds = fd.getFolders(); //変数「fd」内のフォルダを配列で取得
var files = fd.getFiles(); //変数「fd」内のファイルを配列で取得
```

## フォルダ一覧全てに対して処理
```js
while (fds.hasNext()){
  var fd = fd.next();
  var fdname = fd.getName(); //フォルダ名を取得
  Logger.log(fdname); //フォルダ名
  var fdid = fd.getId(); //フォルダIDを取得
  Logger.log(fdid); //フォルダID
}
```

## ファイル一覧全てに対して処理
```js
while (fds.hasNext()){
  var fd = fd.next();
  var fdname = fd.getName(); //フォル名を取得
  Logger.log(fdname); //フォルダ名
}
```

## フォルダ作成
```js
const fdid = 'sample12345678'; //フォルダIDを宣言
var fd = DriveApp.getFolderById(fdid); //フォルダIDからフォルダを開く
```

# フォーム操作全般
```js
function form_test(){
  //フォームを開く
  const formid = 'sample12345678'; //フォームIDを宣言
  var form = FormApp.openById(joinformid); //フォームIDからフォームを開く

  //フォーム名変更
  form.setTitle("くるくるアンケート");

  //フォームの回答用URLを取得
  var form_url =  form.getPublishedUrl();
}
```

## フォームを開く
```js
const formid = 'sample12345678'; //フォームIDを宣言
var form = FormApp.openById(joinformid); //フォームIDからフォームを開く
```

## フォーム名変更
```js
form.setTitle("くるくるアンケート");
```

## フォームの回答用URLを取得
```js
var form_url =  form.getPublishedUrl();
```

# スライド操作全般
```js
function slide_test(){
  //スライドを開く
  const slideid = 'sample12345678'; //スライドIDを宣言
  var slide_file = SlidesApp.openById(slideid); //スライドIDからスライドを開く

  //全スライドを配列で取得
  var slides = slide_file.getSlides();

  //スライド内のエレメントを配列で取得
  var slide = slides[0]; //1ページ目のスライド
  var pageElements = slide.getPageElements();
}
```

## スライドを開く
```js
const slideid = 'sample12345678'; //スライドIDを宣言
var slide_file = SlidesApp.openById(slideid); //スライドIDからスライドを開く
```

## 全スライドを配列で取得
```js
var slides = slide_file.getSlides();
```

## スライド内のエレメントを配列で取得
```js
var slide = slides[0]; //1ページ目のスライド
var pageElements = slide.getPageElements();
```

# メール操作全般
```js
function mail_test(){
  const to_address = 'hogehoge@hoge.hoge';
  const title = 'あけおめ';
  const text = '昨年はお世話になりました。\n今年もよろしくね～';
  const cc_address = 'hugahuga@hugahuga.huga,piyopiyo@piyopiyo.piyo';
  const bcc_address = 'hagehage@hagehage.hage';

  GmailApp.createDraft(to_address,title,text,{cc:cc_address,bcc:bcc_address}); // 下書き
  GmailApp.sendEmail(to_address,title,text,{cc:cc_address,bcc:bcc_address}); //送信
}
```

## メール下書き作成
```js
const to_address = 'hogehoge@hoge.hoge';
const title = 'あけおめ';
const text = '昨年はお世話になりました。\n今年もよろしくね～';
const cc_address = 'hugahuga@hugahuga.huga,piyopiyo@piyopiyo.piyo';
const bcc_address = 'hagehage@hagehage.hage';
GmailApp.createDraft(to_address,title,text,{cc:cc_address,bcc:bcc_address});
// | To      | hogehoge@hoge.hoge     |
// | CC      | hugahuga@huga.huga     |
// |         | piyopiyo@piyo.piyo     |
// | BCC     | hagehage@hage.hage     |
// | :------ | :--------------------- |
// | Title   | あけおめ                |
// | Text    | 昨年はお世話になりました |
// |         | 今年もよろしくね～      |
```
引数は「送信先」「タイトル」「本文」「パラメータ」の順。
パラメータの中に、辞書型でCC、BCCをカンマ区切りで指定可能。

## メール送信
```js
const to_address = 'hogehoge@hoge.hoge';
const title = 'あけおめ';
const text = '昨年はお世話になりました。\n今年もよろしくね～';
const cc_address = 'hugahuga@hugahuga.huga,piyopiyo@piyopiyo.piyo';
const bcc_address = 'hagehage@hagehage.hage';
GmailApp.sendEmail(to_address,title,text,{cc:cc_address,bcc:bcc_address});
```
関数名が「sendEmail」に変わるだけ。

# その他参考記事
少々長いコードになるが、やっていることは概ねここまでで説明した関数を組み合わせたもの。

## フォルダごとコピー
[GoogleAppsScript(GAS)でフォルダをコピー](http://www.googleappsscript.info/2017-07-28/drive_copy_folder.html)

使い方の例としては、各種テンプレートファイルを格納したフォルダを、それぞれの案件や作業毎に名前を変えてコピーするとか。
