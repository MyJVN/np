# getVulnDetailInfo (ver. OKA)

フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=oka&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

<br>

| パラメタ名   | 名称                   | パラメタ値                                                                                        | 必須 | デフォルト |
| ------------ | ---------------------- | ------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method       | メソッド名             | getVulnDetailInfo (固定)                                                                          | ○    | －         |
| feed         | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定                                   | ○    | －         |
| startItem    | エントリ開始位置       | 整数 1 ～応答エントリ数                                                                           | －   | 1          |
| maxCountItem | エントリ取得件数       | 整数 1 ～ 10 (getVulnDetailInfo エントリ上限値)                                                   | －   | 10         |
| vulnId       | 脆弱性対策情報 ID      | JVNDB-YYYY-XXXXXX <br> JVNDB ... プレフィックス <br> YYYY ... 整数 4 桁 <br> XXXXXX ... 整数 6 桁 | ○    | －         |
| ft           | 出力形式               | jvncsaf: CSAF ベースカスタム仕様 <br> jvnstix: STIX ベースカスタム仕様                            | －   | jvncsaf    |
| lang         | 表示言語(日本語／英語) | ja:日本語、en:英語                                                                                | －   | ja         |

<br>

### 解説

<details>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### startItem , maxCountItem

エントリ開始位置、エントリ取得件数を指定します。

