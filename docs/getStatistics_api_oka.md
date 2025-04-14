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

| パラメタ名      | 名称                   | パラメタ値                                                                                                                                                | 必須 | デフォルト |
| --------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method          | メソッド名             | getStatistics (固定)                                                                                                                                      | ○    | －         |
| feed            | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> hnd を指定                                                                                           | ○    | －         |
| nameType        | 製品識別子タイプ       | cpe, jvnpid, vid, pid のいずれかひとつ                                                                                                                    | －   | －         |
| productName     | 製品識別子             | type=cpe: cpe v2.3 形式　<br> type=jvnpid: jvnpid v1.0 形式 <br>nameType=vid: JVN iPedia におけるベンダ番号 <br>nameType=pid: JVN iPedia における製品番号 | －   | －         |
| cweId           | CWE 識別子             | CWE 番号                                                                                                                                                  | －   | －         |
| metricType      | 評価タイプ             | cvssV2, cvssV3, cvssV4 のいずれかひとつ                                                                                                                   | －   | cvssV3     |
| datePublicStart | 発見日開始年           | 整数 4 桁                                                                                                                                                 | －   | 1998       |
| datePublicEnd   | 発見日終了年           | 整数 4 桁                                                                                                                                                 | －   | －         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

- \[例\]  
   JVN iPedia の統計情報を取得したい場合 (1998年以降のCVSS ver3に関する統計情報)  
   ( datePublicStart=1998, metricType=cvssv3 )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka`

#### nameType

製品識別子タイプとして、\[cpe \| jvnpid \| vid \| pid \]のいずれか一つを指定します。

#### productName & nameType=cpe

製品識別子として、CPE 製品識別子を指定します。

- cpe:2.3{part}:{vendor}:{product}  
  {part}フィールド ... \[ h | o | a | \* \]  
  {vendor}:{product}フィールド ... CPE ベンダ名、製品名
- ワイルドカード(\*) 指定可、アスキー文字、大文字／小文字区別なし、複数指定は不可
- バージョンが設定されていない情報とバージョンが設定された全ての情報を取得
- URL エンコードされたエスケープシーケンス
- \[例\]  
   Apache HTTPD 全てのバージョンに関する統計情報を取得したい場合  
   ( datePublicStart=1998, metricType=cvssV3 )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&nameType=cpe&ProductName=cpe:2.3:a:apache:http_server`

#### cweId

CWE 識別子として、CWE 番号を指定します。

- 複数指定は不可
- \[例\]  
   CWE-79 に関する統計情報を取得したい場合  
   ( datePublicStart=1998, metricType=cvssV3 )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&cweId=CWE-79`

#### metricType

評価タイプとして、\[ cvssV2 \| cvssV3 \| cvssV4 \]のいずれか一つを指定します。

- \[例\]  
   CVSS Ver4 に関する統計情報を取得したい場合  
   ( datePublicStart=1998 )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=oka&0etr5cType=cvssV4`

<br>
<br>

## レスポンス

### 概要

- 処理成功時、Result ノードの中に VendorInfo、MyJVN 共通 Status ノードを含む XML を応答します。ただし、フィルタリング結果が 0 件の場合、Result ノードの中に MyJVN 共通 Status ノードのみを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

```
{
  "format": "mjstat:sumJvnDb",
  "version": "4.0.0",
  "timestamp": "2025-04-02T00:38:11+09:00",
  "dataTotal": {
    "vulinfo": 234156,
    "vendor": 30054,
    "product": 77871
  },
  "dataFilter": {"cweId": "CWE-79", "nameType":"jvnpid", "productName": "jvnpid:1.0::ipa" , "metricType": "cvssV3" },
  "data": [
    {
      "year": "1999",
      "total_vulinfo": 4,
      "total_seveirty_critical": 4,
      "total_seveirty_high": 0,
      "total_seveirty_medium": 0,
      "total_seveirty_low": 0,
      "total_seveirty_none": 0,
      "vulinfo": {
        "1": 1,
        "2": 1,
        "3": 1,
        "4": 1
      },
      "seveirty_critical": {
        "1": 1,
        "2": 1,
        "3": 1,
        "4": 1
      },
      "seveirty_high": {
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      },
      "seveirty_medium": {
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      },
      "seveirty_low": {
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      },
      "seveirty_none": {
        "1": 0,
        "2": 0,
        "3": 0,
        "4": 0
      }
    }
  ]
}

```
