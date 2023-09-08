# W6 Target:

1. Find something interesting (Nostr)
1. Start demo project about security network between two networks
1. Read 07_Helium (notes on paper)

Next week: Recall how past papers (i.e., 02, 05, 07) helped on my paper and copy the selected information/paragraphs to generate an example paper.



## Secret network

> Since secret network transactions are inherented from CosmWasm Transactions, the following properies applies:

- Peer-to-Peer Tx
  - $SCRT not privacy token
    - Governance token
    - Stack
    - Pay network
- Smart Contract Tx
  - All tokens except SCRT are private by default
  - call functionalities within Tx -> run code on blockchain

## Secret Contract Steps:

> Example Code: https://github.com/scrtlabs/secret-template/blob/master/src/msg.rs
>
> https://www.youtube.com/watch?v=ZpUz-9sORho&ab_channel=SecretNetwork
>
> https://docs.scrt.network/secret-network-documentation/development/getting-started/setting-up-your-environment

- Running testnet in local

  ```
  docker run -it -p 9091:9091 -p 26657:26657 -p 1317:1317 -p 5000:5000 --name localsecret ghcr.io/scrtlabs/localsecret:v1.6.0
  ```

  Configure `secretcli`

  ```
  secretcli config node http://localhost:26657
  secretcli config chain-id secretdev-1
  secretcli config keyring-backend test
  secretcli config output json
  ```

- Wallet function

  `secretcli keys add myWallet`

  `secretcli query bank balances "secret1.."`

  `curl "http://localhost:5000/faucet?address=secret1..."` using faucet add 1000000000 uscrt

- **Code** Upload

  `secretcli query compute list-code` check code

  `secretcli tx compute store ./contract.wasm.gz --gas 5000000 --from <name> --chain-id secretdev-1` upload code

- **Contract** Instantiating

  `secretcli query compute list-contract-by-code 1` check contract

  `secretcli tx compute instantiate 1 '{"count": 1}' --from <name> --label counterContract -y`

- **Message** Call

  - Query Message

    `secretcli query compute query secret1... '{"get_count": {}}'` 

  - Execute Message

    `secretcli tx compute execute secret1... '{"increment": {}}' --from myWallet` 

    `secretcli tx compute execute secret1... '{"reset": {"count": 0}}' --from myWallet`



## Nostr: An Interesting Protocol

> It's a web3 version of twitter just got popular a few weeks ago

The protocol is based on event objects (which are passed around as plain JSON) and uses standard elliptic-curve cryptography for keys and signing.

##### Event:

```json
{
  "id": "4376c65d2f232afbe9b882a35baa4f6fe8667c4e684749af565f981833ed6a65",
  "pubkey": "6e468422dfb74a5738702a8823b9b28168abab8655faacb6853cd0ee15deee93",
  "created_at": 1673347337,
  "kind": 1,
  "content": "Walled gardens became prisons, and nostr is the first step towards tearing down the prison walls.",
  "tags": [
    ["e", "3da979448d9ba263864c4d6f14984c423a3838364ec255f03c7904b1ae77f206"],
    ["p", "bf2376e17ba4ec269d10fcc996a4746b451152be9031fa48e74553dde5526bce"]
  ],
  "sig": "908a15e46fb4d8675bab026fc230a0e3542bfade63da02d542fb78b2a8513fcd0092619a2c8c1221e581946e0191f2af505dfdf8657a414dbca329186f009262"
}
```

##### KeyPair:

> npub18vwlyfdq47x4y3xvjh3ljfjspk5lg46c9vynx7mr5qjduxyrdapql89khr
>
> nsec1stzkakscl630zul8xsjyndesgw3exvj5mfswh4p2xcxx23t6kmjq8jcdfn

##### Clients:

- Clients are the way that you access and interact with the Nostr protocol.

  - Web: [Coracle](https://coracle.social/), [Snort](https://snort.social/)

  - Desktop: [Gossip](https://github.com/mikedilger/gossip)

  - iOS: [Damus](https://apps.apple.com/app/damus/id1628663131)

  - Android: [Nostros](https://github.com/KoalaSat/nostros/releases), [Amethyst](https://play.google.com/store/apps/details?id=com.vitorpamplona.amethyst), [Nozzle](https://github.com/kaiwolfram/Nozzle/releases)

##### Relays:

> https://nostr.watch/relays/find

- Clients can connects to multiple selected relays
- Relays can support different NIP

##### NIP:

> Nostr Implementation Possibilities (Normally it should be called Nostr Improvement Proposals)

- [NIP-01](https://github.com/nostr-protocol/nips/blob/master/01.md): which describes the basic protocol

- [NIP-05](https://github.com/nostr-protocol/nips/blob/master/05.md): like domain name register that supports human readable identifier for your public key

  > elonmusk@nostrplebs.com -> public key

  - famous relay instance supports NIP5: wss://noster.easydns.ca
  - You can host your DNS if you want, or use thrid party: https://nostrplebs.com/
  - 50% of the cost will be used on the development

- [NIP-50](https://github.com/nostr-protocol/nips/blob/master/50.md)

  - popular relay instance supports NIP50: wss://brb.io
  - Search iphone price



#### Lightning Network (Layer 2 payment protocol) ($SAT coin)

> Only require two transactions on the bitcoin blockchain: open channel and close
>
> Open payment channel on the payment network to reduce load on bitcoin blockchain

##### Alby (lightning wallet)







## Helium's PoL

Notes on the paper









