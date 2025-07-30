# Welcome to MyJVN APIs!

## MyJVN API

| API 名                       | メソッド名          | 概要                                                                         | Ver3.2 <br> HND                                      | Ver4.0 <br> OKA                               |
| ---------------------------- | ------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------- | --------------------------------------------- |
| 注意警戒情報一覧の取得       | getAlertList        | 注意警戒情報一覧を取得します。                                               | [ XML <br> JSON ](docs/getAlertList_api_hnd.md) <br> | [ JSON ](docs/getAlertList_api_oka.md)        |
| ベンダ一覧の取得             | getVendorList       | フィルタリング条件に当てはまるベンダ名(製品開発者)リストを取得します。       | [ XML ](docs/getVendorList_api_hnd.md)               | [ JSON ](docs/getVendorList_api_oka.md)       |
| 製品一覧の取得               | getProductList      | フィルタリング条件に当てはまる製品名リストを取得します。                     | [ XML ](docs/getProductList_api_hnd.md)              | [ JSON ](docs/getProductList_api_oka.md)      |
| 脆弱性対策概要情報一覧の取得 | getVulnOverviewList | フィルタリング条件に当てはまる脆弱性対策の概要情報リストを取得します。       | [ XML ](docs/getVulnOverviewList_api_hnd.md)         | [ JSON ](docs/getVulnOverviewList_api_oka.md) |
| 脆弱性対策詳細情報の取得     | getVulnDetailInfo   | フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。             | [ XML ](docs/getVulnDetailInfo_api_hnd.md)           | [ JSON ](docs/getVulnDetailInfo_api_oka.md)   |
| 脆弱性対策情報統計データの取得     | getStatistics       | 脆弱性対策情報を、登録件数、深刻度、脆弱性種別で集計したデータを取得します。 | [ XML ](docs/getStatistics_api_hnd.md)               | [ JSON ](docs/getStatistics_api_oka.md)       |

<br>
<br>

## MyJVN データフィード

| データフィード名   | 概要                              | Ver3.2 <br> HND           | Ver4.0 <br> OKA            |
| ------------------ | --------------------------------- | ------------------------- | -------------------------- |
| JVNDBRSS           | 脆弱性対策情報の概要              | [ XML ](docs/dataFeed.md) | [ JSON ](docs/dataFeed.md) |
| 脆弱性対策情報詳細 | 脆弱性対策情報の詳細              | [ XML ](docs/dataFeed.md) | [ JSON ](docs/dataFeed.md) |
| ベンダ辞書         | ベンダ名(製品開発者)リスト        | [ XML ](docs/dataFeed.md) | [ JSON ](docs/dataFeed.md) |
| 製品辞書           | 製品名リスト (バージョン表記なし) | [ XML ](docs/dataFeed.md) | [ JSON ](docs/dataFeed.md) |
| 製品辞書           | 製品名リスト (バージョン表記あり) |                           | [ JSON ](docs/dataFeed.md) |

<br>
<br>

## 謝辞

本サイトでは、総務省「ソフトウェア脆弱性を狙ったサイバー攻撃の防御に向けた情報共有基盤に関する実証実験」の成果を活用しています。
