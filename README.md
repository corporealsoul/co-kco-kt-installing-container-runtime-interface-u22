### Installing Container Runtime Interface (CRI), https://kubernetes.io/docs/setup/production-environment/container-runtimes/

**Docker Engine, **https://kubernetes.io/docs/setup/production-environment/container-runtimes/#docker

1. On each of your nodes, install Docker for your Linux distribution as per Install Docker Engine, https://docs.docker.com/engine/install/#server

2. Install cri-dockerd, following the instructions in that source code repository, https://github.com/Mirantis/cri-dockerd,

**Note : **For cri-dockerd, the CRI socket is unix:///var/run/cri-dockerd.sock by default.

<br>

`anup@ubuntu-22042-08:~$ sudo apt-get update`

`anup@ubuntu-22042-08:~$ sudo apt-get install git`

`anup@ubuntu-22042-08:~$ git clone https://github.com/Mirantis/cri-dockerd.git`

`anup@ubuntu-22042-08:~$ cd cri-dockerd/`

`anup@ubuntu-22042-08:~/cri-dockerd$ sudo apt-get update`

`anup@ubuntu-22042-08:~/cri-dockerd$ sudo apt-get install make`

`anup@ubuntu-22042-08:~/cri-dockerd$ make cri-dockerd`

<br>

`[anup@rhel-92-04 cri-dockerd]$ mkdir -p /usr/local/bin`

`[anup@rhel-92-04 cri-dockerd]$ sudo install -o root -g root -m 0755 cri-dockerd /usr/local/bin/cri-dockerd`

`[anup@rhel-92-04 cri-dockerd]$ sudo install packaging/systemd/* /etc/systemd/system`

`[anup@rhel-92-04 cri-dockerd]$ sudo sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service`

<br>

`[anup@rhel-92-04 cri-dockerd]$ sudo systemctl daemon-reload`

`[anup@rhel-92-04 cri-dockerd]$ sudo systemctl status cri-docker.service`

`[anup@rhel-92-04 cri-dockerd]$ sudo systemctl start cri-docker.service`

`[anup@rhel-92-04 cri-dockerd]$ sudo systemctl enable cri-docker.service`

`[anup@rhel-92-04 cri-dockerd]$ sudo systemctl status --now cri-docker.socket`

`[anup@rhel-92-04 cri-dockerd]$ sudo systemctl enable --now cri-docker.socket`

`[anup@rhel-92-04 cri-dockerd]$ ls -ltr /var/run/cri-dockerd.sock `

`[anup@rhel-92-04 cri-dockerd]$ cd`

<br>
