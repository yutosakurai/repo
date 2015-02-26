# github講座

## gitとは

* バージョン管理システムです (ミスった変更を取り消したり、ブランチを分けて並行して開発ができます)
* 変更したファイルをサーバに反映するのも Git 経由でおこないます

## gitのインストール

### Xcodeをインストール

各自で頑張ってください（入ってる場合はOK)

### homebrewをインストール

	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### homebrewを使ってgitをインストールする

	brew install git

インストールが完了すれば、gitのヴァージョンを確認

	git --version

ver2.0以上なら問題なし

## gitの設定を行う

今のままではなにも出来ないのでまずユーザー設定を行う

	git config --global user.name "あなたのユーザー名"
	git config --global user.email あなたのメールアドレス

設定が終われば、適用されているか確認する

	git config -l

先ほど設定した名前とメールアドレスが表示されていればOK

### 便利な設定を行う

	git config --global color.diff   auto
	git config --global color.status auto
	git config --global color.branch auto
	git config --global color.grep   auto

	git config --global core.excludesfile $HOME/.gitignore
	git config --global push.default current

	git config --global alias.st   status
	git config --global alias.co   checkout
	git config --global alias.ci   commit\ -v
	git config --global alias.di   diff
	git config --global alias.br   branch
	git config --global alias.puhs push
	git config --global alias.psuh push
	git config --global alias.pus  push
	git config --global alias.puh  push
	git config --global alias.pl   '!git pull && git submodule update --init'

	echo .DS_Store >> $HOME/.gitignore
	echo Thumbs.db >> $HOME/.gitignore

意味はあまり気にしなくてOK

## gitを使っていく

### gitを使うための準備、ファイルを作成
	
	cd ~

まずはユーザディレクトリに移動

	mkdir <好きなフォルダ名>

ディレクトリを作成する(`git_test`などの名前でOK)

	cd <先ほど作ったフォルダ名>

先ほど作ったフォルダ内に移動する

	touch hello.txt

txtファイルを作成(ファイル名はなんでもOK)

	vim hello.txt

で先ほど作ったファイルをvimで開く

`i`キーを押し、インサートモードに切り替え、適当に文字を入力  
入力を終えたあと、`esc`キーでコマンドモードに戻り

	:wq

で変更を保存  
ファイルが作成されたので次のstepへ 

### gitを実際に使用する

#### ファイルを監視対象に置く

	git status

と入力すると、先ほど作った`hello.txt`が赤文字で表示される  
これは作ったファイルがまだgitで扱う対象になっていないという意味なので

	git add hello.txt

でファイルを対象にする  
(監視対象に置く、とよく言う)

	git status

で再度確認すると、`hello.txt`が緑文字で表示されていると思うので次へ

#### ファイルをコミット(保存)する

先ほど作ったファイルは監視対象に置かれただけで、まだその状態は保存されていないため

	git commit -m "そのファイルに対するコメント"

と入力し、コミットを行う  
(コメント内容は`日付`であったり`変更内容について`を入力することが多い)

	git status

で確認し、`Nothing to commit`と表示されていればOK


