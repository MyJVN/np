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

### 解説

<details>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\] 1 件目から 50 件分のベンダ名を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&startItem=1&maxCountItem=50`

<br>

#### cpeName

CPE 製品名を指定します。

- cpe:/{part}:{vendor}:{product}  
  {part}フィールド ... \[ h \| o \| a \| \* \]  
  {vendor}:{product}フィールド ... CPE 製品名
- いずれか 1 つのみ指定可 \[ cpeName \| vendorId \| productId \]
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定時は "+" で連結
- URL エンコードされたエスケープシーケンス
- \[例\] Apache HTTPD の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a: apache:http_server`
- \[例\] Apache 製品の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a:apache:*`
- \[例\] Apache HTTPD と Microsoft .Net の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a: apache:http_server+cpe:/a:microsoft:.net`
- \[例\] cpe:/a:apache:xerces-c%252B%252B の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&cpeName=cpe:/a:apache:xerces-c%252B%252B`

<br>

#### vendorId

ベンダ番号を指定します。

- いずれか 1 つのみ指定可 \[ cpeName \| vendorId \| productId \]
- 複数指定時は "+" で連結
- \[例\] vendorId=100 の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&vendorId=100`

<br>

#### productId

製品番号を指定します。

- いずれか 1 つのみ指定可 \[ cpeName \| vendorId \| productId \]
- 複数指定時は "+" で連結
- \[例\] productId=10000 の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=hnd&productId=10000`

<br>

#### keyword

製品名の部分一致によりフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

</details>
<br>
<br>

## レスポンス

### 概要

- 処理成功時、Result ノードの中に VendorInfo、MyJVN 共通 Status ノードを含む XML を応答します。ただし、フィルタリング結果が 0 件の場合、Result ノードの中に MyJVN 共通 Status ノードのみを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

### 解説

```
<?xml version="1.0" encoding="UTF-8"?>
<Result version="3.3"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:mjres="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xsi:schemaLocation="http://jvndb.jvn.jp/myjvn/Results https://jvndb.jvn.jp/schema/results_3.3.xsd"
  >
  <VendorInfo
    xml:lang="表示言語 (ja:日本語、en:英語 )">
    <Vendor
      vid="ベンダ番号 (JVN iPedia におけるベンダの識別番号)"
      vname="ベンダ名"
      cpe="CPEベンダ識別子 (CPE v2.2 形式)">
      <Product
        pid="製品番号 (JVN iPedia における製品の識別番号)"
        pname="製品名"
        cpe="CPE製品識別子 (CPE v2.2 形式)" />
      <!-- フィルタリングに当てはまる製品の件数分 Product を繰り返します。 -->
    </Vendor>
    <!-- フィルタリングに当てはまるベンダの件数分 Vendor を繰り返します。 -->
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
    firstRes="応答エントリ開始位置">
    <!-- 各リクエストパラメタ -->
  </status:Status>
</Result>
```

