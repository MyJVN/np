# getVulnOverviewList (ver. OKA)

フィルタリング条件に当てはまる脆弱性対策の概要情報リストを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

 <br>

| パラメタ名                         | 名称                   | パラメタ値                                                                                                                                                | 必須 | デフォルト |
| ---------------------------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method                             | メソッド名             | getVulnOverviewList (固定)                                                                                                                                | ○    | －         |
| feed                               | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定                                                                                           | ○    | －         |
| startItem                          | エントリ開始位置       | 整数 1 ～応答エントリ数                                                                                                                                   | －   | 1          |
| maxCountItem                       | エントリ取得件数       | 整数 1 ～ 50 (getVulnOverviewList エントリ上限値)                                                                                                         | －   | 50         |
| rangeLastModDate                   | 最終更新日の範囲指定   | NONE: 範囲指定なし、DAY: 前日以降 <br> WEEK:過去 1 週間以降、MONTH:過去 1 ヶ月以降                                                                        | －   | －         |
| lastModStartDate                   | 最終更新日開始年月日   | 整数 8 桁                                                                                                                                                 | －   | －         |
| lastModEndDate                     | 最終更新日終了年月日   | 整数 8 桁                                                                                                                                                 | －   | －         |
| pubStartDate                       | 登録日開始年月日       | 整数 8 桁                                                                                                                                                 | －   | －         |
| pubEndDate                         | 登録日終了年月日       | 整数 8 桁                                                                                                                                                 | －   | －         |
| nameType                           | 製品識別子タイプ       | cpe, jvnpid, vid, pid のいずれかひとつ                                                                                                                    | －   | －         |
| productName                        | 製品識別子             | type=cpe: cpe v2.3 形式　<br> type=jvnpid: jvnpid v1.0 形式 <br>nameType=vid: JVN iPedia におけるベンダ番号 <br>nameType=pid: JVN iPedia における製品番号 | －   | －         |
| version <br> versionType           | バージョン             | バージョン情報                                                                                                                                            | －   | －         |
| versionStart <br> versionStartType | 開始バージョン         | バージョン情報                                                                                                                                            | －   | －         |
| versionEnd <br> versionEndType     | 終了バージョン         | バージョン情報                                                                                                                                            | －   | －         |
| cvssV2Metrics                      | CVSSv2 基本評価基準    | CVSS v2 パラメタ                                                                                                                                          | －   | －         |
| cvssV2Severity                     | CVSSv2 深刻度          | LOW:注意、MEDIUM:警告、HIGH:重要                                                                                                                          | －   | －         |
| cvssV3Metrics                      | CVSSv3 基本評価基準    | CVSS v3 パラメタ                                                                                                                                          | －   | －         |
| cvssV3Severity                     | CVSSv3 深刻度          | NONE:なし、LOW:注意、MEDIUM:警告 <br> HIGH:重要、CRITICAL:緊急                                                                                            | －   | －         |
| cvssV4Metrics                      | CVSSv4 基本評価基準    | CVSS v4 パラメタ                                                                                                                                          | －   | －         |
| cvssV4Severity                     | CVSSv4 深刻度          | NONE:なし、LOW:注意、MEDIUM:警告 <br> HIGH:重要、CRITICAL:緊急                                                                                            | －   | －         |
| keyword                            | キーワード             | URL エンコードされたキーワード                                                                                                                            | －   | －         |
| lang                               | 表示言語(日本語／英語) | ja:日本語、en:英語                                                                                                                                        | －   | ja         |

<br>

### 解説

<details>

#### デフォルト

「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

- 期間パラメタ(rangeLastModDate, lastModStartDate & lastModEndDate, pubStartDate & pubEndDate)を指定しない場合には、最新順に一覧を出力します。

<br>

#### startItem , maxCountItem

エントリ開始位置、エントリ取得件数を指定します。

- \[例\] 1 件目から 50 件分の概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&startItem=1&maxCountItem=50`

<br>

#### rangeLastModDate

最終更新日の簡易な範囲を指定します。

- rangeLastModDate と(lastModStartDate & lastModEndDate, pubStartDate & pubEndDate)の同時使用はできません。
- \[ NONE: 範囲指定なし \| DAY: 前日以降 \| WEEK:過去 1 週間以降 \| MONTH:過去 1 ヶ月以降 \]のいずれか一つを指定します。
- \[例\]  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&rangeLastModDate=DAY`

