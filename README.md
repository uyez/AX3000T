# 小米路由器AX3000T解锁SSH，安装ShellCrash直接科学上网，ShellClash
小米路由器AX3000T解锁SSH，安装ShellCrash直接科学上网，不用刷机openwrt<br>
视频教程：▶ https://youtu.be/NfQ-ELR-TD8

## 一、Xiaomi 路由器 AX3000T 解锁SSH:
### 1、Windows搜索cmd，以管理员身份运行：

    curl -X POST http://192.168.31.1/cgi-bin/luci/;stok=XXXXXX/api/misystem/arn_switch -d "open=1&model=1&level=%0Anvram%20set%20ssh_en%3D1%0A"
    curl -X POST http://192.168.31.1/cgi-bin/luci/;stok=XXXXXX/api/misystem/arn_switch -d "open=1&model=1&level=%0Anvram%20commit%0A"
    curl -X POST http://192.168.31.1/cgi-bin/luci/;stok=XXXXXX/api/misystem/arn_switch -d "open=1&model=1&level=%0Ased%20-i%20's%2Fchannel%3D.*%2Fchannel%3D%22debug%22%2Fg'%20%2Fetc%2Finit.d%2Fdropbear%0A"
    curl -X POST http://192.168.31.1/cgi-bin/luci/;stok=XXXXXX/api/misystem/arn_switch -d "open=1&model=1&level=%0A%2Fetc%2Finit.d%2Fdropbear%20start%0A"

## 2、计算SSH密码
https://miwifi.dev/ssh 输入路由器的SN码，在路由器后台可以查询SN码。

用putty软件登录路由器，<a href="https://github.com/eujc/AX3000T/releases/download/gongju/AX3000T.zip" target="_blank">点击下载>></a>

用户名是：root，密码是上一步计算出来的，提示 Are U OK 表示已经登录成功。

## 3、永久开启SSH（重启不会关闭）

    mkdir /data/auto_ssh && cd /data/auto_ssh
    curl -O https://fastly.jsdelivr.net/gh/lemoeo/AX6S@main/auto_ssh.sh
    chmod +x auto_ssh.sh

    uci set firewall.auto_ssh=include
    uci set firewall.auto_ssh.type='script'
    uci set firewall.auto_ssh.path='/data/auto_ssh/auto_ssh.sh'
    uci set firewall.auto_ssh.enabled='1'
    uci commit firewall

## 二、安装ShellCrash（ShellClash）：
ShellCrash安装源：

    export url='https://fastly.jsdelivr.net/gh/juewuy/ShellCrash@master' && sh -c "$(curl -kfsSl $url/install.sh)" && source /etc/profile &> /dev/null

备用安装源：

    export url='https://gh.jwsc.eu.org/master' && sh -c "$(curl -kfsSl $url/install.sh)" && source /etc/profile &> /dev/null

<br>
Clash管理后台：http://192.168.31.1:9999/ui
