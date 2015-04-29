# Git

参考：http://git-scm.com/

<br>
## Git のインストール

### Linux
【Debian/Ubuntu】

    $ apt-get install git

【RedHat/CentOS】

    $ yum install git

### Mac

    $ brew install git


### Windows

http://msysgit.github.com/

<br>
## 初期設定

ユーザ名とメールアドレスの設定

    $ git config --global user.name "<User Name>"
    $ git config --global user.email <E-Mail Address>


設定の確認

    $ git config --list

or

    $ cat ~/.gitconfig


<br>
## Git の基本

### Git リポジトリの取得

#### 既存のディレクトリでのリポジトリの初期化

    $ cd hoge/
    $ git init

※ .git サブディレクトリが作成されリポジトリに必要なメタデータが格納される

<br>
#### 既存のリポジトリのクローン

    $ git clone [URL]

※ SVN等と違い、サーバが保持しているデータをほぼ全てローカルにコピーする<br>
※ git:// プロトコルの他、http(s):// や ssh:// も使用できる

例）

    $ git clone git://github.com/schacon/grit.git


<br>
### 変更内容のリポジトリへの記録

#### 状態の確認

    $ git status


<br>
#### 新しいファイルの追跡／変更ファイルのステージング

    $ git add <File>

例）

    $ vi README
    $ git status
    $ git add README
    $ git status


<br>
#### 差分の表示
ステージされていない変更の閲覧

    $ git diff


ステージされている変更の閲覧

    $ git diff --cached (--staged [ver.1.6.1 以降])


<br>
#### 変更のコミット

    $ git commit
※ エディターが起動するのでコミットメッセージを記入する

or

    $ git commit -m "<Commit Massage>"


<br>
#### ファイルの削除
ハードディスクから削除し、バージョン管理対象からも削除する

    $ (rm <File>)
    $ git rm <File>
    $ git commit


バージョン管理対象から削除するが、ハードディスクには残す

    $ git rm --cached <File>
    $ git commit


<br>
#### ファイルの移動

    $ git mv <From File> <To File>

or

    $ mv <From File> <To File>
    $ git rm <From File>
    $ git add <To File>


<br>
### コミット履歴の閲覧

#### 履歴の表示

    $ git log

直近 N 個のエントリのみを出力する

    $ git log -N

各コミットの diff を表示する

    $ git log -p

各コミットの変更ファイルを表示する

    $ git log --stat

例）ツリー形式で表示する

    $ git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%ci) %C(blue)<%an>%Creset' --abbrev-commit --date-order --all


<br>
### 作業のやり直し

#### 直近のコミットの変更

    $ git commit --amend

※コミットメッセージを変更したい場合は、ステージングエリアに何もない状態でコマンドを実行する<br>
※ステージングエリアに変更ファイルがある場合、前回のコミットに今回の変更が含まれる

例）

    $ git commit -m '1回目のコミット'
    $ git add <コミット忘れのファイル>
    $ git commit --amend


<br>
#### ステージしたファイルの取り消し

    $ git reset HEAD <File>

※git status を実行すると取り消しの方法を教えてくれる


<br>
#### ファイルへの変更の取り消し

    $ git checkout -- <File>

※このコマンドを実行すると変更は全て削除される


<br>
### リモートでの作業

#### リモートの表示

    $ git remote
    $ git remote -v


<br>
#### リモートからのフェッチ、プル
リモートの情報をローカルリポジトリにダウンロードする

    $ git fetch <Remote Name>

※ローカルの環境にマージされたり作業中の内容を書き換えたりはしない


リモートブランチの内容をローカルブランチにマージする

    $ git pull

※ git fetch + git merge

<br>
#### リモートへのプッシュ

    $ git push <Remote Name> <Branch Name>


例）

    $ git push origin master

※他の作業者がリモートにプッシュしている場合は、事前にその内容をローカルにマージしている必要がある

<br>
## ブランチ機能

Git はコミットを実行すると、以下のオブジェクトを作成する

1. プロジェクトの各ファイルの中身を表すバイナリオブジェクト
2. 各サブディレクトリの中身の一覧と、どのファイルがどのバイナリに対応するかをあらわすツリーオブジェクト
3. ルートツリーおよび全てのメタデータ（編集者、親コミットなど）へのポインタを含むコミットオブジェクト

次のコミットを行うと、そのコミットには直近のコミットへのポインタが格納される

<br>
### ブランチとは
* Git のブランチはこれらのコミットオブジェクトを指すポインタ（オブジェクトの場所を格納する変数）にすぎない
* コミットを重ねるとこのポインタが自動的に進んでいく（ポインタの中身が新しいコミットオブジェクトの場所に更新される）
* ブランチはひとつのコミットを指すポインタであるが、親コミットをたどることで、そのコミットの履歴をたどることが出来る

