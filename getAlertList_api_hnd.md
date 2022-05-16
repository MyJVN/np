# getAlertList (ver. HND)
注意警戒情報一覧を取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=hnd&パラメタ名=パラメタ値&...
  * リクエスト URL は、HTTPS の GET および POST に対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし ("method="など) の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。

| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト[1] |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getAlertList (固定) | ○ | － |
feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 hnd を指定 | ○ | －
startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～50 (getAlertListエントリ上限値) | － | 50 |
datePublished | 更新日年 | 半角整数4桁 | － | － |
dateFirstPublished | 発行日年 | 半角整数4桁 | － | － |
cpeName | CPE 製品名 |  [ cpeName \| vendorId \| productId ] | － | － |
ft | 応答フォーマット | xml または json | － | － |
