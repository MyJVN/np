# getVulnOverviewList (ver. HND)

フィルタリング条件に当てはまる脆弱性対策の概要情報リストを取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=hnd&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

| パラメタ名               | 名称                   | パラメタ値                                                      | 必須 | デフォルト |
| ------------------------ | ---------------------- | --------------------------------------------------------------- | ---- | ---------- |
| method                   | メソッド名             | getVulnOverviewList (固定)                                      | ○    | －         |
| feed                     | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> hnd を指定 | ○    | －         |
| startItem                | エントリ開始位置       | 整数 1 ～応答エントリ数                                         | －   | 1          |
| maxCountItem             | エントリ取得件数       | 整数 1 ～ 50 (getVulnOverviewList エントリ上限値)               | －   | 50         |
| cpeName                  | CPE 製品名             | cpe v2.2 形式                                                   | －   | －         |
| vendorId                 | ベンダ番号             | 整数                                                            | －   | －         |
| productId                | 製品番号               | 整数                                                            | －   | －         |
| keyword                  | キーワード             | URL エンコードされたキーワード                                  | －   | －         |
| severity                 | CVSS 深刻度            | n:なし、l:注意、m:警告、h:重要、c:緊急                          | －   | －         |
| vector                   | CVSS 基本評価基準      | CVSS 基本評価基準 CVSS v3.0 形式                                | －   | －         |
| rangeDatePublic          | 発見日の範囲指定       | n:範囲指定なし、w:過去 1 週間、m:過去 1 ヶ月                    | －   | w          |
| rangeDatePublished       | 更新日の範囲指定       | n:範囲指定なし、w:過去 1 週間、m:過去 1 ヶ月                    | －   | w          |
| rangeDateFirstPublished  | 発行日の範囲指定       | n:範囲指定なし、w:過去 1 週間、m:過去 1 ヶ月                    | －   | w          |
| datePublicStartY         | 発見日開始年           | 整数 4 桁                                                       | －   | －         |
| datePublicStartM         | 発見日開始月           | 整数 2 桁 1 ～ 12                                               | －   | －         |
| datePublicStartD         | 発見日開始日           | 整数 2 桁 1 ～ 31                                               | －   | －         |
| datePublicEndY           | 発見日終了年           | 整数 4 桁                                                       | －   | －         |
| datePublicEndM           | 発見日終了月           | 整数 2 桁 1 ～ 12                                               | －   | －         |
| datePublicEndD           | 発見日終了日           | 整数 2 桁 1 ～ 31                                               | －   | －         |
| datePublishedStartY      | 更新日開始年           | 整数 4 桁                                                       | －   | －         |
| datePublishedStartM      | 更新日開始月           | 整数 2 桁 1 ～ 12                                               | －   | －         |
| datePublishedStartD      | 更新日開始日           | 整数 2 桁 1 ～ 31                                               | －   | －         |
| datePublishedEndY        | 更新日終了年           | 整数 4 桁                                                       | －   | －         |
| datePublishedEndM        | 更新日終了月           | 整数 2 桁 1 ～ 12                                               | －   | －         |
| datePublishedEndD        | 更新日終了日           | 整数 2 桁 1 ～ 31                                               | －   | －         |
| dateFirstPublishedStartY | 発行日開始年           | 整数 4 桁                                                       | －   | －         |
| dateFirstPublishedStartM | 発行日開始月           | 整数 2 桁 1 ～ 12                                               | －   | －         |
| dateFirstPublishedStartD | 発行日開始日           | 整数 2 桁 1 ～ 31                                               | －   | －         |
| dateFirstPublishedEndY   | 発行日終了年           | 整数 4 桁                                                       | －   | －         |
| dateFirstPublishedEndM   | 発行日終了月           | 整数 2 桁 1 ～ 12                                               | －   | －         |
| dateFirstPublishedEndD   | 発行日終了日           | 整数 2 桁 1 ～ 31                                               | －   | －         |
| lang                     | 表示言語(日本語／英語) | ja:日本語、en:英語                                              | －   | ja         |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

