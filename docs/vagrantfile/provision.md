# プロビジョニング

Vagrantfileに`vm.provision`の記述を行う事により、Windows(Host OS)からVM(Guest OS)へファイル/ディレクトリのアップロード、またVM(Guest OS)にログインすることなくシェルやAnsible等を実行することが出来ます。

## ファイル/ディレクトリアップロード

パラメータに`file`を指定し、`source`, `destination`にパスを指定することにより、  
Host OSからVMへファイル/ディレクトリのアップロードを行う事が出来ます。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "file", source: "<Host OSパス>", destination: "<VMパス>"
end
```

### file

ファイルもしくはディレクトリのアップロードを行う事を明示する値です。

### source

アップロード元であるHost OSのパスを指定します。  
絶対パス・相対パスどちらも指定可能で、相対パスの起点はVagrantfileがある場所です。

### destination

アップロード先であるVMのパスを指定します。  
相対パスを記述することは出来ず、絶対パスを記述する必要があります。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "file", source: "~/.gitconfig", destination: "$HOME/.gitconfig"
end
```

Host OSのホームディレクトリ配下にある`.gitconfig`ファイルをVMの/home/vagrantディレクトリ配下へ`.gitconfig`というファイル名でコピーします。  
Vagrantの実行はvagrantユーザで行われるため、$HOMEには`/home/vagrant`という値が格納されます。

## シェル

パラメータに`shell`を指定及び、`inline`もしくは`path`を指定することによりVM内でシェルが実行されます。  
`inline`内に実行したいコマンドを記述することによりVM内でコマンドが実行されます。  
また、`inline`ではなく`path`を記述することにより`script.sh`のようなシェルスクリプトを実行することも可能です。   
当機能を利用することによりパッケージのインストール等を自動的に行う事が出来ます。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "shell",
    inline: "<実行したいコマンド>", privileged: true
end
```

### shell

シェルの実行を行う事を明示する値です。

### inline

Vagrantfileに直接実行するコマンドを記述する場合に利用します。  
実行したいコマンドをダブルクオーテーションで囲むことによりVM内でコマンドが実行されます。  
### path
script.shのような外部スクリプトを実行する際に利用します。  
VMではなくHost OS上のパスを指定する必要があることに注意してください。  
絶対パス・相対パスどちらも指定可能で、相対パスの起点はVagrantfileがある場所です。  
### privileged
特権ユーザとして実行が必要な場合、trueを指定します。  
オプション項目であるため、指定しない場合でもシェルは実行されます。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "shell",
    inline: "cp /home/vagrant/.gitconfig $HOME/.gitconfig", privileged: true
end
```

VM上の`/home/vagrant/.gitconfig`を`/root/.gitconfig`へコピーします。  
**privileged**: trueを指定することにより特権ユーザで実行されるため$HOMEには`/root`という値が格納されます。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "shell", path: "script.sh"
end
```

Host OSのVagrantfileが配置されているディレクトリに存在する`script.sh`をVM上で実行します。

## Ansible

Host OS上もしくはVM上でAnsibleを実行することが出来ます。  
本項ではVM上でAnsibleを実行する手順を紹介します。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "<プレイブック>"
    ansible.inventory_path = "<インベントリファイル>"
    ansible.limit = "<対象ホストの制限>"
    ansible.raw_arguments  = [ "<ansible-playbook実行時に指定する引数>" ]
  end
end
```

### ansible_local

VM上でAnsibleを実行することを明示する値です。  
なおHost OS上でAnsibleを実行する際はansibleを指定します。

### ansible.playbook

プレイブックであるymlファイルを指定します。

### ansible.inventory_path

インベントリファイルを指定します。  
ansible-playbookの-i(--inventory)オプションと同義です。

### ansible.limit

Ansibleを実行するホストを制限する場合に利用します。  
ansible-playbookの-l(--limit)オプションと同義です。

### ansible.raw_arguments

ansible-playbookを実行する際、追加の引数を設定したい場合利用します。

!!!Example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "site.yml"
    ansible.inventory_path = "inventory.ini"
    ansible.limit = "all"
    ansible.raw_arguments  = [ "-e @vars.yml" ]
  end
end
```

プレイブックに`site.yml`を指定、インベントリに`inventory.ini`を指定、  
実行対象はすべてのホスト、ansible-playbookに`-e @vars.yml`のオプションを追加してAnsibleを実行します。  
VM上で以下を実行する事と同義です。

`ansible-playbook -i inventory.ini site.yml -l all -e @vars.yml`

## Reference

プロビジョニングで利用できる機能は他にも存在します。  
詳細は以下の公式サイトをご覧ください。

[Basic Usage - Provisioning | Vagrant by HashiCorp](https://www.vagrantup.com/docs/provisioning/basic_usage)
