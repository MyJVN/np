# getVulnDetailInfo (ver. OKA)

フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=oka&パラメタ名=パラメタ値&...`
  - リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

<br>

| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVulnDetailInfo (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> okaを指定 | ○ | － |
| vulnId | 脆弱性対策情報ID | JVNDB-YYYY-XXXXXX <br> JVNDB ... プレフィックス <br> YYYY ... 整数4桁 <br> XXXXXX ... 整数6桁 | ○ | － |
| ft | 出力形式 | jvncsaf: CSAFベースカスタム仕様 <br> jvnstix: STIXベースカスタム仕様 | － | jvncsaf |
| lang | 表示言語(日本語／英語) | ja:日本語、en:英語 | － | ja |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

#### vulnId

脆弱性対策情報IDを指定します。

- 複数指定は不可
- \[例\]
    JVNDB-2017-009608を取得したい場合  
    `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=oka&vulnId=JVNDB-2017-009608`

<br>
<br>

## レスポンス (jvncsaf)

### 概要
- 処理成功時、documentノード、product_treeノード、vulnerabilitiesノード、MyJVN共通Statusノードを含むJSONを応答します。
- エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。

### JSONスキーマ
- TBD

### 例
- \[ getVulnDetailInfo_oka.json \]

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
    "title": "エアバッグコントロールユニットにおける暗号アルゴリズムの使用に関する脆弱性",
    "lang": "ja",
    "notes": [
      {
        "category": "description",
        "text": "2014 年以降に製造された不特定の乗用車のエアバッグコントロールユニット (別名 pyrotechnical control unit または PCU) には、暗号アルゴリズムの使用に関する脆弱性が存在します。"
      }
    ],
    "tracking": {
      "generator": {
        "date": "2026-04-01T00:00:00+09:00",
        "engine": {
          "version": "4.0.0",
          "name": "MyJVN API"
        }
      },
      "id": "JVNDB-2017-009608",
      "current_release_date": "2025-04-06T03:00:00+09:00",
      "initial_release_date": "2017-11-16T15:06:40+09:00",
      "status": "final",
      "version": "2.0.0",
      "revision_history": [
        {
          "date": "2018-02-17T10:37:52+09:00",
          "number": "1.0.0",
          "summary": "[2017年11月16日] 掲載"
        },
        {
          "date": "2025-04-06T03:00:00+09:00",
          "number": "2.0.0",
          "summary": "更新"
        }
      ]
    },
    "publisher": {
      "category": "coordinator",
      "name": "IPA",
      "namespace": "https://www.ipa.go.jp"
    }
  },
  "product_tree": {
    "branches": [
      {
        "category": "vendor",
        "name": "PCU",
        "product": {
          "product_id": "jvnpid:1.0::pcu:pcu",
          "name": "PCU",
          "product_identification_helper": {
            "cpe": "cpe:2.3:h:pcu:pcu:*:*:*:*:*:*:*:*"
          }
        }
      },
      {
        "category": "vendor",
        "name": "PCU",
        "product": {
          "product_id": "jvnpid:1.0::pcu:pcu2",
          "name": "PCU2"
        }
      }
    ]
  },
  "vulnerabilities": [
    {
      "cve": "CVE-2017-14937",
      "cwes": [
        {
          "id": "CWE-327",
          "name": "Use of a Broken or Risky Cryptographic Algorithm"
        }
      ],
      "product_status": {
        "known_affected": ["jvnpid:1.0::pcu:pcu", "jvnpid:1.0::pcu:pcu2"]
      },
      "threats": [
        {
          "category": "impact",
          "details": "情報を取得される可能性があります。"
        }
      ],
      "remediations": [
        {
          "category": "vendor_fix",
          "details": "参考情報を参照して適切な対策を実施してください。",
          "product_ids": ["jvnpid:1.0::pcu:pcu", "jvnpid:1.0::pcu:pcu2"]
        }
      ],
      "scores": [
        {
          "cvss_v2": {
            "version": "2.0",
            "vectorString": "AV:N/AC:M/Au:S/C:P/I:P/A:P",
            "baseScore": 6,
            "baseSeverity": "HIGH",
            "accessVector": "NETWORK",
            "accessComplexity": "MEDIUM",
            "authentication": "SINGLE",
            "confidentialityImpact": "PARTIAL",
            "integrityImpact": "PARTIAL",
            "availabilityImpact": "PARTIAL"
          },
          "cvss_v3": {
            "version": "3.0",
            "vectorString": "CVSS:3.0/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:L/A:L",
            "baseScore": 7.6,
            "baseSeverity": "HIGH",
            "attackVector": "NETWORK",
            "attackComplexity": "LOW",
            "privilegesRequired": "NONE",
            "userInteraction": "REQUIRED",
            "scope": "UNCHANGED",
            "confidentialityImpact": "HIGH",
            "integrityImpact": "LOW",
            "availabilityImpact": "LOW"
          },
          "cvss_v4": {
            "version": "4.0",
            "vectorString": "CVSS:4.0/AV:N/AC:L/AT:P/PR:N/UI:N/VC:H/VI:H/VA:H/SC:H/SI:H/SA:H",
            "baseScore": 9.5,
            "baseSeverity": "CRITICAL",
            "attackVector": "NETWORK",
            "attackComplexity": "LOW",
            "attackRequirements": "PRESENT",
            "privilegesRequired": "NONE",
            "userInteraction": "NONE",
            "vulnConfidentialityImpact": "HIGH",
            "vulnIntegrityImpact": "HIGH",
            "vulnAvailabilityImpact": "HIGH",
            "subConfidentialityImpact": "HIGH",
            "subIntegrityImpact": "HIGH",
            "subAvailabilityImpact": "HIGH"
          },
          "products": ["jvnpid:1.0::pcu:pcu", "jvnpid:1.0::pcu:pcu2"]
        }
      ]
    }
  ],
  "references": [
    {
      "category": "external",
      "summary": "CVE-2017-14937",
      "url": "http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-14937"
    },
    {
      "category": "external",
      "summary": "CVE-2017-14937",
      "url": "https://nvd.nist.gov/vuln/detail/CVE-2017-14937"
    },
    {
      "category": "external",
      "summary": "Vulnerability in pyrotechnical control units of passenger cars",
      "url": "http://www.mmt.hs-karlsruhe.de/downloads/IEEM/Schwachstellen/PCU_Vulnerability_Description_HsKA.PDF"
    }
  ],
  "jvnextension": {
    "entry": [],
    "cpeApplicability": [],
    "spdx": [],
    "cyclonedx": [],
    "$comment": "バージョンチェック用"
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

## レスポンス (jvnstix)

### 概要
- 処理成功時、documentノード、product_treeノード、vulnerabilitiesノード、MyJVN共通Statusノードを含むJSONを応答します。
- エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。

### JSONスキーマ
- TBD

### 例
- \[ getVulnDetailInfo_oka.json \]

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
        "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003": {
          "extension_type": "new-sdo"
        }
      },
      "document": {},
      "product_tree": {},
      "vulnerabilities": [],
      "jvnextension": {
        "entry": [],
        "cpeApplicability": [],
        "spdx": [],
        "cyclonedx": [],
        "$comment": "バージョンチェック用"
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
  ]
}
```