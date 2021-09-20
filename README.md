# glados_ppa
Debian repo for the glados packages

Included packages:

- [glados](https://github.com/Lernstick/glados)
- [yii2-glados](https://github.com/chaoos/yii2-glados)
- [rdiff-backup](https://packages.debian.org/bullseye/rdiff-backup) version >=2

## Usage

    # install curl and sudo
    apt install curl sudo
    # add the GPG key of the Repo
    curl -s --compressed "https://chaoos.github.io/glados_ppa/debian/KEY.gpg" | sudo apt-key add -
    # include the glados list into sources.list
    sudo curl -s --compressed -o /etc/apt/sources.list.d/glados.list https://chaoos.github.io/glados_ppa/glados.list
    # update the local package cache
    sudo apt update
    # install glados
    sudo apt install glados

## Update the Repo

    git clone https://github.com/chaoos/glados_ppa # clone the repo
    export EMAIL="email@example.com" # set email
    cd debian/ # change to debian dir

Add .deb packages into the debian directory

    dpkg-scanpackages --multiversion . > Packages # create package list
    gzip -k -f Packages # gzip the list
    apt-ftparchive release . > Release # create release file
    gpg --default-key "${EMAIL}" -abs -o - Release > Release.gpg # sign
    gpg --default-key "${EMAIL}" --clearsign -o - Release > InRelease
    


