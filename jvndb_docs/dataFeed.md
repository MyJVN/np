# データフィード

## JVNDBRSS (脆弱性対策情報の概要)

### Ver3.2 HND

#### XML スキーマ

- JVNRSS 3.2：https://jvndb.jvn.jp/schema/jvnrss_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd

#### 解説

<details>
```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://purl.org/rss/1.0/"
  xmlns:rss="http://purl.org/rss/1.0/"
  xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
  xmlns:dc="http://purl.org/dc/elements/1.1/"
  xmlns:dcterms="http://purl.org/dc/terms/"
  xmlns:sec="http://jvn.jp/rss/mod_sec/3.0/"
  xmlns:marking="http://data-marking.mitre.org/Marking-1"
  xmlns:tlpMarking="http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1"
  xsi:schemaLocation="http://purl.org/rss/1.0/ https://jvndb.jvn.jp/schema/jvnrss_3.2.xsd"
  xml:lang="ja"
  >
  <channel rdf:about="https://jvndb.jvn.jp/apis/myjvn">
    <title>JVNDB 脆弱性対策情報</title>
    <link>https://jvndb.jvn.jp/apis/myjvn</link>
    <description>JVNDB 脆弱性対策情報</description>
    <dc:date>データフィード生成日</dc:date>
    <dcterms:issued />
    <dcterms:modified>データフィード生成日</dcterms:modified>
    <items>
      <rdf:Seq>
        <rdf:li
          rdf:resource="脆弱性対策情報の概要のURL" />
        <!-- 脆弱性対策概要情報の件数分 <rdf:li rdf:resource= を繰り返します。 -->
      </rdf:Seq>
    </items>
  </channel>
  <item
    rdf:about="脆弱性対策情報の概要のURL">
    <title>脆弱性対策情報のタイトル</title>
    <link>脆弱性対策情報の概要のURL</link>
    <description>脆弱性対策情報の概要</description>
    <sec:identifier>脆弱性対策情報の識別子 (JVNDB-西暦-番号)</sec:identifier>
    <sec:references /><!-- getOverviewList 参考情報フィールド参照 -->
    <sec:cpe /><!-- getOverviewList 製品識別子フィールド参照 -->
    <sec:cvss /><!-- getOverviewList 脆弱性深刻度フィールド参照 -->
    <dc:date>最終更新日</dc:date>
    <dcterms:issued>登録日</dcterms:issued>
    <dcterms:modified>最終更新日</dcterms:modified>
  </item>
  <!-- 脆弱性対策概要情報の件数分 item を繰り返します。 -->
  <status:Status
    version="3.3"
    method="getVulnOverviewList"
    feed="hnd"
    lang="ja"
    retCd= 0
    retMax=""
    errCd=""
    errMsg=""
    totalRes="エントリ総数"
    totalResRet="エントリ数"
    firstRes=""
    lt="1">
  </status:Status>
</rdf:RDF>
```
</details>
<br>

### Ver4.0 OKA

#### JSON スキーマ

- MyJVN Feed：https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json

#### 解説

<details>
```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json",
  "feed": {
    "generator": {
      "date": "データフィード生成日",
      "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 脆弱性対策情報",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "entry": [
      {
        "title": "脆弱性対策情報のタイトル",
        "id": "脆弱性対策情報の識別子 (JVNDB-西暦-番号)",
        "summary": "脆弱性対策情報の概要",
        "link": "脆弱性対策情報の概要のURL",
        "modified": "最終更新日",
        "created": "登録日",
        "public": "公表日",
        "references": [ { "$comment": "getOverviewList 参考情報フィールド参照" } ],
        "products": [ { "$comment": "getOverviewList 影響を受ける製品フィールド参照" } ],
        "metrics": [ { "$comment": "getOverviewList 脆弱性深刻度フィールド参照" } ],
        "cwes": [ { "$comment": "getOverviewList 脆弱性種別フィールド参照" } ]
      },
      { "$comment": "title,id などを繰り返します。" }
    ]
  },
  "status:Status": {
    "version": "4.0.0",
    "method": "getVulnOverviewList",
    "feed": "oka",
    "lang": "ja",
    "retCd": 0,
    "retMax": "",
    "errCd": "",
    "errMsg": "",
    "totalRes": "エントリ総数",
    "totalResRet": "エントリ数",
    "firstRes": "",
    "lt": "1"
  }
}
```
</details>
<br>
<br>