- rangeDatePublic, rangeDatePublished, rangeDateFirstPublished を指定しない場合には、デフォルト値(w:過去 1 週間)に従い、過去 1 週間分の一覧を出力します。

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\]  
   1 件目から 50 件分のベンダ名を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=hnd&startItem=1&maxCountItem=50`

#### cpeName

CPE ベンダ名を指定します。

- cpe:/{part}:{vendor}  
   {part}フィールド ... \[ \* \| (NULL) \]  
   {vendor}フィールド ... CPE ベンダ名
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定時は "+" で連結
- URL エンコードされたエスケープシーケンス

#### keyword

脆弱性概要情報の部分一致によるフィルタリングします。

- ワイルドカード "\*" 指定不可 ("\*"を指定した場合、"\*"を含む項目をフィルタリング)
- 大文字／小文字区別なし
- charset=UTF-8

#### vector, severity

CVSSv3 基本評価基準、CVSSv3 深刻度を指定します。

- vector では、CVSSv3.0 形式を指定します。CVSS:3.0/AV:\[N,A,L,P\]/AC:\[L,H\]/PR:\[N,L,R\]/UI:\[N,R\]/S:\[C,U\]/C:\[N,L,H\]/I:\[N,L,H\]/A:\[N,L,H\]
- severity では、\[ n:なし \| l:注意 \| m:警告 \| h:重要 \| c:緊急 \]のいずれか一つを指定します。
- \[例\]  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=hnd&vector=CVSS:3.0/AV:L/AC:L/PR:L/UI:N/S:C/C:H/I:N/A:N`  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=hnd&severity=m`

#### rangeDatePublic , rangeDatePublished , rangeDateFirstPublished

発見日、更新日、発行日の範囲を指定します。

- \[例\]  
   `https://jvndb.jvn.jp/myjvn?method=getVulnOverviewList&feed=hnd&rangeDatePublic=n&rangeDatePublished=n&rangeDateFirstPublished=n`

<br>
<br>

## レスポンス

### 概要

- 処理成功時、JVNRSS 3.2(RSS 1.0 + mod_sec)、MyJVN 共通 Status ノードを含む XML を応答します。ただし、フィルタリング結果が 0 件の場合、Result ノードの中に MyJVN 共通 Status ノードのみを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### XML スキーマ

- JVNRSS 3.2：https://jvndb.jvn.jp/schema/jvnrss_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

### 例

- [ getVulnOverviewList_hnd.xml ](../examples/getVulnOverviewList_hnd.xml)

### 解説

```
<?xml version="1.0" encoding="UTF-8" ?>
<rdf:RDF xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="http://purl.org/rss/1.0/"
xmlns:rss="http://purl.org/rss/1.0/"
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:dcterms="http://purl.org/dc/terms/"
xmlns:sec="https://jvn.jp/rss/mod_sec/"
xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
xsi:schemaLocation="http://purl.org/rss/1.0/
https://jvndb.jvn.jp/schema/jvnrss_3.2.xsd"
xml:lang="ja">

<channel rdf:about="セキュリティ情報のチャンネルURI">
  <title>セキュリティ情報のチャンネルタイトル</title>
  <link>セキュリティ情報が掲載されているURI</link>
  <description>セキュリティ情報の概要</description>
  <dc:date>レスポンス生成日時</dc:date>
  <dcterms:issued />
  <dcterms:modified>レスポンス生成日時</dcterms:modified>
  <items>
  <rdf:Seq>
  <rdf:li rdf:resource="item要素のrdf:about属性と同じURI"/>
  <!-- フィルタリングに当てはまる脆弱性対策概要情報の件数分 <rdf:li rdf:resource= を繰り返します。 -->
  </rdf:Seq>
  </items>
</channel>

<item rdf:about="ベンダが掲載するセキュリティ情報のURI">
  <title>セキュリティ情報のタイトル</title>
  <link>セキュリティ情報のURI</link>
  <description>セキュリティ情報の概要</description>
  <sec:identifier>ベンダ固有のセキュリティ情報ID</sec:identifier>
  <sec:references source="発行元省略名" id="識別番号" title="タイトル" >関連情報</sec:references>
  <!-- 参考情報の件数分 sec:references ノードを繰り返します。 -->

  <sec:cpe version="CPEバージョン" vendor="ベンダ名" product="製品名">CPE製品名</sec:cpe>
  <!-- 製品情報の件数分 sec:cpe ノードを繰り返します。 -->

  <sec:cvss version="CVSS バージョン" type="基本|現状|環境評価基準" severity="typeで指定された評価基準の深刻度" score="typeで指定された評価基準の評価値" vector="短縮表記"/>
  <!-- 評価の件数分 sec:cvss ノードを繰り返します。 -->

  <dc:date>更新日</dc:date>
  <dcterms:issued>発行日</dcterms:issued>
  <dcterms:modified>更新日</dcterms:modified>
</item>
<!-- フィルタリングに当てはまる脆弱性対策概要情報の件数分itemノードを繰り返します。 -->

<status:Status
version="3.3"
method="getVulnOverviewList"
feed="hnd"
lang="表示言語"
retCd="リターンコード (0:成功時、1:エラー時) "
retMax="エントリ上限値"
errCd="エラーコード (処理成功時は空文字列) "
errMsg="エラーメッセージ (処理成功時は空文字列) "
totalRes="応答エントリ総数"
totalResRet="応答エントリ数"
firstRes="応答エントリ開始位置" >
<!-- 各リクエストパラメタ -->
</status:Status>
</rdf:RDF>
```
