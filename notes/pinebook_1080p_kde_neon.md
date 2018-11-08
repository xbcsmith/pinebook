# KDE Neon

## Intro

Kernel is too old.

## Install eMMC

### Commands

    IMAGE_URL=http://mirror.cc.columbia.edu/pub/software/kde-applicationdata/neon/images/pinebook-remix-nonfree/useredition/20181028-1500/neon-pinebook-remix-useredition-20181028-1500-arm64-1080p.img.gz

    SHA256=8cffcdc0ff11f23dd79bdd4140838a2c5e50f14d75e9dfb035c5e1349bc71983

    ARCHIVER="gzip -d"

    EMMC="/dev/mmcblk1"


    if [[ "$(id -u)" -ne "0" ]]; then
        echo "This script requires root."
        exit 1
    fi

    if [[ ! -d /sys/devices/soc.0/1c10000.sdmmc/mmc_host/mmc1 ]]; then
        echo "You should boot from SD card"
        exit 1
    fi

    if [[ ! -e /dev/mmcblk1 ]]; then
        echo "You should boot from SD card"
        exit 1
    fi

        umount -f /dev/mmcblk1*

    curl -L -f "$IMAGE_URL" | $ARCHIVER | dd bs=30M of=/dev/mmcblk1

    sync

### Alternative

    curl -kO $IMAGE_URL

    sha256sum neon-pinebook-remix-useredition-20181028-1500-arm64-1080p.img.gz


    cat neon-pinebook-remix-useredition-20181028-1500-arm64-1080p.img.gz | gzip -d | dd bs=24M of=/dev/mmcblk1