## 脆弱性対策情報詳細 (脆弱性対策情報の詳細)

### Ver3.2 HND

#### XML スキーマ

- VULDEF 3.2：http://jvndb.jvn.jp/schema/vuldef_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 解説

<details>
```
<?xml version="1.0" encoding="UTF-8"?>
<VULDEF-Document 
  version="3.2"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://jvn.jp/vuldef/"
  xmlns:vuldef="http://jvn.jp/vuldef/"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xmlns:sec="http://jvn.jp/rss/mod_sec/3.0/"
  xmlns:marking="http://data-marking.mitre.org/Marking-1"
  xmlns:tlpMarking="http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1"
  xsi:schemaLocation="http://jvn.jp/vuldef/ https://jvndb.jvn.jp/schema/vuldef_3.2.xsd
                      http://jvn.jp/rss/mod_sec/3.0/ https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
                      http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1 https://jvndb.jvn.jp/schema/tlp_marking.xsd
                      http://jvndb.jvn.jp/myjvn/Status https://jvndb.jvn.jp/schema/status_3.3.xsd"
  xml:lang="ja"
  >
  <Vulinfo>
    <VulinfoID>脆弱性対策情報の識別子 (JVNDB-西暦-番号)</VulinfoID>
    <VulinfoData>
      <Title>タイトル</Title>
      <VulinfoDescription>
        <Overview>セキュリティ情報の概要</Overview>
      </VulinfoDescription>
      <Affected /><!-- getVulnDetailInfo 影響を受ける製品フィールド参照 -->
      <Impact /><!-- getVulnDetailInfo 想定される影響フィールド参照 -->
      <Solution /><!-- getVulnDetailInfo 対策フィールド参照 -->
      <Related /><!-- getVulnDetailInfo 関連情報フィールド参照 -->
      <History /><!-- getVulnDetailInfo 履歴フィールド参照 -->
      <DateFirstPublished>登録日</DateFirstPublished>
      <DateLastUpdated>最終更新日</DateLastUpdated>
      <DatePublic>公表日</DatePublic>
    </VulinfoData>
  </Vulinfo>
  <!-- 脆弱性対策詳細情報の件数分 Vulinfo を繰り返します。 -->
  <sec:handling />
  <status:Status
    version="3.3"
    method="getVulnDetailInfo"
    feed="hnd"
    lang="ja"
    retCd= 0
    retMax=""
    errCd=""
    errMsg=""
    totalRes="エントリ総数"
    totalResRet="エントリ数"
    firstRes=""
    lt="1">
  </status:Status>
</VULDEF-Document>
```
</details>
<br>

### Ver4.0 OKA

#### JSON スキーマ

- VULDEF (STIX) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN：https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json
- MyJVN STIX SDO (Stix Domain Object)：https://jvndb.jvn.jp/schema/jvn-jp-sdo.json

#### 解説

<details>
```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json",
  "type": "bundle",
  "id": "bundle--UUIDv4",
  "objects": [
    {
      "type": "extension-definition",
      "id": "extension-definition--b2440624-45a6-11ec-81d3-0242ac130003",
      "$comment": "getVulnDetailInfo extension-definition フィールド参照"
    },
    {
      "type": "identity",
      "id": "identity--298980da-697f-431b-ae10-505b3542c427",
      "$comment": "getVulnDetailInfo identity フィールド参照"
    },
    {
      "type": "jvn-jp-sdo",
      "id": "jvn-jp-sdo--UUIDv4 (bundle UUIDv4と同値)",
      "spec_version": "2.1",
      "created": "データフィード生成日",
      "modified": "データフィード生成日",
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
                "date": "データフィード生成日",
                "engine": { "version": "4.0.0", "name": "MyJVN API" }
              }
            },
            "$comment": "getVulnDetailInfo アドバイザリフィールド参照"
          },
          "product_tree": { "$comment": "getVulnDetailInfo 製品フィールド参照" },
          "vulnerabilities": [ { "$comment": "getVulnDetailInfo 脆弱性対策フィールド参照" } ],
          "jvn_extension": {
            "generator": {
              "date": "データフィード生成日",
              "engine": { "version": "4.0.0", "name": "MyJVN API" }
            },
            "$comment": "getVulnDetailInfo CPE Applicability Statements 参照"
          }
        },
        { "$comment": "document,product_tree,vulnerabilities,jvn_extension を繰り返します。" }
      ]
    }
  ],
  "status:Status": {
    "version": "4.0.0",
    "method": "getVulnDetailInfo",
    "feed": "oka",
    "lang": "ja",
    "retCd": 0,
    "retMax": "",
    "errCd": "",
    "errMsg": "",
    "totalRes": "エントリ総数",
    "totalResRet": "エントリ数",
    "firstRes": "",
    "lt": "1"
  }
}
```
</details>
<br>
<br>

