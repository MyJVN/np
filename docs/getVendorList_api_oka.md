# getVendorList (ver. OKA)

フィルタリング条件に当てはまるベンダ名(製品開発者)リストを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getVendorList&feed=oka&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

 <br>

| パラメタ名   | 名称                   | パラメタ値                                                      | 必須 | デフォルト |
| ------------ | ---------------------- | --------------------------------------------------------------- | ---- | ---------- |
| method       | メソッド名             | getVendorList (固定)                                            | ○    | －         |
| feed         | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定 | ○    | －         |
| startItem    | エントリ開始位置       | 整数 1 ～応答エントリ数                                         | －   | 1          |
| maxCountItem | エントリ取得件数       | 整数 1 ～ 10,000 (getVendorList エントリ上限値)                 | －   | 10,000     |
| nameType     | ベンダ識別子タイプ     | cpe, jvnpid のいずれかひとつ                                    | －   | －         |
| vendorName   | ベンダ識別子           | type=cpe: cpe v2.3 形式　<br> type=jvnpid: jvnpid v1.0 形式     | －   | －         |
| keyword      | キーワード             | URL エンコードされたキーワード                                  | －   | －         |
| lang         | 表示言語               | ja:日本語、en:英語                                              | －   | ja         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\]  
   1 件目から 50 件分のベンダ名を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVendorList&feed=oka&startItem=1&maxCountItem=50`

<br>

#### nameType

ベンダ識別子タイプとして、\[ cpe \| jvnpid \]のいずれか一つを指定します。

#### vendorName (type=cpe)

ベンダ名として、CPE ベンダ識別子を指定します。

- cpe:2.3:{part}:{vendor}  
   {part}フィールド ... \[ \* \| (NULL) \]  
   {vendor}フィールド ... CPE ベンダ名
- アスキー文字、大文字／小文字区別なし、複数指定は不可
- URL エンコードされたエスケープシーケンス
- \[例\]  
   Microsoft の場合  
   `https://jvndb.jvn.jp/myjvn?method=getVendorList&feed=oka&type=cpe&vendorName=cpe:2.3::microsoft`

  cpeName=cpe:2.3::%25%40mail の場合  
   `https://jvndb.jvn.jp/myjvn?method=getVendorList&feed=oka&type=cpe&vendorName=cpe:2.3::%40mail`

#### vendorName (type=jvnpid)

ベンダ識別子として、JVN ベンダ識別子を指定します。

- jvnpid:1.0::{vendor}  
   {vendor}フィールド ... JVN ベンダ名
- アスキー文字、大文字／小文字区別なし、複数指定は不可
- \[例\]  
   Microsoft の場合  
   `https://jvndb.jvn.jp/myjvn?method=getVendorList&feed=oka&type=jvnpid&vendorName=jvnpid:1.0::microsoft`

<br>

#### keyword

ベンダ名の部分一致によりフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

<br>
<br>

## レスポンス

### 概要

- 処理成功時、jvn_product_dictionary、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250414
  [ jvnpid_1.0.json ](../schema/jvnpid_1.0.json)

### 例

- [ getVendorList_oka.json ](../examples/getVendorList_oka.json)

### 解説

```
{
  "jvn_product_dictionary": {
    "generator": {
      "engine": {
        "version": "4.0.0",
        "name": "MyJVN API"
      }
    },
    "title": "JVNDB ベンダ一覧",
    "id": "jvnpid:1.0::ipa:myjvn_api_getVendorList:4.0.0",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "更新日",
    "lang": "ja",
    "author": {
      "name": "IPA",
      "uri": "https://www.ipa.go.jp/"
    },
    "vendors": [
      {
        "vendor_id": "JVNベンダ名",
        "vid": "ベンダ番号",
        "vname": "ベンダ名",
        "cpe": "CPEベンダ名"
      },
      { "$comment": "vendor_id,vid,vnameなどを繰り返します。" }
    ]
  },
  "status": {
    "version": "4.0.0",
    "method": "getVendorList",
    "feed": "oka",
    "lang": "表示言語",
    "retCd": "リターンコード (0:成功時、1:エラー時)",
    "retMax": "エントリ上限値",
    "errCd": "エラーコード (処理成功時は空文字列)",
    "errMsg": "エラーメッセージ (処理成功時は空文字列)",
    "totalRes": "応答エントリ総数",
    "totalResRet": "応答エントリ数",
    "firstRes": "応答エントリ開始位置",
    "各リクエストパラメタ": "各リクエストパラメタ値"
  }
}
```

<br>

- jvn_product_dictionary [type:object]

  - vendors [type:array]

    - vendor_id [type:string] [required]  
      JVN Vendor Name (jvnpid 1.0 format)  
      JVN ベンダ名 (jvnpid 1.0 形式)  
      \[例\] `jvnpid:1.0::dendai.ac.jp`
    - vid [type:integer] [required]  
      Vendor unique number in JVN iPedia  
      JVN iPedia におけるベンダの識別番号  
      \[例\] `99999999991`
    - vname [type:string] [required]  
      Vendor Title  
      ベンダ名  
      \[例\] `東京電機大学`
    - cpe [type:string] [required]  
      CPE Vendor Name (CPE v2.3 format)  
      CPE ベンダ名 (CPE v2.3 形式)  
      \[例\] `cpe:2.3::dendai.ac.jp`

  - generator [type:object]

    - engine [type:object]
      - name [type:string] [required]  
        `MyJVN API`
      - version [type:string] [required]  
        `4.0.0`

  - title [type:string] [required]  
    `JVNDB ベンダ一覧`
  - id [type:string] [required]  
    `jvnpid:1.0::ipa:myjvn_api_getVendorList:4.0.0`
  - link [type:string] [required]  
    `https://jvndb.jvn.jp/myjvn`
  - updated [type:string] [format:"yyyy-MM-ddTHH:mm:ss+09:00"] [required]  
    The date and time (timestamp) when the VendorList was created.
    更新日
  - lang [type:string] [required]  
    表示言語 (ja:日本語、en:英語 )
    Must be one of: ja, en

  - author [type:object]
    - name [type:string] [required]  
      `IPA`
    - uri [type:string] [required]  
      `https://www.ipa.go.jp/`

- status [type:object]
