# getAlertList (ver. HND)

注意警戒情報一覧を取得します。

## リクエスト

- `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=hnd&パラメタ名=パラメタ値&...`
  - リクエスト URL は、HTTPS の GET および POST に対応しています。

### パラメタ

- メソッド名、パラメタ名は大文字小文字を区別しています。
- 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
- 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。
- 整数は半角数字を使用します。

<br>

| パラメタ名         | 名称                   | パラメタ値                                                      | 必須 | デフォルト |
| ------------------ | ---------------------- | --------------------------------------------------------------- | ---- | ---------- |
| method             | メソッド名             | getAlertList (固定)                                             | ○    | －         |
| feed               | フィードフォーマット名 | フィードフォーマット(=API バージョン)を示す名称 <br> hnd を指定 | ○    | －         |
| startItem          | エントリ開始位置       | 1 ～応答エントリ数                                              | －   | 1          |
| maxCountItem       | エントリ取得件数       | 1 ～ 50 (getAlertList エントリ上限値)                           | －   | 50         |
| datePublished      | 更新年                 | 整数 4 桁                                                       | －   | －         |
| dateFirstPublished | 発行年                 | 整数 4 桁                                                       | －   | －         |
| cpeName            | CPE 製品識別子         | CPE v2.2 形式                                                   | －   | －         |
| ft                 | 応答フォーマット       | xml または json                                                 | －   | xml        |

<br>

### 解説

<details>

#### デフォルト

該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)に MyJVN API 側で自動的に設定する値です。

<br>

#### startItem , maxCountItem

エントリ開始位置とエントリ取得件数を指定します。

- \[例\] 1 件目から 50 件分の注意警戒情報を取得したい場合  
  `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=hnd&startItem=1&maxCountItem=50`

<br>

#### datePublished , dateFirstPublished

更新年、発行年を指定します。

- \[例\] 2024 年に更新された注意警戒情報を取得したい場合  
  `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=hnd&datePublished=2024`

<br>

#### cpeName

CPE 製品識別子を指定します。

- cpe:/{part}:{vendor}:{product}  
   {part}フィールド ... \[ h \| o \| a \| \* \]  
   {vendor}:{product}フィールド ... CPE ベンダ名、CPE 製品名
- ワイルドカード "\*" 指定可、アスキー文字、大文字／小文字区別なし
- 複数指定時は "+" で連結
- URL エンコードされたエスケープシーケンス
- \[例\] cpe:/a:apache:xerces-c%2B%2B の場合  
   `cpeName=cpe:/a:apache:xerces-c%252B%252B`
- \[例\] Wordpress に関する注意警戒情報を取得したい場合  
   `https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=hnd&cpeName=cpe:/a:wordpress:wordpress`

</details>
<br>
<br>

## レスポンス(XML)

### 概要

- 処理成功時、Atom(+mod_sec)と MyJVN 共通 Status ノードで構成する XML(UTF-8)を応答します。ただし、フィルタリング結果が 0 件の場合、entry ノードの中に「該当する脆弱性対策情報はありません。」というエントリを含む XML を応答します。
- エラー発生時、MyJVN 共通 Status ノードにエラーコードとエラーメッセージを格納します。

### XML スキーマ

- Atom：https://jvndb.jvn.jp/schema/atom.xsd
- mod_sec3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
- MyJVN 共通 Status ノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

### 解説

