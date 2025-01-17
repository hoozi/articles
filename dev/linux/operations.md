# Linux常用操作

## 用户操作

（1）列出当前用户

```bash
$ whoami
```

（2）列出所有用户

```bash
$ sudo cat /etc/shadow
```

（3）列出所有用户的密码

```bash
$ sudo cat /etc/passwd
```

（4）创建用户

```bash
$ sudo useradd [用户名]
```

然后，为该用户设置密码。

```bash
$ sudo passwd [用户名]
```

## 组操作

（1）显示当前用户所在的组

```bash
$ groups
```

（2) 显示特定用户所在的组

```bash
$ groups [userID]
```

(3) 查看所有的组

```bash
$ cat /etc/group
```

/etc/group文件的记录格式如下。

```
group_name:passwd:GID:user_list
```

每条记录分四个字段：

1. 用户组名称；
2. 用户组密码；
3. GID
4. 用户列表，每个用户之间用,号分割；本字段可以为空；如果字段为空表示用户组为GID的用户名；

## 挂载USB盘

（1）将USB盘插入电脑

（2）列出所有储存设备。

```bash
$ sudo fdisk -l
```

你会看到储存盘都是`/dev/sdXN`的形式，其中X是盘号，N是分区号。

（3）在文件系统中创建一个挂载点。

```bash
$ sudo mkdir /media/externaldrive
```

（4） 此时，只有root用户才能读取U盘，因此要将U盘变为所有用户都可以读取。

```bash
$ sudo chgrp -R users /media/externaldrive
$ sudo chmod -R g+w /media/externaldrive
```

（5）挂载USB盘。

```bash
sudo mount [/dev/sdXN] /media/externaldrive
```

（6）刻录镜像盘

```bash
$ sudo dd if=debian-*-netinst.iso of=/dev/sdX
```

## 信号（signal）

信号是进程间的一种通信机制，用于内核向某个进程发送消息。

- SIGTERM信号表示内核要求进程终止，进程可以自行退出，也可以不理会这个信号。
- SIGKILL信号用于立即终止进程，进程不能忽略该信号。

```bash
# 发出SIGTERM
$ kill [processID]
```

## nmcli 网络操作

```bash
# 查看所有网络连接
$ nmcli connection show

# 显示所有网络接口
$ nmcli device status

# 显示所有wifi连接
$ nmcli dev wifi list

# 连接某个已经成功的连接
$ nmcli con up id

# 连接某个wifi
$ nmcli dev wifi connect <name> password <password>
```

## 截图

xfce截图。

```bash
$ xfce4-screenshooter -f
```

Gnome截图。

```bash
$ gnome-panel-screenshot
$ gnome-panel-screenshot --delay 10
```

ImageMagick截图。

```bash
$ import MyScreenshot.png
```

然后，用鼠标选中所要截图的范围。

其他参数

```bash
# 10秒后抓取整个屏幕
$ sleep 10; import -window root MyScreenshot2.png

# 抓取图片后，并打开编辑软件
$ sleep 15; import -window root MyScreenshot3.png; gimp MyScreenshot3.png

# 抓取图片后，将宽度缩为500像素
$ import -window root -resize 500 AnotherScreenshot.png
```

scrot截图

```bash
# 安装
$ sudo aptitude install scrot

$ scrot MyScreenshot.png

# 设置质量和延迟，并进行编辑
$ scrot -q 85 -d 5 screenshot.png && gimp screenshot.png &
```

GIMP也可以用来截图，命令为`File —> Acquire —> Screen Shot`。
