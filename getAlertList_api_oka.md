# getAlertList (ver. OKA)
注意警戒情報一覧を取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。

| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getAlertList (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> okaを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～50 (getAlertListエントリ上限値) | － | 50 |
| datePublished | 更新日年 | 半角整数4桁 | － | － |
| dateFirstPublished | 発行日年 | 半角整数4桁 | － | － |
| productName | 製品名 | CPE,SWID,SPDX,purl,Hash | － | － |
| ft | 応答フォーマット | xml または json | － | － |

\*1)  
「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)にMyJVN API側で自動的に設定する値です。  

## レスポンス
* 概要
  * 処理成功時、feedノード、MyJVN共通Statusノードを含むJSONを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* JSONスキーマ
  * TBD
* 例
  * [ getAlertList_oka.json ](examples/getAlertList_oka.json)

```
{
    "feed": {
        "title": "IPA注意警戒サービスAPI",
        "updated": "更新日",
        "id": "swid:ipa.go.jp+myjvn_alert+1.0.0",
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
                "category": {
                    "term": "カテゴリ名",
                    "label": "カテゴリラベル"
                },
                "update": "更新日",
                "published": "発行日",
                "sec:items": [
                    {
                        "sec:item": {
                            "sec:title": "関連情報のタイトル",
                            "sec:identifier": "関連情報の識別子",
                            "sec:link": "関連情報の概要のURL",
                            "sec:published": "発行日",
                            "sec:updated": "更新日",
                            "sec:author": {"name": "発行者"},
                            "sec:prod": [
                                "swid製品名",
                                "cpe製品名",
                                "spdx製品名",
                                "purl製品名"
                            ]
                        }
                    },
                    {"//_comment": "sec:itemタグを繰り返します。"}
                ]
            }
        ],
        "status:Status": {
            "version": "3.3",
            "method": "getAlertList",
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
}
```
