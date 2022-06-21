# Welcome to MyJVN APIs!

* MyJVN API

| API名 | メソッド名 | 概要 | バージョン | 形式 |
| ---- | ---- | ---- | ---- | ---- | 
| 注意警戒情報一覧の取得 | getAlertList | 注意警戒情報一覧を取得します。 | [ HND ](getAlertList_api_hnd.md) | XML,JSON | 
| | | | [ OKA ](getAlertList_api_oka.md) | JSON | 
| ベンダ一覧の取得 | getVendorList | フィルタリング条件に当てはまるベンダ名(製品開発者)リストを取得します。 | [ HND ](getVendorList_api_hnd.md) | XML | 
| | | | [ OKA ](getVendorList_api_oka.md) | JSON | 
| 製品一覧の取得 | getProductList | フィルタリング条件に当てはまる製品名リストを取得します。 | [ HND ](getProductList_api_hnd.md) | XML | 
| | | | [ OKA ](getProductList_api_oka.md) | JSON | 
| 脆弱性対策概要情報一覧の取得 | getVulnOverviewList | フィルタリング条件に当てはまる脆弱性対策の概要情報リストを取得します。 | [ HND ](getVulnOverviewList_api_hnd.md) | XML | 
| | | | [ OKA ](getVulnOverviewList_api_oka.md) | JSON | 
| 脆弱性対策詳細情報の取得 | getVulnDetailInfo | フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。 | [ HND ](getVulnDetailInfo_api_hnd.md) | XML | 
| | getVulnCsafInfo | | [ OKA ](getVulnCsafInfo_api_oka.md) | JSON | 
| | getVulnStixInfo | | [ OKA ](getVulnStixInfo_api_oka.md) | JSON | 


* MyJVNデータフィード

| データフィード名 | 概要 | バージョン | 形式 |
| ---- | ---- | ---- | ---- | 
| JVNDBRSS | 脆弱性対策情報の概要 | HND | XML |
| | | OKA | JSON |
| 脆弱性対策情報詳細 | 脆弱性対策情報の詳細 | HND | XML |
| | | OKA | JSON |
| ベンダ一覧 | ベンダ名(製品開発者)リスト | HND | XML |
| | | OKA | [ JSON ](examples/jvnVendorDictionary_oka.json) |
| 製品一覧 | 製品名リスト | HND | XML |
| | バージョンなし | OKA | [ JSON ](examples/jvnProductDictionary_oka.json) |
| | バージョンあり | OKA | [ JSON ](examples/jvnProductDictionary_oka.json) |

* SBOM

| タイプ | 形式(例題) |
| ---- | ---- |
| SWID | [ XML ](sbom-swid.xml) |
| CycloneDX | [ JSON ](examples/sbom-cyclonedx.json) |
| SPDX | JSON |


* 謝辞

本サイトでは、総務省「ソフトウェア脆弱性を狙ったサイバー攻撃の防御に向けた情報共有基盤に関する実証実験」の成果を活用しています。 
