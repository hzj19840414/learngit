﻿1. 编辑和帮助功能
     ？，可以代替找出帮助
     Tab，命令不齐
     上下键调出最近使用过的命令
     show history查看最近使用的命令，特权模式
     show terminal查看历史记录的大小，特权模式
     Terminal history size设置历史缓存空间大小，特权模式

2. privilege模式

  \>,用户模式，开机的默认，只有一些show命令可用
  #，特权模式，用户模式下enable命令进入，disable退出
  (config)#,全局配置模式，特权模式下config terminal命令进入，exit/end命令退出
  (config-if),接口模式，interface s0/0,进入接口
  (config-subif),子接口模式，interface f 0/0.1 

3. 路由器和交换机的基本配置
     hostname newswichName，设置主机名称，全局配置模式
     no hostname，恢复默认
     show running-config,特权模式
     do,IOS版本12.3以上可用
     shutdown/no shutdown,激活端口和关闭端口
     description,描述
     ip address ip地址  子网掩码;设定ip地址
     show running-config;查看路由当前的配置
     show startup-config;开机时的配置
     copy running-config startup-config;保存配置
      or
     write
     erase startup-config;删除配置
     reload;从新加载

4. 密码设置
     enable password 123456,全局配置模式，明文
     enable secret 123456,全局配置模式，密文，如何和上一个都有设定，以这个为准
     line console 0;password 123456;login,进入控制台，设定密码，login才生效，明文
     line vty 0 4;password 123456;login,进入虚拟终端，设定密码，login才生效，明文
     service password-encryption,所有密码都变成密文

5. 常用show命令
     show interface;查看一二层端口信息
     show ip route
     show ip interface;查看三层
     show ip interface brief
     show protocols
     show ip protocols
     show controler
     show version;IOS的版本，有那些端

6. vlan基础
     1.作用：
       交换机分割冲突域，不能分割广播域，vlan可以分割广播以
       数据安全
       带宽利用
       速度

     2.建立vlan
       vlan vlanid [name vlanname],全局配置模式，直接生效
       vlan database;vlan vlanid [name vlanname];exit,退出才生效
       switchport accesss vlan vlanid,进入端口模式，加入vlan
     3.vlan删除
       no switchport access vlan vlanid,将端口从某个vlan删除
         or
       switchprot access vlan 1,从新加入vlan 1也等于删除

   ​	 interface range f0/1-3

   ​	switchport access vlan vlanID,将几个端口一起加入vlan

   ​	interface range f0/2 ,f0/3 ,f0/6

   4. vlan查看
        show vlan 
        show vlan brief

7. vlan-trunk
   
    1. 接入链路:只通过一个vlan的数据（acc ess）
    
    2. 中继链路:可以承载多个vlan的数据（trunk）
           封装的协议：
             1.IEEE802.1q,插入在标准以太网帧原地址后面，4个字节，12个bit位的vlanID，4096个vlan
             2.Cisco ISL,在原始帧前加入26头字节，后面加入4字节CRC校验，15个bit位的vlanID
             3.异同
               同：都是显式标记，帧被显式标记了vlan信息
               异：IEEE802.1Q是公有协议，ISL是思科私有
                   ISL外部标记，802.1Q内部标记
                   ISL标记长度30字节，802.1Q标记长度4字节
    
    3. 中继的几种模式
         开启 on:将端口设置为永久中继模式
         关闭 off:将端口设置位永久非中继模式
         企望 desirable:端口主动试图将链路变成中继
         自动 auto:端口愿意将链路变成中继链路
         desirable - auto is ok
         auto - auto is ?
    
    4. 配置端口位Trunk
         interface interfaceID
         swicthport mode [access,dynamic,trunk]
         swithcport mode dynamic [auto,desirable]
    
    5. 查看接口模式 
       show interface interfaceID switchport,缺省为dynamic desirable
    
       swicthport trunk allowed vlan remove vlanID
       swicthport trunk allowed vlan add vlanID
       swicthport trunk encapsulation [dot1q,ISL]

8、vtp---vlan trunk protocol

  三种模式：
  server
  client
  transparent

  默认server模式，默认没有域名。在同一个域里面，用trunk链接，生效。网络中第一次有交换机（server模式）命名domain,其他没有域名的设备会自动设定相同的域名。每修改一次，号会增大，如果有设备更改域名，号会清零。 

