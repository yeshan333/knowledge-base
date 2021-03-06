# Linux常规操作

![常见目录名介绍](https://img.vim-cn.com/4f/997ad5a19156a30ad1c9c0cecdb8f6f1e65a6e.png)

## 常用命令

- 常用系统工作命令
  - `reboot`重启系统、poweroff关闭系统
  - `ps -u`查看系统中进程状态，详细信息
  - `top`强大的任务管理器，动态监控进程活动与系统运维状态
  - `kill`杀死指定PID进程
  - `killall`杀死指定服务所有进程
- 系统状态检测
  - `uname -a`查看系统内核与系统版本的详细信息
  - `free -h`查看内存使用量
  - `history`查看历史命令，`history -c`清空历史命令
- 目录操作命令
  - `pwd`查看当前所处工作目录
  - `ls -al`查看当前目录所有文件详细信息
  - `cd`切换目录，`.`当前目录，`..`上一层目录，`~`当前用户家目录，`/`根目录
  - `cp`复制文件或目录，`mv`剪切文件或重命名，`rm -rf`强制删除目录或文件
- 文本查看
  - `cat`适合内容较少的，使用`-n`参数可显示行号
  - `more`适合内容较多的
  - `head -n 20`查看前 20 行，`tail -n 20`查看后 20 行
  - `wc`文本统计，`diff`文本比较
  - `file`查看文件类型
- 打包压缩
  - `tar -czvf etc.tar.gz ect/`将ect/目录进行gzip格式的打包压缩
  - `tar xzvf etc.tar.gz -C xxx/xx`解压到指定的xxx/xx目录
- 搜索
  - `grep`
  - `find`按指定条件查找文件，`find .git/objects -type f`查找.git/objects目录下的所有文本文件。`-type b/d/c/p/l/f`用于指定查找文件类型
- 网络

### 查看机器配置-cheatsheet

- CPU：`cat /proc/cpuinfo`
- Memory：`cat /proc/meminfo && free -h`
- 时间 & 时区：`timedatectl status`
- OS 版本：`cat /etc/os-release`

### Linux 文本处理三剑客

- grep
- awk
- sed

![与SQL类比](https://i.loli.net/2020/04/08/GKUlfpc4aJPEQVA.png)

参考：[轻松掌握 Linux 文本处理三剑客：grep、awk 和 sed 实战演练](https://zhuanlan.zhihu.com/p/83307402)

## 环境变量

Linux系统中，环境变量名称一般为大写形式。可用`env`命令查看当前系统中的所有环境变量。一个变量的值可能会因用户的不同而不同。可使用`export`将变量提升为全局变量。

![最重要的10个环境变量](https://img.vim-cn.com/33/973e013bbd7e79461104fc5c85a8d9f122d9e8.png)


## 用户身份与文件权限管理

### 用户身份管理

```bash
# id username 查看用户信息
root@ecs-kc1-small-1-linux-20200124173515:~# id root
uid=0(root) gid=0(root) groups=0(root)
```

- `passwd username`修改用户密码
- `useradd`创新新用户、`groupadd`创建用户组
- `usermod`修改用户属性、`userdel`删除用户

### 文件权限

![Linux常见文件类型的字符表示](https://img.vim-cn.com/9e/f19e939f7debc4fd9462c51afe1359d133a78e.png)

![文件权限的字符与数字表示](https://img.vim-cn.com/00/31b2267aa815b5665ef5f5e6671a5c853c60b7.png)

![demo](https://img.vim-cn.com/20/f0d7320e6efd5f2578fa4c79466dad8d5fb9f1.png)

- 文件/目录权限设置命令
  - `chmod -Rf 777 testdir/`设置testdir目录权限为777权限，-R参数表示递归操作
  - `chown`设置文件/目录的所有者所属组，chown [参数] 所有者:所有组 文件或目录名

```bash
Usage: chmod [OPTION]... MODE[,MODE]... FILE...
  or:  chmod [OPTION]... OCTAL-MODE FILE...
  or:  chmod [OPTION]... --reference=RFILE FILE...
Change the mode of each FILE to MODE.
With --reference, change the mode of each FILE to that of RFILE.

  -c, --changes          like verbose but report only when a change is made
  -f, --silent, --quiet  suppress most error messages
  -v, --verbose          output a diagnostic for every file processed
      --no-preserve-root  do not treat '/' specially (the default)
      --preserve-root    fail to operate recursively on '/'
      --reference=RFILE  use RFILE's mode instead of MODE values
  -R, --recursive        change files and directories recursively
      --help     display this help and exit
      --version  output version information and exit
```

[一些特殊权限](https://zhuanlan.zhihu.com/p/61306636)

## 进程管理工具 Systemd 常用命令

```bash
# 查看某个 Unit 的日志
$ sudo journalctl -u nginx.service

# 查看某个 Unit 状态
$ sudo systemctl status mongod

# 让某个 Unit 开机时启动
$ sudo systemctl enable mongod

# 立即启动一个服务
$ sudo systemctl start apache.service

# 立即停止一个服务
$ sudo systemctl stop apache.service

# 重启一个服务
$ sudo systemctl restart apache.service

# 杀死一个服务的所有子进程
$ sudo systemctl kill apache.service

# 重新加载一个服务的配置文件, 一旦配置文件修改就需要使用
$ sudo systemctl reload apache.service

# 查看某个服务的配置文件
$ systemctl cat sshd.service

# 重新加载所有配置文件
$ sudo systemctl daemon-reload
```

> 参考：[Systemd 入门教程：命令篇](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)

## /proc 文件系统，系统性能指标数据的源头


## tcpdump 常用

!> 命令格式tcpdump [选项] [过滤表达式]

![常用总结](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20201115185251.png)


## Linux 虚拟化架构

KVM - https://www.redhat.com/zh/topics/virtualization/what-is-KVM#

XEN -

OpenVZ -