<h3>GIT  指令</h3>

<h4>1.1 Local</h4>
  <h4>1.1.1初始化</h4>
    <h5>1.1.1.1全局变量</h5>
      <p>git config --global user.name "pan"</p>
      <p>git config --global user.email "xiaoming@163.com"</p>
      <p>git config --global color.ui "always"</p>
      <p>解决中文乱码问题</p>
      <p>解决bash控制台ls命令中文文件名乱码--在Git\etc\git-completion.bash文件中追加一行alias ls='ls --show-control-chars --color=auto'</p>
      <p>解决bash控制台git commit 无法输入中文注释--修改Git\etc\inputrc文件 set output-meta on / set convert-meta off</p>
      <p>解决git log命令中文注释乱码（只bash控制台可用）--在Git\etc\profile中追加一行export LESSCHARSET=iso8859</p>
      <p>解决gitk显示中文注释乱码--git config --global i18n.commitencoding ISO-8859 / git config --global i18n.logoutputencoding ISO-8859</p>

   <h4>1.1.1.2初始化新版本库 git init （只会在根目录下创建一个名为.git文件夹）</h4>

   <h5>1.1.1.3设置忽略的文件</h5>
      <p>设置每个人都要忽略的文件1.在根目录新建一个名为.gitignore的文本文件 在命令行执行echo *.jpg>.gitignore</p>
        <p>2.将.gitignore文件加入版本可并提交</p>
      <p>设置只有自己需要忽略的文件--修改.git/info/exclude文件  （可使用正则表达式，例如*.[oa]等价于*.o和*.a）</p>

   <h5>1.1.1.4添加新文件到版本库</h5>
      <p>添加单个文件--git addsomefile.txt</p>
      <p>添加所有txt文件--git add *.txt</p>
      <p>添加所有文件--git add .（包括子目录，但不包含空目录）</p>

   <h5>1.1.1.5提交 -- git commit -m "add some files"</h5>

  <h4>1.1.2日常操作</h4>
    <h5>1.1.2.1提交</h5>
      <p>提交所有修改--git commit -a -m "some msg"</p>
      <p>提交单个文件--git commit -m "add msg to readme.txt" readme.txt</p>
      <p>增补提交--git commit -C head -a --amend（不会产生新的提交历史记录）</p>

   <h4>1.1.2.2撤销修改</h4>
      <p>撤销暂未提交的修改1.撤销1、2个文件 git checkout head readme.txt todo.txt</p>
        <p>2.撤销所有txt文件 git checkout head *.txt</p>
        <p>3.撤销所有文件git checkout head .</p>
      <p>撤销提交-反转提交git revert --no-commit head（相当于提交最近一次提交的反操作）</p>
      <p>取消暂存git reset head 或git reset head <filename></p>
      <p>复位到head之前的版本git reset --hard head^^</p>

   <h5>1.1.2.3分支</h5>
      <p>列出本地分支git branch</p>
      <p>列出所有分支git branch -a</p>
      <p>基于当前分支的末梢创建新分支git branch <branchname></p>
      <p>检出分支git checkout <branchname></p>
      <p>基于当前分支的末梢创建新分支并检出分支git checkout -b <branchname></p>
      <p>基于某次提交、分支或标签创建新分支git branch emputy cf70sd5e（用来查看某个历史断面很方便）</p>
      <p>合并分支-合并并提交git merge <branchname>（如果有冲突不会自动提交，如果冲突很多可以使用git checkout head .撤销）</p>
      <p>合并分支-合并但不提交git merge --no-commit（有待测试）</p>
      <p>合并分支-压合合并后提交git merge --squash <branchname></p>
      <p>合并分支-压合合并但不提交git merge --squash --no-commit <branchname></p>
      <p>合并分支-拣选合并-挑选某次提交合并但不提交git cherry-pick --no-commit ef50se</p>
      <p>重命名分支git branch -m <branchname> <newname>（不会覆盖已存在的同名分支）</p>
      <p>重命名分支git branch -M <branchname> <newname>（会覆盖已存在的同名分支）</p>
      <p>删除分支git branch -d <branchname>（如果分支没有被合并会删除失败）</p>
      <p>删除分支git branch -D <branchname>（强制删除）</p>

   <h5>1.1.2.4解决冲突git merge tool（1.会生成.BACKUP .BASE .LOCAL .REMOTE四个文件 2.自动条用冲突解决工具 3.解决之后手动删除.orig文件 4.提交）</h5>

   <h5>1.1.2.5标签</h5>
      <p>创建标签-为当前分支最近一次提交创建标签git tag 1.0（注意标签无法重命名）</p>
      <p>创建标签-为Contacts分支最近一次提交创建标签git tag contacts_1.1 contacts（也可以把标签命名为contact/1.1）</p>
      <p>创建标签-位某次历史提交创建标签git tag 1.1 ef42cb23</p>
      <p>显示标签列表git tag</p>
      <p>检出标签git checkout 1.0（查看标签断面，但不能提交）</p>
      <p>由标签创建分支git branch b1.1 1.1 或git checkout -b b1.0 1.0</p>
      <p>删除标签git tag -d 1.0</p>

   <h5>1.1.2.6查看状态</h5>
      <p>当前状态git status</p>
      <p>历史记录git log</p>
      <p><p>历史记录gitk（查看当前分支历史记录） gitk <branchname>（查看某分支历史记录） gitk --all（查看所有分支）</p>
      <p>每个分支最后的提交 git branch -v</p>

   <h5>1.1.2.7导出版本库</h5>
      <p>git archive --format=zip head>nb.zip</p>
      <p>git archive --format=zip --prefix=nb1.0/head>nb.zip</p>


<h3>1.2 Remote</h3
  <h4>1.2.1初始化</h4>
    <h5>1.2.1.1克隆版本库git clone <url></h5>

   <h5>1.2.1.2别名</h5>
      <p>添加远程版本库的别名git remote add <别名> <远程版本库的url></p>
      <p>删除远程库的别名和相关分支git remote rm <别名></p>

   <h5>1.2.1.3创建一个无本地分支的库git init -bare（当需要一个公用的中央库是，非常适合把它建成bare库）</h5>

  <h4>1.2.2日常操作</h4>
    <h5>1.2.2.1分支</h5>
      <p>列出远程分支git branch -r</p>
      <p>删除远程库中已经不存在的分支git remote prune origin</p>

   <h5>1.2.2.2从远程库获取</h5>
      <p>获取但不合并git fetch <远程版本库></p>
      <p>获取并合并到当前本地分支git pull</p>
      <p>推入远程库git push origin master（远程库的master不能是当前分支）</p>

