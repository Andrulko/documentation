# ZMQ events

This table contains the ZMQ events that the IRI publishes and that clients can subscribe to.

All events that you subscribe to must be in lowercase letters except the trytes of the address event, which must be in uppercase letters.

All events return at least one buffer object that contains space-separated data. The first item in the buffer is always the name of the event.

The information in the Returned data column is displayed as though the buffer had been converted to a string and split on a space character into an array.

Index 0 of each array of returned data is not displayed because it is always the name of the event.

| **Events**                                                                                                                                                          | **Description**                                                     | **Returned data**                                                              |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------- |:------------------------------------------------------------------- |:------------------------------------------------------------------------------ |
| [`mctn`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/service/tipselection/impl/WalkerAlpha.java#L87) | The number of transactions that were traversed during tip selection | Index 1: Total number of transactions that were traversed during tip selection |
| [`dnscv`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L188)                        | Neighbor DNS validations                                            |                                                                                |

- Index 1: Neighbor's hostname
- Index 2: Neighbor's IP address

|[`dnscc`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L196)|Neighbor DNS confirmations| Index 1: Neighbor's hostname |[`dnscu`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L200) |Update to a Neighbor's IP address| Index 1: Neighbor's hostname |[`hmr`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L359)|The ratio of received transactions that the IRI stored in cache to received transaction that the IRI randomly removed (hit to miss ratio)|

- Index 1: Hit count
- Index 2: Miss count

|[`antn`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L374) |Information about non-tethered neighbors that were added (available only on the testnet network)| Index 1: URL of a non-tethered neighbor |[`rntn`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L391)|Information about non-tethered neighbors that were refused (available only on the testnet network)|

- Index 1: URL of the neighbor
- Index 2: The maximum number of peers that are specified in the IRI configuration options

|[`rstat`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/Node.java#L641) |Information about the tip transaction requester|

- Index 1: Number of received tip transactions that the IRI is yet to process 
- Index 2: Number of tip transactions that the IRI is yet to broadcast to its neighbors
- Index 3: Number of tip transactions that the IRI is yet to request from its neighbors
- Index 4: Number of requested tip transaction that the IRI is yet to send as a reply to its neighbors
- Index 5: Number of stored transactions in the ledger

|[`rtl`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/network/TransactionRequester.java#L120) |Transaction that the IRI randomly removed from the request queue| Index 1: Transaction hash that was removed |[`lmi`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/MilestoneTracker.java#L158) |The latest milestone index|

- Index 1: Index of the previous solid subtangle milestone
- Index 2: Index of the latest solid subtangle milestone

|[`lmsi`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/MilestoneTracker.java#L191) |The latest solid subtangle milestone|

- Index 1: Index of the previous solid subtangle milestone
- Index 2: Index of the latest solid subtangle milestone

|[`lmhs`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/MilestoneTracker.java#L192)| The latest solid subtangle milestone transaction hash| Index 1: Milestone transaction hash |[`sn`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/LedgerValidator.java#L147)| Transaction in the ledger that the IRI has recently confirmed|

- Index 1: Transaction hash
- Index 2: Address
- Index 3: Trunk transaction hash
- Index 4: Branch transaction hash
- Index 5: Bundle hash

|[`tx_trytes`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/storage/ZmqPublishProvider.java#L63)| Signature of a transaction that the IRI has recently confirmed| Index 1: Transaction signature |[`tx`](https://github.com/iotaledger/iri/blob/5883633a06312602c4a2439906d7ade49ed7f2f4/src/main/java/com/iota/iri/storage/ZmqPublishProvider.java#L68) |Transactions that the IRI has recently appended to the ledger| **Array 0**

- Index 1: Transaction hash
- Index 2: Address
- Index 3: Amount of IOTA
- Index 4: Obsolete tag
- Index 5: Timestamp of the bundle creation (seconds since the last snapshot)
- Index 6: Index of the transaction in the bundle
- Index 7: Last transaction index of the bundle
- Index 8: Bundle hash
- Index 9: Trunk transaction hash
- Index 10: Branch transaction hash
- Index 11: Timestamp of the attachment to the Tangle (milliseconds since the last snapshot)
- Index 12: Tag

**Array 1**

- Index 0: "tx_trytes"
- Index 1: Transaction signature

|[81 character address or 90 character address with checksum](https://github.com/iotaledger/iri/blob/f02d787d47eb9a04e764c15562a281ea8d7d92c1/src/main/java/com/iota/iri/LedgerValidator.java#L147)| Activity on an address|

- Index 1: Index of the latest solid subtangle milestone
- Index 2: 
- Index 3: Address 
- Index 4: Trunk transaction hash
- Index 5: Branch transaction hash
- Index 6: Bundle hash

||