# getVulnStixInfo (ver. OKA)
フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getVulnStixInfo&feed=oka&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
 
| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVulnStixInfo (固定) | ○ | － |
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
  * [ getVulnStixInfo_oka.json ](examples/getVulnStixInfo_oka.json)

```
{
    "type": "bundle",
    "id": "bundle--63c46abd-9f5a-472a-8b10-c51208c10000",
    "objects": [
        {
            "id": "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003",
            "type": "extension-definition",
            "spec_version": "2.1",
            "name": "CSAF embedded in STIX",
            "description": "This schema is to deliver CSAF using STIX.",
            "created": "2021-11-11T11:11:11.000000Z",
            "modified": "2021-11-11T11:11:11.000000Z",
            "created_by_ref": "identity--298980da-697f-431b-ae10-505b3542c427",
            "schema": "http://jvndb.jvn.jp/schema/jvn.sdo",
            "version": "2.0",
            "extension_types": ["new-sdo"]
        },
        {
            "type": "identity",
            "spec_version": "2.1",
            "id": "identity--298980da-697f-431b-ae10-505b3542c427",
            "created": "2021-11-11T11:11:11.000000Z",
            "modified": "2021-11-11T11:11:11.000000Z",
            "name": "MyJVN",
            "description": "Japan Vulnerability Notes - MyJVN",
            "identity_class": "system"
        },
        {
            "type": "jvn-jp-sdo",
            "spec_version": "2.1",
            "id": "jvn-jp-sdo--ac97aae4-83f1-46ca-a351-7aeb76678189",
            "created": "2021-11-15T09:16:08.989000Z",
            "modified": "2021-11-15T09:16:08.989000Z",
            "name": "JVN CSAF embedded in STIX",
            "extensions": {
                "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003": {"extension_type": "new-sdo"}
            },
            "document": {
                "lang": "ja",
                "title": "タイトル",
                "category": "Security Advisory",
                "csaf_version": "2.0",
                "tracking": {
                    "id": "脆弱性情報ID",
                    "initial_release_date": "公開日",
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
                            "title": "タイトル",
                            "category": "general",
                            "text": "概要"
                        }
                    ],
                    "discovery_date": "発見日",
                    "release_date": "公開日",
                    "cve": "CVE-0000-000000",
                    "cwe": {
                        "id": "CWE-000",
                        "name": "Information Exposure"
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
                            "details": "対策",
                            "category": "vendor_fix"
                        }
                    ]
                }
            ],
            "status:Status": {
                "version": "3.3",
                "method": "getVulnStixInfo",
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
    ]
}
```