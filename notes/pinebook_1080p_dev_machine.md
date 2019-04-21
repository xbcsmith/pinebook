# Pinebook Dev Machine

## Introduction

Using something debian based like bionic


## Configuration

### Sudo

    sudo usermod -aG sudo $USER

### Change default Editor

    sudo update-alternatives --config editor

## Install go and rust

### golang 1-12

    sudo add-apt-repository ppa:longsleep/golang-backports
    sudo apt-get update
    sudo apt-get install golang-go

    mkdir -p ~/go/{src,bin}

### rust

    sudo apt-get install rustc cargo dh-cargo

## Install Docker

    sudo apt-get remove docker docker-engine docker.io
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo apt-key fingerprint 0EBFCD88
    sudo add-apt-repository "deb [arch=arm64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) edge"
    sudo apt-get install docker-ce
    # Expose port to world... seems safe
    mkdir /etc/docker
    cat > /etc/docker/daemon.json << EOF
    {
    "debug": true,
    "hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"]
    }


    EOF

    sed -i 's~dockerd -H fd://~dockerd~g' /lib/systemd/system/docker.service
    sudo sed -i 's~StartLimitInterval=60s~StartLimitInterval=60s\nIPForward=yes\n~g' /lib/systemd/system/docker.service


    # adduser $USER
    sudo groupadd docker
    sudo usermod -aG docker $USER

    # sudo systemctl daemon-reload
    sudo systemctl enable docker
    sudo systemctl start docker
    docker run --rm -it aarch64/hello-world

## Devel Pkgs

    sudo apt-get -y update && sudo apt-get -y install build-essential devscripts fakeroot debhelper dpkg-dev automake autotools-dev autoconf libtool perl libperl-dev systemtap-sdt-dev libssl-dev clang make cmake m4 bison flex docbook-dsssl docbook-xml docbook-xsl docbook opensp xsltproc gettext unzip wget libguestfs-tools  openjdk-8-jre-headless openjdk-8-jdk-headless pkg-config zip


    sudo apt-get -y install python-autopep8 python3-flake8 flake8 python-flake8 isort python-isort python3-isort vim-autopep8 python-wheel python3-wheel python-pip python3-pip tox python-dev python3-dev python-logilab-common python-unittest2 python-mock python3-virtualenv virtualenvwrapper tox

## All the pythons

    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt-get update
    sudo apt-get install python3.6 python3.6-venv python3.7 python3.7-venv