```
<?xml version="1.0" encoding="utf-8"?>
<feed
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://www.w3.org/2005/Atom"
  xmlns:sec="http://jvn.jp/rss/mod_sec/3.0/"
  xmlns:marking="http://data-marking.mitre.org/Marking-1"
  xmlns:tlpMarking="http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1"
  xmlns:status="http://jvndb.jvn.jp/myjvn/Status"
  xsi:schemaLocation="http://www.w3.org/2005/Atom https://jvndb.jvn.jp/schema/atom.xsd
                      http://jvn.jp/rss/mod_sec/3.0/ https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
                      http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1 https://jvndb.jvn.jp/schema/tlp_marking.xsd
                      http://jvndb.jvn.jp/myjvn/Status https://jvndb.jvn.jp/schema/status_3.3.xsd"
  xml:lang="ja"
  >
  <title type="text">IPA注意警戒サービスAPI</title>
  <updated>レスポンス生成日</updated>
  <id>swid:ipa.go.jp+myjvn_alert+1.0.0</id>
  <link rel="alternate"
    type="text/html"
    hreflang="ja"
    href="https://jvndb.jvn.jp/apis/myjvn/" />
  <author>
    <name>IPA</name>
    <uri>https://www.ipa.go.jp/</uri>
  </author>
  <sec:handling>
    <marking:Marking>
      <marking:Marking_Structure xsi:type="tlpMarking:TLPMarkingStructureType"
        marking_model_name="TLP"
        marking_model_ref="http://www.us-cert.gov/tlp/" color="WHITE" />
    </marking:Marking>
  </sec:handling>
  <entry>
    <title>注意警戒情報のタイトル</title>
    <id>注意警戒情報の識別子 (MYJVN-ALT-西暦-番号)</id>
    <summary>注意警戒情報の概要</summary>
    <link href="注意警戒情報のURL" />
    <published>登録日</published>
    <updated>最終更新日</updated>
    <category
      term="カテゴリ名 (Info, Low, Critical)"
      label="カテゴリラベル (INFO, 注意, 緊急)" />
    <sec:items>
      <sec:item>
        <sec:title>関連情報のタイトル</sec:title>
        <sec:identifier>関連情報の識別子 (MYJVN-ALT-西暦-番号-サブ番号)</sec:identifier>
        <sec:summary>関連情報の概要</sec:summary>
        <sec:link href="関連情報の概要のURL" />
        <sec:cpe>CPE製品識別子 (CPE v2.2 形式)</sec:cpe>
        <sec:published>登録日</sec:published>
        <sec:updated>最終更新日</sec:updated>
      </sec:item>
      <!-- sec:item を繰り返します。 -->
    </sec:items>
  </entry>
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
</feed>
```

<br>
<br>

## レスポンス(JSON)

### 概要

- 処理成功時、feed、MyJVN 共通 Status を含む JSON(UTF-8)を応答します。
- エラー発生時、MyJVN 共通 Status にエラーコードとエラーメッセージを格納します。

### JSON スキーマ

- JVN Feed for MyJVN getAlert：http://jvndb.jvn.jp/schema/getalert1.json?20250419

### 解説

```
{
  "$schema": "https://jvndb.jvn.jp/schema/getalert1.json",
  "feed": {
    "title": "IPA注意警戒サービスAPI",
    "id": "swid:ipa.go.jp+myjvn_alert+1.0.0",
    "author": {
      "name": "IPA",
      "uri": "https://www.ipa.go.jp/"
    },
    "updated": "レスポンス生成日",
    "link": "https://jvndb.jvn.jp/apis/myjvn/",
    "sec:handling": {
      "marking:Marking": {
        "marking:Marking_Structure": {
          "xsi:type": "tlpMarking:TLPMarkingStructureType",
          "marking_model_name": "TLP",
          "marking_model_ref": "http://www.us-cert.gov/tlp/",
          "color": "WHITE"
        }
      }
    },
    "entry": [
      {
        "title": "注意警戒情報のタイトル",
        "id": "注意警戒情報の識別子 (MYJVN-ALT-西暦-番号)",
        "summary": "注意警戒情報の概要",
        "link": "注意警戒情報のURL",
        "category": {
          "term": "カテゴリ名 (Info, Low, Critical)",
          "label": "カテゴリラベル (INFO, 注意, 緊急)"
        },
        "update": "最終更新日",
        "published": "登録日",
        "sec:items": [
          {
            "sec:item": {
              "sec:title": "関連情報のタイトル",
              "sec:identifier": "関連情報の識別子 (MYJVN-ALT-西暦-番号-サブ番号)",
              "sec:link": "関連情報の概要のURL",
              "sec:published": "登録日",
              "sec:updated": "最終更新日",
              "sec:author": { "value": "発行者" },
              "sec:cpe": [
                {
                  "value": "CPE製品識別子 (CPE v2.2 形式)"
                }
              ]
            }
          },
          { "//_comment": "sec:itemタグを繰り返します。" }
        ]
      }
    ],
    "status:Status": {
      "version": "3.3",
      "method": "getAlertList",
      "feed": "hnd",
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
}
```
