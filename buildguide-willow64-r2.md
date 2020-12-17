# Willow64 ビルドガイド

この度は Willow64組み立てキットをお買い上げいただきありがとうございます。

本ドキュメントはWillow64を組み立てるための手順について記しています。
組み立てを始める前に本書をよくお読みいただき全体をご理解してから作業を始めることをおすすめします。


## 想定するユーザスキル
- パソコン操作 (必須)

  Windows PC もしくは MACが必要です。
  このキットの作者はWindows10を利用しているため、ビルドガイドもその環境を想定した記述となっていますが、MACについてもほとんど同じですので各自で読み替えてください。

  PC環境の設定については参考となる情報を本書の末尾にまとめますので必要に応じて参照してください。

- はんだ付け (必須)

  本組み立てキットは、はんだ付けの工程が必要です。
  表面実装タイプの部品を取り扱う箇所があるため 組み立て難易度としてはやや高い部類になります。
  はんだ付けの経験があることに越したことはありませんが、初めてでも前向きなやる気があれば問題ありません。
  はんだ付けについての様々な情報やテクニックについては本書末尾にまとめていますので、必要に応じて参照してください。
  
- 黒い画面の操作 (あると良い)

  キーボードの頭脳となるマイクロコンピュータへファームウェアを書き込む作業があります。
  本ドキュメントではなるべく簡易な方法について説明をしますが、本格的に本キーボードの機能を利用するには、”黒い画面”(コンソールからのCUI操作) と向き合う必要がでてきます。
  こちらについてもネット上に様々な優れた情報が存在するので、本書末尾にまとめますので必要に応じて参照してください。

- トラブル解決力 (なるべく必要)

  こういった繊細なガジェットを作り上げるときには、様々なトラブルにぶち当たる可能性があります。
  本書でもなるべくトラブルシュートが可能な情報を載せるようにしていますが全てを網羅することはできません。
  その時はユーザ自身で解決までもっていく必要があるということを念頭に置いてください。 

  自身でトラブル解決をしていく熱意とスキルは重要なポイントとなります。
  問題を一気に解決しようと焦ることなく、自分の行った行為に対し自己レビューし、く一つ一つ被疑箇所を切り分けていくとった地道な作業は問題解決の王道であり、その過程でスキルが蓄積されていくものです。

  作者やコミュニティーに質問する前に、ネットなどで過去事例を調べることは最低限必要なことです。大抵のことはこれで解決できるはずです。
  質問を投げる場合でも、回答を得られやすい上手な質問をまとめるスキルが必要です。


## 準備
組み立てを始める前に、本章の内容を確認し準備が十分に整っていることを確認してから次に進んでください。
### 組み立てキット内容物
パッケージを開けたら、まず内容物が正しく揃っているかを確認します。

- PCB  (プリント基板) 右手 1、左手 1
- マウントプレート(ステンレス) 右手 1、左手 1
- ボトムプレート (アクリル) 右手 1、左手 1
- アンダーカバー (アクリル) 右手 、，左手 1
- スイッチソケット 128
- ダイオード(SMD) 128 (予備としてプラス少々)
- タクトスイッチ  2
- TRRSジャック  2
- ネジ(M2 L3)  32
- ネジ(M2 L5)  8
- ネジ(M2 L9) 6
- スペーサ(3.5mm) 8
- スペーサ(8.0mm) 6
- ゴム足 8
  
### 組み立てキット以外に必要な部品
組み立てキット以外に必要な部品が揃っていることを確認します。
なるべく日本の自作キーボード界隈でよく使われている部品を選定しているので
本書末尾のショップ一覧から入手可能です。

#### 必ず必要な部品
- ProMicro 
  
  キーボードの頭脳として、左右一つづつ。

- スプリングピンヘッダ 4

  ProMicroをPCBに装着する際に取り外し可能とするパーツです。
  スプリングピンヘッダがない場合は、通常のピンヘッダをPCb側にはんだ付けすることで代用できますがProMicrowo取り外すことはできなくなります。

