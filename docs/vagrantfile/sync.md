# ファイル共有

Vagrantfileに`vm.synced_folder`の記述を行う事により、  
Windows(Host OS)とVM(Guest OS)間でファイル共有を行う事が出来ます。

ファイル共有を行う事によりHost OS⇔VM間のファイル転送が不要となります。

ファイル共有を行うには各種パラメータを設定する必要があり、  
**Host OSのディレクトリパス**および**VMのディレクトリパス**の指定は必須、その他はオプションとなっています。

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.synced_folder "<Host OSディレクトリパス>", "<VMディレクトリパス>", owner: "<ディレクトリ所有者>", group: "<ディレクトリグループ>", type: "<同期フォルダタイプ>"
end
```

## 必須パラメータ

### 第1パラメータ

Host OSのディレクトリパスを指定します。  
絶対パス・相対パスどちらも指定可能で、`"."`と記述した場合Vagrantfileがある場所を示します。

### 第2パラメータ

VMのディレクトリパスを指定します。  
第1パラメータと違い、絶対パスを記述する必要があります。

## オプションパラメータ

### owner

同期ディレクトリに設定される所有者を指定します。  
指定しない場合vagrantが設定されます。

### group

同期ディレクトリに設定されるグループを指定します。  
指定しない場合vagrantが設定されます。

### type

同期ディレクトリに設定されるファイルタイプを指定します。  
ファイルタイプは**virtualbox**, **nfs**, **rsync**, **smb**が存在し、指定しない場合virtualboxが設定されます。  
特別な理由が無い限りvirtualboxを指定することを推奨します。

---

以下の例ではHost OSのVagrantfileのディレクトリとVMの/vagrantディレクトリを同期します。  
また、所有者およびグループをvagrantに設定しています。

!!!example

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", type: "virtualbox"
end
```

## Reference

設定できるオプションは他にも存在しますが、詳細は以下の公式サイトをご覧ください。

[Basic Usage - Synced Folders | Vagrant by HashiCorp](https://www.vagrantup.com/docs/synced-folders/basic_usage)
