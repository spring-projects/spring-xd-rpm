# spring-xd-packaging
Packaging and release code and artifacts for Spring XD

### Building the Spring XD Release RPM:

Prepare by copying `spring-xd-1.2.0.{version}-dist.zip` to `rpmbuild/SOURCES/`

Build using:

    $ rpmbuild -bb rpmbuild/SPECS/spring-xd-noarch.spec


### Building Spring XD RPM with Vagrant

You need to install [Vagrant](http://docs.vagrantup.com/v2/installation/) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads). Then add the `chef/centos-6.5` box for VirtualBox.

We are providing a Vagrant file for easy building of the RPM. Follow these steps from the root directory of this project:

    vagrant up

That should start the VM and you can now ssh to it using:

    vagrant ssh

The first time the VM is started we should install `rpm-build`

    $ sudo yum -y install rpm-build

Now copy the Spring XD release distribution zip file (set XD_VERSION to the correct version):

    $ export XD_VERSION='1.2.0.RC1'
    $ export XD_REPO='http://repo.spring.io/libs-milestone-local'
    $ wget -P rpmbuild/SOURCES  ${XD_REPO}/org/springframework/xd/spring-xd/${XD_VERSION}/spring-xd-${XD_VERSION}-dist.zip

Finally build the RPM:

    $ rpmbuild -bb rpmbuild/SPECS/spring-xd-noarch.spec

The Spring XD RPM should now be available in `rpmbuild/RPMS/noarch`
