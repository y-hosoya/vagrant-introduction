# Vagrantfileとは

`Vagrantfile`はVM作成するときのconfig（VM定義）やprovision（起動後の処理）を記述するファイルです。  
設定できるものは以下などがあります。

- config
    - 使用するboxの指定
    - VMのスペック定義
    - IPアドレス、ポート、Hostnameの設定
- provision
    - VM起動後にシェルスクリプトを実行
    - VM起動後にAnsibleを実行

ファイルはRuby言語で記述されています。  
Ruby言語の規約に従えば自由な記述が出来ますが、Ruby知識が無くても`Vagrantfile`を作成することが出来ます。

[準備](../../how_to_use/preparation)で作成した`Vagrantfile`は以下になってました。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos8" # 使用するBoxを指定している
end
```

この2行目にBoxの指定するコーディングがされていることが分かります。  

!!!warning
    `vm.box`はVM作成する上で必須のパラメータになります。

実際、上記の3行のみでVMを作成することが出来ますが、MemoryやDiskSizeなどはデフォルトの値となります。  
これを指定するために、次章より`Vagrantfile`の詳細を見ていきます。

また指定した値は、VM起動後も変更することが可能です。

## Reference

- [Vagrantfile | Vagrant by HashiCorp](https://www.vagrantup.com/docs/vagrantfile)
