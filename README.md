# zfs-integration
Integration of ZFS into Virtualization Software
(CentOS 7-1708)

# TODO:

ZFS Installation

1. Install from source/repo
    * yum install epel-release
    * yum install http://download.zfsonlinux.org/epel/zfs-release.el7_4.noarch.rpm
    * gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-zfsonlinux
    * yum update
    * yum install kernel-devel zfs
    * lsmod | grep zfs
        * modprobe zfs
1. pool setup
    * zpool create <<POOL_NAME>> raidz DEV1 DEV2...
    
Integration of ZFS into libvirt

1. Spec Build
    * yum install yum-utils rpm-build
    * yumdownloader --source libvirt
    * rpm -ivh ./libvirt-<<VERSION_NUMBER>>.src.rpm
    * cp ~/rpmbuild/SPECS/libvirt.spec ~/rpmbuild/SPECS/libvirt.spec.orig
    * vi ~/rpmbuild/SPECS/libvirt.spec
        * Integrate ZFS into spec file
    * yum-buildep libvirt
    * rpmbuild -ba ~/rpmbuild/SPECS/libvirt.spec
1. Installation
    * yum install createrepo
    * createrepo ~/rpmbuild/RPMS/x86_64
    * vi /etc/yum.repos.d/libvirt.repo
        * Add local repo data
    * yum update
    * yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer bridge-utils
    * to use virt-manager through ssh on windows system:
        * on virtual server: yum install "@X Window System" xorg-x11-xauth xorg-x11-fonts-* xorg-x11-utils
        * on windows 10 debian console /etc/ssh/ssh_config
            * ForwardAgent yes
            * ForwardX11 yes
            * ForwardX11Trusted yes
            * Port 22
            * Protocol 2
            * GSSAPIAuthentication yes
            * XauthLocation /usr/bin/xauth
        * on windows 10 debian console ~/.bashrc
            *export DISPLAY=localhost:0
    * add zfs pool through virt-manager or virsh
    
    
Integration of ZFS into OpenNebula

1. Installed Opennebula Frontend and Node on single host with working ZFS
1. Configuration of ZFS datastore
   * Using Instructions from: https://github.com/OpenNebula/addon-zfs
   * Configured default ONE system datastore from ssh to shared
   * visudo -f /etc/sudoers.d/opennebula
      * added a line for zfs with the zfs and dd commands added for passwordless sudo by oneadmin
   * manually added the datastore through the GUI, the command line didn't seem to work   
