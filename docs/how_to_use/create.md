# VM作成

作業ディレクトリ上で以下のコマンドを実行することでVMを操作できます。

## Create VM

`vagrant up`を実行してVMを起動することができます。  
また、VMが未作成の場合は作成されます。

```console
PS C:\Users\user01\vagrant_test> vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'generic/centos8'...
==> default: Matching MAC address for NAT networking...

snip...
```

処理が完了して`vagrant status`コマンドを実行すると、VMの起動状態を確認できます。  
以下は起動後の状態なので、**running (virtualbox)**と表示されています。

```console
PS C:\Users\user01\vagrant_test> vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```

## SSH VM

`vagrant ssh`を実行してVMにsshすることが出来ます。

```console
PS C:\Users\user01\vagrant_test> vagrant ssh
[vagrant@centos8 ~]$
```

## Power Off VM

`vagrant halt`を実行してVMをPower Offすることが出来ます。

```console
PS C:\Users\user01\vagrant_test> vagrant halt
==> default: Attempting graceful shutdown of VM...
PS C:\Users\user01\vagrant_test> vagrant status
Current machine states:

default                   poweroff (virtualbox)

The VM is powered off. To restart the VM, simply run `vagrant up`
```

## Pause VM

`vagrant suspend`を実行してVMを一時停止することが出来ます。

```console
PS C:\Users\user01\vagrant_test> vagrant suspend
==> default: Saving VM state and suspending execution...
PS C:\Users\user01\vagrant_test> vagrant status
Current machine states:

default                   saved (virtualbox)

To resume this VM, simply run `vagrant up`.
```

## Destroy VM

`vagrant destroy`を実行してVMを削除することが出来ます。  
また、`-f`オプションで強制的に削除できます。

```console
PS C:\Users\user01\vagrant_test> vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Forcing shutdown of VM...
==> default: Destroying VM and associated drives...
PS C:\Users\user01\vagrant_test> vagrant status
Current machine states:

default                   not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
```

以上でVM作成から削除まで実行することが出来ました。

## Reference

他にもコマンドがありますが、詳細は以下の公式サイトをご覧ください。

- [Command-Line Interface | Vagrant by HashiCorp](https://www.vagrantup.com/docs/cli)