## ベンダ一覧 (ベンダ名（製品開発者）リスト)

### Ver3.2 HND

#### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 解説

<details>
```
<?xml version="1.0" encoding="UTF-8"?>
<Result version="3.3"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:mjres="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xsi:schemaLocation="http://jvndb.jvn.jp/myjvn/Results https://jvndb.jvn.jp/schema/results_3.3.xsd"
  >
  <VendorInfo xml:lang="ja">
    <Vendor
      vid="ベンダ番号 (JVN iPedia におけるベンダの識別番号)"
      vname="ベンダ名 [例] 独立行政法人情報処理推進機構 (IPA)"
      cpe="CPEベンダ識別子 (CPE v2.2 形式) [例] cpe:/:ipa" />
    <!-- ベンダの件数分 Vendor を繰り返します。 -->
  </VendorInfo>
  <status:Status
    version="3.3"
    method="getVendorList"
    feed="hnd"
    lang="ja"
    retCd= 0
    retMax=""
    errCd=""
    errMsg=""
    totalRes="エントリ総数"
    totalResRet="エントリ数"
    firstRes=""
    lt="1">
  </status:Status>
</Result>
```
</details>
<br>

### Ver4.0 OKA

#### JSON スキーマ

- Vendor and Product Dictionary for MyJVN：https://jvndb.jvn.jp/schema/jvnpid_1.0.json

#### 解説

<details>
```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json",
  "jvn-product-dictionary": {
    "generator": {
      "date": "データフィード生成日",
      "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号)",
        "vname": "ベンダ名 [例] 独立行政法人情報処理推進機構 (IPA)",
        "vfqdn": "ベンダプライマリドメイン [例] ipa.go.jp",
        "vname_i18n": {
          "ja": "ベンダ名日本語 [例] 独立行政法人情報処理推進機構 (IPA)",
          "en": "ベンダ名英語 [例] INFORMATION-TECHNOLOGY PROMOTION AGENCY, JAPAN (IPA)"
        },
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::ipa"
      },
      { "$comment": "vendor_id,vid,vname,vname_i18n を繰り返します。" }
    ]
  },
  "status:Status": {
    "version": "4.0.0",
    "method": "getVendorList",
    "feed": "oka",
    "lang": "ja",
    "retCd": 0,
    "retMax": "",
    "errCd": "",
    "errMsg": "",
    "totalRes": "エントリ総数",
    "totalResRet": "エントリ数",
    "firstRes": "",
    "lt": "1"
  }
}
```
</details>
<br>
<br>

## 製品一覧 (製品名リスト)

### Ver3.2 HND

#### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 解説

<details>
```
<?xml version="1.0" encoding="UTF-8"?>
<Result version="3.3"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:mjres="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xsi:schemaLocation="http://jvndb.jvn.jp/myjvn/Results https://jvndb.jvn.jp/schema/results_3.3.xsd"
  >
  <VendorInfo
    xml:lang="ja">
    <Vendor
      vid="ベンダ番号 (JVN iPedia におけるベンダの識別番号)"
      vname="ベンダ名"
      cpe="CPEベンダ識別子 (CPE v2.2 形式) [例] cpe:/:ipa">
      <Product
        pid="製品番号 (JVN iPedia における製品の識別番号)"
        pname="製品名"
        cpe="CPE製品識別子 (CPE v2.2 形式) [例] cpe:/a:ipa:myjvn_api" />
      <!-- フィルタリングに当てはまる製品の件数分 Product を繰り返します。 -->
    </Vendor>
    <!-- フィルタリングに当てはまるベンダの件数分 Vendor を繰り返します。 -->
  </VendorInfo>
  <status:Status
    version="3.3"
    method="getProductList"
    feed="hnd"
    lang="ja"
    retCd= 0
    retMax=""
    errCd=""
    errMsg=""
    totalRes="エントリ総数"
    totalResRet="エントリ数"
    firstRes=""
    lt="1">
  </status:Status>
</Result>
```
</details>
<br>

