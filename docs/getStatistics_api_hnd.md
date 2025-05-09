# getStatistics (ver. HND)

脆弱性対策情報を、登録件数(脆弱性統計情報)、深刻度(CVSSv3 統計情報)、脆弱性種別(CWE 統計情報)で集計したデータを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

 <br>

| パラメタ名       | 名称                   | パラメタ値                                                                                                                               | 必須 | デフォルト |
| ---------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---- | ---------- |
| method           | メソッド名             | getStatistics (固定)                                                                                                                     | ○    | －         |
| feed             | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> hnd を指定                                                                          | ○    | －         |
| theme            | データ集計種別         | sumAll: 全てのテーマ <br> sumJvnDb: 登録件数(脆弱性統計情報) <br> sumCvss: 深刻度(CVSSv3 統計情報) <br> sumCwe: 脆弱性種別(CWE 統計情報) | ○    | －         |
| type             | データ集計タイプ       | y: 年毎の集計 <br> q: 四半期毎の集計 <br> m: 月毎の集計                                                                                  | －   | －         |
| cweId            | CWE 識別子             |                                                                                                                                          | －   | －         |
| pid              | 製品 ID                | 整数                                                                                                                                     | －   | －         |
| cpeName          | CPE 製品名             | cpe v2.2 形式                                                                                                                            | －   | －         |
| datePublicStartY | 発見日開始年           | 整数 4 桁                                                                                                                                | －   | －         |
| datePublicStartM | 発見日開始月           | 整数 2 桁(1 ～ 12)                                                                                                                       | －   | －         |
| datePublicEndY   | 発見日終了年           | 整数 4 桁                                                                                                                                | －   | －         |
| datePublicEndM   | 発見日終了月           | 整数 2 桁(1 ～ 12)                                                                                                                       | －   | －         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### 年毎の集計(type=y)：開始年以降、現在年まで

- \[例\] 2004 年以降の場合 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=y&datePublicStartY=2004`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=y&datePublicStartY=2004`

- \[例\] 2004 年以降、cweId=CWE-79 の場合 ( theme=sumAll, sumCWE )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumAll&cweId=CWE-79&type=y&datePublicStartY=2004`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCwe&cweId=CWE-79&type=y&datePublicStartY=2004`

<br>

#### 年毎の集計(type=y)：終了年まで

- \[例\] 2010 年以前の場合 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=y&datePublicEndY=2010`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=y&datePublicEndY=2010`

<br>

#### 年毎の集計(type=y)：範囲指定

- \[例\] 2004 年～ 2010 年 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=y&datePublicStartY=2004&datePublicEndY=2010`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=y&datePublicStartY=2004&datePublicEndY=2010`

<br>
<br>
#### 四半期毎の集計(type=q)：開始年以降、現在年まで

- \[例\] 2004 年以降の場合 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=q&datePublicStartY=2004`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=q&datePublicStartY=2004`

- \[例\] 2004 年以降、cweId=CWE-79 の場合 ( theme=sumAll, sumCWE )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumAll&cweId=CWE-79&type=q&datePublicStartY=2004`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCwe&cweId=CWE-79&type=q&datePublicStartY=2004`

<br>

#### 四半期毎の集計(type=q)：終了年まで

- \[例\] 2010 年以前の場合 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=q&datePublicEndY=2010`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=q&datePublicEndY=2010`

<br>

#### 四半期毎の集計(type=q)：範囲指定

- \[例\] 2004 年～ 2010 年 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=q&datePublicStartY=2004&datePublicEndY=2010`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=q&datePublicStartY=2004&datePublicEndY=2010`

<br>
<br>

#### 月毎の集計(type=m)：開始年月以降、現在年月まで

- \[例\] 2004 年 2 月以降の場合 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=m&datePublicStartY=2004&datePublicStartM=2`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=m&datePublicStartY=2004&datePublicStartM=2`

- \[例\] 2004 年 2 月以降、cweId=CWE-79 の場合 ( theme=sumAll, sumCWE )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumAll&cweId=CWE-79&type=m&datePublicStartY=2004&datePublicStartM=2`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCwe&cweId=CWE-79&type=m&datePublicStartY=2004&datePublicStartM=2`