- Cherry MK互換スイッチ  64

  自作キーボードの醍醐味の部分なのでお好みで準備ください。chockには非対応です。

- キーキャップ

  ここもこだわりポイントです。ANSI USタイプが適合します。

- TRRSケーブル (もしくはTRSケーブル)  1
  左右に別れたキーボードを連結します。

- USB B microケーブル 1

  パソコンとキーボードを接続するのに利用します。

(以下オプション)
- スタビライザ(2U)  2

  なくてもキーボードとしては機能します。スタビライザがあるとShiftキーの片側を押したときに斜めになったりしないので入力が安定するかもしれません。
  安いスタビライザを使うとカチャカチャとうるさい場合があるのでお好みによって調達してください。

- LED (マイコン内蔵RGB LED SK6812MINI-E) 64

  なくてもキーボードとしての機能は十分ですが、LEDを実装すると  キーボードを光で演出する、動作モードを光で知らせる、CAPSLOCKやNUMLOCK状態を表示する、といったことが可能となります
  部品の入手や実装は少し大変ですが、所有する満足度も上がるのお勧めします。

- エポキシ接着剤

  ProMicroのUSBコネクタの強度が弱くすぐ取れてしまうことが多いので、ほぼ必須です。
  (注意や対処を怠ると、最初の動作確認中の段階でも ProMicroのUSBコネクタが断線してしまうう場合がありますので注意ください) 
### 必要なツール
電子工作の基本的なツールを用意します。

- はんだごて

- はんだ

- ピンセット / 逆作用ピンセット

  極小さいパーツをハンダづけするため、必須です。

- 精密ドライバ

  M2サイズ

- テスタ(マルチメータ)

  はんだ付けした部分の導通確認に利用します。

以降はお好みに応じて用意します 
- はんだ付けの周辺グッズ
  
  コテ台、スポンジ、作業マット、吸煙ファン、等

- ハンダ吸い取り線

  はんだ付けは失敗しない、という方は不要です

- フラックス

  表面実装部品を扱うため強い推奨です。

- フラックス洗浄剤

  フラックスを使うと基板表面が茶色く汚れます。白い基板のため汚れが目立ちますし、中長期的な品質維持のためにもはんだ付け後にフラックス洗浄することをお勧めします。

- ラジオペンチ

  スペーサをネジで固定するときの保持等に。

- マスキングテープ

  はんだ付けする際のパーツの固定等に。アクリルプレートの保護シートを剥がすときに便利です。
 

## 組立工程概要
組み立て全体の工程について概要を示します。
作業段取りのイメージを頭に入れてから作業を開始するようにしましょう。

0. ファームウェア書き込み環境の準備
1. ProMicroの組み立て
2. 確認用ファームウェアの書き込み
3. TRRSコネクタとリセットスイッチの取り付け
4. ProMicroの取り付け
5. LEDのはんだ付け(オプション)
6. ダイオードのはんだ付け
7. スイッチソケットのはんだ付け
8. スイッチの動作確認
9. ケースの組み立て
10. キースイッチとキーキャップの取り付け
11. 動作確認と本稼働用のファームウェアの書き込み

## 組み立て作業詳細

### 0. ファームウェア書き込み環境の準備

##### QMK Toolboxのダウンロードとインストール
 QMK Toolboxは、ファームウェアをマイコン(ProMicro)へ書き込むために必要となります。
 (既に環境がある方は不要です)

下記から QMK Toolboxをダウンローして自身のPCへインストールします。

https://qmk.fm/ja/toolbox/

インストール方法はサイトの情報に従ってください。

#### Willow64用のファームウェアをダウンロード
Willow64のファームウェアは、 動作確認用、標準キーマップおよび作者常用の参考用キーマップの3種類が公開されています(2020年12月現在)。

