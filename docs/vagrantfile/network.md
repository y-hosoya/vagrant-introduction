# ネットワーク

Vagrantfileに`vm.network`の記述を行う事によりWindows(Host OS)とVM(Guest OS)間での  
プライベートネットワークやポートフォワーディング等ネットワークに関する設定を行う事が出来ます。

## プライベートネットワーク

パラメータに`private_network`を指定する事により、Host OSとVM間で通信を行う事が出来ます。  

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "<IPアドレス>"
end
```

### private_network
プライベートネットワークを設定する事を明示する値です。

### ip
VMのIPアドレスを指定します。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "192.168.211.3"
end
```

`192.168.211.3`というプライベートIPアドレスをVMに設定します。

## パブリックネットワーク

パラメータに`public_network`を指定する事により、外部ネットワークとVM間で通信を行う事が出来ます。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "public_network", ip: "192.168.0.17"
end
```

### public_network

パブリックネットワークを設定する事を明示する値です。

### ip
VMのIPアドレスを指定します。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "public_network", ip: "192.168.0.17"
end
```

`192.168.0.17`というIPアドレスをVMに設定し、外部ネットワークからのアクセスを可能にします。

## ポートフォワーディング

パラメータに`forwarded_port`を指定及び、Host OS, VMのポート番号を指定する事により、  
Host OSからVMに対するポートフォワーディングを行う事が出来ます。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "forwarded_port", guest: <VMポート番号>, host: <Host OSポート番号>
end
```

### forwarded_port

ポートフォワーディングを設定する事を明示する値です。

### guest

VM上のポート番号を指定します。

### host

Host OSから接続する際のポート番号を指定します。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "forwarded_port", guest: 80, host: 8080
end
```

Host OSの`8080`ポートにアクセスがあった際、VMの`80`ポートに通信を転送します。

## Reference

- [Basic Usage - Networking | Vagrant by HashiCorp](https://www.vagrantup.com/docs/networking/basic_usage)
- [Vagrantのネットワーク周りのあれこれ - Septeni Engineer's Blog](https://labs.septeni.co.jp/entry/20140707/1404670069)
