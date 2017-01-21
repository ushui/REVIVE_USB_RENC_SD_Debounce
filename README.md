# REVIVE USB ロータリーエンコーダ対応 スライダー/ダイヤル入力 チャタリング対策版（PID004D）
[REVIVE USB ロータリーエンコーダ対応 チャタリング対策版（PID004C）](https://github.com/ushui/REVIVE_USB_RENC_Debounce)のジョイスティック機能のうち、レバー入力をスライダー/ダイヤル入力へ置き換えたものです。  
詳細については上記リンク先を参照してください。  

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

## スライダー入力とダイヤル入力の仕様について
初期入力値は127で、0～255の値を送信します。  
入力するたびに値がいくつか増減し、255を上回ると0になり、0を下回ると255になります。  
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
2017/01/21 スライダー入力とダイヤル入力に関する記述を追加。  
2017/01/20 readme作成。
***
作成者： ushui（ゆーしゅい）  
Twitter: [@kaede_hrc](https://twitter.com/kaede_hrc)  
