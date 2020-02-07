# Neutrino
We will run a light client using neutrino and understand the differences.


## Neutrino limitations
* Long scans.
* No Access to the mempool
* No access to fee estimation of full node.
* Don't validate channels on-chain.
## Running neutrino node.
* cd neutrino-lnd-node
### running the node
* lnd -C ./lnd.conf --lnddir .
### creating and unlocking the wallet
* lncli --rpcserver=localhost:10004 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon create
### checking the node is running
* lncli --rpcserver=localhost:10004 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon getinfo
* optional setting alias:
    * alias lncli-neutrino ="lncli --rpcserver=localhost:10004 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon"

## Excercise
* Open channel to Alice
* Send payment to Carol