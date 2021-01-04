# vapor-proxy

Vapory mining proxy with web-interface.

**Proxy feature list:**

* Rigs availability monitoring
* Keep track of accepts, rejects, blocks stats
* Easy detection of sick rigs
* Daemon failover list

![Demo](https://raw.githubusercontent.com/sammy007/vapor-proxy/master/proxy.png)

### Building on Linux

Dependencies:

  * go >= 1.4
  * gvap

Export GOPATH:

    export GOPATH=$HOME/go

Install required packages:

    go get github.com/vaporyco/vapash
    go get github.com/vaporyco/go-vapory/common
    go get github.com/goji/httpauth
    go get github.com/gorilla/mux
    go get github.com/yvasiyarov/gorelic

Compile:

    go build -o vapor-proxy main.go

### Building on Windows

Follow [this wiki paragraph](https://github.com/vaporyco/go-vapory/wiki/Installation-instructions-for-Windows#building-from-source) in order to prepare your environment.
Install required packages (look at Linux install guide above). Then compile:

    go build -o vapor-proxy.exe main.go

### Building on Mac OS X

If you didn't install [Brew](http://brew.sh/), do it. Then install Golang:

    brew install go

And follow Linux installation instructions because they are the same for OS X.

### Configuration

Configuration is self-describing, just copy *config.example.json* to *config.json* and specify endpoint URL and upstream URLs.

#### Example upstream section

```javascript
"upstream": [
  {
    "pool": true,
    "name": "EuroHash.net",
    "url": "http://vap-eu.eurohash.net:8888/miner/0xb85150eb365e7df0941f0cf08235f987ba91506a/proxy",
    "timeout": "10s"
  },
  {
    "name": "backup-gvap",
    "url": "http://127.0.0.1:8545",
    "timeout": "10s"
  }
],
```

In this example we specified [EuroHash.net](https://eurohash.net) mining pool as main mining target and a local gvap node as backup for solo.

With <code>"submitHashrate": true|false</code> proxy will forward <code>vap_submitHashrate</code> requests to upstream.

#### Running

    ./vapor-proxy config.json

#### Mining

    vapminer -F http://x.x.x.x:8546/miner/5/gpu-rig -G
    vapminer -F http://x.x.x.x:8546/miner/0.1/cpu-rig -C

### Pools that work with this proxy

* [EuroHash.net](https://eurohash.net) EU Vapory mining pool
* [SuprNova.cc](https://eth.suprnova.cc) SuprNova ETH Pool

Pool owners, apply for listing here. PM me for implementation details.

### TODO

**Currently it's solo-only solution.**

* Report block numbers
* Report luck per rig
* Maybe add more stats
* Maybe add charts

### Donations

* **ETH**: [0x5e7d4ab47b6f44d7ba5dc8777bd2fb6c9a1671b9](https://etherchain.org/account/0x5e7d4ab47b6f44d7ba5dc8777bd2fb6c9a1671b9)

* **BTC**: [1BEm4XLZTnSah5ZDmmfeeHjoa6TBriYNVk](https://blockchain.info/address/1BEm4XLZTnSah5ZDmmfeeHjoa6TBriYNVk)

Thanks to a couple of dudes who donated some Vapor to me, I believe, you can do the same.

### License

The MIT License (MIT).
