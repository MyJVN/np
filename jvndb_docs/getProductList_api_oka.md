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

### 解説

<details>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\] 1 件目から 50 件分のベンダ名を取得したい場合  
  `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&startItem=1&maxCountItem=50`

<br>

#### nameType

製品識別子タイプとして、\[ cpe \| jvnpid \| vid \| pid \]のいずれか一つを指定します。

<br>

#### productName (type=cpe)

製品識別子として、CPE 製品識別子を指定します。

- cpe:2.3{part}:{vendor}:{product}  
   {part}フィールド ... \[ h \| o \| a \| \* \]  
   {vendor}:{product}フィールド ... CPE 製品名
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定は不可
- URL エンコードされたエスケープシーケンス
- \[例\] Apache HTTPD の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=cpe&productName=cpe:2.3:a:apache:http_server`
- \[例\] Apache 製品の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=cpe&productName=cpe:2.3:a:apache:*`
- \[例\] cpe:/a:apache:xerces-c%252B%252B の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=cpe&productName=cpe:/a:apache:xerces-c%252B%252B`

<br>

#### productName (type=jvnpid)

製品識別子として、JVN 製品識別子を指定します。

- jvnpid:1.0::{vendor}  
   {vendor}フィールド ... JVN ベンダ名  
   {product}フィールド ... JVN 製品名
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定は不可
- \[例\] Apache HTTPD の場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&type=jvnpid&ProductName=jvnpid:1.0::apache:http_server`

<br>

#### productName & nameType=vid

製品識別子として、JVN iPedia におけるベンダ番号を指定します。

- \[例\] Apache Software Foundation(vid=8)に関する概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=vid&ProductName=8`

<br>

#### productName & nameType=pid

製品識別子として、JVN iPedia における製品番号を指定します。

- \[例\] Apache HTTPD(pid=141)に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=pid&ProductName=141`

<br>

#### version & versionType

cpe あるいは、jvnpid のバージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart, versionEnd)の同時使用はできません。
- version の指定あり、versionType の指定なしの場合には、equal がデフォルト値となります。
- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\] Apache HTTPD 1.3.1.1 に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&version=1.3.1.1`
- versionType

  | オペレータ名 | 使用可パラメタ | 操作 |
  | --------------------- | ---------------------- | ---------------------- |
  | no | version | バージョンが設定されていない情報を取得 (version 値は未設定) |
  | all | version | バージョンが設定された全ての情報を取得 (version 値は未設定) |
  | equal | version | version の値に一致したバージョンを持つ情報を取得 <br> versitonType が指定されていない場合のデフォルト値 |

<br>

#### versionStart & versionStartType

cpe あるいは、jvnpid の開始バージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart, versionEnd)の同時使用はできません。
- versionStart,versionEnd は同時使用あるいは、いずれか一方のみの指定ができます。
- versionStart の指定あり、versionStartType の指定なしの場合には、including がデフォルト値となります。
- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\] Apache HTTPD 1.3.1.1 以上に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&versionStart=1.3.1.1&versionStartType=including`
- versionStartType

  |オペレータ名 | 使用可パラメタ | 操作|
  | --------------------- | ---------------------- | ---------------------- |
  |including | versionStartType | バージョンを含む<br> versionStartType が指定されていない場合のデフォルト値|
  |excluding | versionStartType | バージョンを含まない|

<br>

#### versionEnd & versionEndType

cpe あるいは、jvnpid の終了バージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart, versionEnd)の同時使用はできません。
- versionStart,versionEnd は同時使用あるいは、いずれか一方のみの指定ができます。
- versionEnd の指定あり、versionEndType の指定なしの場合には、including がデフォルト値となります。
- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\] Apache HTTPD 1.3.1.1 以下に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&versionEnd=1.3.1.1&versionEndType=including`
- versionEndType

  |オペレータ名 | 使用可パラメタ | 操作|
  | --------------------- | ---------------------- | ---------------------- |
  |including | versionEndType | バージョンを含む<br> versionEndType が指定されていない場合のデフォルト値|
  |excluding | versionEndType | バージョンを含まない|

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

- 処理成功時、jvn_product_dictionary、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。
- バージョン情報については、製品一覧 (製品名リスト) バージョン表記あり に登録されている製品のみを出力します。

### JSON スキーマ

- Vendor and Product Dictionary for MyJVN：https://jvndb.jvn.jp/schema/jvnpid_1.0.json

### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json",
  "jvn_product_dictionary": {
    "generator": {
      "date": "レスポンス生成日",
      "engine": {
        "version": "4.0.0",
        "name": "MyJVN API"
      }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日",
    "lang": "表示言語 (ja:日本語、en:英語 )",
    "author": {
      "name": "IPA",
      "uri": "https://www.ipa.go.jp/"
    },
    "distribution": {
      "tlp": {
        "label": "CLEAR",
        "url": "https://www.first.org/tlp/"
      }
    },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号)",
        "vname": "ベンダ名",
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::ipa",
        "products": [
          {
            "$comment": "jvnpid がバージョン情報を出力しない場合",
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api",
            "pid": "製品番号 (JVN iPedia における製品の識別番号)",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "product_ids": [
              {
                "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:*:*:*:*:*:*:*:*",
                "id_refs": [
                  {
                    "nameType": "purl",
                    "value": "Package-Manager値"
                  },
                  {
                    "nameType": "swid",
                    "value": "一意な識別子"
                  }
                ]
              }
            ]
          },
          {
            "$comment": "jvnpid がバージョン情報を出力する場合",
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api:4.0.0",
            "pid": "製品番号 (JVN iPedia における製品の識別番号)",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "version": "バージョン [例] 4.0.0",
            "product_ids": [
              {
                "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:4.0.0:*:*:*:*:*:*:*",
                "id_refs": [
                  {
                    "nameType": "purl",
                    "value": "Package-Manager値"
                  },
                  {
                    "nameType": "sha256",
                    "value": "ハッシュ値"
                  },
                  {
                    "nameType": "spdx",
                    "value": "一意な識別子"
                  },
                  {
                    "nameType": "uuid",
                    "value": "一意な識別子"
                  },
                  {
                    "nameType": "tei",
                    "value": "TEI (Transparency Exchange API) 識別子"
                  },
                  {
                    "nameType": "swid",
                    "value": "一意な識別子"
                  }
                ]
              }
            ]
          },
          { "$comment": "product_id,pid,pname などを繰り返します。" }
        ]
      },
      { "$comment": "vendor_id,vid,vname などを繰り返します。" }
    ]
  },
  "status": {
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