### 新しいブランチの作成

    $ git branch <New Branch Name>

※ 単に新たな移動先を指す新しいポインタが生成されるだけ<br>
※ 新しいポインタは元のブランチのポインタと同じ位置を指している<br>
※ 新しいブランチを作成するだけで、そのブランチに切り替えるわけではない<br>

<br>
### ブランチの削除

    $ git branch -d <Branch Name>

<br>
### ブランチの切り替え

    $ git checkout <Branch Name>

※ HEAD が <Branch Name> を指すようになる<br>
※ HEAD は、自分が作業しているローカルブランチへのポインタ<br>
※ ブランチを切り替えると、作業ディレクトリのファイルが、そのブランチが指すコミットのスナップショットに変更される

<br>
### ブランチ一覧の表示

    $ git branch

※ *（アスタリスク）の付いているブランチが、現在チェックアウトされているブランチ

<br>
### ブランチのマージ

    $ git checkout master
    $ git merge hotfix

※ hotfix が master にマージされる

<br>
#### fast-forward
マージ先 (master) がマージ元 (hotfix) の直接の親である場合、マージ先はポインタをマージ元と同じ位置に移動するだけとなる（この処理を “fast-forward” という）

<br>
#### マージコミット
マージ先 (master) がマージ元 (hotfix) の直接の先祖出ない場合、各ブランチが指すスナップショットとそれらの共通の先祖との間で三方向のマージが行われる<br>
この三方向のマージ結果から新たなスナップショットが作成され、新しいコミットが作られる

<br>
#### マージ時のコンフリクト
マージ時にコンフリクトが起こった場合、処理は中断されマージコミットは作成されない<br>
直接コンフリクトの起こったファイルを編集し、コンフリクトを解決する必要がある<br>
コンフリクトが解決出来たら、 git add を実行しファイルをステージする<br>
git commit を実行してマージコミットを完了させる

<br>
### ブランチのリベース

    $ git checkout develop
    $ git rebase topic

※ 2つのブランチの共通の先祖から現在のブランチ (develop) 上の各コミットの変更点をリベース先 (topic) から順に変更を適用していく<br>
※ fast-forward のマージが出来るようになる

    $ git checkout develop
    $ git merge topic
    $ git branch -d topic

リベースを使うとコミットの履歴が複雑になるのを防げる<br>
リモートブランチ上で自分のコミット履歴をすっきりさせるために利用できる

例）

    $ git checkout develop
    $ git fetch
    $ git rebase origin/develop
    $ git push origin develop

※ リベースはコミットを書き換える（リベースの前後でのコミットはハッシュ値が異なる）ので注意が必要<br>
※ リモートブランチにプッシュ済みのコミットはリベースしてはならない

## git-flow

### git-flow とは

Git のブランチを活かした効率的な作業フロー及びそのフローを実現するためのツール

<br>
### git-flow のブランチモデル

#### develop ブランチ

開発を行うためのブランチ<br>
開発者は主にこのブランチ上で作業を行う<br>
feature ブランチなど、他のブランチで行った作業はこのブランチにマージされる

<br>
#### feature ブランチ

主要な機能を実装するためのブランチ<br>
新機能の実装やバグフィックスなど、タスクごとに feature ブランチを作成し、作業を行う

<br>
#### release ブランチ

リリースの準備を行うためのブランチ<br>
プロダクトをリリースする前にこのブランチを作成し、必要な場合は微調整を行う<br>
release ブランチを作成することで、リリース準備と次のバージョンに向けた開発のコードを分けることができる

<br>
#### master ブランチ

リリースしたソースコードを管理するためのブランチ<br>
このブランチは常に本番サーバへのデプロイが可能な状態にしておく<br>
リリース作業を行うと release ブランチは master ブランチへマージされて、リリースタグが付けられる<br>
開発者はこのブランチへのコミットは行わない

<br>
#### hotfix ブランチ

リリースされたソフトウェアに対して緊急の修正を行うためのブランチ<br>
hotfix ブランチは master ブランチから作成され、修正対応が完了したらリリースを管理する master ブランチと develop ブランチにマージされる

<br>
### コマンド

#### 初期化

    $ git flow init

<br>
#### Feature

    $ git flow feature start <Name>
    $ git flow feature publish <Name>
    $ git flow feature pull <Name>
    $ git flow feature finish <Name>

<br>
#### Release

    $ git flow release start <Name>
    $ git flow release finish <Name>

<br>
#### Hotfix

    $ git flow hotfix start <Name>
    $ git flow hotfix finish <Name>


