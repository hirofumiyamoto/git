git
===

インストール確認
git --version
Gitが無事インストールされていればバージョンが表示

lsで日本語を表示させる
$ vi ~/.bashrc
alias ls='ls --show-control-chars'

初期設定
git config --global user.name "Hoge Fuga"
git config --global user.email
"hoge@example.com"
git config --global color.ui auto

Passwordを毎回聞かれてしまうので、勝手に答えてもらうようにしておく
◆Linux, Mac, Cygwinでの方法  以下を流し込んで終わり
*****
echo -e "machine path\n\
login YOURID\n\
password YOURPASSWORD" > ~/.netrc
chmod 600 ~/.netrc
*****
◆msys git での方法  (改行しないでも権限変更しないでもいけました。が、危険なので要権限変更。以下を流し込んで終わり
*****
echo -e "machine path\n\
login YOURID\n\
password YOURPASSWORD" > ~/_netrc
chmod 600 ~/_netrc
*****
netrcの中身が以下のような形式で作成出来ていれば良い
machine path
login YOURID
password YOURPASSWORD

リポジトリをクローンしたいディレクトリへ移動
cd path/to/git/

Gitのリポジトリをクローンする
例) Repository super-fugaを落としたい。
git clone ssh://path/to/super-fuga
git clone https://path/p/super-fuga.git

最新ファイルを落として基点をリベースする
git fetch
git rebase -i origin/branch_name

ファイルを追加してコミットする
git initgit add path/to/file.extgit ci -m "comment"

変更ファイルの確認
git status

変更内容を確認する
git show

ファイルの差分を表示する
git diff

インデックスと HEADの差分を表示する
git diff --cached

ファイルをコミット予定にする
git add filename

プッシュする
git push origin branch_name

リモートブランチの一覧
git branch -r

ローカルブランチを作成する
git branch -f local_branch_name origin/branch_name

ローカルブランチを移る
git checkout other_branch_name

親を付け直すコミットの親が意図したものと異なる場合は rebaseして amendする必要があります
  01.
    コミットを指定してハードリセットし rebaseする
    git reset --hard hash && git rebase -i origin/branch_name
  02.
    Change-Idを付与して amendする
    git commit --amendChange-Idはリポジトリ管理サイトにあるコミット詳細ページから確認できます
  03.
    pushする
    git push origin branch_name

コンフリクトを解消する
path conflictが発生してマージされない場合は、下記の順でコマンドを入力しコンフリクトを解消します
  git fetch
  git fetch ssh://path/to/repository refs/changes/* && git checkout FETCH_HEAD -b work*
  git rebase -i origin/branch_name
  git rebase --continue
  git checkout --theirs path/to/file.ext
  git add path/to/file.ext
  git rebase --continue
  git push origin branch_name

コンフリクトの有無を確認する
git ls-files -u

ブランチの順序を付け直す
git rebase --onto master branchY branchX

Gitツリーを表示する
gitk --all&

Git GUIを起動する
git gui& 

リベースする
git rebase -i origin/branch_name

リベースを続行する
git rebase --continue

リベースを中止する
git rebase --abort

リモートブランチの削除
git push origin :branch name

ローカルブランチを削除する
git branch -d branch_name 

ローカルブランチのリネーム
git push origin :branch name git branch -m

作業途中の状態を横にのける
git stash

スタッシュしたものを復元
git stash pop

スタッシュ したものを削除
git stash clean

コミットログ閲覧ツール
brew install tig && tig 

不要なオブジェクトを削除・最適化
git gc

最新の変更を取り消す
git reset --soft HEAD^

全ての変更を取り消す
git reset --hard
