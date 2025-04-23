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

| パラメタ名 | 名称                   | パラメタ値                                                                                        | 必須 | デフォルト |
| ---------- | ---------------------- | ------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method     | メソッド名             | getVulnDetailInfo (固定)                                                                          | ○    | －         |
| feed       | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定                                   | ○    | －         |
| vulnId     | 脆弱性対策情報 ID      | JVNDB-YYYY-XXXXXX <br> JVNDB ... プレフィックス <br> YYYY ... 整数 4 桁 <br> XXXXXX ... 整数 6 桁 | ○    | －         |
| ft         | 出力形式               | jvncsaf: CSAF ベースカスタム仕様 <br> jvnstix: STIX ベースカスタム仕様                            | －   | jvncsaf    |
| lang       | 表示言語(日本語／英語) | ja:日本語、en:英語                                                                                | －   | ja         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### vulnId

脆弱性対策情報 ID を指定します。

- 複数指定は不可
- \[例\] JVNDB-2017-009608 を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=oka&vulnId=JVNDB-2017-009608`

<br>
<br>

## レスポンス (jvncsaf)

### 概要

- 処理成功時、document、product_tree、vulnerabilities、jvn_extension、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- VULDEF (CSAF) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN
  - https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.csaf.json?20250419
  - [ myjvn_vuldef_1.0.csaf.json ](../schemas/myjvn_vuldef_1.0.csaf.json)

- VULDEF extension
  - https://jvndb.jvn.jp/schema/jvnpid_extension_1.0.json?20250419
  - [ jvnpid_extension_1.0.json ](../schemas/jvnpid_extension_1.0.json)

### 例

- [ getVulnDetailInfo_oka_JVNDB-2017-009608 (CVE=1, CWE=1, CVSS=2, Ver=NONE) ](../examples/getVulnDetailInfo_oka_JVNDB-2017-009608.json)
- [ getVulnDetailInfo_oka_JVNDB-2018-009328 (CVE=1, CWE=1, CVSS=2, Ver=PRESENT) ](../examples/getVulnDetailInfo_oka_JVNDB-2018-009328.json)
- [ getVulnDetailInfo_oka_JVNDB-2021-002774 (CVE=1, CWE=0, CVSS=0, Ver=PRESENT) ](../examples/getVulnDetailInfo_oka_JVNDB-2021-002774.json)
- [ getVulnDetailInfo_oka_JVNDB-2022-000097 (CVE=3, CWE=2, CVSS=6, Ver=NONE ) ](../examples/getVulnDetailInfo_oka_JVNDB-2022-000097.json)

### 解説

```
{
  "document": {
    "category": "myjvn_security_advisory",
    "csaf_version": "2.1",
    "distribution": {
      "tlp": {
        "label": "WHITE",
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
        "date": "更新日",
        "engine": {
          "version": "4.0.0",
          "name": "MyJVN API"
        }
      },
      "id": "脆弱性対策情報の識別子 (JVNDB-西暦-番号) 
             [例] JVNDB-2025-001234",
      "current_release_date": "更新日",
      "initial_release_date": "発行日",
      "status": "final",
      "version": "更新バージョ",
      "revision_history": [
        {
          "date": "発行日",
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
        "summary": "アドバイザリID",
        "url": "アドバイザリURL",
        "source": "アドバイザリ情報源"
      }
    ]
  },
  "product_tree": {
    "branches": [
      {
        "category": "vendor",
        "name": "ベンダ名",
        "product": {
          "product_id": "JVN製品識別子 (jvnpid 1.0 形式) 
                         [例] jvnpid:1.0::dendai.ac.jp:myjvn_api",
          "name": "製品名",
          "product_identification_helper": {
            "cpe": "CPE製品識別子 (CPE v2.3 形式) 
                    [例] cpe:2.3:a:dendai.ac.jp:myjvn_api:*:*:*:*:*:*:*:*"
          }
        }
      }
    ]
  },
  "vulnerabilities": [
    {
      "cve": "CVE番号 
              [例] CVE-2025-0000",
      "cwes": [
        {
          "id": "CWE 番号 
                 [例] CWE-502",
          "name": "CWE 説明 
                   [例] 信頼できないデータのデシリアライゼーション(CWE-502)"
        }
      ],
      "product_status": {
        "known_affected": ["JVN製品識別子"]
      },
      "threats": [
        {
          "category": "impact",
          "details": "想定される影響 
                      [例] 情報を取得される可能性があります。"
        }
      ],
      "remediations": [
        {
          "category": "vendor_fix",
          "details": "対策 
                      [例] 参考情報を参照して適切な対策を実施してください。",
          "product_ids": ["JVN製品識別子"]
        }
      ],
      "metrics": [
        {
          "content": {
            "cvss_v2": {
              "version": "CVSSバージョン 2.0",
              "vectorString": "パラメタ短縮表記 
                               [例] AV:N/AC:M/Au:N/C:N/I:P/A:N",
              "baseScore": "基本値",
              "baseSeverity": "基本値深刻度 (LOW, MEDIUM, HIGH)",
              "$comment": "cvss_v2 基本評価値一覧"
            },
            "cvss_v3": {
              "version": "CVSSバージョン 3.0 or 3.1",
              "vectorString": "パラメタ短縮表記 
                               [例] CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
              "baseScore": "基本値",
              "baseSeverity": "基本値深刻度 (NONE, LOW, MEDIUM, HIGH, CRITICAL)",
              "$comment": "cvss_v3 基本評価値一覧"
            },
            "cvss_v4": {
              "version": "CVSSバージョン 4.0",
              "vectorString": "パラメタ短縮表記 
                               [例] CVSS:4.0/AV:N/AC:H/AT:N/PR:N/UI:N/VC:H/VI:H/VA:H/SC:H/SI:L/SA:L",
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
          "products": ["JVN製品識別子"]
        }
      ]
    }
  ],
  "jvn_extension": {
    "version": "4.0.0",
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
            "version": "8.1.2",
            "status": "affected",
            "description": "バージョン 8.1.2"
          },
          {
            "version": "開始バージョン",
            "status": "影響有無 (affected, unaffected, unknown)",
            "lessThan": "終了バージョン",
            "versionType": "バージョン形式 (semver, custom)",
            "description": "バージョンに関する説明"
          },
          {
            "version": "0.0.0",
            "status": "affected",
            "lessThan": "1.0.6",
            "versionType": "semver",
            "description": "バージョン 1.0.6未満"
          },
          {
            "version": "2.1.0",
            "status": "affected",
            "lessThanOrEqual": "2.1.3",
            "versionType": "semver",
            "description": "バージョン 2.1.0以上 2.1.3以下"
          },
          {
            "version": "開始バージョン",
            "status": "影響有無 (affected, unaffected, unknown)",
            "lessThanOrEqual": "終了バージョン",
            "versionType": "バージョン形式 (semver, custom)",
            "description": "バージョンに関する説明"
          },
          {
            "version": "3.1.1a",
            "status": "affected",
            "lessThan": "3.1.1d",
            "versionType": "custom",
            "description": "バージョン 3.1.1a以上 3.1.1d未満"
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
                "criteria": "jvnpid:1.0::example_org:example_product:8.1.2"
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
                "criteria": "cpe:2.3:a:example_org:example_product:*:*:*:*:*:*:*:*",
                "versionStartIncluding": "0.0.0",
                "versionEndExcluding": "1.0.6"
              },
              {
                "vulnerable": true,
                "criteria": "cpe:2.3:a:example_org:example_product:*:*:*:*:*:*:*:*",
                "versionStartIncluding": "2.1.0",
                "versionEndIncluding": "2.1.3"
              },
              {
                "vulnerable": true,
                "criteria": "jvnpid:1.0::example_org:example_product",
                "versionStartIncluding": "3.1.1a",
                "versionEndExcluding": "3.1.1d"
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

<br>
<br>

## レスポンス (jvnstix)

### 概要

- 処理成功時、objects、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- VULDEF (STIX) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN
  - https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json?20250419
  - [ myjvn_vuldef_1.0.stix.json ](../schemas/myjvn_vuldef_1.0.stix.json)

- MyJVN STIX SDO (Stix Domain Object)
  - https://jvndb.jvn.jp/schema/jvn-jp-sdo.json?20250419
  - [ mjvn-jp-sdo.json ](../schemas/jvn-jp-sdo.json)

### 例

- [ getVulnDetailInfo_oka_JVNDB-2017-009608_jvnstix (CVE=1, CWE=1, CVSS=2, Ver=NONE) ](../examples/getVulnDetailInfo_oka_JVNDB-2017-009608_jvnstix.json)

### 解説

```
{
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
      "id": "jvn-jp-sdo--UUIDv4",
      "spec_version": "2.1",
      "created": "2025-04-06T09:16:08.000Z",
      "modified": "2025-04-06T09:16:08.000Z",
      "name": "MyJVN API VULDEF-Document embedded in STIX",
      "extensions": {
        "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003": {
          "extension_type": "new-sdo"
        }
      },
      "VULDEF-Document": [
        {
          "document": {},
          "product_tree": {},
          "vulnerabilities": [],
          "jvn_extension": {}
        }
      ]
    }
  ],
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

