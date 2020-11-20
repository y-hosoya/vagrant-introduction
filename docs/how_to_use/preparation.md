# 準備

Vagrantでは、作成する仮想マシンをディレクトリに分けて管理することが出来ます。  
ディレクトリに配置された`Vagrantfile`を参照し、記載されている仮想マシンの定義/起動/構築を行います。

## 作業ディレクトリ作成

以下の例では、ホームディレクトリに移動して`vagrant_test`という名前でディレクトリを作成します。

```console
PS C:\Users\user01> mkdir vagrant_test


    ディレクトリ: C:\Users\user01


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2020/11/11     13:10                vagrant_test
```

作成したディレクトリに移動します。

```console
PS C:\Users\user01> cd vagrant_test
PS C:\Users\user01\vagrant_test>
```

## ディレクトリの初期化

`vagrant init <作成したいOS(Box)>`コマンドを実行することで、`Vagrantfile`を作成することができます。  
以下ではCentOS8の`Vagrantfile`を作成しています。

```console
PS C:\Users\user01\vagrant_test> vagrant init generic/centos8 --minimal
==> vagrant: A new version of Vagrant is available: 2.2.13 (installed version: 2.2.10)!
==> vagrant: To upgrade visit: https://www.vagrantup.com/downloads.html

A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

!!! Tip
    上記のコマンドは`--minimal`をオプションを付けて実行しています。  
    オプション無しで実行した場合は、コメントアウトで`Vagrantfile`の使い方が記載されたファイルが作成されます。
    (行数が多いので割愛。)  
    `Vagrantfile`の詳細は[Vagrantfileとは](../../vagrantfile/vagrantfile)を参してください。

`Vagrantfile`が作成されたことを確認します。

```console
PS C:\Users\user01\vagrant_test> ls


    ディレクトリ: C:\Users\user01\vagrant_test


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2020/11/11     13:17           3091 Vagrantfile

PS C:\Users\user01\vagrant_test> cat Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
end
```

## プラグインのインストール(Optional)

Vagrantには多くのプラグインが用意されており、便利機能を追加することができます。  
[Available Vagrant Plugins · hashicorp/vagrant Wiki](https://github.com/hashicorp/vagrant/wiki/Available-Vagrant-Plugins)で使用できるプラグイン一覧が確認できます。

プラグインをインストールするには`vagrant plugin install <プラグイン名>`を実行します。

```console
PS C:\Users\user01\vagrant_test> vagrant plugin install vagrant-vbguest
Installing the 'vagrant-vbguest' plugin. This can take a few minutes...
Fetching micromachine-3.0.0.gem
Fetching vagrant-vbguest-0.27.0.gem
Installed the plugin 'vagrant-vbguest (0.27.0)'!
```

ここでは`vagrant-vbguest`をインストールしています。  
ゲストOS側とホストOS側のGuestAdditionを揃えてくれるプラグインです。  
[dotless-de/vagrant-vbguest: A Vagrant plugin to keep your VirtualBox Guest Additions up to date](https://github.com/dotless-de/vagrant-vbguest)

`vagrant plugin list`コマンドでインストールされているプラグインの一覧が確認できます。

```console
PS C:\Users\user01\vagrant_test> vagrant plugin list
vagrant-rdp (0.6.0, global)
  - Version Constraint: > 0
vagrant-vbguest (0.24.0, global)
vagrant-winnfsd (1.4.0, global)
  - Version Constraint: > 0
```

以上でVMを作成する準備が出来ました。

!!! Tip
    - 上記ではCentOS8を使用しましたが、[こちら](https://app.vagrantup.com/boxes/search)から使用するOSを検索できます(詳細は[OS一覧](./box.md)ページ参照)
    - `vagrant init`コマンドは、`Vagrantfile`のみを作成するものです。
        - Memory,IPアドレス,ホスト名などを指定する場合は、`Vagranfile`を編集することで指定のVM作成が可能です(詳細はvagrantfileページ参照)
        - GitHubなどで既に`Vagrantfile`が用意されている場合は実施する必要はありません(詳細はvagrantfileページ参照)

## Reference

- [Plugin Usage - Plugins | Vagrant by HashiCorp](https://www.vagrantup.com/docs/plugins/usage)
