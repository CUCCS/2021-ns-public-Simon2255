# 基于 VirtualBox 的网络攻防基础环境搭建
## 实验目的
· 掌握 VirtualBox 虚拟机的安装与使用；

· 掌握 VirtualBox 的虚拟网络类型和按需配置；

· 掌握 VirtualBox 的虚拟硬盘多重加载；
## 实验环境
以下是本次实验需要使用的网络节点说明和主要软件举例：

VirtualBox 虚拟机

攻击者主机（Attacker）：Kali Rolling 2109.2

网关（Gateway, GW）：Debian Buster

靶机（Victim）：From Sqli to shell / xp-sp3 / Kali
## 实验要求
1. 虚拟硬盘配置成多重加载，效果如下图所示；
![](img/1.png)
2. 搭建满足如下拓扑图所示的虚拟机网络拓扑；
![](img/2.png)
3. 完成以下网络连通性测试：

. 靶机可以直接访问攻击者主机

. 攻击者主机无法直接访问靶机

. 网关可以直接访问攻击者主机和靶机

. 靶机的所有对外上下行流量必须经过网关

. 所有节点均可以访问互联网
## 实验过程
1. 将Debian10与xp设置为多重加载：
   ![](img/3.png)
   ![](img/4.png)
2. 设置虚拟机并修改其网卡等设置如下：
   
   . 网关Gateway为虚拟机debian-gw，其网络配置如下图：
   ![](img/5.png)
   其网络地址如下：
   ![](img/6.png)
   从上往下依次为：NAT Host-Only intnet1 intnet2

   . 靶机Victim-Kali-1的配置及网络ip如下
   ![](img/7.png)
   ![](img/8.png)
   网卡为intenet1

   . 靶机Victim-xp-1的配置及网络IP如下
   ![](img/9.png)
   ![](img/10.png)
   网卡为intenet1

   . 靶机Victim-Debian-2的配置及网络ip如下
   ![](img/11.png)
   ![](img/12.png)
   网卡为intenet2

   . 靶机Victim-xp-2的配置及网络ip如下
   ![](img/13.png)
   ![](img/14.png)
   网卡为intenet2

   . Attacker的配置及网络IP如下
   ![](img/15.png)
   ![](img/16.png)
   网卡为NAT
3. 完成所要求的网络连通性测试：
   
   . 靶机可以直接访问攻击者主机

   用靶机xp-1 xp-2 Debian-2都能访问攻击者主机的ip地址：
   ![](img/17.png)
   ![](img/18.png)
   ![](img/19.png)

   . 攻击者主机无法直接访问靶机

   当用攻击者主机访问靶机ip时，都出现了ping不通的情况
   ![](img/20.png)
   ![](img/21.png)

   . 网关可以直接访问攻击者主机和靶机
   ![](img/22.png)

   . 靶机的所有对外上下行流量必须经过网关

    在网关debian-gw上输入如下指令进行抓包：
    ![](img/23.png)
    在对应的靶机中ping网站，并访问www.cuc.edu.cn：
    ![](img/24.png)
    得到的文件用wireshark分析如下：
    ![](img/25.png)
    ![](img/26.png)
    有对应的网站信息，于是可以看出访问流量必须经过网关

    . 所有节点均可以访问互联网
    ![](img/27.png)
    ![](img/28.png)
    无论是攻击者主机还是靶机都可以访问网站