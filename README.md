# glados_repo
Debian repo for the glados packages

Included packages:

- [glados](https://github.com/Lernstick/glados)
- [yii2-glados](https://github.com/chaoos/yii2-glados)


## Usage for Debian 10

```shell
# install curl, sudo, gpg
apt install curl sudo gnupg

# add the GPG key of the Repo
curl -s --compressed "https://chaoos.github.io/glados_ppa/debian/KEY.gpg" | sudo apt-key add -

# include the glados list into sources.list
sudo curl -s --compressed -o /etc/apt/sources.list.d/glados.list https://chaoos.github.io/glados_ppa/glados_debian10.list

# update the local package cache
sudo apt update

# first install rdiff-backup version >=2 from the backports, else glados installation will fail
sudo apt install -t buster-backports rdiff-backup

# install glados
sudo apt install glados
```

## Usage for Debian 11

```shell
# install curl, sudo, gpg
apt install curl sudo gnupg

# add the GPG key of the Repo
curl -s --compressed "https://chaoos.github.io/glados_ppa/debian/KEY.gpg" | sudo apt-key add -

# include the glados list into sources.list
sudo curl -s --compressed -o /etc/apt/sources.list.d/glados.list https://chaoos.github.io/glados_ppa/glados_debian11.list

# update the local package cache
sudo apt update

# install glados
sudo apt install glados
```

## Update the Repo

```shell
git clone https://github.com/chaoos/glados_ppa # clone the repo
export EMAIL="email@example.com" # set email
cd debian/ # change to debian dir
```

Add .deb packages into the debian directory

```shell
dpkg-scanpackages --multiversion . > Packages # create package list
gzip -k -f Packages # gzip the list
apt-ftparchive release . > Release # create release file
gpg --default-key "${EMAIL}" -abs -o - Release > Release.gpg # sign
gpg --default-key "${EMAIL}" --clearsign -o - Release > InRelease
```
    
Commit the changes to the master branch

```shell
git add -A
git commit -m "glados version <version>, ..."
git push -u origin master
```

