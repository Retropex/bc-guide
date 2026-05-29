This steps work on Debian stable.

1. Activate the stable-backport repo:

```
cat << EOF | sudo tee /etc/apt/sources.list.d/debian-backports.sources
Types: deb deb-src
URIs: http://deb.debian.org/debian
Suites: trixie-backports
Components: main
Enabled: yes
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg
EOF
```

2. Update apt and install Bitcoin Knots and DATUM Gateway:

```
sudo apt update && sudo apt install bitcoin-knots/trixie-backports datum-gateway/trixie-backports
```

### Pleb configuration script

```
sudo dpkg-reconfigure -pmedium bitcoin-knots datum-gateway
```

### Advanced configuration script

```
sudo dpkg-reconfigure -plow bitcoin-knots datum-gateway
```