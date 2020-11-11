# OS一覧

Vagrantでは様々なOSの仮想マシンを作成することが出来ます。

## Vagrant Box

使用できる仮想マシンのテンプレートを**Box**と呼びます。  
`Vagrantfile`にBoxの名前を記載することで、使用するBoxを指定します。

[Vagrant Cloud](https://app.vagrantup.com/boxes/search)から、任意のBoxを検索することが出来ます。

### Exmaple

[準備](../preparation)で使用した**generic/centos8**のページを確認してみます。  
[Vagrant box generic/centos8 - Vagrant Cloud](https://app.vagrantup.com/generic/boxes/centos8)

**Vagrantfile**のタブには以下が記載されています。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
end
```

上記の`Vagrantfile`を作成して作業ディレクトリに配置し、`vagrant up`を実行することでVMを作成することが出来ます。

**New**のタブには以下が記載されています。

```shell
vagrant init generic/centos8
vagrant up
```

`vagrant init`を実行すると、引き数として実行されたBoxを**Vagrant Cloud**へ探し、  
それに該当する`Vagrantfile`(**Vagrantfile**のタブのもの)が作成されます。

---

また、Boxの詳細バージョンを指定する事もできます。  
**v3.1.4**をクリックして指定バージョンのページに移動すると、Vagrantfileとコマンドに追加された項目があります。  
この追加行によってバージョンを指定することが可能です。

**Vagrantfile**タブ

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8"
  config.vm.box_version = "3.1.4" # 追加された行
end
```

**New**タブ

```shell
vagrant init generic/centos8 \
  --box-version 3.1.4 # 追加された行
vagrant up
```
