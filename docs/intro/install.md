# インストール

Vagrantを使用するためには、仮想化ソフトウェアがインストールされている必要があります。

ここでは、Windows10にVirtualBoxとVagrantをインストールします。

## VirtualBoxインストール

以下のページから、使用するOS種類を選択してインストールします。  
[Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)

インストールが完了したら**PowerShell**で以下のコマンドを実行します。
バージョンが表示され、無事にインストールされていることを確認します。

```console
PS C:\Users\user01> cd 'C:\Program Files\Oracle\VirtualBox\'
PS C:\Program Files\Oracle\VirtualBox> .\VBoxManage.exe --version
6.1.14r140239
```

## Vagrantインストール

以下のページから、使用するOS種類を選択してインストールします。  
[Downloads | Vagrant by HashiCorp](https://www.vagrantup.com/downloads)

インストールが完了したら**PowerShell**で以下のコマンドを実行します。
バージョンが表示され、無事にインストールされていることを確認します。

```console
PS C:\Program Files\Oracle\VirtualBox> vagrant --version
Vagrant 2.2.10
```

以上でVagrantを使用する準備が完了しました。
