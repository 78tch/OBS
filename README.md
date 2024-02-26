# OBS Studio 設定
## １．設定項目ごとの影響範囲について
OBSには、設定項目がたくさんあって、最初は全体像の把握が難しいが、大きく３つに分類できる。なにか設定をするときは、それがこの３つの設定のうち、どれに関する設定なのかを把握する必要がある。  
  
1. 「グローバル設定」：「パソコンやアプリ全体」に対する、切り替えられない設定  
2. 「ベーシック設定」：「録画の場合」「配信の場合」など、用途ごとに切替える設定（プロファイル）  
3. 「シーン」：映像素材などソースの設定。映像は、「解説したいソフトの画面」、「Webカメラ」などを、音声は「デスクトップ音声」、「マイク」などを設定する。録画したい動画の内容に応じて、その都度、設定を変更することになる。  
## ２．切り替えられない全体的な設定
1. １台のパソコンにおいて１回だけ設定する、アプリ全体に関する設定項目。「設定->一般」や「設定->詳細設定」で設定した設定内容などがそうである。
2. アプリ全体にかかる設定なので、切り替えられない。「obs-studio ->global.ini」に保存される。テキストファイルなので、読めば、どういう設定項目があるとか、どういう設定値が入っているか、などが分かる。

## ３．切り替えられる全体的な設定（プロファイル）
1. 「プロファイル」で設定できるのは、配信・録画の品質に関する項目。「解像度、fps、録画フォーマット、エンコーダ、音声サンプルレート、グローバル音声デバイス（全体で共通の音声ソース）、モニタリングデバイス」など。
2. 設定項目の場所は、「設定->出力」（エンコード設定）、「設定->音声」（オーディオ設定）、「設定->映像」（出力解像度設定）など。
3. 設定内容は設定ファイルに保存される。iniファイルで「obs-studio -> basic->profiles->プロファイル名->basic.ini」にまとめて保存される。設定ファイルを切り替えることで、設定を呼び出せる。
4. Macの設定ファイルの保存場所は「Macintosh HD->ユーザ->ユーザー名->ライブラリ（初期状態では非表示フォルダ）->Application Support->obs-studio -> basic->profiles」のなか。

### ３－１．保存形式設定
1. 「設定->出力->基本->録画->録画ファイルのパス」で指定した場所に、録画したファイルが保存される。
2. ファイル形式はデフォルトの「mkv」。mp4に変換したい場合、事後に「ファイル->録画の再多重化」で録画ファイルを選択し、「再多重化」とすると、mp4形式に変換される。
3. コーデックはH.264が一般的か。環境によってはH.265が選択可能。
4. 「設定->音声->一般->サンプルレート」は「44.1 KHz」がよいと思われる。

### ３－２．「音声ミキサー」設定
1. 「設定->音声->グローバル音声デバイス」での「デスクトップ音声」や「マイク音声」の設定は、シーンに関係なく全体に共通で有効となる。一方、「シーン->ソース」に「音声入力キャプチャ」などを追加すると、「そのシーンでのみ有効な音声」となる。「音声ミキサー」には、両方（そのシーンにおいて有効な音声ソース）が表示される。
2. Macは「デスクトップ音声」を有効にできない。「ソース」に「macOS スクリーン->画面キャプチャ」を指定すると、「音声ミキサー」に「macOS スクリーンキャプチャ」というのが表示される。ただし権限許可が必要で、「システム設定->プライバシーとセキュリティ->画面収録」で、OBSのトグルをONにすると、キャプチャが始まる。（※Ver.28以前では、「SoundFlower」などの仮想オーディオデバイスを導入しなければならなかったが、不要になった。）なお、「ウィンドウキャプチャ」や「アプリケーションキャプチャ」では、音声が録音できないようである。

### ３－３．モニター（録音される音の確認）
1. 「設定->音声->詳細設定->モニタリングデバイス」にヘッドホンなどを指定する。
2. 「音声ミキサー->オーディオの詳細プロパティ」でモニターしたい音声の「音声モニタリング」を「モニターオフ」から「モニターと出力」等にして、音声の設定を調整する。
3. 実際に録画する際には、「モニターオフ」に戻す。そのまま録画すると、元の音声とモニタ音声がずれて二重に録音されてしまう。

