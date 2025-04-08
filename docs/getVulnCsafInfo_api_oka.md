# getVulnCsafInfo (ver. OKA)
フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getVulnCsafInfo&feed=oka&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
 
| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVulnCsafInfo (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> okaを指定 | ○ | － |
| vulnId | 脆弱性対策情報ID | 整数 (半角数字) <br> JVNDB-YYYY-XXXXXX <br> JVNDB ... プレフィックス <br> YYYY ... 整数4桁 (半角数字) <br> XXXXXX ... 整数6桁 (半角数字) | ○ | － |
| lang | 表示言語(日本語／英語) | ja:日本語、en:英語 | － | ja |

\*1)  
「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)にMyJVN API側で自動的に設定する値です。  

## レスポンス
* 概要
  * 処理成功時、documentノード、product_treeノード、vulnerabilitiesノード、MyJVN共通Statusノードを含むJSONを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* JSONスキーマ
  * TBD
* 例
  * [ getVulnCsafInfo_oka.json ](examples/getVulnCsafInfo_oka.json)

```
{
    "document": {
        "lang": "ja",
        "title": "脆弱性対策情報タイトル",
        "category": "csaf_security_advisory",
        "csaf_version": "2.0",
        "tracking": {
            "id": "JVNDB-0000-000000",
            "initial_release_date": "登録日",
            "current_release_date": "最終更新日"
        }
    },
    "product_tree": {
        "full_product_names": [
            {
                "name": "製品名",
                "product_id": "製品識別子"
            }
        ]
    },
    "vulnerabilities": [
        {
            "notes": [
                {
                    "title": "概要",
                    "category": "summary",
                    "text": "脆弱性対策情報概要"
                }
            ],
            "discovery_date": "公表日",
            "cve": "CVE-0000-000000",
            "cwe": {
                    "id": "CWE-000",
                    "name": "CWEタイトル"
            },
            "scores": [
                {
                    "products": ["製品識別子"],
                    "cvss_v2": {
                        "version": "2.0",
                        "vectorString": "AV:L/AC:L/Au:N/C:P/I:N/A:N",
                        "baseScore": 2.1,
                        "baseSeverity": "LOW"
                    },
                    "cvss_v3": {
                        "version": "3.1",
                        "vectorString": "CVSS:3.1/AV:L/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N",
                        "baseScore": 4.0,
                        "baseSeverity": "MEDIUM"
                    }
                }
            ],
            "product_status": {
                "known_affected": ["製品識別子"]
            },
            "threats": [
                {
                    "category": "impact",
                    "details": "想定される影響"
                }
            ],
            "remediations": [
                {
                    "category": "vendor_fix",
                    "details": "対策"
                },
                                {
                    "category": "workaround",
                    "details": "ワークアラウンド"
                }
            ]
        }
    ],
    "jvn-extension": {
        "extension_version": "1.0",
        "jvndbid": "JVNDB-0000-000000",
        "title": "脆弱性対策情報タイトル",
        "jvndbinfo": [
            {
                "cve": "CVE-0000-0000",
                "product_status": {
                    "known_affected": [
                        {
                            "product_id": "製品識別子",
                            "version": {
                                "and": {"lessThan": "2.1.8.0.0"}
                            }
                        }
                    }
                }
            }
        ]
    },
    "status:Status": {
        "version": "4.0",
        "method": "getVulnCsafInfo",
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

* document  
    JVNDB脆弱性対策情報のタイトル、ID、公表日などの文書情報を格納するエリア    
* product_tree  
    製品に関する情報を格納するエリア
* vulnerabilities  
    脆弱性に関する情報を格納するエリア
* jvn-extension  
    脆弱性影響有無に関する支援情報を格納するエリア
