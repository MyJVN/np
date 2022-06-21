# getProductList (ver. OKA)
フィルタリング条件に当てはまる製品名リストを取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getProductList&feed=oka&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。

| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getProductList (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> okaを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～10,000 (getProductListエントリ上限値)  | － | 10,000 |
| productName | 製品名 | CPE,SWID,SPDX,purl,Hash (\*2) | － | － |
| vendorId | ベンダ番号 | 整数(半角数字) | － | － |
| productId | 製品番号 | 整数(半角数字) | － | － |
| keyword | キーワード | URLエンコードされたキーワード (\*3) | － | － |
| lang | 表示言語(日本語／英語) | ja:日本語、en:英語 | － | ja |

\*1)  
「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)にMyJVN API側で自動的に設定する値です。  
\*2)  
\*3)  
ベンダ名の部分一致によるフィルタリング  
ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)  
大文字／小文字区別なし  
charset=UTF-8  

## レスポンス
* 概要
  * 処理成功時、jvn-product-dictionaryノード、MyJVN共通Statusノードを含むJSONを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* JSONスキーマ  
  * TBD 
* 例
  * [ getProductList_oka.json ](examples/getProductList_oka.json)

```
{
    "jvn-product-dictionary": {
        "generator": {
            "product_name": "MyJVN API",
            "product_version": "oka",
            "schema_version": "4.0",
            "language": "ja-JP",
            "updated": "更新日"
        },
        "title": "MyJVN getProductList API",
        "id": "jvnpid:1.0:ipa:myjvn_api_getProductList:4.0.0.0.0",
        "link": "https://jvndb.jvn.jp/apis/myjvn/",
        "author": {
            "name": "IPA",
            "uri": "https://www.ipa.go.jp/"
        },
        "vendors": [
            {
                "vendor_id": "ベンダ識別子",
                "vid": "ベンダ番号",
                "vname": "ベンダ名",
                "cpe": "CPEベンダ名",
                "products": [
                    {
                        "product_id": "製品識別子",
                        "pid": "製品番号",
                        "pname": "製品名",
                        "product_ids": [
                            {"swid": "SWID識別子"},
                            {"cpe": "CPE製品名"},
                            {"spdxid": "SPDX識別子"},
                            {"purl": "purl識別子"},
                            {"sha256": "ハッシュ値"}
                        ]
                    },
                    {"//_comment": "product_id,pid,pnameなどのタグを繰り返します。"}
                ]
            },
            {"//_comment": "vendor_id,vid,vnameなどのタグを繰り返します。"}
        ]
    },
    "status:Status": {
        "version": "4.0",
        "method": "getProductList",
        "feed": "hnd",
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