- startItem , maxCountItem を指定した場合、出力形式は ft=jvnstix となります。
- \[例\] 1 件目から 50 件分の概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&startItem=1&maxCountItem=50`

<bf>

#### vulnId

脆弱性対策情報 ID を指定します。

- ft=jvncsaf の場合には、複数指定は不可
- ft=jvnstix の場合には、複数指定は可、複数指定時は "+" で連結
- \[例\] JVNDB-2017-009608 を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=oka&vulnId=JVNDB-2017-009608`
- \[例\] JVNDB-2017-009608, JVNDB-2018-009328 を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=oka&vulnId=JVNDB-2017-009608+JVNDB-2018-009328&ft=jvnstix`

#### ft

出力形式を指定します。

- ft=jvncsaf の場合
  - CSAF ベースカスタム仕様で出力
  - vulnId の複数指定は不可
  - startItem , maxCountItem を指定しても、これらパラメタは処理されません。
- ft=jvnstix の場合
  - STIX ベースカスタム仕様で出力
  - vulnId の複数指定は可、複数指定時は "+" で連結

</details>
<br>
<br>

## レスポンス (jvncsaf)

### 概要

- 処理成功時、document、product_tree、vulnerabilities、jvn_extension、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- VULDEF (CSAF) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN：https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.csaf.json
- VULDEF extension：https://jvndb.jvn.jp/schema/jvnpid_extension_1.0.json

### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.csaf.json",
  "document": {
    "category": "myjvn_security_advisory",
    "csaf_version": "2.1",
    "distribution": {
      "tlp": {
        "label": "CLEAR",
        "url": "https://www.first.org/tlp/"
      }
    },
    "title": "タイトル",
    "lang": "表示言語 (ja:日本語、en:英語 )",
    "notes": [
      {
        "category": "description",
        "text": "セキュリティ情報の概要"
      }
    ],
    "tracking": {
      "generator": {
        "date": "レスポンス生成日",
        "engine": {
          "version": "4.0.0",
          "name": "MyJVN API"
        }
      },
      "id": "脆弱性対策情報の識別子 (JVNDB-西暦-番号)",
      "current_release_date": "最終更新日",
      "initial_release_date": "登録日",
      "public_date": "公表日",
      "status": "final",
      "version": "更新バージョン",
      "revision_history": [
        {
          "date": "履歴記載日",
          "number": "更新バージョン",
          "summary": "更新内容"
        }
      ]
    },
    "publisher": {
      "category": "coordinator",
      "name": "IPA",
      "namespace": "https://www.ipa.go.jp"
    },
    "references": [
      {
        "category": "external",
        "summary": "参考情報のタイトル or 概要",
        "url": "参考情報のURL",
        "source": "情報源"
      }
    ]
  },
  "product_tree": {
    "branches": [
      {
        "branches": [
          {
            "$comment": "jvnpid がバージョン情報を出力しない場合",
            "product": {
              "product_id": "JVN製品識別子1 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api",
              "name": "製品名 [例] マイジェイブイエヌ API",
              "product_identification_helper": {
                "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:*:*:*:*:*:*:*:*",
                "purls": [
                  "Package-Manager値"
                ],
                "id_refs": [
                  {
                    "nameType": "swid",
                    "value": "一意な識別子"
                  }
                ]
              }
            },
            "category": "product_name",
            "name": "製品名 [例] マイジェイブイエヌ API"
          },
          {
            "branches": [
              {
                "$comment": "jvnpid がバージョン情報を出力する場合",
                "category": "product_version",
                "name": "バージョン [例] 4.0.0",
                "product": {
                  "product_id": "JVN製品識別子2 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api:4.0.0",
                  "name": "製品名＋バージョン [例] マイジェイブイエヌ API 4.0.0",
                  "product_identification_helper": {
                    "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:4.0.0:*:*:*:*:*:*:*",
                    "purls": [
                      "Package-Manager値"
                    ],
                    "hashes": [
                      {
                        "file_hashes": [
                          {
                            "algorithm": "アルゴリズム",
                            "value": "ハッシュ値"
                          }
                        ]
                      }
                    ],
                    "sbom_urls": [
                      "一意な識別子"
                    ],
                    "serial_numbers": [
                      "一意な識別子"
                    ],
                    "id_refs": [
                      {
                        "nameType": "swid",
                        "value": "一意な識別子"
                      }
                    ]
                  }
                }
              }
            ],
            "category": "product_name",
            "name": "製品名 [例] マイジェイブイエヌ API"
          }
        ],
        "category": "vendor",
        "name": "ベンダ名"
      }
    ]
  },
  "vulnerabilities": [
    {
      "cve": "CVE番号",
      "cwes": [
        {
          "id": "CWE 番号",
          "name": "CWE 説明",
          "url": "CWE 掲載 URL",
          "version": "CWEバージョン",
          "source": "情報源"
        }
      ],
      "notes": [
        {
          "category": "description",
          "text": "脆弱性に関する補足情報"
        }
      ],
      "product_status": {
        "known_affected": ["JVN製品識別子1", "JVN製品識別子2"]
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
          "details": "対策",
          "product_ids": ["JVN製品識別子1", "JVN製品識別子2"]
        }
      ],
      "metrics": [
        {
          "content": {
            "cvss_v2": {
              "version": "CVSSバージョン 2.0",
              "vectorString": "パラメタ短縮表記",
              "baseScore": "基本値",
              "baseSeverity": "基本値深刻度 (LOW, MEDIUM, HIGH)",
              "$comment": "cvss_v2 基本評価値一覧"
            },
            "cvss_v3": {
              "version": "CVSSバージョン 3.0 or 3.1",
              "vectorString": "パラメタ短縮表記",
              "baseScore": "基本値",
              "baseSeverity": "基本値深刻度 (NONE, LOW, MEDIUM, HIGH, CRITICAL)",
              "$comment": "cvss_v3 基本評価値一覧"
            },
            "cvss_v4": {
              "version": "CVSSバージョン 4.0",
              "vectorString": "パラメタ短縮表記",
              "baseScore": "基本値",
              "baseSeverity": "基本値深刻度 (NONE, LOW, MEDIUM, HIGH, CRITICAL)",
              "$comment": "cvss_v4 基本評価値一覧"
            },
            "ScoringSystem": {
              "name": "スコアリングシステムの名称",
              "version": "バージョン",
              "vectorString": "パラメタ短縮表記",
              "baseScore": "基本値",
              "baseSeverity": "基本値深刻度"
            },
            "source": "情報源",
            "type": "情報区分 (null, Primary)"
          },
          "products": ["JVN製品識別子1", "JVN製品識別子2"]
        }
      ]
    }
  ],
  "jvn_extension": {
    "generator": {
      "date": "レスポンス生成日",
      "engine": {
        "version": "4.0.0",
        "name": "MyJVN API"
      }
    },
    "title": "JVNDB 脆弱性対策詳細情報",
    "link": "https://jvndb.jvn.jp/apis/",
    "updated": "",
    "vulnid": "脆弱性対策情報の識別子 (JVNDB-西暦-番号)",
    "lang": "ja",
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
    "affected": [
      { "$comment": "可読ベースのバージョンチェック用" },
      {
        "vendor": "ベンダ名",
        "product": "製品名",
        "versions": [
          {
            "version": "開始バージョン",
            "status": "影響有無 (affected, unaffected, unknown)",
            "description": "バージョンに関する説明"
          },
          {
            "version": "開始バージョン",
            "status": "影響有無 (affected, unaffected, unknown)",
            "lessThan": "終了バージョン",
            "versionType": "バージョン形式 (semver, custom)",
            "description": "バージョンに関する説明"
          },
          {
            "version": "開始バージョン",
            "status": "影響有無 (affected, unaffected, unknown)",
            "lessThanOrEqual": "終了バージョン",
            "versionType": "バージョン形式 (semver, custom)",
            "description": "バージョンに関する説明"
          }
        ]
      }
    ],
    "cpeApplicability": [
      { "$comment": "CPEベースのバージョンチェック用" },
      {
        "nodes": [
          {
            "operator": "OR",
            "negate": false,
            "cpeMatch": [
              {
                "vulnerable": true,
                "criteria": "CPE製品識別子 あるいは、JVN製品識別子"
              },
              {
                "vulnerable": true,
                "criteria": "CPE製品識別子 あるいは、JVN製品識別子",
                "versionStartIncluding": "開始バージョン",
                "versionEndIncluding": "終了バージョン"
              },
              {
                "vulnerable": true,
                "criteria": "CPE製品識別子 あるいは、JVN製品識別子",
                "versionStartIncluding": "開始バージョン",
                "versionEndExcluding": "終了バージョン"
              },
              {
                "vulnerable": true,
                "criteria": "CPE製品識別子 あるいは、JVN製品識別子",
                "versionStartExcluding": "開始バージョン",
                "versionEndIncluding": "終了バージョン"
              },
              {
                "vulnerable": true,
                "criteria": "CPE 製品識別子あるいは、JVN製品識別子",
                "versionStartExcluding": "開始バージョン",
                "versionEndExcluding": "終了バージョン"
              }
            ]
          }
        ]
      }
    ]
  },
  "status": {
    "version": "4.0.0",
    "method": "getVulnDetailInfo",
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
<br>

## レスポンス (jvnstix)

### 概要

- 処理成功時、objects、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- VULDEF (STIX) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN：https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json
- MyJVN STIX SDO (Stix Domain Object)：https://jvndb.jvn.jp/schema/jvn-jp-sdo.json

### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json",
  "type": "bundle",
  "id": "bundle--UUIDv4",
  "objects": [
    {
      "type": "extension-definition",
      "id": "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003",
      "spec_version": "2.1",
      "created": "2021-11-11T11:11:11.000Z",
      "modified": "2021-11-11T11:11:11.000Z",
      "name": "VULDEF-Document embedded in STIX",
      "created_by_ref": "identity--298980da-697f-431b-ae10-505b3542c427",
      "schema": "http://jvndb.jvn.jp/schema/jvn-jp-sdo.json",
      "version": "1.0",
      "extension_types": ["new-sdo"]
    },
    {
      "type": "identity",
      "id": "identity--298980da-697f-431b-ae10-505b3542c427",
      "spec_version": "2.1",
      "created": "2021-11-11T11:11:11.000Z",
      "modified": "2021-11-11T11:11:11.000Z",
      "name": "MyJVN API",
      "identity_class": "system"
    },
    {
      "type": "jvn-jp-sdo",
      "id": "jvn-jp-sdo--UUIDv4 (bundle UUIDv4と同値)",
      "spec_version": "2.1",
      "created": "レスポンス生成日",
      "modified": "レスポンス生成日",
      "name": "MyJVN API VULDEF-Document embedded in STIX",
      "extensions": {
        "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003": {
          "extension_type": "new-sdo"
        }
      },
      "VULDEF-Document": [
        {
          "document": {
            "tracking": {
              "generator": {
                "date": "レスポンス生成日",
                "engine": {
                  "version": "4.0.0",
                  "name": "MyJVN API"
                }
              }
            },
            "$comment": "その他のフィールドはレスポンス (jvncsaf) を参照のこと"
          },
          "product_tree": {
            "$comment": "フィールドはレスポンス (jvncsaf) を参照のこと"
          },
          "vulnerabilities": [
            { "$comment": "フィールドはレスポンス (jvncsaf) を参照のこと" }
          ],
          "jvn_extension": {
            "generator": {
              "date": "レスポンス生成日",
              "engine": {
                "version": "4.0.0",
                "name": "MyJVN API"
              }
            },
            "$comment": "その他のフィールドはレスポンス (jvncsaf) を参照のこと"
          }
        },
        "$comment": "document,product_tree,vulnerabilities,jvn_extension を繰り返します。"
      ]
    }
  ],
  "status": {
    "version": "4.0.0",
    "method": "getVulnDetailInfo",
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
