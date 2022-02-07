# 删库后门塔备份
btpanel-v7.7.0-backup  官方原版v7.7.0版本面板备份

**Centos/Ubuntu/Debian安装命令 独立运行环境（py3.7）**

```Bash
curl -sSO https://raw.githubusercontent.com/1kst/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```
去除登录框命令：
```
sed -i "s|if (bind_user == 'True') {|if (bind_user == 'REMOVED') {|g" /www/server/panel/BTPanel/static/js/index.js
rm -rf /www/server/panel/data/bind.pl
```

开心方法：

开始
打开目录/www/server/panel/class找到并编辑panelplugin.py文件
使用Ctrl+F搜索并找到softList['list'] = tmpList这段代码，在其下方添加如下代码：

                softList['pro'] = 1
        for soft in softList['list']:
            soft['endtime'] = 0
            

修改完成后重启面板，重启完成后就可以直接安装收费的插件了，Nginx防火墙也可以直接安装使用



网站监控报表
如果需要使用网站监控报表还需另外修改一次代码：
安装好网站监控报表插件后打开/www/server/panel/plugin/total目录并编辑total_main.py文件
使用Ctrl+F搜索并找到if 'bt_total' in session: return public.returnMsg(True,'OK!');这段代码
在这段代码前加上#将其注释掉，并在其下方加入以下代码：

        session['bt_total'] = True
        return public.returnMsg(True,'OK!');
        
然后再次重启面板，即可使用网站监控报表插件了；
