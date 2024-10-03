# btpanel-v7.7.0
btpanel-v7.7.0-backup  官方原版v7.7.0版本面板备份

**Centos/Ubuntu/Debian安装命令 独立运行环境（py3.7）：**

```Bash
curl -sSO https://raw.githubusercontent.com/caiweill/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```

1.屏蔽强制绑定手机

```Bash
sed -i "s|bind_user == 'True'|bind_user == 'XXXX'|" /www/server/panel/BTPanel/static/js/index.js
```

如需回复

```Bash
sed -i "s|if (bind_user == 'REMOVED') {|if (bind_user == 'True') {|g" /www/server/panel/BTPanel/static/js/index.js
```

2.直接删除宝塔强制绑定手机 js 文件

```Bash
rm -f /www/server/panel/data/bind.pl
```

3.去除宝塔面板各种计算题与延时等待

```Bash
`Layout_file="/www/server/panel/BTPanel/templates/default/layout.html";
JS_file="/www/server/panel/BTPanel/static/bt.js";
if [ grep -c "<script src=\"/static/bt.js\"></script>" $Layout_file -eq '0' ];then sed -i '/{% block scripts %} {% endblock %}/a ' $Layout_file; fi;
wget http://f.cccyun.cc/bt/bt.js -O $JS_file;
bt restart`
```

&nbsp;

**如果遇到重启后宝塔乱码 请DD最新版Debian系统然后修改语言区域：**


```Bash
localectl set-locale LANG=en_US.UTF-8
nano /etc/default/locale
```

```Bash
LANG="en_US.UTF-8"
LC_ALL="en_US.UTF-8"
```

修改后保存文件，重启VPS即可。

后续操作
为了防止自动升级

改成离线模式，并修改hosts

echo "127.0.0.1 www.bt.cn" >> /etc/hosts

宝塔降级常见问题
* Q1：降级后显示宝塔无法启动，但无任何报错

S1：需要将markupsafe==2.0.1添加到panel目录下的requirements.txt文件中并执行/www/server/panel/pyenv/bin/pip3 install -r requirements.txt安装python库后重启面板即可

* Q2：降级后登录宝塔面板时提示密码错误

S2：需要在终端修改宝塔密码

* Q3：降级后登录宝塔面板时无法显示验证码图片或无法下载文件

S3：需要将/www/server/panel/BTPanel/\_\_init\_\_.py文件中的send_file函数中的cache_timeout参数名改为max_age
最新解决办法：ssh运行：/www/server/panel/pyenv/bin/pip install -U Flask==2.1.2
重启宝塔面板即可。
