# getAlertList (ver. OKA)

注意警戒情報一覧を取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

<br>

| パラメタ名                         | 名称                   | パラメタ値                                                                                                                                                | 必須 | デフォルト |
| ---------------------------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method                             | メソッド名             | getAlertList (固定)                                                                                                                                       | ○    | －         |
| feed                               | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定                                                                                           | ○    | －         |
| startItem                          | エントリ開始位置       | 1 ～応答エントリ数                                                                                                                                        | －   | 1          |
| maxCountItem                       | エントリ取得件数       | 1 ～ 50 (getAlertList エントリ上限値)                                                                                                                     | －   | 50         |
| lastModStartDate                   | 最終更新日開始年月日   | 整数 8 桁                                                                                                                                                 | －   | －         |
| lastModEndDate                     | 最終更新日終了年月日   | 整数 8 桁                                                                                                                                                 | －   | －         |
| pubStartDate                       | 登録日開始年月日       | 整数 8 桁                                                                                                                                                 | －   | －         |
| pubEndDate                         | 登録日終了年月日       | 整数 8 桁                                                                                                                                                 | －   | －         |
| nameType                           | 製品識別子タイプ       | cpe, jvnpid, vid, pid のいずれかひとつ                                                                                                                    | －   | －         |
| productName                        | 製品識別子             | type=cpe: cpe v2.3 形式　<br> type=jvnpid: jvnpid v1.0 形式 <br>nameType=vid: JVN iPedia におけるベンダ番号 <br>nameType=pid: JVN iPedia における製品番号 | －   | －         |
| version <br> versionType           | バージョン             | バージョン情報                                                                                                                                            | －   | －         |
| versionStart <br> versionStartType | 開始バージョン         | バージョン情報                                                                                                                                            | －   | －         |
| versionEnd <br> versionEndType     | 終了バージョン         | バージョン情報                                                                                                                                            | －   | －         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

- lastModStartDate & lastModEndDate, pubStartDate & pubEndDate の指定がない場合には、全期間が対象となります。

<br>

#### startItem , maxCountItem

- \[例\] 1 件目から 50 件分の注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&startItem=1&maxCountItem=50`

<br>

#### lastModStartDate & lastModEndDate

最終更新日開始年月日、最終更新日終了年月日を指定します。

- (lastModStartDate & lastModEndDate)と (pubStartDate & pubEndDate) とを組み合わせて使用できます。
- lastModStartDate の最小値は 19980101
- lastModStartDate のみの指定の場合には、最終更新日開始年月日以降、API 実行日までが対象となります。
- lastModEndDate のみの指定の場合には、1998 年から最終更新日終了年月日以前が対象となります。
- \[例\] 最終更新日の期間を指定して注意喚起情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&lastModStartDate=20210804&lastModEndDate=20211022`

<br>

#### pubStartDate & pubEndDate

登録日開始年月日、登録日終了年月日を指定します。

- (lastModStartDate & lastModEndDate)と (pubStartDate & pubEndDate) とを組み合わせて使用できます。
- pubStartDate の最小値は 19980101
- pubStartDate のみの指定の場合には、登録日開始年月日以降、API 実行日までが対象となります。
- pubEndDate のみの指定の場合には、1998 年から登録日終了年月日以前が対象となります。
- \[例\] 登録日の期間を指定して注意喚起情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&pubStartDate=20210804&pubEndDate=20211022`
- \[例\] 登録日と最終更新日の期間を指定して注意喚起情報を取得したい場合(2021 年に登録、2025 年に更新された概要情報)  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&pubStartDate=20210101&pubEndDate=20211231&lastModStartDate=20250101&lastModEndDate=20251231`

<br>

#### nameType

製品識別子タイプとして、\[ cpe \| jvnpid \| vid \| pid \]のいずれか一つを指定します。

<br>

#### productName (type=cpe)

製品識別子として、CPE 製品識別子を指定します。

- cpe:2.3{part}:{vendor}:{product}:{version}  
   {part}フィールド ... \[ h \| o \| a \| \* \]  
   {vendor}:{product}:{version}フィールド ... CPE ベンダ名、製品名、バージョン
