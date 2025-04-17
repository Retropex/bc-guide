How to manually edit the conf file of DATUM on [Umbrel](https://umbrel.com).
===

1. Login to your umbrel server.
2. Click on the settigs icon.
3. Go to advanced settings -> terminal -> umbrelOS.
4. Open the config file:

```bash
sudo nano umbrel/app-data/datum/data/settings/datum_gateway_config.json
```
5. Make your changes.
6. Go back to the main view
7. Right click on DATUM and click on restart.
8. Done!


For instance, here is options the DATUM support:

```
{
    "bitcoind": {
        "rpccookiefile": ................. Path to file to read RPC cookie from, for communication with local bitcoind. (string, default: "")
        "rpcuser": ....................... RPC username for communication with local bitcoind. (string, default: "")
        "rpcpassword": ................... RPC password for communication with local bitcoind. (string, default: "")
        "rpcurl": ........................ RPC URL for communication with local bitcoind. (GBT Template Source) (string, REQUIRED)
        "work_update_seconds": ........... How many seconds between normal work updates?  (5-120, 40 suggested) (integer, default: 40)
        "notify_fallback": ............... Fall back to less efficient methods for new block notifications. Can disable if you use blocknotify. (boolean, default: true)
    },
    "stratum": {
        "listen_addr": ................... IP address to listen for Stratum Gateway connections (string, default: "")
        "listen_port": ................... Listening port for Stratum Gateway (integer, default: 23334)
        "max_clients_per_thread": ........ Maximum clients per Stratum server thread (integer, default: 128)
        "max_threads": ................... Maximum Stratum server threads (integer, default: 8)
        "max_clients": ................... Maximum total Stratum clients before rejecting connections (integer, default: 1024)
        "vardiff_min": ................... Work difficulty floor (integer, default: 16384)
        "vardiff_target_shares_min": ..... Adjust work difficulty to target this many shares per minute (integer, default: 8)
        "vardiff_quickdiff_count": ....... How many shares before considering a quick diff update (integer, default: 8)
        "vardiff_quickdiff_delta": ....... How many times faster than our target does the miner have to be before we enforce a quick diff bump (integer, default: 8)
        "share_stale_seconds": ........... How many seconds after a job is generated before a share submission is considered stale? (integer, default: 120)
        "fingerprint_miners": ............ Attempt to fingerprint miners for better use of coinbase space (boolean, default: true)
        "idle_timeout_no_subscribe": ..... Seconds we allow a connection to be idle without seeing a work subscription? (0 disables) (integer, default: 15)
        "idle_timeout_no_shares": ........ Seconds we allow a subscribed connection to be idle without seeing at least one accepted share? (0 disables) (integer, default: 7200)
        "idle_timeout_max_last_work": .... Seconds we allow a subscribed connection to be idle since its last accepted share? (0 disables) (integer, default: 0)
    },
    "mining": {
        "pool_address": .................. Bitcoin address used for mining rewards. (string, REQUIRED)
        "coinbase_tag_primary": .......... Text to have in the primary coinbase tag when not using pool (overridden by DATUM Pool) (string, default: "DATUM Gateway")
        "coinbase_tag_secondary": ........ Text to have in the secondary coinbase tag (Short name/identifier) (string, default: "DATUM User")
        "coinbase_unique_id": ............ A unique ID between 1 and 65535. This is appended to the coinbase. Make unique per instance of datum with the same coinbase tags. (integer, default: 4242)
        "save_submitblocks_dir": ......... Directory to save all submitted blocks to as submitblock JSON files (string, default: "")
    },
    "api": {
        "admin_password": ................ API password for actions/changes (username 'admin'; disabled if blank) (string, default: "")
        "listen_addr": ................... IP address to listen for API/dashboard requests (string, default: "")
        "listen_port": ................... Port to listen for API/dashboard requests (0=disabled) (integer, default: 0)
        "modify_conf": ................... Enable modifying the config file from API/dashboard (boolean, default: false)
    },
    "extra_block_submissions": {
        "urls": .......................... Array of bitcoind RPC URLs to submit our blocks to directly.  Include auth info: http://user:pass@IP (string_array)
    },
    "logger": {
        "log_to_console": ................ Enable logging of messages to the console (boolean, default: true)
        "log_to_stderr": ................. Log console messages to stderr *instead* of stdout (boolean, default: false)
        "log_to_file": ................... Enable logging of messages to a file (boolean, default: false)
        "log_file": ...................... Path to file to write log messages, when enabled (string, default: "")
        "log_rotate_daily": .............. Rotate the message log file at midnight (boolean, default: true)
        "log_calling_function": .......... Log the name of the calling function when logging (boolean, default: true)
        "log_level_console": ............. Minimum log level for console messages (0=All, 1=Debug, 2=Info, 3=Warn, 4=Error, 5=Fatal) (integer, default: 2)
        "log_level_file": ................ Minimum log level for log file messages (0=All, 1=Debug, 2=Info, 3=Warn, 4=Error, 5=Fatal) (integer, default: 1)
    },
    "datum": {
        "pool_host": ..................... Remote DATUM server host/ip to use for decentralized pooled mining (set to "" to disable pooled mining) (string, default: "datum-beta1.mine.ocean.xyz")
        "pool_port": ..................... Remote DATUM server port (integer, default: 28915)
        "pool_pubkey": ................... Public key of the DATUM server for initiating encrypted connection. Get from secure location, or set to empty to auto-fetch. (string, default: "f21f2f0ef0aa1970468f22bad9bb7f4535146f8e4a8f646bebc93da3d89b1406f40d032f09a417d94dc068055df654937922d2c89522e3e8f6f0e649de473003")
        "pool_pass_workers": ............. Pass stratum miner usernames as sub-worker names to the pool (pool_username.miner's username) (boolean, default: true)
        "pool_pass_full_users": .......... Pass stratum miner usernames as raw usernames to the pool (use if putting multiple payout addresses on miners behind this gateway) (boolean, default: true)
        "always_pay_self": ............... Always include my datum.pool_username payout in my blocks if possible (boolean, default: true)
        "pooled_mining_only": ............ If the DATUM pool server becomes unavailable, terminate miner connections (otherwise, 100% of any blocks you find pay mining.pool_address) (boolean, default: true)
        "protocol_global_timeout": ....... If no valid messages are received from the DATUM server in this many seconds, give up and try to reconnect (integer, default: 60)
    }
}
```

[!NOTE]

If you break DATUM with a wrong config file you just have to uninstall and reinstall DATUM to fix it.