johnsonshu translating

Create Local YUM repository on CentOS 7 / RHEL 7 using DVD
================================================================================

YUM is the package management tool that helps you to install or update the package through the network or local, at the same time it provides easy method to install a package with it’s dependent packages. Configuration files are under /etc directory, /etc/yum.conf is the mail global file that contains the global options such as cache directory,log directory etc… To add new or update the existing repository, you must got to the /etc/repos.d directory and create or open a file that ends on .repo respectively.

### Create Source: ###

Before creating new repository file, you must know the repository source ( whether the packages stored locally or remotely); Repository sources can be created either using createrepo package or mounting the DVD on the directory, mounting the DVD/CD ROM will lead to save the space on hdd used by being copied to HDD.

Mount the CD/DVD ROM on the any directory of your wish, for testing mount it on /cdrom.

    # mkdir /cdrom
    # mount /dev/cdrom /cdrom

Configuration file:

Create the new repo file called cdrom.repo under /etc/repos.d directory.

    # vi /etc/yum.repos.d/local.repo

Add the following details.

    [LocalRepo]
    name=Local Repository
    baseurl=file:///cdrom
    enabled=1
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

1. **[LocalRepo]** – Name of the Section.
2. **name** = Name of the repository
3. **baseurl** = Location of the package
4. **Enabled** = Enable repository
5. **gpgcheck**= Enable secure installation
6. **gpgkey**= Location of the key

### Note: ###
1. gpgcheck is optional (If you set gpgcheck=0, there is no need to mention gpgkey)
2. You may find multiple repository files in /etc/yum.repos.d directory, remove the all the repo files except local.repo. This is to ensure that your system do not look for packages from CentOS or Redhat repositories.
### Installation: ###
Before installing clear the repository cache by issuing the following command.

    # yum clean all

Install the package using the yum command, let’s install the vsftpd package from the local repository.

    # yum install vsftpd

Out put will be like below, it will try to cache the package information. When you give yes to download the package, it will prompt you to accept gpg signing key.


    Loaded plugins: fastestmirror
    LocalRepo                                                | 3.6 kB     00:00
    (1/2): LocalRepo/group_gz                                  | 157 kB   00:00
    (2/2): LocalRepo/primary_db                                | 2.7 MB   00:00
    Determining fastest mirrors
    Resolving Dependencies
    --> Running transaction check
    ---> Package vsftpd.x86_64 0:3.0.2-9.el7 will be installed
    --> Finished Dependency Resolution
     
    Dependencies Resolved
     
    ================================================================================
    Package         Arch            Version               Repository          Size
    ================================================================================
    Installing:
    vsftpd          x86_64          3.0.2-9.el7           LocalRepo          165 k
     
    Transaction Summary
    ================================================================================
    Install  1 Package
     
    Total download size: 165 k
    Installed size: 343 k
    Is this ok [y/d/N]: y
    Downloading packages:
    warning: /cdrom/Packages/vsftpd-3.0.2-9.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
    Public key for vsftpd-3.0.2-9.el7.x86_64.rpm is not installed
    Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    Importing GPG key 0xF4A80EB5:
    Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
    Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
    Package    : centos-release-7-0.1406.el7.centos.2.3.x86_64 (@anaconda)
    From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    Is this ok [y/N]: y
    Running transaction check
    Running transaction test
    Transaction test succeeded
    Running transaction
    Installing : vsftpd-3.0.2-9.el7.x86_64                                    1/1
    Verifying  : vsftpd-3.0.2-9.el7.x86_64                                    1/1
     
    Installed:
    vsftpd.x86_64 0:3.0.2-9.el7
     
    Complete!

That’s all you have successfully configured the local repository on the machine, but it is limited to single machine where the CD or DVD is mounted. Follow the guide to setup the repository for the network installation.


--------------------------------------------------------------------------------

via: http://www.itzgeek.com/how-tos/linux/centos-how-tos/create-local-yum-repository-on-centos-7-rhel-7-using-dvd.html

作者：[Raj in][a]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创翻译，[Linux中国](http://linux.cn/) 荣誉推出

[a]:https://plus.google.com/+Itzgeek/
