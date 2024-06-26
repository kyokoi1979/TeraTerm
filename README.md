# TeraTerm用マクロ
下記のことが出来ます。

* リストを読み込み、1台あるいはリスト内全てのサーバへのログイン
* 踏み台を利用した多段ログイン(2段まで)
* コマンドリストによる、ログイン後処理の自動化(あくまでコマンドを順番に実行するだけです)
* ログの自動取得
  * 年月日、ホストリストの登録名、ダイアログで入力したコメントに応じたファイル名を生成
  * 年月日ごとにディレクトリ自動生成して仕分ける機能

## Version
TeraTerm Macro v 1.0.5

## 更新履歴
1.0.5( 2024/6/23 )
- TERATERM.INIを5.2で作成
- ホストリストの書式変更
- パスワードリストに接続先情報を含めて保存するように書式変更
- TeraTermの内部コード変更に伴いリストファイルやマクロをUTF-8に変更

1.0.4( 2021/6/6 )
- ログイン先ホストをチェックするようにした(hostname -sコマンドとリストのホスト名を比較する)
- 接続エラー時の処理を変更
- 不具合修正

1.0.3( 2021/6/6 )
- パスワード情報の暗号化

1.0.2( 2021/6/6 )
1.0.1( 2021/6/5 )
1.0.0( 2021/6/3 )
- 以前作っていたマクロを現バージョンで動くようにした

## 動作確認
下記バージョンで動作確認しています。
その他でも動くと思いますがテストしていません。

5.2(2024/02/29)

## 動作に必要なもの
### ホストリスト(conf/host.list)
- ログイン情報を記入します
- リストはタブ区切り、文字コードはUTF-8(BOM無し)、改行CR+LFで保存する必要があります
- ファイルが存在しない場合、ダイアログから指定できます
- 行の先頭が#の場合はコメントとして扱います

書式については、 `ホストリスト.xlsm` を参照してください。
なお、TeraTermマクロの仕様上、ホストリストをエディタ等で開いた状態では動作しません。

#### ホストリスト.xlsm
- **マクロ付きのファイルになっていますが、TeraTerm側の仕様変更に対応出来ていないので対象範囲をコピーしてリストファイルに上書きしてください**
- **UTF-8で保存できるように書き換えれば使用可能です**


### パスワードファイル(conf/password.dat) 
- 暗号化されたパスワードが保存されていますが簡単に復元可能です
- ファイルの取り扱いには注意してください
- 将来的にもっと安全な実装がされそうな気配もあるので待ちます
  - [add：ttpmacro setpassword、getpassword暗号化機能追加 #213](https://github.com/TeraTermProject/teraterm/issues/213)
- 事前に生成できますが、対象のログイン情報が存在しなければ入力を促されます
- 事前に生成する場合は`パスワードファイル生成.ttl`を実行します

```
[Password]
[接続先]___[ユーザ名]=[暗号化されたパスワード]
192.168.0.1___root=Slhgq?IC`W-*B:mp3J==gll}
```

### TeraTerm設定ファイル(conf/TERATERM.INI)

TeraTermが起動するときの設定ファイルです。

- 環境による差異をなくすため、マクロと同じディレクトリの設定ファイルを読み込むようにしています
- 好みに応じてカスタマイズしてください
- ただし、ログ取得はマクロで行うので自動取得は入れないようにしてください

### コマンドリスト(cmdlist/command_[OS種別].list)

- OS種別ごとにコマンドを自動実行させるために利用します
- リストファイルが無ければダイアログから選択するようになっています
- 中身が空で良いので必ず用意してください
