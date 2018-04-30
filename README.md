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
    * rpm -ivh ./libvirt-<<VERSION>.src.rpm
    * cp ~/rpmbuild/SPECS/libvirt.spec ~/rpmbuild/SPECS/libvirt.spec.orig
    * vi ~/rpmbuild/SPECS/libvirt.spec
        * Integrate ZFS into spec file
    * yum-buildep libvirt
    * rpmbuild -ba ~/rpmbuild/SPECS/libvirt.spec
    
1. Installation
  
Integration of ZFS into OpenNebula

1. Configuration of ZFS datastore
