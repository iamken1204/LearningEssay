# Git Note

## save credentials for pushing to __https__ repositories
[ref](http://stackoverflow.com/questions/11403407/git-asks-for-username-everytime-i-push)   
```bash
$ git config credential.helper store
$ git push a_https_repo master
Username: <type your username>
Password: <type your password>
```

## git upgrading by homebrew
`$ brew upgrade git`

## origin
* 只clone某個branch   
`git clone -b <branch-name> <remote-url>`   
   
===
* 重設remote url   
`git remote set-url <remote-name> <new-remote-url>`

===
* 新增遠端儲存庫 __可以有很多個, e.g. origin origin2...__   
`git remote add <remote_name> <remote_url>`

===
* 顯示某個remote資訊   
`git remote show origin`     
`git remote show origin2`   

===
* 將working tree全部復原   
`git reset HEAD --hard`   

===
* branch更名   
`git branch -m old_name new_name`   
`git branch -M old_name new_name` (強制覆蓋)   

===
* 列出遠端branch   
`git branch -r`   

===
* 重回上一個commit前的狀態   
`git reset HEAD^` (已修改的檔案保留在working tree)   
`git reset HEAD^ --soft` (已修改的檔案放到staging area)   
`git reset HEAD^ --hard` (清除已修改的檔案)

* 重回到上一個commit的狀態   
`git reset --hard` 恢復上一個commit後修改的檔案   
[參考](http://stackoverflow.com/questions/5807137/git-how-to-revert-uncommitted-changes-including-files-and-folders)

===
* 清除無用git檔案,增進效能   
`git gc`   
   
===
* 修改最近一次尚未push的commit訊息   
`git commit --amend -m <new_commit_message>`   
[參考](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git)   

===
* Undo a merge   
`$ git reset --merge ORIG_HEAD`   
[ref](http://stackoverflow.com/questions/2389361/undo-a-git-merge)