<br>

#### lastModStartDate & lastModEndDate

最終更新日開始年月日、最終更新日終了年月日を指定します。

- rangeLastModDate と(lastModStartDate & lastModEndDate, pubStartDate & pubEndDate)の同時使用はできません。
- (lastModStartDate & lastModEndDate)と (pubStartDate & pubEndDate) とを組み合わせて使用できます。
- lastModStartDate の最小値は 19980101
- lastModStartDate のみの指定の場合には、最終更新日開始年月日以降、API 実行日までが対象となります。
- lastModEndDate のみの指定の場合には、1998 年から最終更新日終了年月日以前が対象となります。
- \[例\] 最終更新日の期間を指定して概要情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&lastModStartDate=20210804&lastModEndDate=20211022`

<br>

#### pubStartDate & pubEndDate

登録日開始年月日、登録日終了年月日を指定します。

- rangeLastModDate と(lastModStartDate & lastModEndDate, pubStartDate & pubEndDate)の同時使用はできません。
- (lastModStartDate & lastModEndDate)と (pubStartDate & pubEndDate) とを組み合わせて使用できます。
- pubStartDate の最小値は 19980101
- pubStartDate のみの指定の場合には、登録日開始年月日以降、API 実行日までが対象となります。
- pubEndDate のみの指定の場合には、1998 年から登録日終了年月日以前が対象となります。
- \[例\] 登録日の期間を指定して概要情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&pubStartDate=20210804&pubEndDate=20211022`
- \[例\] 登録日と最終更新日の期間を指定して概要情報を取得したい場合(2021 年に登録、2025 年に更新された概要情報)  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&pubStartDate=20210101&pubEndDate=20211231&lastModStartDate=20250101&lastModEndDate=20251231`

<br>

#### nameType

製品識別子タイプとして、\[cpe \| jvnpid \| vid \| pid \]のいずれか一つを指定します。

<br>

#### productName & nameType=cpe

製品識別子として、CPE 製品識別子を指定します。

- cpe:2.3{part}:{vendor}:{product}  
  {part}フィールド ... \[ h | o | a | \* \]  
  {vendor}:{product}フィールド ... CPE ベンダ名、製品名
- ワイルドカード(\*) 指定可、アスキー文字、大文字／小文字区別なし、複数指定は不可
- バージョンが設定されていない情報とバージョンが設定された全ての情報を取得
- URL エンコードされたエスケープシーケンス
- \[例\]  
   Apache HTTPD 全てのバージョンに関する概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=cpe&ProductName=cpe:2.3:a:apache:http_server`

<br>

#### productName & nameType=jvnpid

製品識別子として、JVN 製品識別子を指定します。

- jvnpid:1.0::{vendor}:{product}  
  {vendor}:{product}フィールド ... JVN ベンダ名、製品名
- ワイルドカード(\*) 指定可、アスキー文字、大文字／小文字区別なし、複数指定は不可
- バージョンが設定されていない情報とバージョンが設定された全ての情報を取得
- URL エンコードされたエスケープシーケンス
- \[例\] Apache HTTPD 全てのバージョンに関する概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=jvnpid&ProductName=jvnpid:1.0::apache:http_server`

<br>

#### productName & nameType=vid

製品識別子として、JVN iPedia におけるベンダ番号を指定します。

- \[例\] Apache Software Foundation(vid=8)に関する概要情報の一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=vid&ProductName=8`

<br>

#### productName & nameType=pid

製品識別子として、JVN iPedia における製品番号を指定します。

