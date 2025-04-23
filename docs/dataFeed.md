# MyJVN データフィード

## JVNDBRSS (脆弱性対策情報の概要)

### Ver3.2 HND

#### XML スキーマ

- JVNRSS 3.2：https://jvndb.jvn.jp/schema/jvnrss_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd

#### 例

- [ dataFeed_jvndb_rss_hnd.xml ](../examples/dataFeed_jvndb_rss_hnd.xml)

#### 解説

```
- rdf:RDF
  - channel: チャンネル情報
    - title, link, description: チャンネルタイトル、URL、概要
    - dc:date：発行日
    - dcterms:modified: 更新日
    - items
  - item: 脆弱性対策情報
    - title, link, description: 脆弱性対策情報タイトル、URL、概要
    - sec:identifier: 脆弱性対策情報識別子
    - sec:references: 参考情報
    - sec:cpe: CPE製品識別子
    - sec:cvss: CVSS深刻度
    - dc:date: 更新日
    - dcterms:issued: 発行日
    - dcterms:modified: 更新日
 :
```

<br>

### Ver4.0 OKA

#### JSON スキーマ

- MyJVN Feed
  - https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json?20250419
  - [ myjvn_feed_1.0.json ](../schemas/myjvn_feed_1.0.json)

#### 例

- [ dataFeed_jvndb_rss_oka.json ](../examples/dataFeed_jvndb_rss_oka.json)

#### 解説

```
- feed
  - generator, title, systemid, link: データフィードタイトル、URL
  - updated: 更新日
  - lang: 表示言語
  - author: 発行者
  - distribution: TLP
  - entry: 脆弱性対策情報
    - title: タイトル
    - id: 脆弱性対策情報識別子
    - summary: 概要
    - link: URL
    - update: 更新日
    - published: 発行日
    - references: 参考情報
    - products: 影響を受ける製品
    - metrics: 脆弱性深刻度
    - cwes: 脆弱性種別
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

- [ dataFeed_jvndb_detail_hnd.xml ](../examples/dataFeed_jvndb_detail_hnd.xml)

#### 解説

```
- VULDEF-Document
  - Vulinfo
    - VulinfoID: 脆弱性対策情報識別子
    - VulinfoData: 脆弱性対策情報
      - Title: タイトル
      - VulinfoDescription: 概要
      - Affected: 影響を受ける製品
      - Impact: 想定される影響
      - Solution: 対策
      - Related: 関連情報
      - History: 履歴
      - DateFirstPublished: 発行日
      - DateLastUpdated: 更新日
      - DatePublic: 発見日
```

<br>

### Ver4.0 OKA

#### JSON スキーマ

- VULDEF (VULINFO) - The Vulnerability Data Publication and Exchange Format Data Model for MyJVN
  - https://jvndb.jvn.jp/schema/myjvn_vuldef_1.0.vulinfo.json?20250419
  - [ myjvn_vuldef_1.0.vulinfo.json ](../schemas/myjvn_vuldef_1.0.vulinfo.json)

#### 例

- [ dataFeed_jvndb_detail_oka.json ](../examples/dataFeed_jvndb_detail_oka.json)

#### 解説

```
- generator, title, systemid, link: データフィードタイトル、URL
- updated: 更新日
- VULDEF-Document
  - document
    - category, csaf_version, distribution
    - title: 概要
    - lang: 表示言語
    - notes: 概要
    - tracking: 脆弱性対策情報識別子、更新日、発行日、履歴
    - publisher: 発行者
    - references: 参考情報
  - product_tree: 製品情報
  - vulnerabilities: 脆弱性情報
    - cve: CVE番号
    - cwes: 脆弱性種別
    - product_status: 影響を受ける製品
    - threats: 想定される影響
    - remediations: 対策
    - metrics: 脆弱性深刻度
```

<br>
<br>

## ベンダ一覧 (ベンダ名（製品開発者）リスト)

### Ver3.2 HND

#### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 例

- [ dataFeed_myjvn_vendor_hnd.xml ](../examples/dataFeed_myjvn_vendor_hnd.xml)

#### 解説

```
- VendorInfo
  - Vendor: ベンダ情報
    - vname: ベンダ名
    - cpe: CPEベンダ識別子
    - vid: ベンダ番号
```

<br>

### Ver4.0 OKA

#### JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  - https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419
  - [ jvnpid_1.0.json ](../schemas/jvnpid_1.0.json)

#### 例

- [ dataFeed_myjvn_product_oka.json ](../examples/dataFeed_myjvn_product_oka.json)

#### 解説

```
- jvn_product_dictionary
  - vendors: ベンダ情報
    - vendor_id: JVNベンダ識別子
    - vid: ベンダ番号
    - vname: ベンダ名
    - vname_i18: ベンダ名(多言語)
    - cpe: CPEベンダ識別子
```

<br>
<br>

## 製品一覧 (製品名リスト)

### Ver3.2 HND

#### XML スキーマ

- Result ノード：https://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

#### 例

- [ dataFeed_myjvn_product_hnd.xml ](../examples/dataFeed_myjvn_product_hnd.xml) バージョン表記なし

#### 解説

```
- VendorInfo
  - Vendor: ベンダ情報
    - vname: ベンダ名
    - cpe: CPEベンダ識別子
    - vid: ベンダ番号
    - Product: 製品情報
      - pname: 製品名
      - cpe: CPE製品識別子
      - pid: 製品番号
```

<br>

### Ver4.0 OKA

#### JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  - https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250419
  - [ jvnpid_1.0.json ](../schemas/jvnpid_1.0.json)

#### 例

- [ dataFeed_myjvn_product_oka.json ](../examples/dataFeed_myjvn_product_oka.json) バージョン表記なし

#### 解説

```
- jvn_product_dictionary
  - vendors: ベンダ情報
    - vendor_id: JVNベンダ識別子
    - vid: ベンダ番号
    - vname: ベンダ名
    - vname_i18: ベンダ名(多言語)
    - cpe: CPEベンダ識別子
    - products: 製品情報
      - product_id: JVN製品識別子
      - pid: 製品番号
      - pname: 製品名
      - pname_i18: 製品名(多言語)
      - product_ids: CPE製品識別子など
    - revision_history: 履歴
```

#### 例

- [ dataFeed_myjvn_product_version_oka.json ](../examples/dataFeed_myjvn_product_version_oka.json) バージョン表記あり

#### 解説

```
- jvn_product_dictionary
  - vendors: ベンダ情報
    - vendor_id: JVNベンダ識別子
    - vid: ベンダ番号
    - vname: ベンダ名
    - vname_i18: ベンダ名(多言語)
    - cpe: CPEベンダ識別子
    - products: 製品情報
      - product_id: JVN製品識別子
      - pid: 製品番号
      - pname: 製品名
      - pname_i18: 製品名(多言語)
      - version: バージョン
      - product_ids: CPE製品識別子など
    - revision_history: 履歴
```
