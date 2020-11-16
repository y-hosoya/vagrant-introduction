# ネットワーク

Vagrantfile内で`vm.network`の記述を行う事により、VMのプライベートネットワークやポートフォワーディング等
ネットワークに関する設定を行う事が出来ます。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "<ネットワーク識別子>", ip: "<IPアドレス>"
end
```

## プライベートネットワーク

Windows(Host OS)とVM(Guest OS)間の通信を行う事が出来ます。
ネットワーク識別子に`private_network`を指定、ipにVMのIPアドレスを指定します。

!!!example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.network "private_network", ip: "192.168.211.3"
end
```

## Reference

- [Basic Usage - Networking | Vagrant by HashiCorp](https://www.vagrantup.com/docs/networking/basic_usage)
- [Vagrantのネットワーク周りのあれこれ - Septeni Engineer's Blog](https://labs.septeni.co.jp/entry/20140707/1404670069)
