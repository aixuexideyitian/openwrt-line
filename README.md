# openwrt

本教程基于lean源码  https://github.com/coolsnowwolf/lede
P3TERX云编译模板   https://github.com/P3TERX/Actions-OpenWrt



教程开始  请全局科学上网


第一步：无脑虚拟机安装Ubuntu，自行百度教程

第二步：ubuntu配置源码

参考教程https://github.com/coolsnowwolf/lede    


ctrl+alt+t打开命令行


命令行输入
sudo apt-get update 
输入密码

然后输入
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync

因为我安装过了，所以很快

使用 git clone https://github.com/coolsnowwolf/lede 命令下载好源代码

下载源码，请科学上网，不然很慢



然后 cd lede 进入目录

【核心】需要酸酸乳等插件需要修改lede/feeds.conf.default
去掉注释#
****************************************************************
src-git packages https://github.com/coolsnowwolf/packages

src-git luci https://github.com/coolsnowwolf/luci

src-git routing https://git.openwrt.org/feed/routing.git

src-git telephony https://git.openwrt.org/feed/telephony.git

src-git freifunk https://github.com/freifunk/openwrt-packages.git

#src-git video https://github.com/openwrt/video.git

#src-git targets https://github.com/openwrt/targets.git

#src-git management https://github.com/openwrt-management/packages.git

#src-git oldpackages http://git.openwrt.org/packages.git

#src-link custom /usr/src/openwrt/custom-feed

src-git xiaorouji https://github.com/xiaorouji/openwrt-passwall

**************************************************************
[核心带代理的库]

LEAN源码地址：  https://github.com/coolsnowwolf/lede

LIEONL源码地址： https://github.com/Lienol/openwrt

有几个库
第一

来自Lienol的passwall
https://github.com/xiaorouji/openwrt-passwall

1.来自其自我介绍

2.goole的搜passwall


3来自文章的介绍

https://mianao.info/2020/05/05/%E7%BC%96%E8%AF%91%E6%9B%B4%E6%96%B0OpenWrt-PassWall%E5%92%8CSSR-plus%E6%8F%92%E4%BB%B6


src-git xiaorouji https://github.com/xiaorouji/openwrt-passwall

第二两个库

https://www.right.com.cn/forum/thread-4051663-1-1.html

看起来比较老

jerrykuku源码地址：https://github.com/jerrykuku/openwrt-package

siropboy源码地址： https://github.com/siropboy/mypackages

*********************************

./scripts/feeds clean

./scripts/feeds update -a

./scripts/feeds install -a




[【核心】make menuconfig 

过程参考如下教程


https://www.right.com.cn/forum/thread-1237348-1-1.html


https://mtom.ml/827.html


https://onedrive.live.com/view.aspx?resid=64C9D95F1BBD0FAF!16042&ithint=file%2cxlsx&authkey=!AKR-UGHOsqhY1cc



target images 教程中此步骤为修改固件大小 一般不要修改

luci >applications  此步骤为选择app插件
  
luci >themes  此步骤选主题

kwrnel modules > network devices  此步骤为选择有线网卡，我的只需要8168网卡驱动，所以取消了其他,强迫症，不要的都取消了

kwrnel modules > wirelcss drivers  此步骤为选无线网卡，一般不选，如果需要无线功能要选很多插件，小白先略过此步


一般选择
kwrnel modules > network devices  选择有线网卡驱动

luci >applications 选择插件

既然咱们是小白，其他就不用管他，默认即可

lean的源码默认选好了完整固件需要的组件
所以我们只需要修改网卡驱动和luci插件

记得最后save保存配置

以上步骤参考教程https://www.right.com.cn/forum/thread-1237348-1-1.html



第三步：配置好make menuconfig 导出lede目录下的 .config 和feeds.conf.default 文件备用  看不到文件按ctrl+h  还看不到就是你没有save保存配置

接着打开 https://github.com/P3TERX/Actions-OpenWrt 项目

此步参考教程 https://p3terx.com/archives/build-openwrt-with-github-actions.html

Fork项目到自己的仓库或 use this template 复制模板到自己仓库

在复制过来的模板上传feeds.conf.default文件  新建一个 .config《无法直接上传我们备份出来的》把备份出来的 .config内容复制进去保存

点击项目页actions  点击 Build OpenWrt 点击run workflow 即可开始编译

已经开始编译，等待2-4个小时即可，在等待时间了可以来十几盘鸡

这是我编译好的
