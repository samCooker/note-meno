
- [install](#install)

- [config](#config)

- [仓库命令](#仓库命令)


# install

# config

- 查看配置

    `git config --list`

- 配置文件

    - windows:

        文件路径: `C:\Users\用户名\.ssh`

    - mac :

        使用命令 `cd ~/.ssh` 进入目录 `open .` 在finder中打开. ~ 表示当前用户目录

        查看git配置文件命令: `cat .gitconfig`

        - 问题:Bad owner or permissions on /Users/cookie/.ssh/config

          解决:`chmod 600 ~/.ssh/config`

    - 修改配置

        - 配置使用git仓库的人员姓名

        `git config --global user.name "Your Name Comes Here"`

        - 配置使用git仓库的人员email

        `git config --global user.email you@yourdomain.example.com`

- 密钥

    - 生成密钥:`ssh-keygen -t rsa`

        会提示输入文件名,默认名id_rsa.输入两次密码.生成的密钥在.ssh文件夹下

    - 添加密钥:`ssh-add -K 文件名`

# 仓库命令

   - 查看仓库: `git remote -v`

   - 添加远程仓库链接：`git remote add 仓库名 仓库远程链接`

   - 删除远程仓库链接：`git remote rm 仓库名`

# tag

   - 添加tag

   - 删除远程tag `git push origin --delete tag <tagname>`

   - 删除本地tag `git tag -d <tagname>`