# 科学上网：VPS 搭建 X-UI 面板





# 问题处理：切换亚马逊云EC2至root账户登录

# root登录服务器（切换 root登录）
sudo -i

# 设置或修改密码
passwd root

# 用root去编辑ssh文件
vim /etc/ssh/sshd_config

主要修改两个地方：

#PermitRootLogin 去掉注释值#后改成yes

PasswordAuthentication no改成yes

保存并退出命令是wq ， 首先按ESC进入Command模式，然后输入“:wq”，回车就可以保存并退出了









 



