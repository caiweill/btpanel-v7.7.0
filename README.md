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
