How to test Bitcoin Knots on debian sid
=============

1. Install debian stable
2. Once installed [switch](https://wiki.debian.org/DebianUnstable/#Installation) the APT repo to sid

```
sudo nano /etc/apt/sources.list.d/debian.sources
```

Your file should look like this after editing it

```
Types: deb deb-src
URIs: mirror+file:///etc/apt/mirrors/debian.list
Suites: unstable
Components: main
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg
```

```
sudo apt update && sudo apt full-upgrade -y
```

3. Once the update is done git clone bitcoin-knots package

```
git clone https://salsa.debian.org/cryptocoin-team/bitcoin-knots.git
```

4. Install the build suit of Knots and gbp

```
sudo apt install -y git-buildpackage cmake pkgconf libevent-dev libboost-dev libsqlite3-dev libminiupnpc-dev systemtap-sdt-dev libzmq3-dev qtbase5-dev qttools5-dev qttools5-dev-tools librsvg2-bin imagemagick libqrencode-dev
```

5. Build the package

```
cd bitcoin-knots
git switch pristine-tar 
git switch debian/latest 
gbp buildpackage 
```

6. Once builded, install it

```
sudo dpkg -i ../bitcoin-knots_29.3.knots20260210-2_amd64.deb
```

By default no configuration prompt is showed. That's expected.

If you want to go through the interactive process please run dpkg-reconfigure:

dpkg-reconfigure is defaulting to low priority.

hardcoded:

datadir=/var/lib/bitcoin // this is to fit in the debian policy
server=1

`dpkg-reconfigure -pmedium bitcoin-knots` (medium priority) is intended for pleb users:

dbcache
prune
txindex

`dpkg-reconfigure -plow bitcoin-knots` (low priority) is intended for industrial users:

pruneduringinit
// others options TBD