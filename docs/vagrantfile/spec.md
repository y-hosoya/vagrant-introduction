# VMスペック

Vagrantfileに記述を行う事により、VM(Guest OS)のhostnameを設定、DiskSizeの変更、MemorySizeの変更、CPUコア数等を変更する事が出来ます。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.hostname = "<hostname>" # hostname指定
  config.disksize.size = "<DiskSize>" # DiskSize指定
  config.vm.provider "virtualbox" do |v|
    v.memory = <MemorySize> # MemorySize指定
    v.cpus = <CPU数> # CPU数指定
  end
end
```

## hostname

`vm.hostname`を指定する事により、VMのhostnameを設定する事が出来ます。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.hostname = "centos"
end
```

hostnameにcentosを設定します。

## DiskSize

`disksize.size`を指定する事により、VMのDiskSizeを設定する事が出来ます。  
なお、disksize.sizeは`vagrant-disksize`というプラグインで管理されているため、  
**PowerShell**で事前にプラグインをインストールする必要があります。

```console
PS C:\Users\user01\vagrant_test> vagrant plugin install vagrant-disksize
Installing the 'vagrant-disksize' plugin. This can take a few minutes...
Fetching vagrant-vbguest-0.27.0.gem
Fetching vagrant-disksize-0.1.3.gem
Successfully uninstalled vagrant-vbguest-0.27.0
Installed the plugin 'vagrant-disksize (0.1.3)'!
```

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.disksize.size = "55GB"
end
```
DiskSizeを55GBに設定します。

!!!warning
  DiskSizeの変更はOS(Box)やProviderによってはサポートされていない場合があります。  
  Vagrantfileに当該の記述を行ってもDiskSizeが変更されない可能性がある事に注意してください。
  (`freebsd/FreeBSD-10.2-RELEASE`のBoxでは変更可能を確認済み)

## MemorySize

`vm.provider`に`virtualbox`を指定、ブロック内に`memory`を指定する事により、VMのMemorySizeを設定する事が出来ます。  
なお、単位はMBとなります。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
  end
end
```

MemorySizeを512MBに設定します。

## CPUコア数

`vm.provider`に`virtualbox`を指定、ブロック内に`cpus`を指定する事により、VMのCPUコア数を設定する事が出来ます。  

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
  end
end
```

CPUコア数を2に設定します。

## Reference

- [Machine Settings | Vagrant by HashiCorp](https://www.vagrantup.com/docs/vagrantfile/machine_settings)
- [Vagrantfileに一行書くだけでVMのディスク容量を増やす方法 | Qiita](https://qiita.com/yut_h1979/items/c84c490053877beee5c1)
- [Providers - VirtualBox - Configuration | Vagrant by HashiCorp](https://www.vagrantup.com/docs/providers/virtualbox/configuration)
