# getVendorList (ver. HND)
フィルタリング条件に当てはまるベンダ名(製品開発者)リストを取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getVendorList&feed=hnd&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
 
| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVendorList (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> hndを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～10,000 (getVendorListエントリ上限値)  | － | 10,000 |
| cpeName | CPEベンダ名 | cpe:/{part}:{vendor}  <br> {part}フィールド ... "\*" または (NULL) <br> {vendor}フィールド ... CPEベンダ名 (\*2) | － | － |
| keyword | キーワード | URLエンコードされたキーワード (\*3) | － | － |
| lang | 表示言語(日本語／英語) | ja:日本語、en:英語 | － | ja |

\*1)  
「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)にMyJVN API側で自動的に設定する値です。  
\*2)  
ワイルドカード "\*" 指定可  
アスキー文字  
大文字／小文字区別なし  
複数指定時は "+" で連結  
URL エンコードされたエスケープシーケンス  
cpe:/a:apache:xerces-c%2B%2B  
cpeName=cpe:/a:apache:xerces-c%252B%252B  
\*3)  
ベンダ名の部分一致によるフィルタリング  
ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)  
大文字／小文字区別なし  
charset=UTF-8  

## レスポンス
* 概要
  * 処理成功時、Resultノードの中にVendorInfo、MyJVN共通Statusノードを含むXMLを応答します。ただし、フィルタリング結果が0件の場合、Resultノードの中にMyJVN共通Statusノードのみを含むXMLを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* XMLスキーマ
  * Resultノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
  * MyJVN共通Statusノード：https://jvndb.jvn.jp/schema/status_3.3.xsd
* 例
  * [ getVendorList_hnd.xml ](examples/getVendorList_hnd.xml)

```
<?xml version="1.0" encoding="UTF-8" ?>
<Result version="3.3"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="http://jvndb.jvn.jp/myjvn/Results"
xmlns:mjres="http://jvndb.jvn.jp/myjvn/Results"
xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
xsi:schemaLocation="http://jvndb.jvn.jp/myjvn/Results　
https://jvndb.jvn.jp/schema/results_3.3.xsd ">

<VendorInfo xml:lang="表示言語">
  <Vendor vname="ベンダ名" cpe="CPEベンダ名" vid="ベンダ番号"/>
  <!-- フィルタリングに当てはまるベンダの件数分Vendorノードを繰り返します。 -->
</VendorInfo>

<status:Status
version="3.3"
method="getVendorList"
feed="hnd"
lang="表示言語"
retCd="リターンコード (0:成功時、1:エラー時) "
retMax="エントリ上限値"
errCd="エラーコード (処理成功時は空文字列) "
errMsg="エラーメッセージ (処理成功時は空文字列) "
totalRes="応答エントリ総数"
totalResRet="応答エントリ数"
firstRes="応答エントリ開始位置" >
<!-- 各リクエストパラメタ -->
</status:Status>
</Result> 
```

* フォーマット
  * xml:lang [type:string] [required]  
    Language  
    表示言語  
    Must be one of: `ja, en`  
  * vname [type:string] [required]  
    Vendor Title  
    ベンダ名  
    ```
    東京電機大学
    ```
  * cpe [type:string] [required]  
    CPE Vendor Name  
    CPEベンダ名  
    Specifies a well-formed CPE name that conforms to the CPE 2.2 specification.  
    ```
    cpe:/:dendai.ac.jp
    ```
  * vid [type:integer] [required]  
    Vendor unique number in JVN iPedia  
    JVN iPedia におけるベンダの識別番号  
