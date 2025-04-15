# getProductList (ver. HND)

フィルタリング条件に当てはまる製品名リストを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

 <br>

| パラメタ名   | 名称                   | パラメタ値                                                      | 必須 | デフォルト |
| ------------ | ---------------------- | --------------------------------------------------------------- | ---- | ---------- |
| method       | メソッド名             | getProductList (固定)                                           | ○    | －         |
| feed         | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> hnd を指定 | ○    | －         |
| startItem    | エントリ開始位置       | 整数 1 ～応答エントリ数                                         | －   | 1          |
| maxCountItem | エントリ取得件数       | 整数 1 ～ 10,000 (getProductList エントリ上限値)                | －   | 10,000     |
| cpeName      | CPE 製品名             | cpe v2.2 形式                                                   | －   | －         |
| vendorId     | ベンダ番号             | 整数                                                            | －   | －         |
| productId    | 製品番号               | 整数                                                            | －   | －         |
| keyword      | キーワード             | URL エンコードされたキーワード                                  | －   | －         |
| lang         | 表示言語               | ja:日本語、en:英語                                              | －   | ja         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\]  
   1 件目から 50 件分のベンダ名を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&startItem=1&maxCountItem=50`

#### cpeName

CPE 製品名を指定します。

- cpe:/{part}:{vendor}:{product}  
  {part}フィールド ... \[ h \| o \| a \| \* \]  
  {vendor}:{product}フィールド ... CPE 製品名
- いずれか 1 つのみ指定可 \[ cpeName \| vendorId \| productId \]
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定時は "+" で連結
- URL エンコードされたエスケープシーケンス
- \[例\]  
   Apache HTTPD の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a: apache:http_server`

  Apache 製品の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a:apache:*`

  Apache HTTPD と Microsoft .Net の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a: apache:http_server+cpe:/a:microsoft:.net`

  cpe:/a:apache:xerces-c%252B%252B の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a:apache:xerces-c%252B%252B`

#### vendorId

ベンダ番号を指定します。

- いずれか 1 つのみ指定可 \[ cpeName \| vendorId \| productId \]
- 複数指定時は "+" で連結
- \[例\]  
   vendorId=100 の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&vendorId=100`

#### productId

製品番号を指定します。

- いずれか 1 つのみ指定可 \[ cpeName \| vendorId \| productId \]
- 複数指定時は "+" で連結
- \[例\]  
   productId=10000 の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&productId=10000`

#### keyword

製品名の部分一致によりフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

<br>
<br>

## レスポンス

### 概要

- 処理成功時、Result ノードの中に VendorInfo、MyJVN 共通 Status ノードを含む XML を応答します。ただし、フィルタリング結果が 0 件の場合、Result ノードの中に MyJVN 共通 Status ノードのみを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

### 例

- [ getProductList_hnd.xml ](../examples/getProductList_hnd.xml)

### 解説

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
  <Vendor vid="ベンダ番号" vname="ベンダ名" cpe="CPEベンダ名">
    <Product pid="製品番号" pname="製品名" cpe="CPE製品名"/>
    <!-- フィルタリングに当てはまる製品の件数分Productノードを繰り返します。 -->
  </Vendor>
  <!-- ベンダの件数分 Vendor ノードを繰り返します。 -->
</VendorInfo>

<status:Status
version="3.3"
method="getProductList"
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

- VendorInfo

  - xml:lang [type:string] [required]  
    Language  
    表示言語  
    Must be one of: `ja, en`
  - Vendor

    - vid [type:integer] [required]  
      Vendor unique number in JVN iPedia  
      JVN iPedia におけるベンダの識別番号  
      \[例\] `99999999991`
    - vname [type:string] [required]  
      Vendor Title  
      ベンダ名  
      \[例\] `東京電機大学`
    - cpe [type:string] [required]  
      CPE Vendor Name  
      CPE ベンダ名  
      CPE Vendor Name that based on the CPE 2.2 specification.  
      \[例\] `cpe:/:dendai.ac.jp`

    - Product
      - pid [type:integer] [required]  
        Product unique number in JVN iPedia
        JVN iPedia における製品の識別番号  
        \[例\] `99999999991001`
      - pname [type:string] [required]  
        Product Title  
        製品名  
        \[例\] `MyJVN API`
      - cpe [type:string] [required]  
        Product identfier by CPE 2.2  
        CPE 製品名  
        CPE Vendor Name that based on the CPE 2.2 specification.  
         \[例\] `cpe:/a:dendai.ac.jp:myjvn_api`
