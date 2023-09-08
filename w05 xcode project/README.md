# W5 Target:

1. Build the iOS App that detects nearby device and upload the web3 address of that device
1. Read 07_HeliumWP.pdf and can they do PoL



## Web3PoL

### Bluetooth

> Basics:
>
> - Swift code detecting nearby devices:
>   - https://punchthrough.com/core-bluetooth-basics/
>   - https://youtu.be/n-f0BwxKSD0
>
> - Bluetooth Core Specification (v5.4): https://www.bluetooth.com/specifications/specs/
>
> Tools:
>
> - Service UUID Generator: https://www.uuidgenerator.net/version1



Random Thought:

- under same wifi?





Improvement:

- only need store advertisementData
  - address
  - time
  - location?
- remove all peripheral list
- remove class

### Web3

> MetaMask connection: https://github.com/maurovz/Glaip
>
> 1. Prompt the user to install MetaMask if they don't already have it installed
> 2. In your iOS app, use the MetaMask API to generate a signature request
> 3. Send the signature request to the user's MetaMask wallet
> 4. The user approves the signature request in MetaMask
> 5. The signature is returned to your iOS app
> 6. Your iOS app uses the signature to authenticate the user



dont want eth public:

- on eth: not safe
- use security network
  - smart contract compute 
  - verifier prove soso in utsc
  - soso allow verifier view location at 12am ~ 1pm
- Some measure of correct and wrong
- Maybe use Kaper
- Cosmos
  - Rust, not Solidity
- GPS distance: 
  - https://docs.rs/geoutils/latest/geoutils/
- We want people near UTSC at given time
  - calculate distance
  - calculate time
- they have Security Network: vialitors miners to calculate
- 3 backand for
- Read other paper we need talk about other papers
- read Helium

Apply for grand in summer.



Decentralized

Privacy -> no need 5 granularity better than paper last week.

We proposing completity differ easily 20k



Read paper

Security Network
