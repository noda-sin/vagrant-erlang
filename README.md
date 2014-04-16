##How to use

1. [こちら](https://www.virtualbox.org/)から，VirtualBoxをインストールして下さい．
2. [こちら](http://www.vagrantup.com/)から，Vagrantをインストールして下さい．
3. Berkshelfと，VagrantのBerkshelf用プラグインが必要です．下記のコマンドでインストールをして下さい．
	
	```
	$ gem install berkshelf
	$ vagrant plugin install vagrant-berkshelf
	```
	
	※エラーが出たら
	
	```
	Installing the 'vagrant-berkshelf' plugin. This can take a few minutes...
	The plugin(s) can't be installed due to the version conflicts below.
	This means that the plugins depend on a library version that conflicts
	with other plugins or Vagrant itself, creating an impossible situation
	where Vagrant wouldn't be able to load the plugins.
	
	You can fix the issue by either removing a conflicting plugin or
	by contacting a plugin author to see if they can address the conflict.
	
	Vagrant could not find compatible versions for gem "celluloid":
	  In Gemfile:
	    vagrant-berkshelf (>= 0) ruby depends on
	      celluloid (~> 0.13.0) ruby
	
	    vagrant (= 1.5.1) ruby depends on
	      celluloid (0.15.2)
	```
	
	`vagrant-berkshelf`のインストールの際に上記のようなエラーが出る場合は，下記の手順を試して下さい．
	
	```
	$ git clone git@github.com:chulkilee/vagrant-berkshelf.git
	$ vagrant-berkshelf/
	$ git checkout c5d6e554d60528a
	$ gem build vagrant-berkshelf.gemspec
	$ vagrant plugin install vagrant-berkshelf-1.4.0.dev1.gem
	```
	
4. リポジトリからVagrantfileとBerksfileを取得して設定を編集します．

	```
	$ git clone git@github.com:fujixerox/erlang-study.git
	$ cd erlang-study/vagrant-erlang
	$ vi Vagrantfile
	```
	
	下記の行で，インスタンスのIPを変更します．
	
	```
	...
	config.vm.network :private_network, ip: "192.168.33.10"
	...	
	```
	
	下記の行で，ローカルのフォルダをVM環境にマウントできます．
	workspaceディレクトリなどをマウントしておくと，捗ると思います．
	
	```
	...
	config.vm.synced_folder "host_dir", "gest_dir"
	...
	```
	
4. 設定が終わったら，下記のコマンドでVMを作ります．
	
	```
	$ vagrant up
	```

5. インスタンスにsshでログインします．

	```
	$ vagrant ssh
	```

6. コンソールでErlang REPLが起動したら成功です！

	```
	$ erl
	>
	```
	
7. 分散プログラミングなどをする際は，iptablesをOFFにするか適当な設定をして下さい．

	```
	$ /etc/init.d/iptables stop
	```
