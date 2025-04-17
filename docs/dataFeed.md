# MyJVN データフィード

## JVNDBRSS (脆弱性対策情報の概要)

### Ver3.2 HND

- XML スキーマ

  - TBD

- \[例\]
  - [ dataFeed_jvndb_rss_hnd.xml ](../examples/dataFeed_jvndb_rss_hnd.xml)
  - 解説
  ```
  - rdf:RDF
    - channel
      - title
      - link
      - description
      - dc:creator
      - dc:date
      - dcterms:modified
      - items
   - item
      - title
      - link
      - description
      - sec:identifier
      - sec:references
      - sec:cpe
      - sec:cvss
      - dc:date
      - dcterms:issued
      - dcterms:modified
   - item
   :
  ```

<br>

### Ver4.0 OKA

- JSON スキーマ

  - TBD

- \[例\]
  - [ dataFeed_jvndb_rss_oka.json ](../examples/dataFeed_jvndb_rss_oka.json)
  - 解説
  ```
  - feed
    - generator
    - title
    - id
    - link
    - updated
    - lang
    - author
    - distribution
    - entry
      - title, id, summary, link, update, published, references, products, metrics, cwes
  ```

<br>
<br>

## 脆弱性対策情報詳細 (脆弱性対策情報の詳細)

### Ver3.2 HND

- XML スキーマ

  - TBD

- \[例\]
  - [ dataFeed_jvndb_detail_hnd.xml ](../examples/dataFeed_jvndb_detail_hnd.xml)
  - 解説
  ```
  - VULDEF-Document
    - Vulinfo
      - VulinfoID
      - VulinfoData
        - Title
        - VulinfoDescription
        - Affected
        - Impact
        - Solution
        - Related
        - History
        - DateFirstPublished
        - DateLastUpdated
        - DatePublic
  ```

<br>

### Ver4.0 OKA

- JSON スキーマ

  - TBD

- \[例\]
  - [ dataFeed_jvndb_detail_oka.json ](../examples/dataFeed_jvndb_detail_oka.json)
  - 解説
  ```
  - format
  - version
  - timestamp
  - VULDEF-Document
    - document
      - category, csaf_version, distribution, title, lang, notes, tracking, publisher, references
    - product_tree
      - branches
    - vulnerabilities
      - cve, cwes, product_status
  ```

<br>
<br>

## ベンダ一覧 (ベンダ名（製品開発者）リスト)

### Ver3.2 HND

- XML スキーマ

  - TBD

- \[例\]
  - [ dataFeed_myjvn_vendor_hnd.xml ](../examples/dataFeed_myjvn_vendor_hnd.xml)
  - 解説
  ```
  - VendorInfo
    - Vendor (vname, cpe, vid)
  ```

<br>

### Ver4.0 OKA

- JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250414
  [ jvnpid_1.0.json ](../schema/jvnpid_1.0.json)

- \[例\]
  - [ dataFeed_myjvn_product_oka.json ](../examples/dataFeed_myjvn_product_oka.json)
  - 解説
  ```
  - jvn_product_dictionary
    - vendors
      - vendor_id, vid, vname, vname_i18, cpe
  ```

<br>
<br>

## 製品一覧 (製品名リスト)

### Ver3.2 HND

- XML スキーマ

  - TBD

- \[例\]
  - [ dataFeed_myjvn_product_hnd.xml ](../examples/dataFeed_myjvn_product_hnd.xml) バージョン表記なし
  - 解説
  ```
  - VendorInfo
    - Vendor (vname, cpe, vid)
      - Product (pname, cpe, pid)
  ```

<br>

### Ver4.0 OKA

- JSON スキーマ

- Vendor and Product Dictionary for MyJVN
  https://jvndb.jvn.jp/schema/jvnpid_1.0.json?20250414
  [ jvnpid_1.0.json ](../schema/jvnpid_1.0.json)

- \[例\]

  - [ dataFeed_myjvn_product_oka.json ](../examples/dataFeed_myjvn_product_oka.json) バージョン表記なし
  - 解説

  ```
  - jvn_product_dictionary
    - vendors
      - vendor_id, vid, vname, vname_i18, cpe
      - products
        - product_id, pid, pname, pname_i18, product_ids
      - revision_history
        - date, number, summary
  ```

- \[例\]
  - [ dataFeed_myjvn_product_version_oka.json ](../examples/dataFeed_myjvn_product_version_oka.json) バージョン表記あり
  - 解説
  ```
  - jvn_product_dictionary
    - vendors
      - vendor_id, vid, vname, vname_i18, cpe
      - products
        - product_id, pid, pname, pname_i18, version, product_ids
      - revision_history
        - date, number, summary
  ```
