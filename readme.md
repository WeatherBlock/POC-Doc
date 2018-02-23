# Gist
An introduction about the POC projects.

The goal of those POC projects is to try some new blockchain technologies to proof they can be used in WeatherBlock project. The code may or may not be used directly in our future WeatherBlock project. 


# Project List
All POC projects have a name started with "POC-". 

The github repo will have the same name. 



## POC-UploadIPFS

Running on a Blueberry Pie 3 hardware with a Sky2(modified firmware). 
Sky2 will send data to 192.168.1.99 (fixed IP) every 5 minutes.
Blueberry pie running on 192.168.1.99 IP address, receive data and save to IPFS.

The IPFS data structure is IPLD. See the project POC-IPLD-DAG.


## POC-P2P-Proof-of-Payment

In WeatherBlock P2P communication layer. All message will need to attach a "proof of payment". like the stamp of USPS. There is no free messaging service in order to prevent Sybil attack. Any intermedium node will check incoming message before transfer to next node, if there is no proof of payment, the message will be dropped. The conditions it need to check including
- Proof of payment
- Sender signature matches sender's public key
- Sender's public key is in the "white list" devices list
- Message is not expired (time). eg. a confirm latest state hash message will be dropped when a newer state releases. 

Test system need to log the dropped messages for auditing.

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

