# SSH用法

## 生成密钥

```bash
$ ssh-keygen -t rsa
```

密钥会在`~/.ssh`目录生成。

服务器安装OpenSSH服务器。

```bash
$ sudo apt-get install openssh-server

# Ubuntu 15.04+
$ systemctl restart ssh

# Ubuntu 14.04
$ service ssh restart
```

将本地密钥推送到服务器。

```bash
$ ssh-copy-id username@host
```

## 命令行参数

`-i`指定登陆服务器所需要的私钥，意为“identity_file”，默认为`~/.ssh/id_dsa`。

```bash
$ ssh johndoe@host.example.com -i ~/.ssh/host.key
```