### Ver4.0 OKA

#### JSON スキーマ

- Vendor and Product Dictionary for MyJVN：https://jvndb.jvn.jp/schema/jvnpid_1.0.json

#### 解説 (バージョン表記なし)

<details>
```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json",
  "jvn-product-dictionary": {
    "generator": {
      "date": "データフィード生成日",
      "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号)",
        "vname": "ベンダ名 [例] 独立行政法人情報処理推進機構 (IPA)",
        "vfqdn": "ベンダプライマリドメイン [例] ipa.go.jp",
        "vname_i18n": {
          "ja": "ベンダ名日本語 [例] 独立行政法人情報処理推進機構 (IPA)",
          "en": "ベンダ名英語 [例] INFORMATION-TECHNOLOGY PROMOTION AGENCY, JAPAN (IPA)"
        },
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::ipa",
        "products": [
          {
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp:myjvn_api",
            "pid": "製品番号 (JVN iPedia における製品の識別番号)",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "pname_i18n": {
              "ja": "製品名日本語 [例] マイジェイブイエヌ API",
              "en": "製品名英語 [例] MyJVN API"
            },
            "product_ids": [
              {
                "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:*:*:*:*:*:*:*:*",
                "$comment": "getProductList 製品識別子フィールド参照"
              }
            ]
          },
          { "$comment": "product_id,pid,pname,pname_i18n などを繰り返します。" }
        ],
        "modified": "ベンダ毎の製品の最終更新日",
        "created": "ベンダ毎の製品の登録日"
      },
      { "$comment": "vendor_id,vid,vname,cpe などを繰り返します。" }
    ]
  },
  "status:Status": {
    "version": "4.0.0",
    "method": "getProductList",
    "feed": "oka",
    "lang": "ja",
    "retCd": 0,
    "retMax": "",
    "errCd": "",
    "errMsg": "",
    "totalRes": "エントリ総数",
    "totalResRet": "エントリ数",
    "firstRes": "",
    "lt": "1"
  }
}
```
</details>

#### 解説 (バージョン表記あり)

<details>
```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json",
  "jvn-product-dictionary": {
    "generator": {
      "date": "データフィード生成日",
      "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号)",
        "vname": "ベンダ名 [例] 独立行政法人情報処理推進機構 (IPA)",
        "vfqdn": "ベンダプライマリドメイン [例] ipa.go.jp",
        "vname_i18n": {
          "ja": "ベンダ名日本語 [例] 独立行政法人情報処理推進機構 (IPA)",
          "en": "ベンダ名英語 [例] INFORMATION-TECHNOLOGY PROMOTION AGENCY, JAPAN (IPA)"
        },
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::ipa",
        "products": [
          {
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api:4.0.0",
            "pid": "製品番号 (JVN iPedia における製品の識別番号)",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "pname_i18n": {
              "ja": "製品名日本語 [例] マイジェイブイエヌ API",
              "en": "製品名英語 [例] MyJVN API"
            },
            "version": "バージョン [例] 4.0.0",
            "product_ids": [
              {
                "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:4.0.0:*:*:*:*:*:*:*",
                "$comment": "getProductList 製品識別子フィールド参照"
              }
            ]
          },
          { "$comment": "product_id,pid,pname,pname_i18n などを繰り返します。" }
        ],
        "modified": "ベンダ毎の製品の最終更新日",
        "created": "ベンダ毎の製品の登録日"
      },
      { "$comment": "vendor_id,vid,vname,cpe などを繰り返します。" }
    ]
  },
  "status:Status": {
    "version": "4.0.0",
    "method": "getProductList",
    "feed": "oka",
    "lang": "ja",
    "retCd": 0,
    "retMax": "",
    "errCd": "",
    "errMsg": "",
    "totalRes": "エントリ総数",
    "totalResRet": "エントリ数",
    "firstRes": "",
    "lt": "1"
  }
}
```
</details>