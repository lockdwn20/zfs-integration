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
1. initial setup
1. pool setup
  
Integration of ZFS into libvirt

1. Spec Build
    1. Dependencies
1. Installation
  
Integration of ZFS into OpenNebula

1. Configuration of ZFS datastore
