# getVulnOverviewList (ver. OKA)
フィルタリング条件に当てはまる脆弱性対策の概要情報リストを取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
 
| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVulnOverviewList (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> okaを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～50 (getVulnOverviewListエントリ上限値)  | － | 50 |
| vendorId | ベンダ番号 | 整数(半角数字) | － | － |
| productId | 製品番号 | 整数(半角数字) | － | － |
| productName | 製品名 | CPE,SWID,SPDX,purl,Hash (\*2) | － | － |
| keyword | キーワード | URLエンコードされたキーワード (\*3) | － | － |
| severity | CVSS深刻度 | n:なし、l:注意、m:警告、h:重要、c:緊急 | － | － |
| vector | CVSS基本評価基準 | CVSS 基本評価基準 <br> CVSS:3.0/AV:[N,A,L,P]/AC:[L,H]/PR:[N,L,R]/UI:[N,R]/S:[C,U]/C:[N,L,H]/I:[N,L,H]/A:[N,L,H]  | － | － |
| rangeDatePublic | 発見日の範囲指定 	n:範囲指定なし、w:過去1週間、m:過去1ヶ月  | － | w |
| rangeDatePublished | 更新日の範囲指定 | n:範囲指定なし、w:過去1週間、m:過去1ヶ月  | － | w |
| rangeDateFirstPublished | 発行日の範囲指定 | n:範囲指定なし、w:過去1週間、m:過去1ヶ月  | － | w |
| datePublicStart | 発見日開始年月日 | 整数8桁 (半角数字)| － | － |
| datePublicEnd | 発見日終了年月日 | 整数8桁 (半角数字)| － | － |
| datePublishedStart | 更新日開始年月日 | 整数8桁 (半角数字)| － | － |
| datePublishedEnd | 更新日終了年月日 | 整数8桁 (半角数字)| － | － |
| dateFirstPublishedStart | 発行日開始年月日 | 整数8桁 (半角数字)| － | － |
| dateFirstPublishedEnd | 発行日終了年月日 | 整数8桁 (半角数字)| － | － |
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
  * 処理成功時、feedノード、MyJVN共通Statusノードを含むJSONを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* JSONスキーマ
  * TBD
* 例
  * [ getVulnOverviewList_oka.json ](examples/getVulnOverviewList_oka.json)


```
{
    "feed": {
        "generator": {
            "product_name": "MyJVN API",
            "product_version": "oka",
            "schema_version": "4.0",
            "language": "ja-JP",
            "updated": "更新日"
        },
        "title": "getVulnOverviewList API",
        "id": "jvnpid:1.0:ipa:myjvn_api_getVulnOverviewList:4.0.0.0.0",
        "link": "https://jvndb.jvn.jp/apis/myjvn/",
        "author": {
            "name": "IPA",
            "uri": "https://www.ipa.go.jp/"
        },
        "sec:handling": {
            "marking:Marking": {
                "marking:Marking_Structure": {
                    "marking_model_name": "TLP",
                    "marking_model_ref": "http://www.us-cert.gov/tlp/",
                    "color": "WHITE"
                }
            }
        },
        "entry": [
            {
                "title": "関連情報のタイトル",
                "id": "関連情報の識別子",
                "summary": "関連情報の概要",
                "link": "関連情報の概要のURL",
                "update": "更新日",
                "published": "発行日",
                "references": [
                    {
                        "url": "https://www.cve.org/CVERecord?id=CVE-2022-29894",
                        "summary": "CVE-2022-29894"
                    },
                    {"//_comment": "url,summaryのタグを繰り返します。"}
                ],
                "products": [
                    {
                        "vendor": "ベンダ名",
                        "product": "製品名",
                        "product_ids": [
                            {"swid": "SWID製品名"},
                            {"cpe": "CPE製品名"},
                            {"spdxid": "spdx製品名"},
                            {"purl": "purl製品名"},
                            {"sha256": "ハッシュ値"}
                        ]
                    },
                    {"//_comment": "vendor,productなどのタグを繰り返します。"}
                ],
                "scores": {
                    "cvss_v2": {
                        "version": "CVSSバージョン 2.0",
                        "vectorString": "パラメータ短縮表記",
                        "baseScore": "基本値",
                        "baseSeverity": "基本値深刻度"
                    },
                    "cvss_v3": {
                        "version": "CVSSバージョン 3.0 or 3.1",
                        "vectorString": "パラメータ短縮表記",
                        "baseScore": "基本値",
                        "baseSeverity": "基本値深刻度"
                    }
                }
            },
            {"//_comment": "title,idなどのタグを繰り返します。"}
        ],
        "status:Status": {
            "version": "3.3",
            "method": "getVulnOverviewList",
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
}
```
