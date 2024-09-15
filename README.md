# Lucky

## 是什么？
`运行于ARM KoolCenter软件中心的，一款由Golang写的集合了 端口转发 / DDNS / Web服务 / Stun内网穿透 / 网络唤醒 / 计划任务 / ACME自动证书 / 网络存储 等功能的强大网络工具。`

## 二进制项目地址
https://github.com/gdy666/lucky


## 机型支持

在asuswrt为基础的固件上，插件目前支持HND和MTK和QCA架构的路由器


---
## 使用技巧

#### 1.使用Lucky自签SSL证书并注入路由器 (固件版本388.4之后，该方法失效)

![image](https://github.com/user-attachments/assets/9b1a992d-418a-4b6d-a8dd-46433886062d)
![image](https://github.com/user-attachments/assets/feb70855-7fc8-4f2a-a939-58eba3a5637d)

备注：`CF`

映射路径：`/koolshare/configs/lucky/ca`

触发脚本：
```
cp /koolshare/configs/lucky/ca/CF.crt /tmp/etc/cert.crt
cp /koolshare/configs/lucky/ca/CF.crt /tmp/etc/cert.pem
cp /koolshare/configs/lucky/ca/CF.key /tmp/etc/key.pem
cat /tmp/etc/key.pem /tmp/etc/cert.pem > /tmp/etc/server.pem
chmod 640 /tmp/etc/key.pem
tar -C / -czf /jffs/cert.tgz etc/cert.pem etc/key.pem
service restart_httpd
local aicloud_enable=$(nvram get aicloud_enable)
if [ "${aicloud_enable}" == "1" ];then
	service restart_webdav
fi
```
