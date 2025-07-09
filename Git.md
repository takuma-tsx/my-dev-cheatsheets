よく使うGitコマンドのチートシート

### コミットログの表示
git log # 全コミット履歴を表示
git log --oneline # 1行で要約して表示
git log --graph --oneline --all # グラフ形式で全ブランチの履歴を表示
git log --since="2 weeks ago" # 2週間以内のコミットを表示
git log --author="Your Name" # 特定の作者のコミットを表示

### 差分の確認
git diff # 未ステージの変更を表示
git diff --staged # ステージ済みの変更を表示
git diff <commit_id_1> <commit_id_2> # 2つのコミット間の差分を表示
git diff <branch_name> # 現在のブランチと指定ブランチの差分を表示
git diff HEAD # 直前のコミットとの差分を表示

### ファイルの履歴を確認
git log -- <file_path> # 特定ファイルのコミット履歴を表示
git blame <file_path> # 各行が誰のコミットで追加されたか表示

### 新しいブランチを作成して切り替える
git switch -c <branch_name>

### ブランチを一覧表示
git branch # ローカルブランチを一覧表示
git branch -r # リモートブランチを一覧表示
git branch -a # 全てのブランチ（ローカル・リモート）を一覧表示

### ブランチを切り替える
git switch <branch_name>

### ブランチを削除する
git branch -d <branch_name> # マージ済みのローカルブランチを削除
git branch -D <branch_name> # マージ済みでなくても強制削除（注意！）
git push origin --delete <branch_name> # リモートブランチを削除

### マージ
git merge <branch_to_merge> # 指定ブランチを現在のブランチにマージ

### 変更をステージング
git add . # 全ての変更をステージング
git add <file_path> # 特定のファイルをステージング

### コミット
git commit -m "feat: Add new feature" # コミットメッセージ付きでコミット
git commit --amend # 直前のコミットを修正（メッセージやステージングされた変更）
git commit --amend --no-edit # メッセージはそのままで直前のコミットを修正

### コミットを取り消す
git reset HEAD~1 # 直前のコミットを取り消し、変更を未ステージに戻す
git reset --hard HEAD~1 # 直前のコミットを取り消し、変更を破棄（注意！）
git revert <commit_id> # 特定のコミットの変更を打ち消す新しいコミットを作成

### リモートリポジトリの確認
git remote -v # 設定されているリモートリポジトリを確認

### フェッチ（リモートの変更を取得）
git fetch # リモートの変更をローカルに取得（マージはしない）

### プル（リモートの変更を取得しマージ）
git pull # リモートの変更を取得し、自動的に現在のブランチにマージ

### プッシュ（ローカルの変更をリモートに送信）
git push # ローカルの変更をリモートにプッシュ
git push -u origin <branch_name> # ローカルブランチをリモートにプッシュし、追跡ブランチを設定

### インタラクティブなリベース
git rebase -i HEAD~<num_of_commits> # 直近の指定数のコミットをインタラクティブに編集
git rebase -i <commit_id> # 指定コミットより新しいコミットをインタラクティブに編集

### 作業ディレクトリを一時保存
git stash save "Work in progress" # 現在の変更を一時保存
git stash list # 保存したstashを一覧表示
git stash apply # 最新のstashを適用
git stash pop # 最新のstashを適用して削除

### コミットメッセージの修正
git commit --amend -m "Updated commit message" # 直前のコミットメッセージを修正