下記のURLからファームウェア(拡張子 .hex)をPCでダウンロードしておきます。

### 1. ProMicroの組み立て
キーボード本体を組み立てる前にProMicroのはんだ付けと動作確認用ファームウェアの書き込みを行います。

下記作業を、2個のProMicroに対して実施します。

#### スプリングピンヘッダのはんだ付け

#### USBコネクタ周辺の補強(オプション)

### 2. 動作確認用ファームウェアの書き込み
エポキシ接着剤で補強を行った場合は十分硬化してから作業します。

下記作業を、2個のProMicroに対して実施します。

#### USBケーブルでPCとProMicroを接続します
ProMicroが通電すると基板上の緑色(ロットによっては赤色)のLEDが点灯します。

#### PC上で QMK Tookboxを起動します

#### ファームウェアファイルを指定し、Auto-Flashの部分をチェックします

#### ピンセットなどを使ってProMicroのリセット端子をショートさせます

QMK Toolbox上で書き込みログが表示されるので注視します。

以上の作業を 2個のProMicroに対して行います

3. TRRSコネクタとリセットスイッチの取り付け

TRRSコネクタとリセットスイッチ(タクトスイッチ)はPCBの裏側にはんだ付けします。

TRRSコネクタの足をPCBの穴にあわせて裏側から差し込み
表側からはんだ付けします。

タクトスイッチの足をPCBの穴に合わせて裏側から差込、お手側からはんだ付けします。タクトスイッチは向きの指定はありません。

はんだ付けのためひっくり返必要があるので、落ちるような場合はマスキングテープ等で仮止めします。

部品に浮きが生じないように気をつけます。

はんだ付けが終わったら、


### 4. LEDのはんだ付け(オプション)

左右のPCB 合計64箇所にLEDをはんだ付けます。


裏から表側に発光面が来るよう、裏面から四角い穴にはめ込みます。
PCBの三角のマークとLEDの足が短い端子をあわせます。

注: PCBの裏表、LEDの装着面、LEDの裏表、LEDの向き 一つでも間違うとLEDは発光しません。
LEDはチェーンのように連鎖した接続となります。途中で一つ間違いや不良があるとそれ以降のLEDは全て動作しないので注意します。

PCBのランドとLEDの足 4箇所をはんだ付けします。 フラックスを塗布するとハンダが乗りやすいです。

長時間はんだごてを押し当てると、LEDが高温になり破損するので注意が必要です。

LEDをはんだ付けした後、ProMicroとPCをUSBケーブルで接続すると、LEDテストモードが動作し赤青緑のライトが交互に光ります。

全てのLEDが同期して光れば試験はパスです。

途中から光らないところがある場合、光らない箇所のLED もしくはその一つ前にLEDのはんだ付けに問題がある場合が多いのでよく見直してください。

ピカピカと不規則に点滅を繰り返すような場合も、はんだ付け不良が原因の場合がほとんどです。問題のある箇所の前後をレビューしてください。


### 4. ダイオードのはんだ付け

左右のPCB 合計64箇所にダイオードをはんだ付けします。

はんだ付けはPCBの裏側に行います。

ダイオードは極性があるので、ダイオードの向きとPCBのシルクを合わせます。

表面実装型のダイオードのはんだ付けはちょっとしたコツが入ります。参考URLの情報を参考にしてみてください。

ダイオードのはんだ付けは、後述のスイッチソケットのハンダ付けより先に行うことをお勧めします。
スイッチソケットを先に取り付けるとダイオードのはんだ付けが難しくなります。

### 5. スイッチソケットのはんだ付け

左右のPCB 合計64箇所にスイッチソケットをはんだ付けします。

はんだ付けはPCBの裏側に行います。

PCBのランドに予備ハンダを盛り、ソケットの上からはんだごてを押し当てて取り付けます。

部品の浮きがないように気をつけてください。

取り付けの向きにも注意してください。

