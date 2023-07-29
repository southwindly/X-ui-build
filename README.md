### 二、安装更新运行环境（以vu服务器，德班系统为例）
#### 安装 X-ui 面板
#### 申请 SSL 证书

**下面是环境的安装方式，大家根据自己的系统选择命令安装就好了。**

#### 1、Debian/Ubuntu系统执行以下命令：
    apt update -y && apt install -y curl && apt install -y socat
    
#### 2、CentOS系统执行以下命令：
    yum update -y && yum update -y && yum install -y socat
    
#### 3、运行Acme脚本
    curl https://get.acme.sh | sh
    
#### 4、申请证书及密钥
【将代码中注释的邮箱和域名，改为你自己的】

    ~/.acme.sh/acme.sh --register-account -m 输入你的解析域名的网址的注册邮箱
--------
    ~/.acme.sh/acme.sh  --issue -d 输入你的域名  --standalone
    
### 5、下载证书及密钥
    ~/.acme.sh/acme.sh --installcert -d 输入你的域名 --key-file /root/private.key --fullchain-file /root/cert.crt

### 三、一键安装&升级x-ui面板脚本
    bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
-------- 
    bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install.sh)


### 注意事项
### - 申请证书报错

- 1、如果在申请证书及密钥这一步搭建失败，检查并放行端口，口令如下：
#### 放行80端口与443端口
    iptables -I INPUT -p tcp --dport 80 -j ACCEPT
--------
    iptables -I INPUT -p tcp --dport 443 -j ACCEPT
#### 查看已开放的端口
    firewall-cmd --list-ports
#### 开放端口（开放后需要要重启防火墙才生效）
    firewall-cmd --zone=public --add-port=3338/tcp --permanent
#### 重启防火墙
    firewall-cmd --reload
#### 停止防火墙
    systemctl stop firewalld

- 2、如果是全新安装，默认网页端口为54321，用户名和密码默认都是admin，如果遇到打不开的情况，可能是端口没有放行，用【方法1】键入停止防火墙代码，或键入开放端口代码。
- 3、V2ray软件：设置——参数设置——V2rayN设置——Core类型改为Xray_Core


### - 证书更新问题
**目前证书在 60 天以后会自动更新，无需任何操作，今后有可能会缩短这个时间，不过都是自动运营，不必关心，之后acme.sh就会自动保持更新了。**
#### 更新Acme的脚本
#### 升级Acme.sh到最新版本
    ~/.acme.sh/acme.sh --upgrade
#### 如果你不想手动升级, 可以开启自动升级:
    ~/.acme.sh/acme.sh  --upgrade  --auto-upgrade


### - 亚马逊EC2至root账户登录

#### 1、root登录服务器（切换 root登录）
#### 2、设置或修改密码
#### 3、用root去编辑ssh文件
#### 4、主要修改两个地方：将#PermitRootLogin XXXXX去掉注释值后改成PermitRootLogin yes，将PasswordAuthentication no改成PasswordAuthentication yes
#### 5、保存并退出命令是wq ， 首先按ESC进入Command模式，然后输入“:wq”，回车就可以保存并退出了

#### 代码如下：
    sudo -i
    passwd root
    vim /etc/ssh/sshd_config
    将#PermitRootLogin XXXXX去掉注释值后改成PermitRootLogin yes
    将PasswordAuthentication no改成PasswordAuthentication yes
























