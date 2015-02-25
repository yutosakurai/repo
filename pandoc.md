# 20150224 markdownファイルをつかってターミナルを教える  

## "pandoc"の導入  

### pandocをインストールする
	brew install pandoc

*homebrew* を使って *pandoc* をインストールする
	
### pandocがインストールされているか確認
	pandoc <適当なマークダウンファイル>.md -s -o <適当なマークダウンファイル>.html

マークダウンと同階層にhtmlファイルが生成されていればOK  
	
## pandocのテンプレート準備

**そのままではなんだか味気ないのでgithub風にcssでアレンジ**
	
まずは
	
	pandoc --version
	
pandocのデフォルトユーザデータディレクトリを確認
	
	Default user data directory: /Users/ユーザー名/.pandoc
	
標準では `.pandoc` が存在していないためつくる
	
	mkdir .pandoc
	
また、テンプレートファイルは `.pandoc/templates` 内に存在することになっているので
	
	cd ~/.pandoc
	mkdir templates
	
`.pandoc` ディレクトリ内に `templates` ディレクトリを作成  
ここに、以下で作成したテンプレートを置く  

### テンプレートファイルの作成

**現在のテンプレートのhtmlを確認**

	pandoc -D html5
	
デフォルトのテンプレートの中身が、以下のようにそのまま表示されるので、全て選択しコピー
	
	<!DOCTYPE html>
	<html$if(lang)$ lang="$lang$"$endif$>
	<head>
	<meta charset="utf-8">
	<meta name="generator" content="pandoc">
	<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
	...

**コピーしたhtmlをもとに、テンプレートを作成**

先ほどコピーしたhtmlを、新規のhtmlファイルにペーストし、 `github.html` と名前をつけて保存  

* [Github Markdown CSS – for Markdown Editor Preview](https://gist.github.com/andyferra/2554919)  

ここからcssファイルをダウンロードし、 `github.css` と名前をつけて保存  

先ほど作成した `github.html` の `<head>` 内に以下を書き、先ほどのcssファイルを参照させる
	
	<link rel="stylesheet" href="github.css">
  
  
`github.html` と `github.html` を `~/.pandoc/templates` 内へ移動させる  





**これでテンプレートは完成となります**

## 使ってみる

	pandoc -s <適当なマークダウンファイル>.md --template=github -o <適当なマークダウンファイル>.html
	
これで先ほど書きだしたhtmlと見た目が異なっていたら成功！！！


## このテンプレートをデフォルトにする

先ほど作成した `github.html` を `default.html` にリネーム

	pandoc <適当なマークダウンファイル>.md -s -o <適当なマークダウンファイル>.html
	
と書くだけでテンプレートが適用された状態でhtmlが生成される

## htmlファイルをアップロードする場合

先ほど設定した`github.css`は、htmlの`<head>`内に

	<link rel="stylesheet" href="/Users/<ユーザー名>/.pandoc/github.css">

と設定されているので、htmlをそのままアップするだけではcssは適用されないため、cssを合わせてアップロードし、`href=""`内を適宜書きかえる
