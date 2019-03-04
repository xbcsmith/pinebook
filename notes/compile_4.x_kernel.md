# Compile 4.x Kernel

## Build Tools

	sudo apt-get -y install bc curl gcc git libssl-dev libncurses5-dev lzop make u-boot-tools

### GCC 5

	apt-get -y install python-software-properties;
	add-apt-repository -y ppa:ubuntu-toolchain-r/test;
	apt-get update
	apt-get -y install gcc-5 g++-5
	update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 50
	update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 50

## Info

### default configuration

PINE64:	sun50iw1p1smp_linux_defconfig

## Compile

	git clone --depth 1 --single-branch -b a64-v6-wip https://github.com/apritzel/linux
	cd linux
	make defconfig
	make -j 4 Image modules dtbs
	sudo cp arch/arm64/boot/dts/*.dtb arch/arm64/boot/Image /boot/pine64
	sudo make modules_install
	sudo make firmware_install
	sudo make headers_install INSTALL_HDR_PATH=/usr
	kver=`make kernelrelease`
	sudo cp .config /boot/config-${kver}
	cd /boot
	sudo update-initramfs -c -k ${kver}
	sudo mv initrd.img-${kver} initrd.img
	sudo mv config-${kver} /boot/pine64

