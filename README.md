# development environment for soccer portal
サカポのサーバサイド開発に必要なミドルウェアを用意する

## 構築手順
* prerequisites
	* [VirtualBox] (https://www.virtualbox.org/wiki/Downloads)
	* [Vagrant] (https://www.vagrantup.com/downloads.html)

### 1.Vagrant plugins セットアップ
```
$ vagrant plugin install vagrant-docker-compose
$ vagrant plugin install vagrant-hostsupdater
```

### 2.リポジトリをチェックアウト
```
$ git clone git@github.com:soccer-portal/devenv.git 
```
Vagrantfile を自分の環境に合わせて修正
```
$ cd devenv
$ vi Vagrantfile

- "ip" => "10.99.3.100",
- "ports" => { 3306 => 3306, 6379 => 6379 },
+ "ip" => "xx.xx.xx.xxx",
+ "ports" => { 3306 => 13306, 6379 => 16379 },
```

### 3.vagrant up
```
$ vagrant up --provision
```
