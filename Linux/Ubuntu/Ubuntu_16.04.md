# Ubuntu 16.04

### Installing Dependencies

We will need git to sync the source code and cmake to set up the build 
environment. Open a terminal window and use the code below to install those 
using these commands.

```
sudo apt-get install git cmake
```

### Update the qtkeychain Libraries

The qtkeychain-dev and qt5keychain-dev libraries need to be at least 
version 0.7.0. On Ubuntu 16.04 these librarys will need updated. We’ll use 
a PPA with the updated libraries. Thanks Filip Dorosz for making these 
libraries available! In your terminal window, we will install the PPA using 
the code below:

```
sudo add-apt-repository ppa:fihufil/test-02
sudo apt-get update
```

Install the updated libraries

```
sudo apt-get install qtkeychain-dev qt5keychain-dev
```

### Install NextCloud Client Dependencies

NextCloud is a fork of OwnCloud and the Desktop client we are compiling actually 
pulls in source code from OwnCloud.

We will need to add the OwnCloud code repository using these commands:

```
sudo sh -c "echo 'deb-src http://download.opensuse.org/repositories/isv:/ownCloud:/desktop/Ubuntu_16.04/ /' >> /etc/apt/sources.list.d/owncloud-client.list"
sudo apt-get update
sudo apt-get build-dep owncloud-client
```

### Download the NextCloud Source Code From Github

The code is located at: https://github.com/nextcloud/client_theming

```
git clone https://github.com/nextcloud/client_theming.git
cd client_theming
git submodule update --init --recursive
```

### Compile and Install

In a terminal window, enter the following code:

```
mkdir build-linux
cd build-linux
cmake -D OEM_THEME_DIR=`pwd`/../nextcloudtheme ../client
make
sudo make install
```

Update the system PATH to include our newly compiled libraries. The NextCloud 
client will be installed to /usr/local/bin/ which is all well and good, but the 
libraries are actually installed to /usr/local/lib/x86_64-linux-gnu
On ubuntu this location is not in the path by default. We need to add it.

```
sudo nano /etc/ld.so.conf.d/x86_64-linux-gnu.conf
```

Add this line at the end:
/usr/local/lib/x86_64-linux-gnu
Apply that change by running:

```
sudo ldconfig
```


### Credits

- http://www.thenerdgarden.com/how-to-compile-nextcloud-client-for-linux/
- https://launchpad.net/~fihufil/+archive/ubuntu/test-02
