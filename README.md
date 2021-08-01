# real-time-kernel-Franka

-For details look: https://frankaemika.github.io/docs/installation_linux.html


Download from below links in a folder 
-----

curl -SLO https://www.kernel.org/pub/linux/kernel/v5.x/linux-5.4.129.tar.xz

curl -SLO https://www.kernel.org/pub/linux/kernel/v5.x/linux-5.4.129.tar.sign

curl -SLO https://www.kernel.org/pub/linux/kernel/projects/rt/5.4/patch-5.4.129-rt61.patch.xz

curl -SLO https://www.kernel.org/pub/linux/kernel/projects/rt/5.4/older/patch-5.4.129-rt61.patch.sign

xz -d linux-5.4.129.tar.xz
xz -d patch-5.4.129-rt61.patch.xz

verify the keys and get signiture if it is not verifyed
------

gpg2 --verify linux-5.4.129.tar.sign
gpg2 --verify patch-5.4.93-rt61.patch.sign

gpg2 --locate-keys torvalds@kernel.org gregkh@kernel.org zanussi@kernel.org

gpg2 --keyserver keyserver.ubuntu.com --search-keys ACF85F9816A8D5F096AE1FD20129F38552C38DF1

key ID: can be changed 


unzip
-----
tar xf linux-5.4.129.tar

cd linux-5.4.129

patch -p1 < ../patch-5.4.129-rt61.patch

make oldconfig

IMPORTANT: linux-5.4.129 dosyasinin icindeki ".config" (gizli dosya) ac asagidaki resim gibi degistir

![config_ayari](https://user-images.githubusercontent.com/74590114/127777691-7bb32ba6-a7c5-4c3f-940a-fed10784b35c.png)


Compile the kernel. As this is a lengthy process, set the multithreading option -j to the number of your CPU cores:
----
IMPORTANT: you have to use 'deb-pkg' othervise it will not work. (I tried with make and didn't worked) 

sudo make -j4 deb-pkg

sudo dpkg -i ../linux-headers-5.4.129-rt61_*.deb ../linux-image-5.4.129-rt61_*.deb

-Restart your system

sudo addgroup realtime

sudo usermod -a -G realtime $(whoami)

-Afterwards, add the following limits to the realtime group in /etc/security/limits.conf:

![kernel_k](https://user-images.githubusercontent.com/74590114/127777867-d5443f07-387d-48ae-baaf-ea20b4d9ac47.png)

vala!! finish







