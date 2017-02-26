# REVIVE USB ロータリーエンコーダ対応 スライダー/ダイヤル入力 チャタリング対策版（PID004D）
[REVIVE USB ロータリーエンコーダ対応 チャタリング対策版（PID004C）](https://github.com/ushui/REVIVE_USB_RENC_Debounce)のジョイスティック機能のうち、レバー入力をスライダー/ダイヤル入力へ置き換えたものです。  
最大6つのロータリーエンコーダを動作させることができます（1つ増やすごとに使えるボタンが2つ減ります）。  

※ロータリーエンコーダはインクリメンタル・ノンクリックタイプを想定しています。  
　エンコーダの仕様によって動作しないことがあるのでご了承ください。   
## 使い方
基盤の組み立て方や配線などは下記を参考にしてください。  
URL: <http://a-desk.jp/modules/forum_module/index.php?cat_id=3> 

1. 上記URLからファームウェア書き込みソフト「HIDBootLoader.exe」をダウンロードする。  

2. このリポジトリから「[REVIVE_USB_RENC_SD_Debounce_latest.zip](https://github.com/ushui/REVIVE_USB_RENC_SD_Debounce/raw/master/REVIVE_USB_RENC_SD_Debounce_latest.zip)」をダウンロードし、解凍する。  
「readme.txt」「REVIVE_USB_RENC_SD_Debounce_CT.exe」「REVIVE_USB_RENC_SD_Debounce_FW.hex」の3つのファイルが解凍される。  

3. 手持ちのREVIVE USBのショートピンをBOOTにしてPCへ接続する。  

4. 「HIDBootLoader.exe」を起動して「Open Hex File」ボタンから「REVIVE_USB_RENC_SD_Debounce_FW.hex」を選択し、  
「Program/Velify」ボタンを押してREVIVE USBのファームウェアを書き換える。  
6. REVIVE USBのショートピンをBOOTから戻して再度PCへ接続する。  

7. 「REVIVE_USB_RENC_SD_Debounce_CT.exe」を起動して好みの設定に変更する。  

## 設定ツールについて
「REVIVE USB, Configuration Tool」にサンプリング周期・一致検出回数・ロータリーエンコーダの設定項目を増やしたものです。  
当ファームウェア以外では動作しません。  
デフォルトでは「サンプリング周期＝3ms／一致検出回数＝10回」に設定していますが、必要であれば変更することができます。  

![REVIVE USB RENC S/D Debounce, Configuration Tool](https://raw.githubusercontent.com/ushui/REVIVE_USB_RENC_SD_Debounce/master/revive_usb_renc_sd_debounce_ct.png)  
### サンプリング周期
チャタリングノイズ除去の効果があります。  
1～174msまで設定可能で、その設定値ごとにスイッチのON/OFF読み出しを行います。  
長く設定すると長い間隔で読み出されるので、チャタリングが起こりにくくなる代わりに遅延が増加します。  
### 一致検出回数
ノイズ除去の効果があります。  
1～255回まで設定可能で、その回数分スイッチがONであれば正しい入力とみなして入力を行います。  
ONからOFFになる時にも回数分OFFであることを確認します。  
大きく設定するとチャタリングノイズ除去の精度向上や外来ノイズの除去が期待できますが、サンプリング周期に比例して遅延が増加します。  
### ロータリーエンコーダの設定
ここで指定したピンがロータリーエンコーダのA相/B相として扱われます。  
「1P/2P」から「11P/12P」までペアになっています。チェックを入れなければ通常のデジタル入力として使えます。  

また、ロータリーエンコーダには通常とは異なる一致検出回数を設定できます。  
デフォルトでは1回です。2回以上にすると早く回さないと反応しなくなったりします（これが悪いことかどうかは用途によります）。  
### 補足
ロータリーエンコーダは信号の変化が速いため、サンプリング周期や一致検出回数の設定値によっては入力が不安定（回した方向へ急な速度で入力される、回した方向とは逆にブレるなど）になりやすいです。  
エンコーダの仕様・使用環境・用途にもよりますが、この2つの適正値はシビアで、チャタリング対策をするには少し手間が必要です。  
A相/B相に割り当てたピンの設定を「マウス/上移動」「マウス/下移動」にしておくなどして、確認しながら少しずつ調整していい塩梅を見つけてください。ボタンとロータリーエンコーダで一致検出回数を個別に設定できるので、**サンプリング周期は適正値がシビアなロータリーエンコーダに合わせてからボタンの一致検出回数を増やす**ことで調整することをおすすめします。  
動作確認を「EC12E2430803」で行ったため、デフォルト値はこれに合わせています。  
### 遅延について
遅延秒数は**サンプリング周期 * 一致検出回数 - (サンプリング周期 / 2)**でおおよそ求められます。  
ロータリーエンコーダとそれ以外で別になりますのでご注意ください。  
## スライダー入力とダイヤル入力の仕様について
初期入力値は127で、0～255の値を送信します。  
入力してからサンプリング周期が訪れたタイミングで値が1ずつ増減し、255を上回ると0になり、0を下回ると255になります。  
無限に回転できるタイプのロータリーエンコーダを想定しました。  
## 動作環境について
設定ツールはWindows XP以降のOSで動作します（Windows Vistaで動作を確認しています）。  
書き込み・設定をWindows上で行ってしまえば、ファームウェア（REVIVE USB）はMacやLinux/UNIX系のOSでも動作するはずです。
## 開発環境・開発言語について
### ハードウェア
REVIVE USB (PIC18F14K50)
### ファームウェア
開発環境：MPLAB IDE 8  
開発言語：C
### ソフトウェア（設定ツール）
開発環境：Visual C# 2010 Express  
開発言語：C#
## ソースコードについて
「Assembly Desk License」ライセンスに準拠します。  

***
2017/02/27 FW ver 1.2に合わせて修正。  
2017/01/22 遅延に関する記述の修正と補足の追加。  
2017/01/21 設定ツールに関する記述を追加。  
2017/01/21 スライダー入力とダイヤル入力に関する記述を追加。  
2017/01/20 readme作成。
***
作成者： ushui（ゆーしゅい）  
Twitter: [@kaede_hrc](https://twitter.com/kaede_hrc)  