### ３－４．アングル（１カメ２カメ）を切り替える設定（シーンコレクション）
1. 「シーンコレクション」は、配信・録画の素材に関する設定項目で、複数の「シーン」を一括で切り替えられるようにセットにしたもの。「シーン」とは、デスクトップ画面、アプリのウィンドウ、Webカメラ、画像、字幕など「ソース」の組み合わせを指定したもの。「設定->ホットキー」（ショートカットのカスタム）も含まれる。
2. 設定内容は、各シーンの各ソース、ホットキーなど。
3. 設定内容は設定ファイルに保存される。jsonファイルで「obs-studio -> basic->scenes->シーンコレクション名.json」に保存される。jsonファイルを切り替えることで、設定を呼び出せる。
4. Macの設定ファイルの保存場所は「Macintosh HD->ユーザ->ユーザー名->ライブラリ（初期状態では非表示フォルダ）->Application Support->obs-studio -> basic->scenes」のなか。


## ４．Mac 特有
1. Ver. 28 でAppleシリコン対応等、変更点があった。  
ソースで「画面キャプチャ」「ウィンドウキャプチャ」が非推奨となり、代わりに「macOS スクリーンキャプチャ」が導入された。これのなかに、方式が「画面キャプチャ」「ウィンドウキャプチャ」「アプリケーションキャプチャ」とある。「画面キャプチャ」では、音声もキャプチャできる。  
※Macでは「設定->音声->デスクトップ音声」は「無効」となっており、ここでWindowsのように「規定」などを選択することはできない。  
2. キャプチャできない場合、「システム設定->プライバシーとセキュリティ->画面収録->OBS」でチェックをオン（許可）にする。なければ「追加」でOBSを追加する。
3. OBSのウィンドウが最前面でない場合、ホットキーが効かなくなる。有効にするには、「システム設定->プライバシーとセキュリティ->アクセシビリティ->下のアプリケーションにコンピュータの制御を許可。」でOBSのチェックをオンにして、OBSを再起動したら、OBSのウィンドウが最前面でなくても、ホットキーが有効になる。

## ５．具体例（構想段階）
### ５－１．3通りの具体例により、どういう設定があるのかを見る。
1. 1通り目：4台のWebカメラの画面を切り替えて操作する様子を動画にする。（1カメ、2カメ、3カメ、4カメに切り替えるイメージ。音声は、カメラごとの音声があり、1カメの音声を全体共通で残すイメージ。）
2. 2通り目：1種類のアプリの画面を、全体・左上の拡大・中央の拡大・右上の拡大と切り替えて操作する様子を動画にする。
3. 3通り目：4種類のアプリのウィンドウを切り替えて操作する様子を動画にする。
4. 3種類の動画は、動画フォーマット（プロファイル）は共通。ソースの取り方（シーンコレクション）が違う。→通常、録る動画によって切り替えたい、となるのは「シーンコレクション」か。


### ５－２．映像設定
1. 「シーン」を1から4まで4つ設定する。
2. ホットキーの「シーン切り替え」を「シーン1」は「Ctrl + 1」などとする。これで、4つのシーンをキーボードで切り替えられる。
3. 各シーンには適当にアプリケーションのウィンドウを指定する。これは、配信・録画のたびに、指定しなおすこと。例１：４種類のアプリ画面をそれぞれ割り当て。例２：１つのウインドウの、全体・左上の拡大・中央の拡大・右上の拡大に割り当て。

### ５－３．シーン
画面全体と、拡大左、拡大中央、タイトルスライドを用意して切り替える。
「シーン」は「画面1」「画面2」「画面3」などとして保存し、「ソース」はその都度、指定しなおせばよい。
「シーン」の切り替えが「ホットキー」でできるので、たとえば１から４までの「シーン」を作って、ホットキーをそれぞれ「Ctrl + 1」などとすれば、「シーン」の切り替えがショートカットでできるようになる。

### ５－４．映像ソースのリサイズ・トリム
1. 通常、枠をドラッグすると「縦横比を維持してリサイズ」になる。
2. Shift を押しながらドラッグすると縦横比を維持せずリサイズになる。
3. まずAltを押してから、枠をドラッグすると、トリミングになる。

