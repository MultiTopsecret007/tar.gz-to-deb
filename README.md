OpenMW
 How to build .deb package from tar.gz
By Pratik Shivarkar | Labels: Deb, Linux, Open Source, Packages, Ubuntu


Image via Wikipedia

Often newbies (not so new) complain after installing a package from source. It's actually easy to install a package from source, but you may face some troubles while un-installing those. especially when you delete compiled directory from where you execute make install command.


Method 1

The common method is to use dh_make and dpkg-buildpackage to create a .deb package and install it. This is how we do it.
Install required packages.

    sudo apt-get install dh-make fakeroot build-essential autotools-dev



Step 1.
Extract the contents of Tarball

    tar -xvzf source.tar.gz



Step 2.
Change directory to source folder

    cd /path/to/source/folder



Step 3.
Create control files, selecting the attributes of package.

    dh_make


Step 4.
Finally compile the package.

    sudo dpkg-buildpackage -rfakeroot


Step 5.
Install all the packages, created by

    dpkg-buildpackage



Method 2

Another method is to use

    checkinstall

, which is quite easier.Some packages may use different build tools, or you may want to build application with qmake, cmake or something else instead of make. Or just wanted to be able to remove package without troubles. Use

    checkinstall


Step 1. Install required packages.

    sudo apt-get install checkinstall


Step 2.
There are no harder steps. Build your package first, your build method may differ.

    ./configure && make


Step 3.
At the end, replace the

    sudo make install

command with following.

    sudo checkinstall -D make install


Check install will also allow you to create package with custom meta-data, It will also create a deb package which you can keep for later use.