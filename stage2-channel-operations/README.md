
# Basic Channel Operations
We will learn how to:
1. Open a payment channel
2. Creating invoices.
2. Sending payment using single and multi hops

## Connecting to a node
* lncli-alice connect 03da76ec38af7d58dcb65818cd640f70a2b4475adeb137b305d576efaac00f79a1@127.0.0.1:10012

## showing connected peers
* lncli-alice listpeers

## opening a channel
* lncli-alice openchannel <bob pub key> 1000000

## listing pending channels
lncli-alice pendinghcannels

## listing opened channels
lncli-alice listchannels

## Single hop payment
lncli-bob addinvoice
lncli-bob decodepayreq --pay_req <payment request>
lncli-alice payinvoice

## Excercises
* Multip hop payment.
* Close / Force Close a channel.

## Using BTCD to explore closing tx
* getrawtransaction
* decoderawtransaction
* decodescript