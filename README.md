# glados_ppa
Debian repo for the glados packages

## Include the repo into apt

    curl -s --compressed "https://chaoos.github.io/glados_ppa/debian/KEY.gpg" | sudo apt-key add -
    sudo curl -s --compressed -o /etc/apt/sources.list.d/glados.list https://chaoos.github.io/glados_ppa/glados.list
    sudo apt update
    sudo apt install glados

## Update the Repo

    git clone https://github.com/chaoos/glados_ppa # clone the repo
    export EMAIL="email@example.com" # set email
    cd debian/ # change to debian dir
    dpkg-scanpackages --multiversion . > Packages # create package list
    gzip -k -f Packages # gzip the list
    apt-ftparchive release . > Release # create release file
    gpg --default-key "${EMAIL}" -abs -o - Release > Release.gpg # sign
    gpg --default-key "${EMAIL}" --clearsign -o - Release > InRelease
    


