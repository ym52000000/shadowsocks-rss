ShadowsocksR 服务端安装教程
说明
不建议使用一键脚本安装，除非你自己能维护其功能，否则安装时若出了问题很难查，而且现在有不少不明来历的一键脚本内嵌后门程序。
此教程为单用户版，适合个人用户。如果你是站长，请查看多用户版教程：
数据库多用户教程
json版多用户教程（仅一台服务器适用）

基本库安装
以下命令均以root用户执行，或sudo方式执行

centos：

yum install git
ubuntu/debian：

apt-get install git
获取源代码
git clone -b manyuser https://github.com/shadowsocksr-backup/shadowsocksr.git

执行完毕后此目录会新建一个shadowsocksr目录，其中根目录的是多用户版（即数据库版，个人用户请忽略这个），子目录中的是单用户版(即shadowsocksr/shadowsocks)。

根目录即 ./shadowsocksr

子目录即 ./shadowsocksr/shadowsocks

服务端配置
进入根目录初始化配置(假设根目录在~/shadowsocksr，如果不是，命令需要适当调整)：

cd ~/shadowsocksr
bash initcfg.sh
以下步骤要进入子目录：

cd ~/shadowsocksr/shadowsocks
####快速运行####

python server.py -p 443 -k password -m aes-256-cfb -O auth_sha1_v4 -o http_simple

#说明：-p 端口 -k 密码  -m 加密方式 -O 协议插件 -o 混淆插件
如果要后台运行：

python server.py -p 443 -k password -m aes-256-cfb -O auth_sha1_v4 -o http_simple -d start
如果要停止/重启：

python server.py -d stop/restart
查看日志：

tail -f /var/log/shadowsocksr.log
用 -h 查看所有参数

####使用配置文件运行####

如果你的ss目录是~/shadowsocksr，进入这里 修改user-config.json中的server_port，password等字段，具体可参见： https://github.com/shadowsocksr-backup/shadowsocks-rss/wiki/config.json

运行子目录内的server.py：

python server.py
如果要在后台运行：

python server.py -d start
如果要停止/重启：

python server.py -d stop/restart
查看日志：

tail -f /var/log/shadowsocksr.log
更新源代码
如果代码有更新可用本命令更新代码

进入shadowsocksr目录
cd shadowsocksr
执行
git pull
成功后重启ssr服务

自启动
System startup script

客户端
注：以下客户端中有： windows客户端和python版客户端，ShadowsocksX-NG（macOS客户端之一）， Android客户端，Shadowrocket（iOS客户端之一，iTunes售价$3美元/￥18人民币）， 可以使用SSR特性，

其他原版客户端只能以兼容的方式连接SSR服务器（SSR可兼容SS客户端）。

Windows / OS X / ShadowsocksX-NG
Linux python / Linux Qt
Android / iOS / Shadowrocket
OpenWRT
OSX上可使用GoAgentX的SSR插件。在你本地的 PC 或手机上使用图形客户端。具体使用参见它们的使用说明。

也可以直接使用 Python 版客户端（命令行）。

其它加密支持
安装libsodium即可支持 salsa20, chacha20, chacha20-ietf 加密（暂不支持AEAD）

其它异常
如果你的服务端python版本在2.6以下，那么必须更新python到2.6.x或2.7.x版本

其它参见 https://github.com/shadowsocksr-backup/shadowsocks-rss/wiki/ulimit
