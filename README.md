Домашнее задание по курсу «Администратор Linux. Professional»
Обновление ядра Linux.
Развернута ВМ с ОС centos8



PS C:\otus\h1> vagrant ssh
[vagrant@kernel-update ~]$ uname -r
4.18.0-240.1.1.el8_3.x86_64
[vagrant@kernel-update ~]$
[vagrant@kernel-update ~]$
[vagrant@kernel-update ~]$ sudo yum install -y https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
CentOS Linux 8 - AppStream                                                              0.0  B/s |   0  B     00:00
Errors during downloading metadata for repository 'appstream':
  - Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=vag [Could not resolve host: mirrorlist.centos.org]
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=vag [Could not resolve host: mirrorlist.centos.org]
[vagrant@kernel-update ~]$ rpm --import https://www.elrepo.org/RPM-GPG-KEY-v2-elrepo.org
error: can't create transaction lock on /var/lib/rpm/.rpm.lock (Permission denied)
error: https://www.elrepo.org/RPM-GPG-KEY-v2-elrepo.org: key 1 import failed.
[vagrant@kernel-update ~]$ sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-v2-elrepo.org
[vagrant@kernel-update ~]$ sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
[vagrant@kernel-update ~]$ sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-v2-elrepo.org

[vagrant@kernel-update ~]$ cd /etc/yum.repos.d/
[vagrant@kernel-update yum.repos.d]$ ll
total 48
-rw-r--r--. 1 root root  719 Nov 10  2020 CentOS-Linux-AppStream.repo
-rw-r--r--. 1 root root  704 Nov 10  2020 CentOS-Linux-BaseOS.repo
-rw-r--r--. 1 root root 1130 Nov 10  2020 CentOS-Linux-ContinuousRelease.repo
-rw-r--r--. 1 root root  318 Nov 10  2020 CentOS-Linux-Debuginfo.repo
-rw-r--r--. 1 root root  732 Nov 10  2020 CentOS-Linux-Devel.repo
-rw-r--r--. 1 root root  704 Nov 10  2020 CentOS-Linux-Extras.repo
-rw-r--r--. 1 root root  719 Nov 10  2020 CentOS-Linux-FastTrack.repo
-rw-r--r--. 1 root root  740 Nov 10  2020 CentOS-Linux-HighAvailability.repo
-rw-r--r--. 1 root root  693 Nov 10  2020 CentOS-Linux-Media.repo
-rw-r--r--. 1 root root  706 Nov 10  2020 CentOS-Linux-Plus.repo
-rw-r--r--. 1 root root  724 Nov 10  2020 CentOS-Linux-PowerTools.repo
-rw-r--r--. 1 root root  898 Nov 10  2020 CentOS-Linux-Sources.repo
[vagrant@kernel-update yum.repos.d]$ sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/CentOS-*.repo
sed: couldn't open temporary file /etc/yum.repos.d/sedrME4wX: Permission denied
[vagrant@kernel-update yum.repos.d]$ sudo sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/CentOS-*.repo
[vagrant@kernel-update yum.repos.d]$ sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/CentOS-*.repo
sed: couldn't open temporary file /etc/yum.repos.d/sedyyXCVP: Permission denied
[vagrant@kernel-update yum.repos.d]$ sudo sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/CentOS-*.repo
[vagrant@kernel-update yum.repos.d]$ sudo sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/CentOS-*.repo
[vagrant@kernel-update yum.repos.d]$ sudo yum install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
CentOS Linux 8 - AppStream                                                              1.7 MB/s | 8.4 MB     00:04
CentOS Linux 8 - BaseOS                                                                 1.6 MB/s | 4.6 MB     00:02
CentOS Linux 8 - Extras                                                                 9.1 kB/s |  10 kB     00:01
elrepo-release-8.el8.elrepo.noarch.rpm                                                   22 kB/s |  19 kB     00:00
Dependencies resolved.
========================================================================================================================
 Package                       Architecture          Version                          Repository                   Size
========================================================================================================================
Installing:
 elrepo-release                noarch                8.4-2.el8.elrepo                 @commandline                 19 k

