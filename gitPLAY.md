# 1.安装git 

# 2.设置用户名和email
- git config --global user.name "sunmlight（用户名）"
- git config --global user.email "sunm8917@gmail.com"
执行完成之后该目录下会新增加一个.gitconfig文件

# 3.为GitHub账号添加SSH Keys
- 创建SSH key
	-ssh-keygen -t rsa -C "sunm8917@gmail.com"
- 然后用cat查看id_rsa.pub文件内的内容，粘帖到github帐号管理的添加SSH key界面中。	-cat ~/.ssh/id_rsa.pub
- 添加到GitHub: 登录GitHub> 点击“Settings”> SSH keys>Add SSH key

# 4.git 问题 warning: push.default 尚未设置
matching 参数是 Git 1.x 的默认行为，其意是如果你执行 git push 但没有指定分支，它将 push 所有你本地的分支到远程仓库中对应匹配的分支。
而 Git 2.x 默认的是 simple，意味着执行 git push 没有指定分支时，只有当前分支会被 push 到你使用 git pull 获取的代码
从上述消息提示中的解释，我们可以修改全局配置，使之不会每次 push 的时候都进行提示。对于 matching 输入如下命令即可：
- $ git config --global push.default matching
而对于 simple ，请输入：
$ git config --global push.default simple
