# Laravel Ansible

## Usage

TODO

## Example of Vagrantfile

```
# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "vagrant"

  # ホストのポート 58080 をvagrantの80につなげる
  config.vm.network "forwarded_port", guest: 80, host: 58080

  # ipアドレス 適当に変更してOK
  config.vm.network :private_network, ip: "192.168.33.11"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  # ホストとディレクトリを同期する
  config.vm.synced_folder "applications", "/home/vagrant/applications", create: true, mount_options: ["uid=vagrant,gid=vagrant"]

  # ansibleの設定
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
  end
end
```
