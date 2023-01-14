# Godot Japan User Community Web Site

本サイトは[Hugo](https://gohugo.io/)で構築されています。  
バージョン: v0.107.0

## Hugoのインストール方法

https://gohugo.io/installation/windows/

Hugoのインストール方法は上記からご確認ください。
拡張版じゃないとSCSS/SASSのコンパイルエラーが出ますので、エディションにご注意ください。

---

## 逆引きリファレンス記事追加および更新方法

### 記事の作成方法

[content/reference](/godot-jp.github.io/tree/main/content/reference)の中から該当するカテゴリーセクション（ディレクトリ）を選び、その中に**新規の記事用のディレクトリを作成してindex.mdとして記事を作成します。**  
ディレクトリ名はURLスラッグになり、`_index.html`のFront Matterヘッダの`title`がページタイトルになります。

該当するカテゴリーが存在しない場合は、[カテゴリーセクションの作成](#%E3%82%AB%E3%83%86%E3%82%B4%E3%83%AA%E3%83%BC%E3%82%BB%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E4%BD%9C%E6%88%90)をご確認ください。

**プロジェクトディレクトリのルートで**以下のコマンドを実行します。

```
hugo new reference/[カテゴリセクション名]/[記事のタイトル]/index.md
```

アクセスする際は`referemce/[カテゴリセクション名]/[記事タイトル]`になります。

#### 記事リソースの管理方法

画像ファイルなどのメディアファイルは、作成した記事のディレクトリに入れて、相対パスで指定ください。  
作成した記事のディレクトリ以下はどのような構成でも構いません。

> 上記の運用ルールは、記事が不要になった際にディレクトリを削除すれば他の記事に影響のない状態で管理するためです。  
つまり、別の記事の画像や外部の画像などを参照する作りには絶対にしないでください。


#### 記事のFront Matterの設定

```
---
title: "記事タイトル"
emoji: "🎈"
toc: true
draft: false
---
```

| 項目 | 説明 |
| --- | --- |
| title | 記事のタイトルのデフォルトはファイル名が入りますので、運用ルールに沿って記事タイトルで記事を作成された場合、特に変更は不要です。 |
| emoji | 記事のヘッダーや記事一覧で表示される絵文字です。基本的に何かしらの絵文字を設定いただければありがたいです。 |
| toc | 目次を表示するかどうかのフラグです。明示的に`false`にしない限りは表示されます。 |
| weight | 記事の重みは、記事の並び順に影響し、`0`以降の数字が小さいほど上位に表示されます。<br/>サイトのレイアウト上、左上から表示されていきます。<br/>`0`の場合は重みは無視されます。 |
| draft | 公開・非公開のフラグですが、本プロジェクトはマージされた時点で公開と見なされ、問題がない限り公開され続けますので`false`としておいてください。 |

### 記事を書く際の機能とルール

#### 記事の重み

<img src="https://user-images.githubusercontent.com/186786/206615089-8530d63f-cc19-48a9-b3e2-aaf3b1fead88.png" width="50%">

`weight`を設定すると、そのカテゴリの中で記事の並び順を変更できます。

ルールとして`weight: 10000`を基準として、重み付けをします。  
数字は大きいですが、重みが未設定（または`0`）の記事より上位に表示されます。

まず、**最初に最上位にしたい記事の場合**は`weight`に`5000`を設定します。  
その記事より上位に表示したいか、下位に表示したいかで値の設定をします。

**特定の記事より上位に表示させたい場合**は、その記事の`weight`から`-100`の値を入力して記事を作成してください。  
もしも、その記事の`weight`よりも`-100`の値が設定された記事がすでに存在しており、**それらの間に記事を表示させたい場合**は、`-50`を設定してください。  
以降も同様に、記事の間に入れ込むような順番にしたい場合は、間の数値として`1/2`ずつの値を入力してください。

こういった状況で数値を小さくして管理すると、全記事の修正が発生する場合があるため、基本的に大きな数字で管理しています。  
ご協力をお願い致します。

#### HTMLタグの使用

本プロジェクトではHTMLタグを許容しています。  
HTMLでほとんど構成することも可能ですが、サイトレイアウトを壊したりセキュリティ的に問題が出る可能性があります。  
マージ条件としてHTMLのレビューを行い、大掛かりなHTMLでの記事の場合は承認されない可能性がありますので、ご注意ください。

#### Table Of Contentsの表示仕様

H1～H2タグが目次として使用されます。  
記事中に、マークダウンとしてH3～H6タグを使用することは可能ですが、目次としてリストされませんのでご注意ください。

<details><summary>ショートコードについて</summary>
#### Youtube

Youtubeの動画を貼りたい場合は以下のショートコードをご利用ください。  
例えば、`https://www.youtube.com/watch?v=[動画ID]`の場合

```
{{< youtube [動画ID] >}}
```

と記述すれば自動的にYoutubeの動画を挿入することができます。  
また、自動再生したい場合は以下のオプションを設定することもできます。

```
{{< youtube id="[動画ID]" autoplay="true" >}}
```

#### Twitter

Twitterのツイートを貼り付けたい場合は、URLからユーザーIDとツイートIDを指定する必要があります。  
例えば、`https://twitter.com/[ユーザーID]/status/[ツイートID]`

```
{{< tweet user="[ユーザーID]" id="[ツイートID]" >}}
```
</details>

### カテゴリーセクションの作成

カテゴリーセクションは、`/reference/[カテゴリーセクション名]`でディレクトリを作成します。  
ディレクトリ名はURLスラッグになり、`_index.html`のFront Matterヘッダの`title`がカテゴリータイトルになります。

カテゴリーの並び順は、記事と同様に重み（weight）によって調整可能で、数字が小さいほど上位に表示されます。  
記事の重み付けと同様に、基準値は`10000`として、最初に最上位にしたいカテゴリーは`5000`を設定して、上位に表示したいか下位に表示したいかで、数値を`100`刻みで調整していきます。  
すでに`100`刻みでのカテゴリーが存在する場合は`50`刻みで間に設定してください。

## ローカルプレビューの方法

コマンドプロンプトで、クローンしたgodot-jpのディレクトリに移動し以下のコマンドを実行するとローカルサーバーが起動します。

```
hugo server
```

コマンドプロンプトで、Ctrl + Cを押すことでサーバーを停止します。
