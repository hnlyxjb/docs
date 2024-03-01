# H3C NX30 pro刷机

## 刷入小分区系统 <!-- {docsify-ignore} -->

## 开启ssh

路由器连网，telnet 连接路由器ip 192.168.xxx.xxx 端口号99 用户名H3C 密码是登录密码，运行以下命令开ssh

>
?> 命令提示符输入代码`telnet H3C@192.168.xxx.xxx`   输入密码连接路由器

```powershell
curl -o /tmp/dropbear.ipk https://downloads.openwrt.org/releases/packages-19.07/aarch64_cortex-a53/base/dropbear_2019.78-2_aarch64_cortex-a53.ipk
opkg install /tmp/dropbear.ipk
/etc/init.d/dropbear enable
/etc/init.d/dropbear start
```

## 刷入Uboot

用[scp](https://winscp.net/translations/dll/6.3.1/chs.zip)将压缩包里的[`uboot.bin`](/software/nx30pro/uboot.bin ':ignore')传到路由器的tmp目录，scp端口号22，用户名和密码依旧是第一步,上传完成运行一下命令刷入uboot，此Uboot可以引导原厂固件

```powershell
mtd write /tmp/uboot.bin FIP
```

## 备份原厂固件

运行一下命令备份[原厂固件](/software/nx30pro/backup.img ':ignore')，备份大小约65M

```powershell
dd if=/dev/mtd5 of=/tmp/backup.img
```

## 刷入固件

- 拔掉电源按住reset按钮不放插入电源，10s后松开，网线连接路由器lan口，设置电脑固定IP 192.168.1.x，浏览器输入192.168.1.1进入uboot模式
- 选择[刷机包](/software/nx30pro/nx30pro.bin ':ignore')`nx30pro.bin`，点击upload等待刷机完成路由器重启，电脑改回自动获取ip
- 浏览器输入ip 192.168.6.1进入路由器登陆界面，默认用户名 root 密码 password

[网盘下载](https://wwd.lanzouj.com/b01g1ihla)	下载链接密码:**8ete**

