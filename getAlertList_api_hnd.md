# getAlertList (ver. HND)
注意警戒情報一覧を取得します。

## リクエスト
* https://jvndb.jvn.jp/myjvn?method=getAlertList&feed=hnd&パラメタ名=パラメタ値&...
  * リクエストURLは、HTTPSのGETおよびPOSTに対応しています。

* パラメタ
  * メソッド名、パラメタ名は大文字小文字を区別しています。
  * 必須パラメタが未指定、または値なし("method="など)の場合はエラーとなります。
  * 必須でないパラメタが未指定、または値なし ("lang="など) の場合はデフォルトを使用します。

| パラメタ名 | 名称 | パラメタ値 | 必須 | デフォルト(\*1) |
| ---- | ---- | ---- | ---- | ---- | 
| method | メソッド名 | getAlertList (固定) | ○ | － |
| feed | フィードフォーマット名 | フィードフォーマット(=APIバージョン)を示す名称 <br> hndを指定 | ○ | － |
| startItem | エントリ開始位置 | 整数 (半角数字) 1～応答エントリ数 | － | 1 |
| maxCountItem | エントリ取得件数 | 整数 (半角数字) 1～50 (getAlertListエントリ上限値) | － | 50 |
| datePublished | 更新日年 | 半角整数4桁 | － | － |
| dateFirstPublished | 発行日年 | 半角整数4桁 | － | － |
| cpeName | CPE 製品名 | cpe:/{part}:{vendor}:{product} <br> {part}フィールド ... "h" \| "o" \| "a" \| "\*" <br> {vendor}:{product}フィールド ... CPE 製品名 (\*2) | － | － |
| ft | 応答フォーマット | xml または json | － | － |

\*1)「デフォルト」は、該当パラメタに指定がない場合(パラメタ自体もしくはパラメタ値が未指定の場合)にMyJVN API側で自動的に設定する値です。  
\*2)  
ワイルドカード "\*" 指定可  
アスキー文字  
大文字／小文字区別なし  
複数指定時は "+" で連結  
URL エンコードされたエスケープシーケンス  
cpe:/a:apache:xerces-c%2B%2B  
cpeName=cpe:/a:apache:xerces-c%252B%252B  
いずれか1つのみ指定可 [ cpeName | vendorId | productId ]  


## レスポンス
* 概要
  * 処理成功時、Atom(+mod_sec)とMyJVN共通Statusノードで構成するXMLを応答します。ただし、フィルタリング結果が0件の場合、entryノードの中に「該当する脆弱性対策情報はありません。」というエントリを含むXMLを応答します。
  * エラー発生時、MyJVN共通Statusノードにエラーコードとエラーメッセージを格納します。
* XMLスキーマ
  * Atom：https://jvndb.jvn.jp/schema/atom.xsd
  * mod_sec3.0：https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd
  * MyJVN共通Statusノード：https://jvndb.jvn.jp/schema/status_3.3.xsd

```
<?xml version=" 1.0" encoding=" utf-8" ?>
<feed
xmlns=" http://www.w3.org/2005/Atom"
xmlns:xsi=" http://www.w3.org/2001/XMLSchema-instance"
xmlns:sec=" https://jvn.jp/rss/mod_sec/3.0/"
xmlns:marking=" http://data-marking.mitre.org/Marking-1"
xmlns:tlpMarking=" http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1"
xmlns:status=" http://jvndb.jvn.jp/myjvn/Status"
xsi:schemaLocation=" http://www.w3.org/2005/Atom
<a href=" https://jvndb.jvn.jp/schema/atom.xsd" >https://jvndb.jvn.jp/schema/atom.xsd</a>
https://jvn.jp/rss/mod_sec/3.0/
<a href=" https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd" >https://jvndb.jvn.jp/schema/mod_sec_3.0.xsd</a>
http://data-marking.mitre.org/extensions/MarkingStructure#TLP-1
<a href=" https://jvndb.jvn.jp/schema/tlp_marking.xsd" >https://jvndb.jvn.jp/schema/tlp_marking.xsd</a>" <br /> xml:lang=" ja" >

<title type=" text" >IPA注意警戒サービスAPI</title>
<updated>2017-07-03T12:29:29Z</updated>
<id>swid:ipa.go.jp+myjvn_alert+1.0.0</id>
<link rel=" alternate" type=" text/html" hreflang=" ja" href=" https://jvndb.jvn.jp/apis/myjvn/" />
<entry>
  <title>注意警戒のタイトル</title>
  <id>注意警戒の識別子</id>
  <summary>注意警戒の概要</summary>
  <link href=" http://www.example-store.com/products/foo.html" />
  <published>2017-07-13T08:29:29+09:00</published>
  <updated>2017-07-13T12:29:29+09:00</updated>
  <category term=" /Critical" label=" 緊急" />
  <sec:items>
    <sec:item>
      <sec:title>関連情報のタイトル</sec:title>
      <sec:identifier>関連情報の識別子</sec:identifier>
      <sec:summary>関連情報の概要</sec:summary>
      <sec:link href="関連情報の概要のURL" />
      <sec:cpe>cpe製品名</sec:cpe>
      <sec:published>2022-05-17T00:00:00+09:00</sec:published>
      <sec:updated>2022-05-17T11:50:48+09:00</sec:updated>

    </sec:item>
    sec:item ノードを繰り返します。
  </sec:items>
</entry>
<status:Status
version=" 3.3"
method=" getAlertList"
feed=" hnd"
lang=" 表示言語"
retCd=" リターンコード (0:成功時、1:エラー時) "
retMax=" エントリ上限値"
errCd=" エラーコード (処理成功時は空文字列) "
errMsg=" エラーメッセージ (処理成功時は空文字列) "
totalRes=" 応答エントリ総数"
totalResRet=" 応答エントリ数"
firstRes=" 応答エントリ開始位置"
各リクエストパラメタ>
</status:Status>
```

* JSONスキーマ
 * getalert: 

```
{
    "feed": {
        "title": "注意警戒のタイトル",
        "updated": "更新日",
        "id": "注意警戒の識別子",
        "link": "関連情報の概要のURL",
        "author": {
            "name": "発行者",
            "uri": "発行者のURL"
        },
        "sec:handling": {
            "marking:Marking": {
                "marking:Marking_Structure": {
                    "marking_model_name": "TLP",
                    "marking_model_ref": "http://www.us-cert.gov/tlp/",
                    "color": "WHITE"
                }
            }
        },
        "entry": [
            {
                "title": "関連情報のタイトル",
                "id": "関連情報の識別子",
                "summary": "関連情報の概要",
                "link": "関連情報の概要のURL",
                "category": {
                    "term": "Info",
                    "label": "INFO"
                },
                "update": "更新日",
                "published": "発行日",
                "sec:items": [
                    {
                        "sec:item": {
                            "sec:title": "関連情報のタイトル",
                            "sec:identifier": "関連情報の識別子",
                            "sec:link": "関連情報の概要のURL",
                            "sec:published": "発行日",
                            "sec:updated": "更新日",
                            "sec:author": {"name": "発行者"},
                            "sec:cpe": [
                                {"value": "cpe製品名"}
                            ]
                        }
                    },
                    {
                        "sec:item"ノードを繰り返します。
                    }
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