Transaction Summary
========================================================================================================================
Install  1 Package

Total size: 19 k
Installed size: 8.3 k
Is this ok [y/N]: y
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                1/1
  Installing       : elrepo-release-8.4-2.el8.elrepo.noarch                                                         1/1
  Verifying        : elrepo-release-8.4-2.el8.elrepo.noarch                                                         1/1

Installed:
  elrepo-release-8.4-2.el8.elrepo.noarch

Complete!
[vagrant@kernel-update yum.repos.d]$ sudo yum --enablerepo elrepo-kernel install kernel-ml -y
ELRepo.org Community Enterprise Linux Repository - el8                                  181 kB/s | 230 kB     00:01
ELRepo.org Community Enterprise Linux Kernel Repository - el8                           1.2 MB/s | 2.2 MB     00:01
Dependencies resolved.
========================================================================================================================
 Package                        Architecture        Version                            Repository                  Size
========================================================================================================================
Installing:
 kernel-ml                      x86_64              6.12.10-1.el8.elrepo               elrepo-kernel              143 k
Installing dependencies:
 kernel-ml-core                 x86_64              6.12.10-1.el8.elrepo               elrepo-kernel               64 M
 kernel-ml-modules              x86_64              6.12.10-1.el8.elrepo               elrepo-kernel               61 M

Transaction Summary
========================================================================================================================
Install  3 Packages

Total download size: 125 M
Installed size: 170 M
Downloading Packages:
(1/3): kernel-ml-6.12.10-1.el8.elrepo.x86_64.rpm                                        239 kB/s | 143 kB     00:00
(2/3): kernel-ml-core-6.12.10-1.el8.elrepo.x86_64.rpm                                   1.2 MB/s |  64 MB     00:54
(3/3): kernel-ml-modules-6.12.10-1.el8.elrepo.x86_64.rpm                                908 kB/s |  61 MB     01:09
------------------------------------------------------------------------------------------------------------------------
Total                                                                                   1.8 MB/s | 125 MB     01:09
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                1/1
  Installing       : kernel-ml-core-6.12.10-1.el8.elrepo.x86_64                                                     1/3
  Running scriptlet: kernel-ml-core-6.12.10-1.el8.elrepo.x86_64                                                     1/3
  Installing       : kernel-ml-modules-6.12.10-1.el8.elrepo.x86_64                                                  2/3
  Running scriptlet: kernel-ml-modules-6.12.10-1.el8.elrepo.x86_64                                                  2/3
  Installing       : kernel-ml-6.12.10-1.el8.elrepo.x86_64                                                          3/3
  Running scriptlet: kernel-ml-core-6.12.10-1.el8.elrepo.x86_64                                                     3/3
dracut: Disabling early microcode, because kernel does not support it. CONFIG_MICROCODE_[AMD|INTEL]!=y

  Running scriptlet: kernel-ml-6.12.10-1.el8.elrepo.x86_64                                                          3/3
  Verifying        : kernel-ml-6.12.10-1.el8.elrepo.x86_64                                                          1/3
  Verifying        : kernel-ml-core-6.12.10-1.el8.elrepo.x86_64                                                     2/3
  Verifying        : kernel-ml-modules-6.12.10-1.el8.elrepo.x86_64                                                  3/3

Installed:
  kernel-ml-6.12.10-1.el8.elrepo.x86_64                        kernel-ml-core-6.12.10-1.el8.elrepo.x86_64
  kernel-ml-modules-6.12.10-1.el8.elrepo.x86_64

Complete!
[vagrant@kernel-update yum.repos.d]$ uname -r
4.18.0-240.1.1.el8_3.x86_64
[vagrant@kernel-update yum.repos.d]$ sudo reboot
Connection to 127.0.0.1 closed by remote host.
PS C:\otus\h1> vagrant ssh
Last login: Tue Jan 21 12:05:04 2025 from 10.0.2.2
[vagrant@kernel-update ~]$ uname -r
6.12.10-1.el8.elrepo.x86_64
[vagrant@kernel-update ~]$