- ワイルドカード(\*) 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定は不可
- バージョンが未指定(NULL)、もしくはワイルドカード(\*)が指定された場合、全てのバージョン情報を取得します。
- URL エンコードされたエスケープシーケンス
- \[例\] Apache HTTPD 全てのバージョンに関する注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&type=cpe&ProductName=cpe:2.3:a:apache:http_server`
- \[例\] Apache HTTPD 1.3.1.1 に関する注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&cpeName=cpe:2.3:a:apache:http_server:1.3.1.1`

<br>

#### productName (type=jvnpid)

製品識別子として、JVN 製品識別子を指定します。

- jvnpid:1.0::{vendor}:{product}:{version} <br> {vendor}:{product}:{version}フィールド ... JVN ベンダ名、製品名、バージョン
- ワイルドカード(\*) 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定は不可
- バージョンが未指定(NULL)、もしくはワイルドカード(\*)が指定された場合、全てのバージョン情報を取得します。
- URL エンコードされたエスケープシーケンス
- \[例\] Apache HTTPD 全てのバージョンに関する注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&type=jvnpid&ProductName=jvnpid:1.0::apache:http_server`

<br>

#### productName (type=vid)

製品識別子として、JVN iPedia におけるベンダ番号を指定します。

- \[例\] Apache Software Foundation(vid=8)に関する注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&type=vid&ProductName=8`

<br>

#### productName (type=pid)

製品識別子として、JVN iPedia における製品番号を指定します。

