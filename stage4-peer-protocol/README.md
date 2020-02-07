
# Peers Protocol
* We will trace the peer messages when forwarding payments.
* We will explore the various transactions and scripts.

## Modify log verbosity
debuglevel=PEER=trace,LNWL=trace

## Send payment
* lncli-bob addinvoice 100
* lncli-alice payinvoice --pay_req <payment request>
* explore messages:
    * update_add_htlc
    * comit_sig
    * revoke_and_ack
    * update_fulfill_htlc

## Cancelling payment
* Pay hold invoice from alice to carol.
* Explore channels states:
    * lncli-alice listchannels
        * See pending htlc for the initiated node.
    * lncli-bob listchannels
        * See pending htlc for the forwarding node.

* Cancel hold invoice
    * Explore message:
        * update_fail_htlc

## Excercise - Close channel with pending htlc
* Explore closing tx with htlc.
* Explore spending the htlc output.