- \[例\] Apache HTTPD(pid=141)に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=pid&ProductName=141`

<br>

#### version & versionType

cpe あるいは、jvnpid のバージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart, versionEnd)の同時使用はできません。
- version の指定あり、versionType の指定なしの場合には、equal がデフォルト値となります。
- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\] Apache HTTPD 1.3.1.1 に関する概要情報一覧を取得したい場合
  `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&version=1.3.1.1`
- versionType

  | オペレータ名 | 使用可パラメタ | 操作 |
  | --------------------- | ---------------------- | ---------------------- |
  | no | version | バージョンが設定されていない情報を取得 (version 値は未設定) |
  | all | version | バージョンが設定された全ての情報を取得 (version 値は未設定) |
  | equal | version | version の値に一致したバージョンを持つ情報を取得 <br> versitonType が指定されていない場合のデフォルト値 |

<br>

#### versionStart & versionStartType

cpe あるいは、jvnpid の開始バージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart, versionEnd)の同時使用はできません。
- versionStart,versionEnd は同時使用あるいは、いずれか一方のみの使用ができます。
- versionStart の指定あり、versionStartType の指定なしの場合には、including がデフォルト値となります。
- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\] Apache HTTPD 1.3.1.1 以上に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&versionStart=1.3.1.1&versionStartType=including`
- versionStartType

  |オペレータ名 | 使用可パラメタ | 操作|
  | --------------------- | ---------------------- | ---------------------- |
  |including | versionStartType | バージョンを含む<br> versionStartType が指定されていない場合のデフォルト値|
  |excluding | versionStartType | バージョンを含まない|

<br>

#### versionEnd & versionEndType

