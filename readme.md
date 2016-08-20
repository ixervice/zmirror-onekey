# [zmirror](https://github.com/aploium/zmirror) 一键部署脚本

使用[zmirror](https://github.com/aploium/zmirror)快速部署镜像的脚本  

## 前置需求

1. 一台墙外VPS, OpenVZ/Xen/KVM均可  

2. 操作系统:    
    * 支持的操作系统:  
        * Ubuntu 14.04/15.04/15.10/16.04+  
        * Debian 8 (不支持HTTP/2)  
    * 推荐的操作系统:  
        * Ubuntu 16.04 x86_64
    
    * 全新(刚安装完成)的操作系统. 如果系统中有其他东西, 可能会产生冲突   
    * root权限  

3. 域名
    * 每个镜像要求一个三级域名(类似于`g.zmirrordemo.com`这样的, 有三部分, 两个点)  
    * 域名已经在DNS记录中正确指向你的VPS
  
## 运行方法

```shell
sudo apt-get install python3 wget -y
wget https://raw.githubusercontent.com/aploium/zmirror-onekey/master/deploy.py
sudo python3 deploy.py
```

然后按照脚本给予的提示继续, 如果有不懂的, 可参考下面的安装视频  
如果遇到bug, 请发issues提出  

## 安装过程视频
请点击下面的图片打开  
"视频"中的文字可以被选中和复制  
[![asciicast](https://asciinema.org/a/83322.png)](https://asciinema.org/a/83322)  

## 特性

* 支持一次部署多个镜像, 支持同VPS多镜像  
* 自动安装 [let's encrypt](https://letsencrypt.org/) 并申请证书, 启用HTTPS  
* 自动添加 let's encrypt 的定期renew脚本到crontab  
* 启用[HTTP/2](https://zh.wikipedia.org/wiki/HTTP/2) ps:Debian8不支持HTTP/2  
* 启用[HSTS](https://zh.wikipedia.org/zh-cn/HTTP%E4%B8%A5%E6%A0%BC%E4%BC%A0%E8%BE%93%E5%AE%89%E5%85%A8)  

## FAQ

1. **有没有部署完成的Demo?**  

    当然有, 请戳 [zmirror-demo](https://github.com/aploium/zmirror#demo)  

2. **安装后的 let's encrypt 目录在哪? 证书在哪?**  
    
    let's encrypt本体在: `/etc/certbot/`
    申请到的证书位置, 请看 [certbot文档-where-are-my-certificates](https://certbot.eff.org/docs/using.html#where-are-my-certificates)

3. **为什么安装的是Apache2, 而不是Nginx, 我可以选择吗?**  
    
    因为Apache2的wsgi对python更友好  
    而且Nginx没有Visual Host功能  
    在性能上, 由于性能瓶颈是zmirror本身, 所以Apache和Nginx之间的性能差距可以被忽略  
    
    目前一键脚本只能安装Apache2, 不支持Nginx, 也没有支持Nginx的计划, 如果需要Nginx, 请手动部署  
    手动部署可以参考 [zmirror wiki](https://github.com/aploium/zmirror/wiki)  
    当然, 如果你能写一份Nginx部署教程, 我会很感谢的~ :)  

4. **安装的Apache版本?**
    
    在Ubuntu中, 使用的是 PPA:ondrej/apache2 理论上应该是最新版, 或者接近最新版(2.4.23+)  
    在Debian8中, 使用系统的 apt-get 安装, 版本比较旧, 所以Debian不支持HTTP/2  

5. **Let's encrypt 证书自动更新?**

    安装脚本会自动创建定期更新证书的脚本, 脚本位置为 `/etc/cron.weekly/zmirror-letsencrypt-renew.sh`  

6. **网速太慢?**

    如果你的VPS提供商允许的话, 可以试试看[net-speeder](https://github.com/snooda/net-speeder)  
    
    或者换一个网速快的VPS, Demo站使用的VPS是[Ramnode](https://clientarea.ramnode.com/aff.php?aff=2990)  
    服务器地点是LA(Los Angeles), 速度相当快.  
    ps: 如果你也想试试看的话, 请点击[这个链接](https://clientarea.ramnode.com/aff.php?aff=2990)进入, 这里有我的推广小尾巴, 你买了的话我会有一丢丢(好像是10%)分成  
    ramnode允许使用net-speeder  
