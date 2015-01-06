# Git 指令筆記

## origin
* 只clone某個branch   
`git clone -b <branch-name> <remote-url>`   
   
===
* 重設remote url   
`git remote set-url <new-remote-url>`

===
* 新增遠端儲存庫 _可以有很多個, e.g. origin origin2..._   
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
