使用安装DVD为 CentOS7/RHEL7 创建本地YUM仓库
================================================================================

YUM包管理工具，可以帮助您通过网络或本地安装或更新软件包。同时，它提供了简单的方法来安装依赖软件包。它的配置文件在/etc目录下，/etc/yum.conf配置文件中包含全局选项（例如缓存目录，日志目录等)。要添加新的YUM仓库或更新现有的YUM仓库，需要在/etc/repos.d目录下，新建或者打开既存的.repo文件。

### 创建仓库源: ###

在创建新的YUM仓库配置文件之前，你必须确定YUM仓库的位置（无论是本地或远程的）。YUM仓库可以使用createrepo软件包来创建。或者，你可以直接挂载(mount)安装DVD，这样你就不需要拷贝软件包到硬盘去创建仓库了。

挂载(mount) CD/DVD ROM 到你指定的目录，下面的例子是挂载到 /cdrom

    # mkdir /cdrom
    # mount /dev/cdrom /cdrom

配置文件:

在 /etc/repos.d目录下，创建新的 .repo文件。

    # vi /etc/yum.repos.d/local.repo

内容：

    [LocalRepo]
    name=Local Repository
    baseurl=file:///cdrom
    enabled=1
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

1. **[LocalRepo]** – 分段名
2. ***name*** = 仓库名
3. **baseurl** = 软件包的位置
4. **Enabled** = 是否有效
5. **gpgcheck**= 安装前安全检查
6. **gpgkey**= 安全检查gpgkey

### 说明: ###
1. gpgcheck 是可选项 (假如gpgcheck=0， gpgkey就不需要去管了)
2. /etc/yum.repos.d目录下可能有多个仓库配置文件，除了local.repo，请把其他的文件都删除掉。（译注：也可以移到别的备份目录，需要的时候再拿回来。）这可以保证系统不会从CentOS或Redhat的远程仓库找软件包。
### 安装: ###
在安装之前，需要清除软件仓库的缓存。 请执行下面的命令。

    # yum clean all

然后安装需要的软件包。这里我们从本地仓库安装vsftpd软件包。

    # yum install vsftpd

输出结果如下。 它会尝试缓存软件包的信息。当你选Yes的时候，会提示你去接受pgp签名


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

根据上面的步骤，你已经配置好了本地软件仓库。这个方法仅限于使用CD/DVD的单机环境。如果想设置网络仓库源，请参考手册。


--------------------------------------------------------------------------------

via: http://www.itzgeek.com/how-tos/linux/centos-how-tos/create-local-yum-repository-on-centos-7-rhel-7-using-dvd.html

作者：[Raj in][a]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创翻译，[Linux中国](http://linux.cn/) 荣誉推出

[a]:https://plus.google.com/+Itzgeek/
