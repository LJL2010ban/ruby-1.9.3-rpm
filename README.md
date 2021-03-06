# What is this spec?

This spec is an attempt to push for a stable replacement of Ruby 1.8.x with 1.9.3+ on RHEL based systems. I have based it off of the work of [FrameOS](http://www.frameos.org) specs for Ruby 1.9.3 and Ruby Enterprise Edition.

### How to install

#### RHEL/CentOS 5/6

    yum install -y rpm-build rpmdevtools readline-devel ncurses-devel gdbm-devel tcl-devel openssl-devel db4-devel byacc libyaml-devel libffi-devel make
    rpmdev-setuptree
    cd ~/rpmbuild/SOURCES
    RUBY_VER=ruby-1.9.3
    RUBY_SUBVER=p545
    wget http://ftp.ruby-lang.org/pub/ruby/1.9/${RUBY_VER}-${RUBY_SUBVER}.tar.gz
    cd ~/rpmbuild/SPECS
    wget https://raw.github.com/imeyer/${RUBY_VER}-rpm/master/ruby19.spec
    rpmbuild -bb ruby19.spec
    ARCH=`uname -m`
    KERNEL_REL=`uname -r`
    KERNEL_TMP=${KERNEL_REL%.$ARCH}
    DISTRIB=${KERNEL_TMP##*.}
    yum localinstall ~/rpmbuild/RPMS/${ARCH}/${RUBY_VER}${RUBY_SUBVER}-1.${DISTRIB}.${ARCH}.rpm

**PROFIT!**

If you are having trouble on the last line because of installed rubies, then run:

`yum remove ruby-* puppet facter`

If yum can't find libyaml, install the [epel repo](http://www.rackspace.com/knowledge_center/article/installing-rhel-epel-repo-on-centos-5x-or-6x).

### What it does

+ Builds
+ Installs
+ Overwrites/upgrades your currently installed ruby package (**DANGEROUS**)

### What it does **not** do

+ Split packages into ruby-libs, ruby-devel, etc (looking for help here)
+ Install alongside Ruby 1.8.x

###

+ If you upgrade from an already installed 1.8.x, you will need to re-install all of your gems. If anyone has a decent way to do this programatically, i'll add it to the doc.

### Requirements

+ EPEL Yum repository (for rpmdev-setuptree)

### Distro support

Tested working (as sane as I could test for) on:

* CentOS 5.x x86_64
* CentOS 6.3 (Final)

### Personal thoughts

This is by no means, correct, or sane. Nor does it follow any sort of policy for packaging. I leave that to the people who are most familiar with such things, and will willingly accept patches that add those features.
