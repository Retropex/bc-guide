### Steps to install Bitcoin Knots and DATUM Gateway on Devuan stable

Note: these steps are only for Devuan stable (excalibur).

1. Activate the stable-backport repo:

```
cat << EOF | sudo tee -a /etc/apt/sources.list
deb     http://deb.devuan.org/merged excalibur-backports main
deb-src http://deb.devuan.org/merged excalibur-backports main
EOF
```

2. Update apt and install Bitcoin Knots and DATUM Gateway

```
sudo apt update && sudo apt install bitcoin-knots/excalibur-backports datum-gateway/excalibur-backports
```

### Optionnal configuration scripts:

You can choose between two configuration mode:

3. Pleb configuration script:

```
sudo dpkg-reconfigure -pmedium bitcoin-knots datum-gateway
```

3. Advanced configuration script:

```
sudo dpkg-reconfigure -plow bitcoin-knots datum-gateway
```