- \[例\] Apache HTTPD(pid=141)に関する注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=oka&type=pid&ProductName=141`

<br>

#### version & versionType

cpe あるいは、jvnpid のバージョン(0 文字以上の ASCII 文字列)を指定します。

- version と(versionStart,versionEnd)の同時使用はできません。
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

- version と(versionStart,versionEnd)の同時使用はできません。
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

#### keyword

製品名の部分一致によりフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

<br>
<br>

## レスポンス(JSON)

### 概要

- 処理成功時、feed、MyJVN 共通 status を含む JSON(UTF-8)を応答します。
- エラー発生時、MyJVN 共通 status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- MyJVN Feed
  - https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json?20250419 
  - [ myjvn_feed_1.0.json ](../schemas/oka/myjvn_feed_1.0.json)

### 例

- [ getAlertList_oka.json ](../examples/oka/getAlertList_oka.json)

### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_feed_1.0.json?20250419",
  "feed": {
    "generator": {
      "date": "レスポンス生成日 [例] 2025-04-30T11:36:12+09:00",
      "engine": {
        "version": "4.0.0",
        "name": "MyJVN API"
      }
    },
    "title": "IPA注意警戒サービスAPI",
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
        "title": "注意警戒情報のタイトル [例] MyJVN APIに関するセキュリティ情報",
        "id": "注意警戒情報の識別子 (MYJVN-ALT-西暦-番号) [例] MYJVN-ALT-2025-0000",
        "summary": "注意警戒情報の概要 [例] 更新に関する連絡です。",
        "link": "注意警戒情報のURL [例] https://www.ipa.go.jp/security/",
        "category": {
          "term": "カテゴリ名 (Info, Low, Medium, High, Critical)",
          "label": "カテゴリラベル (お知らせ, 注意, 警告, 重要, 緊急)"
        },
        "modified": "最終更新日 [例] 2025-04-26T07:36:21+09:00",
        "created": "登録日 [例] 2025-04-04T14:45:58+09:00",
        "public": "公表日 [例] 2025-04-01T10:23:42+09:00",
        "items": [
          {
            "$comment": "jvnpi dがバージョン情報を出力しない場合",
            "title": "関連情報のタイトル [例] IPA security-alert",
            "id": "関連情報の識別子 (MYJVN-ALT-西暦-番号-サブ番号) [例] MYJVN-ALT-2025-0000-0001",
            "summary": "関連情報の概要 [例] MyJVN APIの仕様",
            "link": "関連情報の概要のURL [例] https://www.ipa.go.jp/security/security-alert/",
            "modified": "最終更新日 [例] 2025-04-26T07:36:21+09:00",
            "created": "登録日 [例] 2025-04-04T14:45:58+09:00",
            "public": "公表日 [例] 2025-04-01T10:23:42+09:00",
            "author": "発行者 [例] IPA",
            "products": [
              {
                "$comment": "jvnpid がバージョン情報を出力しない場合",
                "vname": "ベンダ名 [例] 東京電機大学",
                "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp:myjvn_api",
                "pname": "製品名 [例] マイジェイブイエヌ API",
                "product_ids": {
                  "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:dendai.ac.jp:myjvn_api:*:*:*:*:*:*:*:*",
                  "id_refs": [
                    {
                      "nameType": "purl",
                      "value": "Package-Manager値 [例] pkg:rpm/dendai.ac.jp/myjvn_api"
                    },
                    {
                     "nameType": "swid",
                     "value": "一意な識別子 [例] swid:dendai.ac.jp+myjvn_api"
                    }
                  ]
                }
              }
            ]
          },
          {
            "$comment": "jvnpid がバージョン情報を出力する場合",
            "title": "関連情報のタイトル [例] IPA security-alert MyJVN API v4.0.0に関する更新情報",
            "id": "関連情報の識別子 (MYJVN-ALT-西暦-番号-サブ番号) [例] MYJVN-ALT-2025-0000-0002",
            "summary": "関連情報の概要 [例] MyJVN API v4.0.0の仕様",
            "link": "関連情報の概要のURL [例] https://www.ipa.go.jp/security/security-alert/",
            "modified": "最終更新日 [例] 2025-04-26T07:36:21+09:00",
            "created": "登録日 [例] 2025-04-04T14:45:58+09:00",
            "public": "公表日 [例] 2025-04-01T10:23:42+09:00",
            "author": "発行者 [例] IPA",
            "products": [
              {
                "$comment": "jvnpid がバージョン情報を出力する場合",
                "vname": "ベンダ名 [例] 東京電機大学",
                "product_id": "JVN製品識別子 (jvnpid 1.0 形式) [例] jvnpid:1.0::dendai.ac.jp:myjvn_api:4.0.0",
                "pname": "製品名 [例] マイジェイブイエヌ API",
                "version": "バージョン [例] 4.0.0",
                "product_ids": {
                  "cpe": "CPE製品識別子 (CPE v2.3 形式) [例] cpe:2.3:a:dendai.ac.jp:myjvn_api:4.0.0:*:*:*:*:*:*:*",
                  "id_refs": [
                    {
                      "nameType": "purl",
                      "value": "Package-Manager値 [例] pkg:rpm/dendai.ac.jp/myjvn_api@4.0.0"
                    },
                    {
                      "nameType": "sha256",
                      "value": "ハッシュ値 [例] 4ce633e7bc8cb97e9ea4e966a70b4748b46c7f7c0e572b0172ca4d24b5795561"
                    },
                    {
                      "nameType": "spdx",
                      "value": "一意な識別子 [例] http://dendai.ac.jp/spdxdocs#SPDXRef-myjvn_api-v4.0.0"
                    },
                    {
                      "nameType": "uuid",
                      "value": "一意な識別子 [例] 186ce5f8-0049-953a-37da-bc89c6f07aa1"
                    },
                    {
                      "nameType": "tei",
                      "value": "TEI (Transparency Exchange API) 識別子 [例] urn:tei:uuid:dendai.ac.jp:186ce5f8-0049-953a-37da-bc89c6f07aa1"
                    },
                    {
                      "nameType": "swid",
                      "value": "一意な識別子 [例] swid:dendai.ac.jp+myjvn_api+4.0.0"
                    }
                  ]
                }
              }
            ]
          }
          { "$comment": "title,id などを繰り返します。" }
        ]
      }
    ]
  },
  "status": {
    "version": "4.0",
    "method": "getAlertList",
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