<br>

#### 月毎の集計(type=m)：終了年まで

- \[例\] 2010 年 3 月以前の場合 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=m&datePublicEndY=2010&datePublicEndM=3`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=m&datePublicEndY=2010&datePublicEndM=3`

<br>

#### 月毎の集計(type=m)：範囲指定

- \[例\] 2004 年 2 月～ 2010 年 3 月 ( theme=sumJvnDb, sumCvss )  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumJvnDb&type=m&datePublicStartY=2004&datePublicStartM=2&datePublicEndY=2010&datePublicEndM=3`  
   `https://jvndb.jvn.jp/myjvn?method=getStatistics&feed=hnd&theme=sumCvss&type=m&datePublicStartY=2004&&datePublicStartM=2&datePublicEndY=2010&datePublicEndM=3`

<br>
<br>

## レスポンス

### 概要

- 処理成功時、Result ノードの中に VendorInfo、MyJVN 共通 Status ノードを含む XML を応答します。ただし、フィルタリング結果が 0 件の場合、Result ノードの中に MyJVN 共通 Status ノードのみを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### XML スキーマ

- Result ノード：http://jvndb.jvn.jp/schema/results_3.3.xsd
- MyJVN 共通 Status ノード：http://jvndb.jvn.jp/schema/status_3.3.xsd

### 例

- [ getStatistics_hnd_sumJvnDb.xml ](../examples/hnd/getStatistics_hnd_sumJvnDb.xml)
- [ getStatistics_hnd_sumCvss.xml ](../examples/hnd/getStatistics_hnd_sumCvss.xml)
- [ getStatistics_hnd_sumAll.xml ](../examples/hnd/getStatistics_hnd_sumAll.xml)
- [ getStatistics_hnd_sumCwe.xml ](../examples/hnd/getStatistics_hnd_sumCwe.xml)

### 解説

