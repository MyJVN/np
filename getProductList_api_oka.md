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
| productName | 製品名 | cpe, nvdid, swid, spdxid, purl, Hash (\*2) | － | － |
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
                        "product_id": "JVN製品識別子",
                        "pid": "製品番号",
                        "version": "バージョン",
                        "pname": "製品名",
                        "product_ids": [
                            {"cpe": "CPE製品名"},
                            {"nvdid": "UUID値"},
                            {"swid": "グローバルなユニークID"},
                            {"spdxid": "SPDXID値"},
                            {"purl": "Package-Manager値"},
                            {"alg": "ハッシュ値"}
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
* jvn-product-dictionary

  * vendors [type:array]
    * vendor_id [type:string] [required]  
      JVNPID Vendor Name  
      JVNPIDベンダ名  
      ```
      jvnpid:1.0:dendai.ac.jp
      ```
    * vid [type:integer] [required]  
      Vendor unique number in JVN iPedia  
      JVN iPedia におけるベンダの識別番号  
      ```
      12345
      ```
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

  * products [type:array]  
    * product_id [type:string] [required]  
      JVNPID Product Name  
      JVNPID製品名  
      ```
      jvnpid:1.0:dendai.ac.jp:myjvn_api:4.0.0.0.0
      ```
    * pid [type:integer] [required]  
      Product unique number in JVN iPedia  
      JVN iPedia における製品の識別番号  
      ```
      67891
      ```
    * version [type:string]  
      Version  
      バージョン 
      ```
      4.0.0
      ```
    * pname [type:string] [required]  
      Product Title  
      製品名  
      ```
      MyJVN API
      ```
    * product_ids [type:array]
    * cpe [type:string] [required]  
      Product identfier by CPE 2.3  
      CPE製品名  
      ```
      cpe:2.3:a:dendai.ac.jp:myjvn_api:4.0.0:*:*:*:*:*:*:*
      ```
    * nvdid [type:string]  
      Product identfier in NVD  
      NVD製品識別子
      ```
      c1a2dcb3-4a17-44b5-96c8-e1e839a44061
      ```
    * swid [type:string]  
      Product identfier by SWID (=Product Identifier by Vendor)   
      SWID製品識別子 (=ベンダが割り当てた製品識別子)  
      ```
      c1a2dcb3-4a17-44b5-96c8-e1e839a44061
      ```
    * spdxid [type:string]  
      SPDX identfier  
      SPDX識別子
      ```
      SPDXRef-c1a2dcb3-4a17-44b5-96c8-e1e839a44061
      ```
    * purl [type:string]  
      Product identfier by Package-Manager 
      Package-Manager製品識別子 
      ```
      pkg:rpm/dendai.ac.jp/myjvn@4.0.0
      ```
    * [type:object]
      * alg [type:enum (of string)]  
        Must be one of:MD5, SHA-1, SHA-256, SHA-384, SHA-512, SHA3-256, SHA3-384, SHA3-512, BLAKE2b-256, BLAKE2b-384, BLAKE2b-512, BLAKE3
      * content [type:string] [required]  
        Must match regular expression: ^([a-fA-F0-9]{32}|[a-fA-F0-9]{40}|[a-fA-F0-9]{64}|[a-fA-F0-9]{96}|[a-fA-F0-9]{128})$
          ```
          7eb51a1d04047d4742ffd69bb88500e2
          ```

  * generator [type:object]
    * product_name [type:string] [required]  
      Must be one of: `MyJVN API`  
    * product_version [type:string] [required]  
      Must be one of: `oka`  
    * schema_version [type:string] [required]  
      Must be one of: `4.0`  
    * language [type:string] [required]  
      Must be one of: `ja-JP, en-US`  
    * updated [type:string] [required]  
      The date and time (timestamp) when the VendorList was created.  

  * title [type:string] [required]  
    Must be one of: `MyJVN getVendorList API`  
  * id [type:string] [required]  
    Must be one of: `jvnpid:1.0:ipa:myjvn_api_getVendorList:4.0.0.0.0`  
  * link [type:string] [required]  
    Must be one of: `https://jvndb.jvn.jp/myjvn?method=getVendorList` 

  * author [type:object]
    * name [type:string] [required]  
      Must be one of: `IPA`  
    * uri [type:string] [required]  
      Must be one of: `https://www.ipa.go.jp/`  
