# MyJVN データフィード

## JVNDBRSS (脆弱性対策情報の概要)

### Ver3.2 HND

#### XML スキーマ

- JVNRSS 3.2：https://jvndb.jvn.jp/schema/jvnrss_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd

#### 例

- [ dataFeed_jvndb_rss_hnd.xml ](../examples/hnd/dataFeed_jvndb_rss_hnd.xml)

#### 解説

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
    <dc:date>データフィード生成日 [例] 2025-04-30T11:36:12+09:00</dc:date>
    <dcterms:issued />
    <dcterms:modified>データフィード生成日 [例] 2025-04-30T11:36:12+09:00</dcterms:modified>
    <items>
      <rdf:Seq>
        <rdf:li
          rdf:resource="脆弱性対策情報の概要のURL [例] https://jvndb.jvn.jp/ja/contents/2025/JVNDB-2025-000000.html" />
        <!-- 脆弱性対策概要情報の件数分 <rdf:li rdf:resource= を繰り返します。 -->
      </rdf:Seq>
    </items>
  </channel>
  <item
    rdf:about="脆弱性対策情報の概要のURL [例] https://jvndb.jvn.jp/ja/contents/2025/JVNDB-2025-000000.html">
    <title>脆弱性対策情報のタイトル [例] MyJVN API セキュリティ情報</title>
    <link>脆弱性対策情報の概要のURL [例] https://jvndb.jvn.jp/ja/contents/2025/JVNDB-2025-000000.html</link>
    <description>脆弱性対策情報の概要 [例] MyJVN API は、APIを介してセキュリティ情報を提供するシステムです。</description>
    <sec:identifier>脆弱性対策情報の識別子 (JVNDB-西暦-番号) [例] JVNDB-2025-000000</sec:identifier>
    <sec:references /><!-- getOverviewList 参考情報フィールド参照 -->
    <sec:cpe /><!-- getOverviewList 製品識別子フィールド参照 -->
    <sec:cvss /><!-- getOverviewList 脆弱性深刻度フィールド参照 -->
    <dc:date>最終更新日 [例] 2025-04-26T07:36:21+09:00</dc:date>
    <dcterms:issued>登録日 [例] 2025-04-04T14:45:58+09:00</dcterms:issued>
    <dcterms:modified>最終更新日 [例] 2025-04-26T07:36:21+09:00</dcterms:modified>
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

<br>

### Ver4.0 OKA

#### JSON スキーマ

- MyJVN Feed
  - https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json?20250419
  - [ myjvn_feed_1.0.json ](../schemas/myjvn_feed_1.0.json)

#### 例

- [ dataFeed_jvndb_rss_oka.json ](../examples/oka/dataFeed_jvndb_rss_oka.json)

#### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json?20250419",
  "feed": {
    "generator": {
      "date": "データフィード生成日 [例] 2025-04-30T11:36:12+09:00",
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
        "title": "脆弱性対策情報のタイトル [例] MyJVN API セキュリティ情報",
        "id": "脆弱性対策情報の識別子 (JVNDB-西暦-番号) [例] JVNDB-2025-000000",
        "summary": "脆弱性対策情報の概要 [例] MyJVN API は、APIを介してセキュリティ情報を提供するシステムです。",
        "link": "脆弱性対策情報の概要のURL [例] https://jvndb.jvn.jp/ja/contents/2025/JVNDB-2025-000000.html",
        "modified": "最終更新日 [例] 2025-04-26T07:36:21+09:00",
        "created": "登録日 [例] 2025-04-04T14:45:58+09:00",
        "public": "公表日 [例] 2025-04-01T10:23:42+09:00",
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

<br>
<br>

## 脆弱性対策情報詳細 (脆弱性対策情報の詳細)

### Ver3.2 HND

#### XML スキーマ

- VULDEF 3.2：http://jvndb.jvn.jp/schema/vuldef_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 例

- [ dataFeed_jvndb_detail_hnd.xml ](../examples/hnd/dataFeed_jvndb_detail_hnd.xml)

#### 解説

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
    <VulinfoID>脆弱性対策情報の識別子 (JVNDB-西暦-番号) [例] JVNDB-2025-000000</VulinfoID>
    <VulinfoData>
      <Title>タイトル [例] MyJVN API セキュリティ情報</Title>
      <VulinfoDescription>
        <Overview>セキュリティ情報の概要 [例] MyJVN API は、APIを介してセキュリティ情報を提供するシステムです。</Overview>
      </VulinfoDescription>
      <Affected /><!-- getVulnDetailInfo 影響を受ける製品フィールド参照 -->
      <Impact /><!-- getVulnDetailInfo 想定される影響フィールド参照 -->
      <Solution /><!-- getVulnDetailInfo 対策フィールド参照 -->
      <Related /><!-- getVulnDetailInfo 関連情報フィールド参照 -->
      <History /><!-- getVulnDetailInfo 履歴フィールド参照 -->
      <DateFirstPublished>登録日 [例] 2025-04-04T14:45:58+09:00</DateFirstPublished>
      <DateLastUpdated>最終更新日 [例] 2025-04-26T07:36:21+09:00</DateLastUpdated>
      <DatePublic>公表日 [例] 2025-04-01T10:23:42+09:00</DatePublic>
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

<br>

### Ver4.0 OKA

#### JSON スキーマ

- VULDEF (STIX) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN
  - https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json?20250419
  - [ myjvn_vuldef_1.0.stix.json ](../schemas/myjvn_vuldef_1.0.stix.json)

#### 例

- [ dataFeed_jvndb_detail_oka.json ](../examples/oka/dataFeed_jvndb_detail_oka.json)

#### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.stix.json?20250419",
  "type": "bundle",
  "id": "bundle--UUIDv4 [例] bundle--7194eb1c-7b39-4d5b-82a5-161a538ec11d",
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
      "id": "jvn-jp-sdo--UUIDv4 (bundle UUIDv4と同値) [例] jvn-jp-sdo--7194eb1c-7b39-4d5b-82a5-161a538ec11d",
      "spec_version": "2.1",
      "created": "データフィード生成日 [例] 2025-04-30T20:36:12.000Z",
      "modified": "データフィード生成日 [例] 2025-04-30T20:36:12.000Z",
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
                "date": "データフィード生成日 [例] 2025-04-30T11:36:12+09:00",
                "engine": { "version": "4.0.0", "name": "MyJVN API" }
              }
            },
            "$comment": "getVulnDetailInfo アドバイザリフィールド参照"
          },
          "product_tree": { "$comment": "getVulnDetailInfo 製品フィールド参照" },
          "vulnerabilities": [ { "$comment": "getVulnDetailInfo 脆弱性対策フィールド参照" } ],
          "jvn_extension": {
            "generator": {
              "date": "データフィード生成日 [例] 2025-04-30T11:36:12+09:00",
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

<br>
<br>

## ベンダ一覧 (ベンダ名（製品開発者）リスト)

### Ver3.2 HND

#### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 例

- [ dataFeed_myjvn_vendor_hnd.xml ](../examples/hnd/dataFeed_myjvn_vendor_hnd.xml)

#### 解説

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
      vid="ベンダ番号 (JVN iPedia におけるベンダの識別番号) [例] 99999999991"
      vname="ベンダ名 [例] 東京電機大学"
      cpe="CPEベンダ識別子 (CPE v2.2 形式) [例] cpe:/:dendai.ac.jp" />
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

<br>

### Ver4.0 OKA

#### JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  - https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419
  - [ jvnpid_1.0.json ](../schemas/jvnpid_1.0.json)

#### 例

- [ dataFeed_myjvn_product_oka.json ](../examples/oka/dataFeed_myjvn_product_oka.json)

#### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419",
  "jvn-product-dictionary": {
    "generator": {
      "date": "データフィード生成日 [例] 2025-04-30T11:36:12+09:00",
      "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日 [例] 2025-04-26T07:36:21+09:00",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号) [例] 99999999991",
        "vname": "ベンダ名 [例] 東京電機大学",
        "vfqdn": "ベンダプライマリドメイン [例] dendai.ac.jp",
        "vname_i18n": {
          "ja": "ベンダ名日本語 [例] 東京電機大学",
          "en": "ベンダ名英語 [例] Tokyo Denki University"
        },
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::dendai.ac.jp"
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

<br>
<br>

## 製品一覧 (製品名リスト)

### Ver3.2 HND

#### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 例

- [ dataFeed_myjvn_product_hnd.xml ](../examples/hnd/dataFeed_myjvn_product_hnd.xml) バージョン表記なし

#### 解説

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
      vid="ベンダ番号 (JVN iPedia におけるベンダの識別番号) [例] 99999999991"
      vname="ベンダ名 [例] 東京電機大学"
      cpe="CPEベンダ識別子 (CPE v2.2 形式) [例] cpe:/:dendai.ac.jp">
      <Product
        pid="製品番号 (JVN iPedia における製品の識別番号) [例] 99999999991001"
        pname="製品名 [例] マイジェイブイエヌ API"
        cpe="CPE製品識別子 (CPE v2.2 形式) [例] cpe:/a:dendai.ac.jp:myjvn_api" />
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

<br>

### Ver4.0 OKA

#### JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  - https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419
  - [ jvnpid_1.0.json ](../schemas/jvnpid_1.0.json)

#### 例

- [ dataFeed_myjvn_product_oka.json ](../examples/oka/dataFeed_myjvn_product_oka.json) バージョン表記なし

#### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419",
  "jvn-product-dictionary": {
    "generator": {
      "date": "データフィード生成日 [例] 2025-04-30T11:36:12+09:00",
      "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日 [例] 2025-04-26T07:36:21+09:00",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号) [例] 99999999991",
        "vname": "ベンダ名 [例] 東京電機大学",
        "vfqdn": "ベンダプライマリドメイン [例] dendai.ac.jp",
        "vname_i18n": {
          "ja": "ベンダ名日本語 [例] 東京電機大学",
          "en": "ベンダ名英語 [例] Tokyo Denki University"
        },
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::dendai.ac.jp",
        "products": [
          {
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp:myjvn_api",
            "pid": "製品番号 (JVN iPedia における製品の識別番号) [例] 99999999991001",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "pname_i18n": {
              "ja": "製品名日本語 [例] マイジェイブイエヌ API",
              "en": "製品名英語 [例] MyJVN API"
            },
            "product_ids": [{ "$comment": "getProductList 製品識別子フィールド参照" }]
          },
          { "$comment": "product_id,pid,pname,pname_i18n などを繰り返します。" }
        ],
        "modified": "ベンダ毎の製品の最終更新日 [例] 2025-04-06T02:00:00+09:00",
        "created": "ベンダ毎の製品の登録日 [例] 2024-04-01T12:10:56+09:00"
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

#### 例

- [ dataFeed_myjvn_product_version_oka.json ](../examples/oka/dataFeed_myjvn_product_version_oka.json) バージョン表記あり

#### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419",
  "jvn-product-dictionary": {
    "generator": {
      "date": "データフィード生成日 [例] 2025-04-30T11:36:12+09:00",
      "engine": "engine": { "version": "4.0.0", "name": "MyJVN API" }
    },
    "title": "JVNDB 製品一覧",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "JVNDB 製品一覧の最終更新日 [例] 2025-04-26T07:36:21+09:00",
    "lang": "ja",
    "author": { "name": "IPA", "uri": "https://www.ipa.go.jp/" },
    "distribution": { "tlp": { "label": "CLEAR", "url": "https://www.first.org/tlp/" } },
    "vendors": [
      {
        "vendor_id": "JVNベンダ識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp",
        "vid": "ベンダ番号 (JVN iPedia におけるベンダの識別番号) [例] 99999999991",
        "vname": "ベンダ名 [例] 東京電機大学",
        "vfqdn": "ベンダプライマリドメイン [例] dendai.ac.jp",
        "vname_i18n": {
          "ja": "ベンダ名日本語 [例] 東京電機大学",
          "en": "ベンダ名英語 [例] Tokyo Denki University"
        },
        "cpe": "CPEベンダ識別子 (CPE v2.3 形式) [例] cpe:2.3::dendai.ac.jp",
        "products": [
          {
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp:myjvn_api:4.0.0",
            "pid": "製品番号 (JVN iPedia における製品の識別番号) [例] 99999999991001",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "pname_i18n": {
              "ja": "製品名日本語 [例] マイジェイブイエヌ API",
              "en": "製品名英語 [例] MyJVN API"
            },
            "version": "バージョン [例] 4.0.0",
            "product_ids": [{ "$comment": "getProductList 製品識別子フィールド参照" }]
          },
          { "$comment": "product_id,pid,pname,pname_i18n などを繰り返します。" }
        ],
        "modified": "ベンダ毎の製品の最終更新日 [例] 2025-04-06T02:00:00+09:00",
        "created": "ベンダ毎の製品の登録日 [例] 2024-04-01T12:10:56+09:00"
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
