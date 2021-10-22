## Install OpenCV 4.2.0 with GAPI support on Ubuntu
``` bash
# Install debian packaging tools
$ sudo apt install devscripts equivs

# Create working dir
$ mkdir opencv420_w_gapi && cd opencv420_w_gapi

# Clone debian official build env
$ git clone --depth=1 -b debian/4.2.0+dfsg-5 https://salsa.debian.org/science-team/opencv.git
$ cd opencv

# Install dependencies
# This step may require installing libvtk6-dev which breaks some ros2 dependencies. Just install it for a moment then continue steps.
# I don't confirm but you may reinstall removed packages later
$ sudo mk-build-deps -i

# Apply patch to enable gapi which involves 3rd software
$ patch -p1 < /path/to/opencv420_w_gapi.patch

# Build - costs around 16GB of disk?
$ dpkg-buildpackage -b -rfakeroot -us -uc

# Install; Overriding dependency may be required: --force-depends-version
$ sudo dpkg -i ../*.deb
```
Repeat these steps for each OpenCV release in Ubuntu. might be a pain though

