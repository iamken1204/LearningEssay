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
