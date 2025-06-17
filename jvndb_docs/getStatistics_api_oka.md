# getStatistics (ver. OKA)

脆弱性対策情報を、登録件数(脆弱性統計情報)、深刻度(CVSS 統計情報)、脆弱性種別(CWE 統計情報)で集計したデータを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

 <br>

| パラメタ名   | 名称                   | パラメタ値                                                                                                                                                | 必須 | デフォルト |
| ------------ | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method       | メソッド名             | getStatistics (固定)                                                                                                                                      | ○    | －         |
| feed         | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> oka を指定                                                                                           | ○    | －         |
| pubStartDate | 登録日開始年           | 整数 4 桁                                                                                                                                                 | －   | －         |
| pubEndDate   | 登録日終了年           | 整数 4 桁                                                                                                                                                 |
| nameType     | 製品識別子タイプ       | cpe, jvnpid, vid, pid のいずれかひとつ                                                                                                                    | －   | －         |
| productName  | 製品識別子             | type=cpe: cpe v2.3 形式　<br> type=jvnpid: jvnpid v1.0 形式 <br>nameType=vid: JVN iPedia におけるベンダ番号 <br>nameType=pid: JVN iPedia における製品番号 | －   | －         |
| cweId        | CWE 識別子             | CWE 番号                                                                                                                                                  | －   | －         |
| metricType   | 評価タイプ             | cvssV2, cvssV3, cvssV4 のいずれかひとつ                                                                                                                   | －   | cvssV3     |
|              |

<br>

### 解説

<details>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

- 必須パラメタ以外を指定しない場合には、pubStartDate=現在の年、metricType=cvssV3 を適用するため、CVSS Ver3 に関する、現在の年の 1 月～ 12 月分の統計情報を出力します。

- \[例\] 必須パラメタのみを指定して統計情報を取得したい場合  
   ( pubStartDate=現在の年, metricType=cvssv3 )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka`

<br>

#### pubStartDate & pubEndDate

登録日開始年、登録日終了年を指定します。

- pubStartDate の最小値は 1998
- pubStartDate のみの指定の場合には、登録日開始年以降、API 実行日までが対象となります。
- pubEndDate のみの指定の場合には、1998 年から登録日終了年以前が対象となります。
- \[例\] 登録日の期間を指定して統計情報を取得したい場合 (metricType=cvssV3)  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&pubStartDate=2005`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&pubEndDate=2025`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&pubStartDate=2005&pubEndDate=2025`

<br>

#### nameType

製品識別子タイプとして、\[ cpe \| jvnpid \| vid \| pid \]のいずれか一つを指定します。

<br>

#### productName & nameType=cpe

製品識別子として、CPE 製品識別子を指定します。

- productName & nameType, cweId, metricType, pubStartDate & pubEndDate は、組み合わせて使用できます。
- cpe:2.3{part}:{vendor}:{product}  
  {part}フィールド ... \[ h | o | a | \* \]  
  {vendor}:{product}フィールド ... CPE ベンダ名、製品名
- ワイルドカード(\*) 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定は不可
- URL エンコードされたエスケープシーケンス
- \[例\] Apache HTTPD 全てのバージョンに関する統計情報を取得したい場合  
   ( lastModStartDate=現在の年, metricType=cvssV3 )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&nameType=cpe&ProductName=cpe:2.3:a:apache:http_server`

<br>

#### cweId

CWE 識別子として、CWE 番号を指定します。

- productName & nameType, cweId, metricType, pubStartDate & pubEndDate は、組み合わせて使用できます。
- 複数指定は不可
- \[例\] CWE-79 に関する統計情報を取得したい場合 (pubStartDate=現在の年, metricType=cvssV3)  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&cweId=CWE-79`

<br>

#### metricType

評価タイプとして、\[ cvssV2 \| cvssV3 \| cvssV4 \]のいずれか一つを指定します。

- productName & nameType, cweId, metricType, pubStartDate & pubEndDate は、組み合わせて使用できます。
- \[例\] CVSS Ver4 に関する統計情報を取得したい場合 (pubStartDate=現在の年)  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&metricType=cvssV4`

</details>
<br>
<br>

## レスポンス

### 概要

- 処理成功時、datatotal、data、MyJVN 共通 status を含む JSON を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- MyJVN Statistics：https://jvndb.jvn.jp/schema/myjvn_statistics_1.0.json

### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/myjvn_statistics_1.0.json",
  "generator": {
    "date": "レスポンス生成日",
    "engine": {
      "version": "4.0.0",
      "name": "MyJVN API"
    }
  },
  "title": "JVNDB 脆弱性対策統計データ",
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
  "dataTotal": {
    "$comment": "脆弱性対策情報総件数、ベンダ総件数、製品総件数",
    "vulninfo": 234156,
    "vendor": 30054,
    "product": 77871
  },
  "dataFilter": {
    "$comment": "指定されたパラメタを記録します。",
    "nameType": "製品識別子タイプ",
    "productName": "製品識別子",
    "cweId": "CWE 番号",
    "metricType": "評価タイプ",
    "lastModStartDate": "最終更新日開始年",
    "lastModEndDate": "最終更新日終了年",
    "pubStartDate": "登録日開始年",
    "pubEndDate": "登録日終了年"
  },
  "data": [
    {
      "$comment": "該当年、該当年の脆弱性対策情報の件数、深刻度(緊急、重要、警告、注意、なし)の件数",
      "year": "2025",
      "total_vulninfo": 4,
      "total_severity_critical": 4,
      "total_severity_high": 0,
      "total_severity_medium": 0,
      "total_severity_low": 0,
      "total_severity_none": 0,
      "vulninfo": {
        "$comment": "毎月の脆弱性対策情報の件数",
        "1": 1,
        "2": 1,
        "3": 1,
        "4": 1
      },
      "severity_critical": {
        "$comment": "毎月の深刻度(緊急)の件数",
        "1": 1,
        "2": 1,
        "3": 1,
        "4": 1
      },
      "severity_high": {
        "$comment": "毎月の深刻度(重要)の件数",
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      },
      "severity_medium": {
        "$comment": "毎月の深刻度(警告)の件数",
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      },
      "severity_low": {
        "$comment": "毎月の深刻度(注意)の件数",
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      },
      "severity_none": {
        "$comment": "毎月の深刻度(なし)の件数",
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      }
    }
  ],
  "status": {
    "version": "4.0.0",
    "method": "getStatistics",
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
