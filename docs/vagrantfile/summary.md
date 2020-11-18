# Vagrantfileまとめ

今まで説明した内容を元に`Vagrantfile`を記載すると以下のようになりました。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
  config.vm.box_version = "3.1.4"
  config.vm.hostname = "centos"
  config.vm.network "private_network", ip: "192.168.211.5"
  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", type: "virtualbox"
  config.vm.provision "shell",
    inline: "dnf install -y python3-pip && pip3 install --user -r /vagrant/requirements.txt"
end
```

リポジトリに配置してありますので、移動して以下を実行してみます。

```shell
vagrant up
vagrant ssh
```

無事にVMにログイン出来ることを確認します。

```console
vagrant ssh
[vagrant@centos ~]$
```

ホスト名やIPアドレスが、`Vagrantfile`で指定した値であることを確認します。

```console
[vagrant@centos ~]$ hostname
centos
[vagrant@centos ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ce:0d:d7 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute eth0
       valid_lft 86173sec preferred_lft 86173sec
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:6d:eb:70 brd ff:ff:ff:ff:ff:ff
    inet 192.168.211.5/24 brd 192.168.211.255 scope global noprefixroute eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe6d:eb70/64 scope link
       valid_lft forever preferred_lft forever
[vagrant@centos ~]$
```
