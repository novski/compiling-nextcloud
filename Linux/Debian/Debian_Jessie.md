# compiling Nextcloud client for Debian Jessie
#### This Tutorial is based on www.c-rieger.de/how-to-install-nextcloud-deskt and tested with Debian Jessie and corrected or extended in some parts

`$` is a usercomand

`#` is a root comand

## 1. Prerequesites:
`$ sudo -s`

`# apt install build-essential git cmake openssl libssl-dev sqlite3 libsqlite3-dev qt5-default libqt5webkit5-dev qttools5-dev qttools5-dev-tools python-sphinx texlive-latex-base inotify-tools qt5keychain-dev`

### 2. Change to your working-directory:

`# cd /usr/local/src`

### 3. and start the Nextcloud procedure:

`# git clone https://github.com/nextcloud/client_theming.git`

`# cd client_theming`

`# git submodule update --init`

`# cd client`

`# git submodule update --init`

`# cd ..`

`# mkdir build-linux`

`# cd build-linux`

`# cmake -D OEM_THEME_DIR=`pwd`/../nextcloudtheme ../client`

### 4. Now we change the lower ‘n’ to an upper ‘N’, otherwise no icon would appear in Ubuntu’s dashboard:

`# sed -i 's/Icon=nextcloud/Icon=Nextcloud/g' src/gui/nextcloud.desktop`

`# sed -i 's/Icon\[\(.*\)\]=nextcloud/Icon\[\1\]=Nextcloud/g' src/gui/nextcloud.desktop`

`# make && make install`

### 5. Edit your environment (/etc/environment) and add the following row at the end of this file:

`# nano /etc/environment`

`# LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib/x86_64-linux-gnu`

### 6. Add this line:

`# nano /etc/ld.so.conf.d/x86_64-linux-gnu.conf`

`# /usr/local/lib/x86_64-linux-gnu`

### 7. And at least execute:

`# ldconfig




## fast version:


```sudo -s && apt install build-essential git cmake openssl libssl-dev sqlite3 libsqlite3-dev qt5-default libqt5webkit5-dev qttools5-dev qttools5-dev-tools python-sphinx texlive-latex-base inotify-tools qt5keychain-dev && cd /usr/local/src && git clone https://github.com/nextcloud/client_theming.git && cd client_theming && git submodule update --init && cd client && git submodule update --init && cd .. && mkdir build-linux && cd build-linux && cmake -D OEM_THEME_DIR=`pwd`/../nextcloudtheme ../client && sed -i 's/Icon=nextcloud/Icon=Nextcloud/g' src/gui/nextcloud.desktop && sed -i 's/Icon\[\(.*\)\]=nextcloud/Icon\[\1\]=Nextcloud/g' src/gui/nextcloud.desktop && make && make install && nano /etc/environment```

and follow step 5 above...

***

# Credits:

https://www.c-rieger.de/how-to-install-nextcloud-desktop-client-for-ubuntu/

http://blog.tordeu.com/?p=374