### ５－５．「音声ミキサー->マイク」のフィルタ設定
1. ノイズ抑制：「RNNoise（高品質、CPU使用率高め）」にする。（初期値）
2. ゲイン：5～10 dBぐらい。
4. コンプレッサー：大きい声でも割れないように（しきい値を下げる）。小さい声でも聞き取れるように（出力ゲインを上げる）。
5. ノイズゲート：なくてもよいか。聞こえ方が不自然になりがち。
   の順にかける。
実際にしゃべって、モニターしながら、試しに録画して聞き返しながら、設定数値を調整していく。

### ５－６．コンプレッサー設定
1.  基本的には、マイクのみ「フィルタ」で設定する。調整は、マイク音声をヘッドホンで聴きながらやる。
2.  「音声ミキサー->オーディオの詳細プロパティ->（マイクの）音声モニタリング->モニターのみ（出力はミュート）」で、調整作業をする。設定が固まったら、「モニターオフ」にする。※「モニターのみ（出力はミュート）」のままだと、録画時に無音になってしまう。
3.  「マイク->フィルタ->コンプレッサー->OK->」
4.  比率：音量が閾値を超えた部分の圧縮率。大きいほど強く圧縮し音割れは防げるが不自然になる。「2～10」ぐらいとする。大きい声を出してみて、かかり具合を確認する。
5.  閾値：レベルメーターのどこを超えたら発動するか、の値。大きい声を出して、かかり始めが自然になる数値を探す。初期値は「-18dB」。黄色が「-20～-9」、赤が「-9～0」
6.  アタックタイム
7.  リリースタイム
8.  出力ゲイン
9.  サイド

## ５－７．良さげなホットキー
1. 録画開始：
2. 録画終了：（同じホットキーを指定すると、トグルにできる。）
3. 録画一時停止：
4. 録画再開：
5. マイク->ミュート：
6. マイク->ミュート解除：
7. シーン切り替え：「シーン1」に切り替え「Ctrl + 1」
8. シーン切り替え：「シーン2」に切り替え「Ctrl + 2」
9. シーン切り替え：「シーン3」に切り替え「Ctrl + 3」
10. シーン切り替え：「シーン4」に切り替え「Ctrl + 4」

## ５－８．メインウィンドウ（OBSのウィンドウ）にフォーカスがあるときもないときもホットキーを有効にする設定
1. Windows はもともとそういう動作をする。
2. Mac の場合は、「システム設定->プライバシーとセキュリティ->アクセシビリティ->下のアプリケーションにコンピュータの制御を許可。」でOBSを有効にして、OBSを再起動したら、OBSのウィンドウが最前面でなくても、ホットキーが有効になる。
3. Ubuntu の場合は、
4. 「設定->詳細設定->ホットキー」に、「ホットキーを無効にしない」という設定あり。変更する必要はあまりないと思われるが、「メインウィンドウにフォーカスがあるときはホットキーを無効にする」または「メインウィンドウにフォーカスがないときはホットキーを無効にする」と変更することができる。

## ５－９．プログラマブルキーボード設定
|キー|操作|ホットキー設定|
|:--|:--|:--:|
|KEY1|シーン1切り替え|Ctrl + Alt + 1|
|KEY2|シーン2切り替え|Ctrl + Alt + 2|
|KEY3|シーン3切り替え|Ctrl + Alt + 3|
|KEY4|シーン4切り替え|Ctrl + Alt + 4|
|KEY5|ソース1表示／非表示|Ctrl + Alt + Shift + 1|
|KEY6|ソース2表示／非表示|Ctrl + Alt + Shift + 2|
|KEY7|ソース3表示／非表示|Ctrl + Alt + Shift + 3|
|KEY8|ソース4表示／非表示|Ctrl + Alt + Shift + 4|
|KEY9|録画／終了|Ctrl + Alt + r|
|KEY10|一時停止／再開|Ctrl + Alt + s|
|KEY11|デスクトップ音声ミュート／解除|Ctrl + Alt + d|
|KEY12|マイクミュート／解除|Ctrl + Alt + m|
|K1 Left|音量小|Volume(-)|
|K1 Centre|ミュート|Mute|
|K1 Right|音量大|Volume(+)|
|K2 Left|||
|K2 Centre|||
|K2 Right|||