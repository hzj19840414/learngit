﻿1. 建立仓库create repository
	`git init`

2. 添加到index--add stage

   `git add filename`

3. commit repos
   `git commit -m "description"`

4. check command result 

   ```
   git status
   git status -s //--short
   e.g.
    M readme	//modify the file only in working directory
   MM rakefile
   A  lib/git.rb	//add to staging first now.-----git add lib/git.rb
   M  lib/git.mb	//modify the file use command "git add" into the staged 
   ?? license.txt	//untrack
   ```

   

5. compare

   ```
   git diff  filename  			//compare with working directory or staged;the means the last modify
   git diff --cached  filename 		//staged and HEAD
   git diff commitID1 commitID2 filename	//compare with commit1 and commit 2 in repository
   git diff commit1 filename 		//compare with commit1 and working directory
   git diff --no-index filename1 filename2	//compare with any two files in the same folder use the git native diff command
   
   git diff HEAD -- readme.txt 		//命令可以查看工作区和版本库里面最新版本的区别
   git diff master   -- readme.txt 	//命令可以查看工作区和版本库里面最新版本的区别
                         									//-- readme.txt It like be copared the single file ,not the tree
   ```

   

6. view commit log

   ```
   git log命令显示从最近到最远的提交日志
   
   git log
   git log --pretty=oneline
   ```

   

7. comebak last version

   ```
   git reset --hard HEAD^
   git reset --hard HEAD~1 //HEAD^^ or HEAD~2
   ```

   

8. jump the one of the version

   git reset --hard "commit id"

9. Git提供了一个命令git reflog用来记录你的每一次命令

   git reflog

10. 撤销修改

    命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

    一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

    总之，就是让这个文件回到最近一次git commit或git add时的状态。

11. cheak the stage area and repos(HEAD) 's dirctory-tree

    git ls-tree -l HEAD

    -l display the file size

    git ls-files -s //display staging area 's dir-tree

12. cheak the git-objection ID
    git cat-file -t git-obj-ID //type is commit;tree;blob
    git cat-file -p git-obj-Id //content

13. git reset  command 's detail

    action 1:reset the contet(ID) in the .git/refs/heads/master
    action 2:reset the stage ,it same to  the repos .git/refs/heads/master
    action 3: reset the working area,same above

    git reset --hard <commit ID> // action 1,2,3
    git reset --soft <commit ID> //action 1
    git reset --mixed <commit ID> //action 1,2;default

    git reset //HEADzhixiangde dir-tree reset the stageing area
    git reset HEAD //same to the "git reset"

14. git check out
    git checkout commitID_or_tag filename1 filename2	//from a commitID in repostory catch a file,files in working directory will be coverd

15. git clone
    git clone https://github.com/hzj19840414/learngit
    git clone git@github.com:hzj19840414/learngit.git

    //above.in working directory create folder named same as the git server

    rename the folder name is mylearn

    git clone https://github.com/hzj19840414/learngit mylearn

    









































