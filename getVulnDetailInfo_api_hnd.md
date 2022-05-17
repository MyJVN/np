# getVulnDetailInfo (ver. HND)
フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=hnd&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
 
| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVulnDetailInfo (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> hndを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～10 (getVulnDetailInfoエントリ上限値)  | － | 10 |
| vulnId | 脆弱性対策情報ID | 整数 (半角数字) <br> JVNDB-YYYY-XXXXXX <br> JVNDB ... プレフィックス <br> YYYY ... 整数4桁 (半角数字) <br> XXXXXX ... 整数6桁 (半角数字) | － | － |
| lang | 表示言語(日本語／英語) | ja:日本語、en:英語 | － | ja |

\*1)  
「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)にMyJVN API側で自動的に設定する値です。  

## レスポンス
* 概要
  * 処理成功時、VULDEF 3.2、MyJVN共通Statusノードを含むXMLを応答します。ただし、フィルタリング結果が0件の場合、Resultノードの中にMyJVN共通Statusノードのみを含むXMLを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* XMLスキーマ
  * VULDEF 3.2：http://jvndb.jvn.jp/schema/vuldef_3.2.xsd
  * mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
  * MyJVN共通Statusノード：https://jvndb.jvn.jp/schema/status_3.3.xsd
* 例
  * [ getVulnDetailInfo_hnd.xml ](examples/getVulnDetailInfo_hnd.xml)

```
<?xml version="1.0" encoding="UTF-8" ?>
<?xml-stylesheet href="VulnDetailInfo.xsl" type=text/xsl"?>
<VULDEF-Document version="3.1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="https://jvn.jp/vuldef/"
xmlns:vuldef="https://jvn.jp/vuldef/"
xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
xsi:schemaLocation="https://jvn.jp/vuldef/
https://jvndb.jvn.jp/schema/vuldef_3.2.xsd
https://jvn.jp/rss/mod_sec/3.0/
https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
http://jvndb.jvn.jp/myjvn/Status
https://jvndb.jvn.jp/schema/status_3.3.xsd"
xml:lang="ja">

<Vulinfo>
  <VulinfoID>脆弱性情報ID</VulinfoID>
  <VulinfoData>
    <Title>タイトル</Title>
    <VulinfoDescription>
      <Overview>概要</Overview>
    </VulinfoDescription>
    <Affected>
    <AffectedItem>
        <Name>ベンダ名</Name>
        <ProductName>製品名</ProductName>
        <VersionNumber>バージョン情報</VersionNumber>
        バージョン情報の件数分 VersionNumber ノードを繰り返します。
      </AffectedItem>
      製品の件数分 AffectedItem ノードを繰り返します。
    </Affected>

    <Impact>
      <Cvss version="CVSS バージョン">
        <Severity type="基本|現状|環境評価基準">typeで指定された評価基準の深刻度</Severity>
        <Vector>短縮表記</Vector>
        <Base>CVSS 基本値</Base>
      </Cvss>
      <ImpactItem>
        <Description>想定される影響</Description>
      </ImpactItem>
    </Impact>

    <Solution>
      <SolutionItem>
        <Description>対策</Description>
      </SolutionItem>
    </Solution>

    <Related>
      <RelatedItem type="advisory">
        <Name>アドバイザリ情報源</Name>
        <VulinfoID>アドバイザリID</VulinfoID>
        <URL>アドバイザリURL</URL>
      </RelatedItem>
      ：アドバイザリ情報の件数分 RelatedItem ノードを繰り返します。
      <RelatedItem type="cwe">
        <Name>JVNDB</Name>
        <VulinfoID>CWE-ID</VulinfoID>
        <Title>CWE名</Title>
        <URL>CWEURL</URL>
      </RelatedItem>
      ：CWE情報の件数分 RelatedItem ノードを繰り返します。
    </Related>

    <History>
      <HistoryItem>
        <Description>更新履歴</Description>
      </HistoryItem>
    </History>

    <DateFirstPublished>公開日</DateFirstPublished>
    <DateLastUpdated>最終更新日</DateLastUpdated>
    <DatePublic>発見日</DatePublic >
  </VulinfoData>

</Vulinfo>
フィルタリングに当てはまる脆弱性対策詳細情報の件数分 Vulinfo ノードを繰り返します。

<status:Status
version="3.3"
method="getVulnDetailInfo"
feed="hnd"
lang="表示言語"
retCd="リターンコード (0:成功時、1:エラー時) "
retMax="エントリ上限値"
errCd="エラーコード (処理成功時は空文字列) "
errMsg="エラーメッセージ (処理成功時は空文字列) "
totalRes="応答エントリ総数"
totalResRet="応答エントリ数"
firstRes="応答エントリ開始位置"
各リクエストパラメタ
</status:Status>
</Result>
</VULDEF-Document> 

```