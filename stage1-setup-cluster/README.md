# Creating a simnet cluster
We will learn how to create a self contained bitcoin/lightning cluster for development.
This cluster doesn't require an internet connectivity and contains all the elements to run and communicate between nodes over a private lightning network.
## Setting up the environment
* mkdir workshop
* cd workshop
* export GOPATH=workshop/gopath
* export PATH=$GOPATH/bin:$PATH
## Installing btcd
From "workshop" dir:
* git clone https://github.com/btcsuite/btcd.git btcd
* cd btcd
* go build -v .
* go build -v ./btcctl
* Add  btcd directory to the system path
## Installing lnd
From "workshop" dir:
* git clone https://github.com/lightningnetwork/lnd.git lnd
* go build -v ./cmd/lnd
* go build -v ./cmd/lncli
* Add  lnd directory to the system path
## Running the cluster nodes
### btcd
* btcd --txindex --simnet --rpcuser=user --rpcpass=password
### Running Alice
* cd alice-lnd-node
#### running the node
* lnd -C ./lnd.conf --lnddir .
#### creating and unlocking the wallet
* lncli --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon create
#### checking the node is running
* lncli --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon getinfo
* optional setting alias:
    * alias lncli-alice="lncli --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon"
### Running Bob
* cd bob-lnd-node
#### running the node
* lnd -C ./lnd.conf --lnddir .
#### creating and unlocking the wallet
* lncli --rpcserver=localhost:10002 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon create
#### checking the node is running
* lncli --rpcserver=localhost:10002 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon getinfo
* optional setting alias:
    * alias lncli-bob="lncli --rpcserver=localhost:10002 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon"

## Working with underline btc wallet
Create new bitcoin address:
* lncli-alice newaddress np2wkh

Running btcd with mining address:
* btcd --simnet --txindex --rpcuser=user --rpcpass=password --miningaddr=<ALICE_ADDRESS>

Generating some blocks:
* btcctl --simnet --rpcuser=user --rpcpass=password generate 400

Check alice balance
* lncli-alice walletbalance

Send coins from Alice to Bob
* lncli-bob newaddress np2wkh
* lncli-alice sendcoins <BOB_ADDRESS> 100000

Check Bob's balance
* lncli-bob walletbalance
