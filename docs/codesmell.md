# 真香定律

>轮子！轮子！轮子！，完了emoji没轮子☸️☸️☸️

>You don’t have to be born with it.

## Frontend

|type|1|2|3|
|:--:|:--:|:--:|:--:|
|Share&Collaboration& dynamic code playgrounds.|[codesandbox](https://codesandbox.io/explore)|[codepen](https://codepen.io/)|[JSFiddle](https://docs.jsfiddle.net/github-integration)|
|Free CDN|[jsDelivr](https://www.jsdelivr.com/)|[Cloudflare](https://www.cloudflare.com/cdn/)|

## Backend


## Ops

|&ensp;|1|2|3|
|:--:|:--:|:--:|:--:|
|CI/CD|[Travis-CI](https://travis-ci.org/)|[Jenkins](https://jenkins.io/zh/)|[GitHub Actions](https://github-actions.netlify.com/)|


## Tools

|&ensp;|1|2|3|
|:--:|:--:|:--:|:--:|


## Efficiency

- [我的vscode settings（GitHub gist）](https://gist.github.com/yeshan333/2f219672ddfcae7b58d64c3df71d7280)

### 前端效率

- vscode插件
  - [Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)：代码美化，可以用来把压缩过后的代码进行美化
  - [CSS Peek](https://marketplace.visualstudio.com/items?itemName=pranaygp.vscode-css-peek)：CSS代码Peek，真香
  - [Easy LESS](https://marketplace.visualstudio.com/items?itemName=mrcrowl.easy-less)：快速compile LESS，写完Less文件后Ctrl+S保存自动生成对应的CSS文件
  - [**Live Server**](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)：vscode快速同步浏览器刷新，可快速启动HTTP服务器，Ctrl+S实时监控变化，再也不用手动刷新重加载了，功能贼🐓儿多，慢慢探索，**终极热重载**

**Live Share**

![Live Share Demo](https://img.vim-cn.com/11/51c83e5889d5b0143d23c0e113ddc4c3c1c651.gif)

**Material Icon Theme**

Material Design Icons for Visual Studio Code，不够帅都用不下去(*^_^*)

![Material Icon](https://img.vim-cn.com/41/b6ebcec3c07861c1a5c6eb918876672d863a32.png)

### 后端效率

- docs string 自动生成：[autoDocstring](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring)

### Google 搜索

free：https://github.com/Alvin9999/new-pac

```shell
# ssr 多用户管理
# 安装教程：http://www.nbmao.com/archives/3052
# 脚本：https://github.com/FunctionXJB/SSR-Bash-Python
yum -y install wget yum install perl
# 安装&更新
wget -q -N --no-check-certificate https://raw.githubusercontent.com/hotmop/SSR-duoyonghu/master/install.sh && bash install.sh
# 卸载
wget -q -N --no-check-certificate https://raw.githubusercontent.com/hotmop/SSR-duoyonghu/master/install.sh && bash install.sh uninstall
```

```shell
# 1.安装wget下载器，http://www.gnu.org/software/wget/
yum -y install wget # 2.逗比ssr脚本，https://github.com/ToyoDAdoubi/doubi#ssrsh
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

**Centos 7 BBR**

```shell
sudo wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
reboot # 重启
# 查看内核是否开启 bbr
sysctl net.ipv4.tcp_available_congestion_control
# 示例结果 net.ipv4.tcp_available_congestion_control = reno cubic bbr

# 查看 bbr 是否装载好了
lsmod | grep bbr
# 示例结果：tcp_bbr                20480  13
```