### 6．キーの動作確認
ケースを組み立てたあとからはんだ付け不良が見つかると修正に手間がかかるため、この段階で各箇所のキーが正しく反応するか動作確認を行います。

PC側で、ブラウザを開き次のURLを開きます。
https://config.qmk.fm/#/test

ProMicroをUSBケーブルでPCと接続します。

PCBの表側から、ピンセットの先端をスイッチソケットの穴に差し込みます。
ピンセットを用いる代わりに本物のスイッチを差し込んで確認しても構いません。
(後述の組立工程のため、確認後はスイッチは一度全て取り外す必要があります)

ブラウザ上の表示でキーが押された状態になることを確認します。

上記の作業を、左右のPCBに対して行います。
動作確認が完了したら、一度USBケーブルを抜きます。


一部のキーが反応しない場合
確認用ファームウェアは全てのキーが文字コードを直接返す設定となっているので、一部のキーが反応しない場合はどこかのはんだ付けに不良がある可能性が大きいです。

全くどのキーも反応しない場合
ProMicroのはんだ付け不良、そもそもProMicroがPCBに挿入されていない、ファームウェアが正しく書き込めていない、などの原因が考えられます。一つづつ前工程に戻って確認してください。

スイッチの動作確認が取れたら次の工程へ進みます。

### 7. ケースの組み立て

トッププレートに写真を参考に表側からネジ(M2 L3)を差し込み、裏側にスペーサ(3.5mm)をネジ止めします(4箇所)。

動作確認の済んだPCBをあわせ、PCB裏側からネジ(M2 L3)で結合します。

トッププレートに写真を参考に表側からネジ(M2 L3)を差し込み、裏側からスペーサ(8.0mm)をネジ止めします(8箇所)。

裏面を表に返し、ボトムプレートを重ねます。
更にアンダーカバープレートを合わせます。

写真を参考に ネジ止めします。
ネジ(M2 L5)とネジ(M2 L9)の二種類のネジを適切な箇所に使います。

ゴム足を貼り付けます。

上記の作業を、左右それぞれに行います。

### 10. キースイッチとキーキャップの取り付け

キースイッチを取り付けます。

スイッチのピンは曲がりやすいので注意します。
まっすぐ上から慎重に差し込むようにします。

スイッチはメーカやモデルによって微妙にサイズが異なるため、プレートの穴はややきつめに仕上げてあります。

キースイッチにキーキャップを取り付けます。
以上で組み立ては完成です。

### 11.  動作確認と本稼働用のファームウェアの書き込み

TRRSケーブルを左右のキーボードのコネクタに差し込みます。
USBケーブルを左側のキーボードに差し込みます。

LEDを実装している場合、この段階でテストモードで点灯することを確認します。

PC側で、ブラウザを開き次のURLを開き、全てのキーが反応することを確認します。
https://config.qmk.fm/#/test

確認が取れたら、本番用ファームウェアの書き込みを行います。


PC側で、QMK Toolboxを起動し、本番用ファームウェア
(willow64_r2_default.hex)をオープンします。
Auto_flushをチェックします。

USBケーブルを左手側のキーボードに差し込みます

裏側にあるリセットスイッチを押して書き込みを実行します。

書き込みが終わったら、USBを右側に指しリセットスイッチを押し書き込みを行います。

USBケーブルを左手に差し替えます。

これで本番用ファームウェアの書き込みは完了です。
改めて動作確認を行ってください。


## 参考情報

### キーボードパーツショップ(日本)


自作キーボード専門
代表的なショップを列挙します(順不同)。前述のみ立てキット以外に必要な部品はほぼ揃います。

- 遊舎工房
- TALP KEYBOARD
- 縁キーボードファクトリ

- 秋月電子通商

 前述のショップでSK6812MINI-Eが品切れの場合はこちらでも取り扱いがあります。


### はんだ付け技能

### 自作キーボード作成ノウハウ

