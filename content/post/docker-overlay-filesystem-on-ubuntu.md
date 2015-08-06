+++
categories = ["misc"]
date = "2015-08-06T18:47:17+09:00"
title = "docker overlay filesystem on ubuntu"

+++

Dockerのfilesystemはいくつかあるんですが、Linux Kernel 3.18からfilesystemに導入されたoverlay filesystemがパフォーマンス良いとのこと。  
試すには、とりあえずKernelを3.18まであげる。今回は現在の最新である3.19にあげてみる。  
ただし、今までのDocker imagesは消えるので注意。

```
cd /tmp
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.19-vivid/linux-headers-3.19.0-031900-generic_3.19.0-031900.201504091832_amd64.deb
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.19-vivid/linux-headers-3.19.0-031900_3.19.0-031900.201504091832_all.deb
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.19-vivid/linux-image-3.19.0-031900-generic_3.19.0-031900.201504091832_amd64.deb
sudo dpkg -i linux-headers-3.19.0-*.deb linux-image-3.19.0-*.deb
```

grubをupdate。

```
sudo update-grub
sudo reboot
```

あとは、Dockerのオプションを変更すれば、overlay stopage driverでDockerが動く。

```
sudo vi /etc/default/docker
DOCKER_OPTS="--storage-driver=overlay"
```

FYI  
http://ubuntuhandbook.org/index.php/2014/12/install-linux-kernel-3-18-ubuntu/  
http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.19-vivid/  
http://blog.cloud66.com/docker-with-overlayfs-first-impression/
