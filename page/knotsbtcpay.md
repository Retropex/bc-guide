How to migrate from Core to Knots on BTCPayServer. (Docker)
=============

1. SSH to your BTCPayServer.
2. Login as root `sudo su -`.
3. Shutdown your BTCPayServer with `btcpay-down.sh`.
4. Edit the file `/etc/profile.d/btcpay-env.sh` with your editior.
5. You should see something like that:

```bash
#!/bin/bash
export COMPOSE_HTTP_TIMEOUT="180"
export BTCPAYGEN_OLD_PREGEN="false"
export BTCPAYGEN_CRYPTO1="btc"
export BTCPAYGEN_CRYPTO2=""
export BTCPAYGEN_CRYPTO3=""
export BTCPAYGEN_CRYPTO4=""
export BTCPAYGEN_CRYPTO5=""
export BTCPAYGEN_CRYPTO6=""
export BTCPAYGEN_CRYPTO7=""
export BTCPAYGEN_CRYPTO8=""
export BTCPAYGEN_CRYPTO9=""
export BTCPAYGEN_LIGHTNING="clightning"
export BTCPAYGEN_REVERSEPROXY="nginx"
export BTCPAYGEN_ADDITIONAL_FRAGMENTS=""
export BTCPAYGEN_EXCLUDE_FRAGMENTS=""
export BTCPAY_DOCKER_COMPOSE="/root/btcpayserver-docker/Generated/docker-compose.generated.yml"
export BTCPAY_BASE_DIRECTORY="/root"
export BTCPAY_ENV_FILE="/root/.env"
export BTCPAY_HOST_SSHKEYFILE=""
export BTCPAY_ENABLE_SSH=true
export PIHOLE_SERVERIP=""
if cat "$BTCPAY_ENV_FILE" &> /dev/null; then
  while IFS= read -r line; do
    ! [[ "$line" == "#"* ]] && [[ "$line" == *"="* ]] && export "$line"
  done < "$BTCPAY_ENV_FILE"
fi
```

6. Just add the two following line at the end of your file:

```bash
export BTCPAYGEN_EXCLUDE_FRAGMENTS="$BTCPAYGEN_EXCLUDE_FRAGMENTS;bitcoin"
export BTCPAYGEN_ADDITIONAL_FRAGMENTS="$BTCPAYGEN_ADDITIONAL_FRAGMENTS;bitcoinknots"
```

7. Source the env variable and run again the setup script.

```bash
source /etc/profile.d/btcpay-env.sh
cd $BTCPAY_BASE_DIRECTORY/btcpayserver-docker
. btcpay-setup.sh -i
```

8. You can verify that Knots is running with `bitcoin-cli.sh --version`, you should see this:

```
Bitcoin Knots RPC client version v28.1.knots20250305
Copyright (C) 2009-2025 The Bitcoin Knots developers
Copyright (C) 2009-2025 The Bitcoin Core developers
```

Done! You are running Knots.
