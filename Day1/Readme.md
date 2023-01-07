### Opearting System ##
<img src="os.png"/>

### VM vs Container ##
<img src="Container vs VM.jpg"/>

<img src="Container vs VM1.jpg"/>

### Use Cases ###

### Docker Architecture ##

<img src="Docker Architecture.jpg"/>

### Installing Docker ##
```
[root@ip-172-31-87-240 ~]# yum install docker 
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Resolving Dependencies
--> Running transaction check
---> Package docker.x86_64 0:20.10.17-1.amzn2.0.1 will be installed
--> Processing Dependency: runc >= 1.0.0 for package: docker-20.10.17-1.amzn2.0.1.x86_64
--> Processing Dependency: libcgroup >= 0.40.rc1-5.15 for package: docker-20.10.17-1.amzn2.0.1.x86_64
--> Processing Dependency: containerd >= 1.3.2 for package: docker-20.10.17-1.amzn2.0.1.x86_64
--> Processing Dependency: pigz for package: docker-20.10.17-1.amzn2.0.1.x86_64
--> Running transaction check
---> Package containerd.x86_64 0:1.6.8-1.amzn2 will be installed
---> Package libcgroup.x86_64 0:0.41-21.amzn2 will be installed
---> Package pigz.x86_64 0:2.3.4-1.amzn2.0.1 will be installed
---> Package runc.x86_64 0:1.1.4-1.amzn2 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

==========================================================================================================================
 Package                  Arch                 Version                              Repository                       Size
==========================================================================================================================
Installing:
 docker                   x86_64               20.10.17-1.amzn2.0.1                 amzn2extra-docker                39 M
Installing for dependencies:
 containerd               x86_64               1.6.8-1.amzn2                        amzn2extra-docker                27 M
 libcgroup                x86_64               0.41-21.amzn2                        amzn2-core                       66 k
 pigz                     x86_64               2.3.4-1.amzn2.0.1                    amzn2-core                       81 k
 runc                     x86_64               1.1.4-1.amzn2                        amzn2extra-docker               2.9 M

Transaction Summary
==========================================================================================================================
Install  1 Package (+4 Dependent packages)

Total download size: 69 M
Installed size: 260 M
Is this ok [y/d/N]: y
Downloading packages:
```
### Non cloud based linux vms ###
[use_link](https://docs.docker.com/engine/install/rhel/)

```
        yum install -y yum-utils device-mapper-persistent-data lvm2
	yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
	yum list docker-ce --showduplicates | sort -r
	yum install -y docker-ce
	yum install -y docker-ce
 ```
 
 ### Start Docker ####
 ```
 [root@master ~]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://docs.docker.com
[root@master ~]# systemctl start docker
[root@master ~]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: active (running) since Sat 2023-01-07 14:01:51 IST; 4s ago
     Docs: https://docs.docker.com
 Main PID: 1737 (dockerd)
    Tasks: 8
   Memory: 26.3M
   CGroup: /system.slice/docker.service
           └─1737 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.174700466+05:30" level=info msg="scheme \"unix\" not registered, ...ule=grpc
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.174717288+05:30" level=info msg="ccResolverWrapper: sending updat...ule=grpc
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.174726871+05:30" level=info msg="ClientConn switching balancer to...ule=grpc
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.190000182+05:30" level=info msg="Loading containers: start."
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.370152512+05:30" level=info msg="Default bridge (docker0) is assi...address"
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.442191457+05:30" level=info msg="Loading containers: done."
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.481430544+05:30" level=info msg="Docker daemon" commit=42c8b31 gr...20.10.22
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.481522668+05:30" level=info msg="Daemon has completed initialization"
Jan 07 14:01:51 master systemd[1]: Started Docker Application Container Engine.
Jan 07 14:01:51 master dockerd[1737]: time="2023-01-07T14:01:51.498441691+05:30" level=info msg="API listen on /var/run/docker.sock"
Hint: Some lines were ellipsized, use -l to show in full.
[root@master ~]#

[root@master ~]# systemctl enable docker
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[root@master ~]#
```

#### Non Root User ###
```
[root@master ~]# useradd srini
[root@master ~]# usermod -aG docker srini
[root@master ~]# echo "welcome1"  |  passwd srini --stdin
Changing password for user srini.
passwd: all authentication tokens updated successfully.
[root@master ~]#
```

### Docker Operations ###
Pulling image from docker hub
```
[srini@master ~]$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[srini@master ~]$ docker  pull oraclelinux:8.4
8.4: Pulling from library/oraclelinux
a4df6f21af84: Pull complete
Digest: sha256:b81d5b0638bb67030b207d28586d0e714a811cc612396dbe3410db406998b3ad
Status: Downloaded newer image for oraclelinux:8.4
docker.io/library/oraclelinux:8.4
[srini@master ~]$

[srini@master ~]$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
oraclelinux   8.4       97e22ab49eea   14 months ago   246MB
[srini@master ~]$
```

### Docker DB ###
[srini@master ~]$ docker  info   |   grep -i root
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
 Docker Root Dir: /var/lib/docker
[srini@master ~]$


[root@master ~]# cd /var/lib/docker
[root@master docker]# ls
buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
[root@master docker]# cd image
[root@master image]# ls
overlay2
[root@master image]# cd overlay2
[root@master overlay2]# ls
distribution  imagedb  layerdb  repositories.json
[root@master overlay2]# cd imagedb
[root@master imagedb]# ls
content  metadata
[root@master imagedb]# cd content
[root@master content]# ls
sha256
[root@master content]# cd sha256/
[root@master sha256]# ls
97e22ab49eea70a5d500e00980537605d56f30f9614b3a6d6c4ae9ddbd642489
[root@master sha256]#
```
