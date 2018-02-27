# Gist
An introduction about the POC projects.

The goal of those POC projects is to try some new blockchain technologies to prove they can be used in the WeatherBlock project. The code may or may not be used directly in our future WeatherBlock project. 


# Project List
All POC projects have a name started with "POC-". 

The github repo will have the same name. 



## POC-UploadIPFS

Running on a Blueberry Pie 3 hardware with a Sky2(modified firmware). 
Sky2 will send data to 192.168.1.99 (fixed IP) every 5 minutes.
Blueberry pie running on 192.168.1.99 IP address, receives data and publish to IPFS.

The IPFS data structure is IPLD. See the project POC-IPLD-DAG.

Blueberry Pie 3 is a connected IPFS node with a small amount of local storage, here on I will refer to these as nodes. The IPFS infrastructure will consist of multiple nodes connected
to one or more super nodes. A super node is a more performant machine that also operates an IPFS node, this super node is pre-embedded with a directory of `nodeIds` and their `publicKey`.
This `nodeId` is the id defined in the IPFS whitepaper and is a globally unique identity. 

The node will initially store the data locally, encrypted with AES and then publish data to IPFS by broadcasting an *IPLD Path* through a pre-defined(?) channel using pubsub(?) or another message passing mechanism. 
Super nodes will subscribe to these broadcasts and listen for the message containing a `nodeId`, *IPLD Path* and signed hash of the path, it can verify the path by decrypting the hash with the known `publicKey` of that `nodeId`.

It will then add this path to its `want_list` (see IPFS Whitepaper) and then send it to all the connected nodes, eventually it will receive those blocks and then `pin` them so they are never lost.

Due to storage limitations of the nodes after it has sent any requested blocks by the super nodes it will verify they are pinned in IPFS and then free their local storage for new data.


#### Data Aggregation

It would be ideal to maintain a distributed map/lookup or *spatial database* of locations to *IPLD Paths*, this allows us to quickly create packages for buyers who would likely
request data over a certain area. This can be done using the common `grid lookup` or some dynamic grid algorithm.

We may also have smart contracts to aggregate data and perform value added analysis, in which case we would setup a stream where in memory we 
preemptively decrypt data, aggregate, discard the AES key and then encrypt the aggregated data for sale.


#### Data Decryption

Because each node's data is stored encrypted in IPFS eventually when the data is sold to a buyer it will need to expose the AES key. Firstly each node trusts a specific certificate chain of verified super nodes, this list 
will grow over time and is distributed. A node will only divulge its AES key to these trusted super nodes. 

When a buyer requests raw data the super node initiating the job will query the *spatial database* for the associated *IPFS Paths* and then execute a decryption function in parallel for each node that's associated with the requested data.

To minimize the chance of exposure of the key we will do in-memory decryption, discard the key and re-encrypt the data with a **NEW** AES key or multi-key shared with the client, the client can then access the data in IPFS directly and decrypt the data.

- TODO: elaborate on executing this via parallelized smart contracts
- TODO: look into rotating the AES keys or some other method of time-based encryption

## POC-P2P-Proof-of-Payment

In WeatherBlock P2P communication layer. All messages will need to attach a "proof of payment". like the stamp of USPS. There is no free messaging service in order to prevent Sybil attack. Any intermedium node will check incoming message before transfer to next node, if there is no proof of payment, the message will be dropped. The conditions it need to check including
- Proof of payment
- Sender signature matches sender's public key
- Sender's public key is in the "white list" devices list
- Message is not expired (time). eg. a confirm latest state hash message will be dropped when a newer state releases. 

Test system need to log the dropped messages for auditing.

- TODO: elaborate on using an existing chain for storage of value

## POC-PureFunctionalInputOutput

## POC-PureFunctionalWaitAndGo

## POC-ResultBasedBFT

## POC-GateKeeper

## POC-AuditorNode

## POC-MergerNode

## POC-HardwareAesRsa

## POC-TestDoubleSpending

## POC-IPLD-DAG

## POC-IPRedux

## POC-ElmCompiler

