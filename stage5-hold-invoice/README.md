
# Hold Invoice
We learn the concept of hold invoice that can be used for various use cases which one of them is offchain/onchain swaps.

## Compile LND with flags to enable more options
* go build -v -tags="experimental signrpc walletrpc chainrpc invoicesrpc routerrpc backuprpc peerrpc submarineswaprpc breezbackuprpc" github.com/lightningnetwork/lnd/cmd/lncli

## Create a 256 bit key and its hash 
* openssl rand -hex 32
* echo <key> | xxd -r -p |  openssl sha256 -hex

## Bob - Create hold invoice
* lncli-bob addholdinvoice <key> 100

## Alice - Pay invoice
* lncli-alice payinvoice --pay_req <pay req>

## Cancel/Settle invoice
* lncli-bob cancelinvoice <hash>
* lncli-bob settleinvoice <key>

## Swap usage of invoices.
* submarine swap
* reverse subswap

```
OP_HASH160
<preimageHash>
OP_EQUAL
OP_IF
<payeePubKey>
OP_ELSE
lockHeight
OP_CHECKSEQUENCEVERIFY
OP_DROP
<payerPubKey>
OP_ENDIF
OP_CHECKSIG
```
