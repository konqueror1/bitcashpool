# Running Mining Pool

# Requirements

* .Net (on Windows) or Mono (on Linux and macOS)
* MySQL 5.7+ (not MariaDB)
* Redis
* bitcashd (https://wallet.choosebitcash.com/linuxinstall.php)

# Build

Build release version of the pool using [Build Instruction](./build.md).

# Install and Configure bitcashd, Mysql, Redis

1. Install MySQL, create user and database for the pool.
1. Install Redis, set up password for it.
1. Install bitcashd from binaries or build it yourself.
1. Create and change configuration using next example in `$BITCASH_DATA_DIR/bitcash.conf` file.
```
rpcuser=YOURRPCUSER
rpcpassword=YOURRPCPASSWORD
rpcallowip=127.0.0.1
whitelist=127.0.0.1

listen=1
server=1
daemon=1
```
1. Start bitcashd or BitCash Wallet.
1. Get the wallet address for the pool (with the RPC command getcurrentaddress).

# Configure Pool

Update configuration file in `build/bin/Relese/config` directory copying it from `config-example.json` file to `config.json`.
`stack.name` and `website.port` are good candidates to be changed.

Create configuration file for the pool in `build/bin/Relese/config/pools/bitcash.json`:

```
{
  "enabled": true,
  "coin": "bitcash.json",
  "daemon": {
    "host": "127.0.0.1",
    "port": 5722,
    "username": "YOURRPCUSER",
    "password": "YOURRPCPASSWORD"
  },
  "meta": {
    "motd": "Welcome to BitCash Pool Server, enjoy your stay!",
    "txMessage": "https://YOURPOOLDOMAIN/"
  },
  "wallet": {
    "address": "YOURWALLETADDRESS"
  },
  "rewards": [{
  }],
  "banning": {
    "enabled": true,
    "duration": 600,
    "invalidPercent": 50,
    "checkThreshold": 100,
    "purgeInterval": 300
  },
  "payments": {
    "enabled": true,
    "interval": 60,
    "minimum": 0.01,
    "validateAddress": false
  },
  "miner": {
    "validateUsername": true,
    "timeout": 300
  },
  "job": {
    "blockRefreshInterval": 50,
    "rebroadcastTimeout": 40
  },
  "stratum": {
    "enabled": true,
    "bind": "0.0.0.0",
    "port": 3333,
    "diff": 1,
    "vardiff": {
      "enabled": true,
      "minDiff": 1,
      "maxDiff": 65536,
      "targetTime": 15,
      "retargetTime": 90,
      "variancePercent": 25
    }
  },
  "storage": {
    "hybrid": {
      "enabled": true,
      "redis": {
        "host": "YOURREDISHOST",
        "password": "YOURREDISPASSWORD",
        "port": 6379,
        "databaseId": 0
      },
      "mysql": {
        "host": "YOURMYSQLHOST",
        "port": 3306,
        "user": "YOURMYSQLUSER",
        "password": "YOURMYSQLPASSWORD",
        "database": "pool"
      }
    },
    "mpos": {
      "enabled": false,
      "mysql": {
        "host": "YOURMYSQLHOST",
        "port": 3306,
        "user": "YOURMYSQLUSER",
        "password": "YOURMYSQLPASSWORD",
        "database": "pool"
      }
    }
  },
  "vanilla": {
    "enabled": false,
    "bind": "localhost",
    "port": 2223
  }
}
```

## Start the Pool

If everything is running and configured properly, you can start the pool using next command:
```
# Windows
build/bin/Release/CoiniumServ.exe
# Linux and macOS
mono build/bin/Release/CoiniumServ.exe
```
