How to test DATUM Gateway on debian sid
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

3. Once the update is done git clone datum-gateway package

```
git clone https://salsa.debian.org/cryptocoin-team/datum-gateway
```

4. Install the build suit of Knots and gbp

```
sudo apt install -y git-buildpackage
```

5. Build the package

```
cd datum-gateway
git switch pristine-tar 
git switch debian/latest 
gbp buildpackage 
```

It may ask you to install more dependency like with the step 4.

6. Once builded, install it

```
sudo dpkg -i ../datum-gateway_0.4.1~beta-3_amd64.deb
```

By default on install dpkg will ask you for all configuration with critical or high priority.

If you want to go through the interactive process please run dpkg-reconfigure:

dpkg-reconfigure is defaulting to low priority.

`dpkg-reconfigure -pcritical datum-gateway` (critical priority):

bitcoin-address

`dpkg-reconfigure -phigh datum-gateway` (high priority) is the default priority on install:

critical +
log to file (usefull for sysVinit systems)
blocknotify

`dpkg-reconfigure -pmedium datum-gateway` (medium priority) is mostly intended for pleb users:

high +
tag secondary

`dpkg-reconfigure -plow datum-gateway` (low priority) is mostly intended for industrial users:

medium+
work_update_seconds
listen_port
max_clients_per_thread
max_threads
max_clients
vardiff_min
coinbase_tag_primary
listen_port-api
modify_conf
log_level_file
pool_pass_workers
pool_pass_full_users
pooled_mining_only