cpe あるいは、jvnpid の終了バージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart,versionEnd)の同時使用はできません。
- versionStart,versionEnd は同時使用あるいは、いずれか一方のみの使用ができます。
- versionEnd の指定あり、versionEndType の指定なしの場合には、including がデフォルト値となります。
- nameType=cpe あるいは、nameType=jvnpid のみ使用可
- \[例\] Apache HTTPD 1.3.1.1 以下に関する概要情報一覧を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&nameType=cpe&productName=cpe:2.3:a:apache:http_server&versionEnd=1.3.1.1&versionEndType=including`
- versionEndType

  |オペレータ名 | 使用可パラメタ | 操作|
  | --------------------- | ---------------------- | ---------------------- |
  |including | versionEndType | バージョンを含む<br> versionEndType が指定されていない場合のデフォルト値|
  |excluding | versionEndType | バージョンを含まない|

<br>

#### cvssV2Metrics、cvssV2Severity

CVSSv2 基本評価基準、CVSSv2 深刻度を指定します。

- \[cvssV2Metrics \| cvssV3Metrics \| cvssV4Metrics \| cvssV2Severity \| cvssV3Severity \| cvssV4Severity\]のいずれか一つを指定します。
- cvssV2Metrics では、Base Metric の部分検索はできません。
- cvssV2Severity では、LOW:注意、MEDIUM:警告、HIGH:重要、のいずれか一つを指定します。
- \[例\]  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&cvssV2Metrics=AV:L/AC:H/Au:M/C:N/I:N/A:N`  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&cvssV2Severity=LOW`

<br>

#### cvssV3Metrics、cvssV3Severity

CVSSv3 基本評価基準、CVSSv3 深刻度を指定します。

- \[cvssV2Metrics \| cvssV3Metrics \| cvssV4Metrics \| cvssV2Severity \| cvssV3Severity \| cvssV4Severity\]のいずれか一つを指定します。
- cvssV3Metrics では、Base Metric の部分検索はできません。
- cvssV3Severity では、NONE:なし、l:注意、MEDIUM:警告、HIGH:重要、CRITICAL:緊急、のいずれか一つを指定します。
- \[例\]  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&cvssV3Metrics=AV:L/AC:L/PR:L/UI:R/S:U/C:N/I:L/A:L`  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&cvssV3Severity=MEDIUM`

<br>

#### cvssV4Metrics、cvssV4Severity

CVSSv4 基本評価基準、CVSSv4 深刻度を指定します。

- \[cvssV2Metrics \| cvssV3Metrics \| cvssV4Metrics \| cvssV2Severity \| cvssV3Severity \| cvssV4Severity\]のいずれか一つを指定します。
- CVSSv4 Base Metric の部分検索ができます。
- \[例\]  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&cvssV4Metrics=AV:A/AC:H/PR:H/UI:N`  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=oka&cvssV4Severity=CRITICAL`

<br>

#### keyword

脆弱性概要情報の部分一致によるフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

</details>
<br>
<br>

## レスポンス

### 概要

- 処理成功時、feed、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。
- バージョン情報については、製品一覧 (製品名リスト) バージョン表記あり に登録されている製品のみを出力します。

### JSON スキーマ

- MyJVN Feed：https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json


### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json",
  "feed": {
    "generator": {
      "date": "レスポンス生成日",
      "engine": {
        "version": "4.0.0",
        "name": "MyJVN API"
      }
    },
    "title": "JVNDB 脆弱性対策情報",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "updated": "",
    "lang": "表示言語 (ja:日本語、en:英語 )",
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
    "entry": [
      {
        "title": "脆弱性対策情報のタイトル",
        "id": "脆弱性対策情報の識別子 (JVNDB-西暦-番号)",
        "summary": "脆弱性対策情報の概要",
        "link": "脆弱性対策情報の概要のURL",
        "modified": "最終更新日",
        "created": "登録日",
        "public": "公表日",
        "references": [
          {
            "summary": "参考情報のタイトル or 概要",
            "url": "参考情報のURL",
            "source": "情報源"
          },
          {
            "$comment": "url,summary などを繰り返します。"
          }
        ],
        "products": [
          {
            "$comment": "jvnpidがバージョン情報を出力しない場合",
            "vname": "ベンダ名",
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "product_ids": {
              "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:*:*:*:*:*:*:*:*",
              "id_refs": [
                {
                  "nameType": "purl",
                  "value": "Package-Manager値"
                },
                {
                  "nameType": "swid",
                  "value": "一意な識別子"
                }
              ]
            }
          },
          {
            "$comment": "jvnpidがバージョン情報を出力する場合",
            "vname": "ベンダ名",
            "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::ipa:myjvn_api:4.0.0",
            "pname": "製品名 [例] マイジェイブイエヌ API",
            "version": "バージョン [例] 4.0.0",
            "product_ids": {
              "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:ipa:myjvn_api:4.0.0:*:*:*:*:*:*:*",
              "id_refs": [
                {
                  "nameType": "purl",
                  "value": "Package-Manager値"
                },
                {
                  "nameType": "sha256",
                  "value": "ハッシュ値"
                },
                {
                  "nameType": "spdx",
                  "value": "一意な識別子"
                },
                {
                  "nameType": "uuid",
                  "value": "一意な識別子"
                },
                {
                  "nameType": "tei",
                  "value": "TEI (Transparency Exchange API) 識別子"
                },
                {
                  "nameType": "swid",
                  "value": "一意な識別子"
                }
              ]
            }
          },
          {
            "$comment": "vname,product_id などを繰り返します。"
          }
        ],
        "metrics": [
          {
            "content": {
              "cvss_v2": {
                "version": "CVSSバージョン 2.0",
                "vectorString": "パラメタ短縮表記",
                "baseScore": "基本値",
                "baseSeverity": "基本値深刻度 (LOW, MEDIUM, HIGH)"
              },
              "cvss_v3": {
                "version": "CVSSバージョン 3.0 or 3.1",
                "vectorString": "パラメタ短縮表記",
                "baseScore": "基本値",
                "baseSeverity": "基本値深刻度 (NONE, LOW, MEDIUM, HIGH, CRITICAL)"
              },
              "cvss_v4": {
                "version": "CVSSバージョン 4.0",
                "vectorString": "パラメタ短縮表記",
                "baseScore": "基本値",
                "baseSeverity": "基本値深刻度 (NONE, LOW, MEDIUM, HIGH, CRITICAL)"
              },
              "ScoringSystem": {
                "name": "スコアリングシステムの名称",
                "version": "バージョン",
                "vectorString": "パラメタ短縮表記",
                "baseScore": "基本値",
                "baseSeverity": "基本値深刻度"
              }
            }
          }
        ],
        "cwes": [
          {
            "id": "CWE 番号",
            "name": "CWE 説明",
            "url": "CWE 掲載 URL"
          }
        ]
      },
      {
        "$comment": "title,id などを繰り返します。"
      }
    ]
  },
  "status:Status": {
    "version": "4.0.0",
    "method": "getVulnOverviewList",
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
