# getProductList (ver. OKA)

フィルタリング条件に当てはまる製品名リストを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

 <br>

| パラメタ名                         | 名称                   | パラメタ値                                                      | 必須 | デフォルト |
| ---------------------------------- | ---------------------- | --------------------------------------------------------------- | ---- | ---------- |
| method                             | メソッド名             | getProductList (固定)                                           | ○    | －         |
| feed                               | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定 | ○    | －         |
| startItem                          | エントリ開始位置       | 整数 1 ～応答エントリ数                                         | －   | 1          |
| maxCountItem                       | エントリ取得件数       | 整数 1 ～ 10,000 (getProductList エントリ上限値)                | －   | 10,000     |
| nameType                           | 製品識別子タイプ       | cpe, jvnpid, vid, pid のいずれかひとつ                          | －   | －         |
| productName                        | 製品識別子             | type=cpe: cpe v2.3 形式　<br> type=jvnpid: jvnpid v1.0 形式     | －   | －         |
| version <br> versionType           | バージョン             | バージョン情報                                                  | －   | －         |
| versionStart <br> versionStartType | 開始バージョン         | バージョン情報                                                  | －   | －         |
| versionEnd <br> versionEndType     | 終了バージョン         | バージョン情報                                                  |
| keyword                            | キーワード             | URL エンコードされたキーワード                                  | －   | －         |
| lang                               | 表示言語               | ja:日本語、en:英語                                              | －   | ja         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\]  
  1 件目から 50 件分のベンダ名を取得したい場合  
  `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&startItem=1&maxCountItem=50`

<br>

#### nameType

製品識別子タイプとして、cpe | jvnpid | vid | pid のいずれか一つを指定します。

#### productName (type=cpe)

製品識別子として、CPE 製品識別子を指定します。

- cpe:2.3{part}:{vendor}:{product} <br> {part}フィールド ... "h" | "o" | "a" | "\*" または (NULL) <br> {vendor}:{product}フィールド ... CPE 製品名
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし、複数指定は不可
- URL エンコードされたエスケープシーケンス
- \[例\]  
   Apache HTTPD の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=cpe&productName=cpe:2.3:a:apache:http_server`

  Apache 製品の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=cpe&productName=cpe:2.3:a:apache:*`

  cpe:/a:apache:xerces-c%252B%252B の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=cpe&productName=cpe:/a:apache:xerces-c%252B%252B`

#### productName (type=jvnpid)

製品識別子として、JVN 製品識別子を指定します。

- jvnpid:1.0::{vendor} <br> {vendor}フィールド ... JVN ベンダ名 <br> {product}フィールド ... JVN 製品名
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし、複数指定は不可
- \[例\]  
   MApache HTTPD の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=jvnpid&ProductName=jvnpid:1.0::apache:http_server`

#### productName & nameType=vid

製品識別子として、JVN iPedia におけるベンダ番号を指定します。

- \[例\]  
   Apache Software Foundation(vid=8)に関する概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=vid&ProductName=8`

#### productName & nameType=pid

製品識別子として、JVN iPedia における製品番号を指定します。

- \[例\]  
   Apache HTTPD(pid=141)に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=pid&ProductName=141`

#### version & versionType

cpe あるいは、jvnpid のバージョン(0 文字以上の ASCII 文字列)を指定します。

- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\]  
   Apache HTTPD 1.3.1.1 に関する概要情報一覧を取得したい場合
  `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&version=1.3.1.1`
- versionType  
  | オペレータ名 | 使用可パラメタ | 操作 |
  | --------------------- | ---------------------- | ---------------------- |
  | no | version | バージョンが設定されていない情報を取得 (version 値は未設定) |
  | all | version | バージョンが設定された全ての情報を取得 (version 値は未設定) |
  | equal | version | version の値に一致したバージョンを持つ情報を取得 <br> versitonType が指定されていない場合のデフォルト値 |

#### versionStart & versionStartType

cpe あるいは、jvnpid の開始バージョン(0 文字以上の ASCII 文字列)を指定します。

- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\]  
   Apache HTTPD 1.3.1.1 以上に関する概要情報一覧を取得したい場合  
  `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&versionStart=1.3.1.1&versionStartType=including`
- versionStartType
  |オペレータ名 | 使用可パラメタ | 操作|
  | --------------------- | ---------------------- | ---------------------- |
  |including | versionEndType | バージョンを含む|
  |excluding | versionEndType | バージョンを含まない|

#### versionEnd & versionEndType

cpe あるいは、jvnpid の終了バージョン(0 文字以上の ASCII 文字列)を指定します。

- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\]  
  Apache HTTPD 1.3.1.1 以下に関する概要情報一覧を取得したい場合  
  `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&versionEnd=1.3.1.1&versionEndType=including`
