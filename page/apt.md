This steps work on Debian 12.

1. Get Léo Haf's key and add it to the apt key list:

```
wget --quiet -O - https://apt.orangepill.ovh/gpg-pubkey.asc | sudo tee /etc/apt/keyrings/leohaf.asc
```

2. Add the repository to your apt repository list and indicate the GPG key to use:

```
echo "deb [signed-by=/etc/apt/keyrings/leohaf.asc arch=$(dpkg --print-architecture)] https://apt.orangepill.ovh bookworm main" | sudo tee /etc/apt/sources.list.d/bitcoin-knots.list
```

3. Update apt and install Bitcoin Knots:

```
sudo apt update && sudo apt install bitcoin-knots
```