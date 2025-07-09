由于学校在2025年7月8号对校园网认证系统进行了升级，无需登录即可白嫖公网ipv6地址的日子一去不复返了（悲）

不过好消息是，新版的ipv6接入变为slaac，意味着安卓手机也可以接入ipv6从而享受免费v6流量

之前放在宿舍的小主机无需认证连上就有v6校园网能用（虽然是/128但也够用了），现在虽然分配了一个/64地址但是必须要认证后才能用

学校并没有给出linux认证的步骤，这里就靠抓包软件给出一个非官方的curl命令（在此感谢[proxypin](https://github.com/wanghongenpin/proxypin)项目，非常好用的安卓抓包软件）

```
curl -X GET 'http://10.2.68.30:801/eportal/portal/login?callback=dr1003&login_method=1&user_account=%2C1%2C`学号`&user_password=`统一认证密码`&wlan_user_ip=`你当前连接到局域网的ipv4地址`&wlan_user_ipv6=&wlan_user_mac=000000000000&wlan_ac_ip=&wlan_ac_name=&jsVersion=4.2.1&terminal_type=2&lang=zh-cn&v=2012&lang=zh' \
  -H 'Host: 10.2.68.30:801' \
  -H 'Connection: keep-alive' \
  -H 'User-Agent: Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Mobile Safari/537.36 EdgA/138.0.0.0' \
  -H 'DNT: 1' \
  -H 'Accept: */*' \
  -H 'Referer: http://10.2.68.30/' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Accept-Language: zh-CN,zh;q=0.9,sq;q=0.8'  \
   --compressed
```

把命令中的  \`中文\` 都替换成自己的信息就ok了（密码中如果有符号不要忘记进行url编码哦

如果有问题欢迎提issue或者pr