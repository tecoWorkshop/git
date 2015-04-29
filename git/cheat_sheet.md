# Git チートシート

## インストール
Debian/Ubuntu

    $ apt-get install git

RedHat/CentOS

    $ yum install git

Mac

    $ brew install git

Windows

    http://msysgit.github.com/


## 基本設定
コミット時に付与されるユーザ名を登録

    $ git config --global user.name "<User Name>"

コミット時に付与されるメールアドレスを登録

    $ git config --global user.email "<E-Mail Address>"

コマンドラインのアウトプットをカラー表示にする

    $ git config --global color.ui auto

## リポジトリの作成
既存のディレクトリでのリポジトリの初期化

    $ git init

既存のリポジトリのクローン

    $ git clone <URL>

## 変更の記録
状態の確認

    $ git status

ステージされていない変更の閲覧

    $ git diff

新しいファイルの追跡／変更ファイルのステージング

    $ git add <File>

ステージされている変更の閲覧

    $ git diff --cached (or --staged)

変更のコミット

    $ git commit -m "<Commit Massage>"

## 作業のやり直し
直近のコミットの変更

    $ git commit --amend

ステージしたファイルの取り消し

    $ git reset HEAD <File>

ファイルへの変更の取り消し

    $ git checkout -- <File>

## ファイル操作
ハードディスクから削除し、バージョン管理対象からも削除する

    $ git rm <File>

バージョン管理対象から削除するが、ハードディスクには残す

    $ git rm --cached <File>

ファイルの移動/ファイル名の変更

    $ git mv <From File> <To File>


## 履歴の閲覧
履歴の表示

    $ git log

各コミットの変更ファイルを表示する

    $ git log --stat

ツリー形式で表示する

    $ git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%ci) %C(blue)<%an>%Creset' --abbrev-commit --date-order --all

コミットのメタデータを表示する

    $ git show <Commit>


## リモート
リモートの表示

    $ git remote

リモートの情報をローカルリポジトリにダウンロードする

    $ git fetch <Remote Name>

リモートブランチの内容をマージする

    $ git merge <Remote Name>/<Branch Name>

リモートブランチの内容をローカルにダウンロードしマージする

    $ git pull

ローカルブランチのコミットをリモートブランチ上にリベースする
（fast-forward なマージが出来ない場合に使用する）

    $ git rebase <Remote Name>/<Branch Name>

リモートへのプッシュ

    $ git push <Remote Name> <Branch Name>


## ブランチ
ブランチ一覧の表示

    $ git branch

新規ブランチの作成

    $ git branch <New Branch Name>

ブランチの切り替え

    $ git checkout <Branch Name>

ブランチを現ブランチにマージする

    $ git merge <Branch Name>

ブランチの削除

    $ git branch -d <Branch Name>

## スタッシュ
一時的に変更を棚上げする

    $ git stash

スタッシュ一覧表示

    $ git stash list

スタッシュ内の最新の内容を反映する

    $ git stash pop

スタッシュ内の最新の内容を破棄する

    $ git stash drop


## git-flow
初期化

    $ git flow init

Feature

    $ git flow feature start <Name>
    $ git flow feature publish <Name>
    $ git flow feature pull <Name>
    $ git flow feature finish <Name>

Release

    $ git flow release start <Name>
    $ git flow release finish <Name>

Hotfix

    $ git flow hotfix start <Name>
    $ git flow hotfix finish <Name>

