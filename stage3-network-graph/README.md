
# The Lightning Network Graph
We will learn about the graph, how it is updated, queried and used for routing.

## Run Carol's node
* cd carol-lnd-node
### running the node
* lnd -C ./lnd.conf --lnddir .
### creating and unlocking the wallet
* lncli --rpcserver=localhost:10003 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon create
### checking the node is running
* lncli --rpcserver=localhost:10003 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon getinfo
* optional setting alias:
    * alias lncli-carol ="lncli --rpcserver=localhost:10003 --lnddir . --macaroonpath ./data/chain/bitcoin/simnet/admin.macaroon"

## Excercise
Open channel from bob to Carol.

## Explore the graph
lncli-alice describegraph

## Query for specific channel policy.
lncli-alice getchaninfo

## Query routes
lncli-alice queryroutes --dest_node <carol node>

## Excercise - Private channel
* Run a new node
* Open a private channel to alice
* Create new invoice with routing hints and pay

### Understanding what affects routing:
* Existing route of connected nodes with open channels.
* Liquidity along the route.
* Policy restrictions:
    * CLTV delta
    * Invoice cltv_expiry    
    * max_htlc_msat, min_htlc_msat