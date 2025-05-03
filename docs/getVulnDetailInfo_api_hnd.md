# getVulnDetailInfo (ver. HND)

フィルタリング条件に当てはまる脆弱性対策の詳細情報を取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=hnd&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

<br>
 
| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getVulnDetailInfo (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> hndを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 1～10 (getVulnDetailInfoエントリ上限値)  | － | 10 |
| vulnId | 脆弱性対策情報ID | JVNDB-YYYY-XXXXXX <br> JVNDB ... プレフィックス <br> YYYY ... 整数4桁 <br> XXXXXX ... 整数6桁 | ○ | － |
| lang | 表示言語 | ja:日本語、en:英語 | － | ja |

<br>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### vulnId

脆弱性対策情報 ID を指定します。

- 複数指定時は "+" で連結
- \[例\] JVNDB-2017-009608 を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getVulnDetailInfo&feed=hnd&vulnId=JVNDB-2017-009608`

<br>
<br>

## レスポンス

### 概要

- 処理成功時、VULDEF 3.2、MyJVN 共通 Status ノードを含む XML を応答します。ただし、フィルタリング結果が 0 件の場合、Result ノードの中に MyJVN 共通 Status ノードのみを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### XML スキーマ

- VULDEF 3.2：http://jvndb.jvn.jp/schema/vuldef_3.2.xsd
- mod_sec 3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

### 例

- [ getVulnDetailInfo_hnd_JVNDB-2017-009608 (CVE=1, CWE=1, CVSS=2, Ver=NONE) ](../examples/getVulnDetailInfo_hnd_JVNDB-2017-009608.xml)
- [ getVulnDetailInfo_hnd_JVNDB-2018-009328 (CVE=1, CWE=1, CVSS=2, Ver=PRESENT) ](../examples/getVulnDetailInfo_hnd_JVNDB-2018-009328.xml)
- [ getVulnDetailInfo_hnd_JVNDB-2021-002774 (CVE=1, CWE=0, CVSS=0, Ver=PRESENT) ](../examples/getVulnDetailInfo_hnd_JVNDB-2021-002774.xml)
- [ getVulnDetailInfo_hnd_JVNDB-2022-000097 (CVE=3, CWE=2, CVSS=6, Ver=NONE ) ](../examples/getVulnDetailInfo_hnd_JVNDB-2022-000097.xml)

### 解説

```
<?xml version="1.0" encoding="UTF-8"?>
<VULDEF-Document 
  version="3.2"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://jvn.jp/vuldef/"
  xmlns:vuldef="http://jvn.jp/vuldef/"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xmlns:sec="http://jvn.jp/rss/mod_sec/3.0/"
  xmlns:marking="http://data-marking.mitre.org/Marking-1"
  xmlns:tlpMarking="http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1"
  xsi:schemaLocation="http://jvn.jp/vuldef/ https://jvndb.jvn.jp/schema/vuldef_3.2.xsd
                      http://jvn.jp/rss/mod_sec/3.0/ https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
                      http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1 https://jvndb.jvn.jp/schema/tlp_marking.xsd
                      http://jvndb.jvn.jp/myjvn/Status https://jvndb.jvn.jp/schema/status_3.3.xsd"
  xml:lang="ja"
  >
  <Vulinfo>
    <VulinfoID>脆弱性対策情報の識別子 (JVNDB-西暦-番号) [例] JVNDB-2025-000000</VulinfoID>
    <VulinfoData>
      <Title>タイトル [例] MyJVN API セキュリティ情報</Title>
      <VulinfoDescription>
        <Overview>セキュリティ情報の概要 [例] MyJVN API は、APIを介してセキュリティ情報を提供するシステムです。</Overview>
      </VulinfoDescription>
      <Affected>
        <AffectedItem>
          <Name>ベンダ名 [例] 東京電機大学</Name>
          <ProductName>製品名 [例] マイジェイブイエヌ API</ProductName>
          <VersionNumber>バージョン [例] 4.0.0</VersionNumber>
          <!-- バージョン情報の件数分 VersionNumber ノードを繰り返します。 -->
        </AffectedItem>
        <!-- 製品の件数分 AffectedItem を繰り返します。 -->
      </Affected>

      <Impact>
        <Cvss version="CVSS バージョン 2.0">
          <Severity type="基本|現状|環境評価基準 (Base, Temp, Env)">typeで指定された評価基準の深刻度 (Low, Medium, High)</Severity>
          <Vector>パラメタ短縮表記 [例] AV:N/AC:L/Au:N/C:C/I:C/A:C</Vector>
          <Base>基本値 [例] 10.0</Base>
        </Cvss>
        <Cvss version="CVSS バージョン 3.0">
          <Severity type="基本|現状|環境評価基準 (Base, Temp, Env)">typeで指定された評価基準の深刻度 (None, Low, Medium,
            High, Critical)</Severity>
          <Vector>パラメタ短縮表記 [例] CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H</Vector>
          <Base>基本値 [例] 9.8</Base>
        </Cvss>
        <ImpactItem>
          <Description>想定される影響 [例] 情報を取得される可能性があります。</Description>
        </ImpactItem>
      </Impact>

      <Solution>
        <SolutionItem>
          <Description>対策 [例] 参考情報を参照して適切な対策を実施してください。</Description>
        </SolutionItem>
      </Solution>

      <Related>
        <RelatedItem type="advisory">
          <Name>情報源 [例] advisory</Name>
          <VulinfoID>参考情報のタイトル or 概要 [例] IPA security-alert</VulinfoID>
          <URL>参考情報のURL [例] https://www.ipa.go.jp/security/security-alert/</URL>
        </RelatedItem>
        <!-- 参考情報の件数分 RelatedItem を繰り返します。 -->
        <RelatedItem type="cwe">
          <Name>JVNDB</Name>
          <VulinfoID>CWE 番号 [例] CWE-502</VulinfoID>
          <Title>CWE 説明 [例] 信頼できないデータのデシリアライゼーション(CWE-502)</Title>
          <URL>CWE 掲載 URL [例] https://cwe.mitre.org/data/definitions/502.html</URL>
        </RelatedItem>
        <!-- CWE情報の件数分 RelatedItem を繰り返します。 -->
      </Related>

      <History>
        <HistoryItem>
          <HistoryNo>更新バージョン [例] 1</HistoryNo>
          <DateTime>履歴記載日 [例] 2025-04-04T14:45:58+09:00</DateTime>
          <Description>更新内容 [例] 初版</Description>
        </HistoryItem>
        <HistoryItem>
          <HistoryNo>更新バージョン [例] 2</HistoryNo>
          <DateTime>履歴記載日 [例] 2025-04-26T07:36:21+09:00</DateTime>
          <Description>更新内容 [例] 更新版</Description>
        </HistoryItem>
      </History>

      <DateFirstPublished>登録日 [例] 2025-04-04T14:45:58+09:00</DateFirstPublished>
      <DateLastUpdated>最終更新日 [例] 2025-04-26T07:36:21+09:00</DateLastUpdated>
      <DatePublic>公表日 [例] 2025-04-01T10:23:42+09:00</DatePublic>
    </VulinfoData>

  </Vulinfo>
  <!-- フィルタリングに当てはまる脆弱性対策詳細情報の件数分 Vulinfo を繰り返します。 -->
  <sec:handling>
    <marking:Marking>
      <marking:Marking_Structure xsi:type="tlpMarking:TLPMarkingStructureType"
        marking_model_name="TLP" marking_model_ref="http://www.us-cert.gov/tlp/" color="WHITE" />
    </marking:Marking>
  </sec:handling>
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
    firstRes="応答エントリ開始位置">
    <!-- 各リクエストパラメタ -->
  </status:Status>
</VULDEF-Document>
```