- versionEndType
  |オペレータ名 | 使用可パラメタ | 操作|
  | --------------------- | ---------------------- | ---------------------- |
  |including | versionEndType | バージョンを含む|
  |excluding | versionEndType | バージョンを含まない|

<br>

#### keyword

製品名の部分一致によりフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

<br>
<br>

## レスポンス

- 概要
  - 処理成功時、jvn-product-dictionary ノード、MyJVN 共通 Status ノードを含む JSON を応答します。
  - エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。
- JSON スキーマ
  - TBD
- 例
  - [ getProductList_oka.json ](examples/getProductList_oka.json)

```
{
  "jvn-product-dictionary": {
    "generator": {
      "engine": {
        "version": "4.0.0",
        "name": "MyJVN API"
      }
    },
    "title": "JVNDB 製品一覧",
    "id": "jvnpid:1.0:ipa:myjvn_api_getProductList:4.0.0",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "更新日",
    "lang": "ja",
    "author": {
      "name": "IPA",
      "uri": "https://www.ipa.go.jp/"
    },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子",
        "vid": "ベンダ番号",
        "vname": "ベンダ名",
        "cpe": "CPEベンダ識別子",
        "products": [
          {
            "product_id": "JVN製品識別子",
            "pid": "製品番号",
            "pname": "製品名",
            "version": "バージョン",
            "product_ids": {
              "cpe": "CPE製品識別子",
              "id_refs": [
                { "key": "sha256", "value": "ハッシュ値 1234DF...234" },
                { "key": "purl", "value": "Package-Manager値 rpm:/" },
                { "key": "swid", "value": "swid:ipa.go.jp+myjvn_alert+1.0.0" }
              ]
            }
          }
          { "//_comment": "product_id,pid,pnameなどのタグを繰り返します。" }
        ]
      },
      { "//_comment": "vendor_id,vid,vnameなどのタグを繰り返します。" }
    ]
  },
  "status:Status": {
    "version": "4.0.0",
    "method": "getProductList",
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

- jvn-product-dictionary

  - vendors [type:array]

    - vendor_id [type:string] [required]  
      JVN Vendor Name  
      JVN ベンダ名  
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

  - products [type:array]

    - product_id [type:string] [required]  
      JVN Product identfier  
      JVN 製品識別子  
      \[例\] `jvnpid:1.0::dendai.ac.jp:myjvn_api`
    - pid [type:integer] [required]  
      Product unique number in JVN iPedia  
      JVN iPedia における製品の識別番号  
       \[例\] `99999999991001`
    - pname [type:string] [required]  
      Product Title  
      製品名  
       \[例\] `MyJVN API`
    - version [type:string] [required]  
      Product Version  
      製品バージョン  
      \[例\] `4.0.0`
    - product_ids [type:object]
      - cpe [type:string] [required]  
        Product identifier (CPE v2.3 format)  
        CPE 製品識別子 (CPE v2.3 形式)  
        \[例\] `cpe:2.3:a:dendai.ac.jp:myjvn_api:*:*:*:*:*:*:*:*`
      - id_refs [type:array]
        - key  
          SWID、spdxid、purl、SHA256 などの参照情報名
        - value  
          SWID、spdxid、purl、SHA256 などの参照情報値
        - Package-Manager の場合  
          \[例\] `{ "key": "purl", "value": "pkg:/ipa/myjvn_api_getProductList:4.0.0" }`
        - UUID の場合  
          \[例\] `{ "key": "uuid", "value": "186ce5f8-0049-953a-37da-bc89c6f07aa1" }`
        - SWID の場合  
          \[例\] `{ "key": "swid", "value": "swid:ipa.go.jp+myjvn_api_getProductList+4.0.0" }`
        - SHA256 の場合  
          \[例\] `{ "key": "sha256", "value": "B93C2754A3B01C367CBA38E5A0C44941B39579CC0383E500C20B1D0AB13E0FFC" }`
        - TEI の場合  
          \[例\] `{ "key": "tei", "value": "urn:tei:uuid:protucts.example.com:186ce5f8-0049-953a-37da-bc89c6f07aa1" }`

  - generator [type:object]

    - engine [type:object]
      - name [type:string] [required]  
        `MyJVN API`
      - version [type:string] [required]  
        `4.0.0`

  - title [type:string] [required]  
    `JVNDB 製品一覧`
  - id [type:string] [required]  
    `jvnpid:1.0::ipa:myjvn_api_getVendorList:4.0.0`
  - link [type:string] [required]  
    `https://jvndb.jvn.jp/myjvn`
  - updated [type:string] [format:"yyyy-MM-ddTHH:mm:ss+09:00"] [required]  
    更新日  
    The date and time (timestamp) when the ProductList was created.
  - lang [type:string] [required]  
    表示言語 (ja:日本語、en:英語 )  
    Must be one of: ja, en

  - author [type:object]
    - name [type:string] [required]  
      `IPA`
    - uri [type:string] [required]  
      `https://www.ipa.go.jp/`
