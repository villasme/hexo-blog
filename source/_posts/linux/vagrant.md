---
title: vagrant
date: 2018-09-13 13:21:13
categories:
- linux
tags:
- linux
- vagrant
---

## 安装VMBox

## 新建 Vagrantfile

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.6.0"

boxes = [
    {
        :name => "docker-host",
        :eth1 => "192.168.205.10",
        :mem => "1024",
        :cpu => "1"
    }
]

Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = opts[:mem]
        v.vmx["numvcpus"] = opts[:cpu]
      end
      config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", opts[:mem]]
        v.customize ["modifyvm", :id, "--cpus", opts[:cpu]]
      end
      config.vm.network :private_network, ip: opts[:eth1]
    end
  end
  config.vm.synced_folder "./labs", "/home/vagrant/labs"
  config.vm.provision "shell", privileged: true, path: "./setup.sh"
end
```

## vagrant-setup.sh

```bash  setup.sh
#/bin/sh

# install some tools
sudo yum install -y git vim gcc glibc-static telnet bridge-utils net-tools

# install docker
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh

# start docker service
sudo systemctl start docker

rm -rf get-docker.sh
```

[vagrant 参考链接](https://segmentfault.com/a/1190000008729625#articleHeader7)