```
<?xml version="1.0" encoding="UTF-8"?>
<Result version="3.3"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:mjres="http://jvndb.jvn.jp/myjvn/Results"
  xmlns:mjstat="http://jvndb.jvn.jp/myjvn/Statistics"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xsi:schemaLocation="http://jvndb.jvn.jp/myjvn/Results https://jvndb.jvn.jp/schema/results_3.3.xsd"
  >

  <!-- theme=sumJvnDb の場合 -->
  <mjstat:sumJvnDb>
    <mjstat:title xml:lang="ja">脆弱性統計情報</mjstat:title>
    <mjstat:title xml:lang="en-US">Statistics Vulnerability Count</mjstat:title>
    <mjstat:resDataTotal
      vulinfo="脆弱性対策情報総件数"
      vendor="ベンダ総件数"
      product="製品総件数" />
    <mjstat:resData
      date="集計期間"
      cntAll="登録件数" />
    <mjstat:resData date="2008" cntAll="71" />
    <mjstat:resData date="2009" cntAll="110" />
    <!-- 集計期間分 mjstat:resData を繰り返します。 -->
    <!-- mjstat:resData の date に記載される値は、 type=y の場合 年(yyyy形式)、 
         type=m の場合 年月(yyyy-mm形式)、 type=q の場合 四半期(yyyy-(1～4)Q形式)となります。 -->
  </mjstat:sumJvnDb>

  <!-- theme=sumCvss の場合 -->
  <mjstat:sumCvss>
    <mjstat:title xml:lang="ja">CVSSスコア</mjstat:title>
    <mjstat:title xml:lang="en-US">CVSS Score</mjstat:title>
    <mjstat:resDataTotal
      vulinfo="脆弱性対策情報総件数"
      vendor="ベンダ総件数"
      product="製品総件数" />
    <mjstat:resData
      date="集計期間"
      cntAll="総件数"
      cntC="深刻度(緊急)の件数"
      cntH="深刻度(重要)の件数"
      cntM="深刻度(警告)の件数"
      cntL="深刻度(注意)の件数"
      cntN="深刻度(なし意)の件数" />
    <mjstat:resData date="2008" cntAll="71" cntC="17" cntH="40" cntM="14" cntL="0" cntN="0" />
    <mjstat:resData date="2009" cntAll="110" cntC="16" cntH="54" cntM="38" cntL="2" cntN="0" />
    <!-- 集計期間分 mjstat:resData を繰り返します。 -->
  </mjstat:sumCvss>

  <!-- theme=sumCwe の場合 -->
  <mjstat:sumCwe
    cweId="CWE 識別子 [例] CWE-79">
    <mjstat:title xml:lang="ja">CWE 識別子のタイトル(日本語) [例] クロスサイトスクリプティング</mjstat:title>
    <mjstat:title xml:lang="en-US">CWE 識別子のタイトル(英語) [例] Cross-site Scripting</mjstat:title>
    <mjstat:resDataTotal
      vulinfo="脆弱性対策情報総件数"
      vendor="ベンダ総件数"
      product="製品総件数" />
    <mjstat:resData
      date="集計期間"
      cntAll="件数" />
    <mjstat:resData date="2008" cntAll="0" />
    <mjstat:resData date="2009" cntAll="9" />
    <!-- 集計期間分 mjstat:resData を繰り返します。 -->
  </mjstat:sumCwe>

  <!-- theme=sumAll の場合 -->
  <mjstat:sumJvnDb>
    <mjstat:title xml:lang="ja">脆弱性統計情報</mjstat:title>
    <mjstat:title xml:lang="en-US">Statistics Vulnerability Count</mjstat:title>
    <mjstat:resDataTotal
      vulinfo="脆弱性対策情報総件数"
      vendor="ベンダ総件数"
      product="製品総件数" />
    <mjstat:resData
      date="集計期間"
      cntAll="登録件数" />
    <mjstat:resData date="2008" cntAll="71" />
    <mjstat:resData date="2009" cntAll="110" />
  </mjstat:sumJvnDb>

  <mjstat:sumCvss>
    <mjstat:title xml:lang="ja">CVSSスコア</mjstat:title>
    <mjstat:title xml:lang="en-US">CVSS Score</mjstat:title>
    <mjstat:resDataTotal
      vulinfo="脆弱性対策情報総件数"
      vendor="ベンダ総件数"
      product="製品総件数" />
    <mjstat:resData
      date="集計期間"
      cntAll="総件数"
      cntC="深刻度(緊急)の件数"
      cntH="深刻度(重要)の件数"
      cntM="深刻度(警告)の件数"
      cntL="深刻度(注意)の件数"
      cntN="深刻度(なし意)の件数" />
    <mjstat:resData date="2008" cntAll="71" cntC="17" cntH="40" cntM="14" cntL="0" cntN="0" />
    <mjstat:resData date="2009" cntAll="110" cntC="16" cntH="54" cntM="38" cntL="2" cntN="0" />
    <!-- 集計期間分 mjstat:resData を繰り返します。 -->
  </mjstat:sumCvss>

  <mjstat:sumCwe
    cweId="CWE 識別子 [例] CWE-79">
    <mjstat:title xml:lang="ja">CWE 識別子のタイトル(日本語) [例] クロスサイトスクリプティング</mjstat:title>
    <mjstat:title xml:lang="en-US">CWE 識別子のタイトル(英語) [例] Cross-site Scripting</mjstat:title>
    <mjstat:resDataTotal
      vulinfo="脆弱性対策情報総件数"
      vendor="ベンダ総件数"
      product="製品総件数" />
    <mjstat:resData
      date="集計期間"
      cntAll="件数" />
    <mjstat:resData date="2008" cntAll="0" />
    <mjstat:resData date="2009" cntAll="9" />
    <!-- 集計期間分 mjstat:resData を繰り返します。 -->
  </mjstat:sumCwe>

  <status:Status
    version="3.3"
    method="getAlertList"
    feed="hnd"
    lang="表示言語"
    retCd="リターンコード (0:成功時、1:エラー時)"
    retMax="エントリ上限値"
    errCd="エラーコード (処理成功時は空文字列)"
    errMsg="エラーメッセージ (処理成功時は空文字列)"
    totalRes="応答エントリ総数"
    totalResRet="応答エントリ数"
    firstRes="応答エントリ開始位置">
    <!-- 各リクエストパラメタ -->
  </status:Status>

</Result>
```
