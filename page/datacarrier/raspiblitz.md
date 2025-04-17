How to disable datacarrier on [Raspiblitz](https://docs.raspiblitz.org).
===

1. SSH to your your Raspiblitz device:

Usually the user is `admin` and the default password is `raspiblitz`

```bash
ssh admin@[YOURIP]
```

2. Use the key combo `Ctrl + c` to escape the UI.
3. Enter this command to disable datacarrier:

```bash
sudo bash -c 'echo "datacarrier=0" >> /mnt/hdd/bitcoin/bitcoin.conf'
```

4. Restart `bitcoind`:

```bash
sudo systemctl restart bitcoind.service
```

Done!