# W1~W2 Read essential:

1. Remarkable papers about Blockchain Oracle. 
2. Remarkable papers about Proof of Location.



## 00_A Study of Blockchain Oracles

> 2020, Cited by 75
>
> A reddit discussion about some part of this paper: 
>
> https://www.reddit.com/r/Chainlink/comments/85tcia/chainlink_vs_oraclize/

#### Paper Summary:

> The first 2 and last 3 pages have very good detailed definition of different types/propertys of Oracle.  it also summarize about Provable's whitepaper, Chainlink's whitepaper, and Human Oracle with examples.

##### Chainlink

- is **decentralized** by aggregating data from various nodes and checking for consensus.
- legitimate concern: the Chainlink on-chain aggregation is single point of failure
  - Chainlink is rely on the Ethereum so the problem is actually the processing speed when Eth network is busy...
  - whitepaper page 14 mentions bumpGas method which gives node operator additional options to control how much they would like to spend on gas

##### Provable

- is "not centralized, but **distributed oracle**". it uses **authenticity proofs** to show that the data are good (prove they are not single point of failure), which is more easy to use with pre-built connectors for popular data sources.

- This paper doesn't mention how does "*anthenticity proofs*" works.
- Truth: Provable is centralized and it is central point of failure, I'm saying that because they can going offine: https://twitter.com/provablethings/status/964382990775103488?s=19

##### Human Oracle is a thing!!!

- Thomas Schelling: "even without prior interaction, people are usually able to anticipate other participants’ actions to some degree." therefore truth by consensus is to be treated with caution.

- Largest decentralized prediction markets include human oracles

  > there usually a yes-share and no-share, the value of those share are constenally changing therefor it's like a market, at end an oracle will provide a grund truth.
  >
  > Decentrolized oracle: crowdsource the answer from various ppl who hold governance token, they can get reward if they truthfully
  >
  > Note: there is TRUMPGO/USD market on FTX, act like a prediction market

  - Augur: based on REP holders in case of an outcome
    - Hold "Reputation Tokens" need report inquired events on a regular basis
    - aggragation of result is based on *consensus algorithm proposed by Truthcoin*
  - Gnosis: based on ETH voting in case of an outcome
    - derives information from centralized oracle (RealityKeys and Oraclize we mentioned)
    - "the ultimate oracle" when users to challenge the result from centralized oracle

#### More Detail:

##### Decentralized Oracle Limitation:

1. requires a predefinied standard on data format
2. inherently inefficient: 
   - all the parties participating will require a fee (User Payment, Oracles Stack)
   - for every request, it will take time before reaching a sufficient number of answers.

##### Provable (Oraclize, intergrating API to web3):

- Authenticity Proof: Demonstrate the data fetched fetched is genuine and untampered (by return data with a authenticity proof ) therefore no single point of failure.

  - This is accomplished by accompanying the returned data together with a document called authenticity proof. The authenticity proofs can build upon different technologies such as auditable virtual machines and Trusted Execution Environments.

- provable_query (have option to be encrypt):

  > `provable_query("URL", "json(https://api.pro.coinbase.com/products/ETH-USD/ticker).price")`

  - data source: URL, WolframAlpha, IPFS
  - argument: full URL, wolframAlpha formula, IPFS multi hash
  - provable_query will trigger `__calback(bytes32 myid, string result)`



## 01_Understanding the Blockchain Oracle Problem A Call for Action

> 2020, Cited by 73
>
> At the beginning of the paper mentioned a lot about most research and coin IPO didn't pay enough attention about Orable or set some error handling about it, then paper provides multiple definition of the "Oracle Problem".
>
> In my understanding "Oracle Problem" from this paper is the problem that the data is not **true** or **update**, like the paper said: "a mango sitting on a store shelf, this product's provenance is unknow to the blockchain, and data should be inserted by oracles"
>
> Then the paper explain how the Oracle problem affects real-world applications: IPRS Protection, Academic Transcript(which paper 00 also mentioned it), Supply Chain and Traceability, Energy, Contracting and Law, and healthcare
>
> I think the Oracle Problem from this paper is worthy of an research independent from Web3, because it is the problem that already exists when web is invented, it's hard to bind every physical product to the digital product.

##### Definitions of Oracle Problem:

> ChatGPT:  The Oracle problem arises when trying to ensure that the external data used by a smart contract is accurate and tamper-proof. Since the data is not stored on the blockchain, it is not protected by the blockchain's security features. As a result, a malicious actor could potentially manipulate the external data used *by a smart contract*, causing it to execute incorrectly.

- The security, authenticity, and trust conflict between third-party oracles and the trustless execution of smart contracts.
  - regarding crowdfunding or gambling, verifying the reliability of extrinsic information without altering the consensus mechanism was indeed a problem: “I think of it as ‘The Oracle Problem’”. 
- The risk of oracles being compromised and feeding the blockchain with false information is called the “oracle problem”. The oracle problem biases all real-world applications, but its impact varies according to the application itself.

##### Example:

- Oracle Problem triggered in the case of attaching physical assets on the blockchain through smart contracts(digital asset),..., what happens in real world may not be affected by the smart contract.

##### Parts I don't understand/agree:

> the paper mention Chainlink(less than 3 years old at time) as a "start-up", maybe because it's out of date
>
> notice that Chainlink created in 2017, Chainlink 2.0 announced in April 2021

- "A problem with centralized oracle: if the data are trusted and verified, the oracle may fail to operate correctly **on the smart contract** either due to malfunction or deliberate tampering."
- "The data confirmed by the majority of the oracle are then uploaded on the chain [58]. This powerful system effectively addresses oracle malfunction or failures; **however, deliberate data tampering or collusion could still be performed by the companies controlling the service**. When decentralization is not sufficient to address the oracle problem, and data authenticity cannot be objectively verified, a 'trust model' is needed for the smart contract environment to keep a certain degreeofreliability [18]"

> If we already use the decentrolize(Chainlink) oracles, then the companies from web2 controlling the service are tampering the data(gold price for example), then that means there are no "real" gold price could be found from web2
>
> therefore the tampered gold price are the "truth by consensus" mentioned from paper 00 which need be treated with caution.

## 02_Blockchain-Based Proof of Location

> I want to study PoL because I realize there are fluat in my GeneralSensor, it's possible for user to modify their geo location on local device, hence pertent they have multiple oracles in the rural area, then getting award by providing fake data.
>
> This paper have breaf introduciton on blockchain, then it gives examples of proofs of location with mobile devices, 2 infrastructure-dependent and 2 infrasructure-independent approach.
>
> The paper then illustrate their "**decentralized and infrastructure-independent proof-of-location scheme**", from my reading, 
>
> - "decentralized" because they are using blockchain that needs to support smart contract
> - "infrastructure-independent" because they are using "short-range communication technologies such as Bluetooth"
>
> The paper then analysis the robustness to talk about how their approach detects various cheating methods. at end paper introduced a performance evaluation.

##### Location Trustworthiness

- Soso: since the scheme depends on "short-range communication technology"

  - Pro: simple, when the "witness" received the message from "prover" who sends the proof of location request, they will simplely reject it if the claimed location in the request are not covered by witness's bluetooth's range, in other word, reject if its not nearby.

    The more short the communication technology can handle, the less "lying tolerance" could be. (or higher accuracy location will be)

  - Con: I may need dive the technology secition learn something about hardware, but the paper didn't mention what happends if some bluetooth device have longer range

    > from my research, the range of bluetooth(class2, class1) can reach 10~100 meters, with external antennas, the range can be increased but cannot exceed the range defined by the class of the device.
    >
    > But if we increase the receiver's bluetooth sensitivity and increase maximum output power (by using higher gain antenna and power amplifier), its possible to increase two honest trusted node to connect to each other

    Therefore this two nodes will have very high chance become "betweenness" when provers finding the shortest path.

    This will encourage miners to increase the range of each node to get higher pay, and harm human health.

    And since the scheme is no longer "short-range" the "lying tolerance" will increased to length of farest node they can reach.

##### User Privacy

- "if a peer has the possibility to periodically change its identifier according to a Poisson distribution, it gains unobservability and an attacker cannot determine the real identity of the peer by observing location proof records."
- Soso: They payoff of is the application scenarios of this scheme are reduced, paper didn't mention how the service provider can identify the user's identity. For example, if he is playing the Web3 version of pokemon go, Etherscan should be able to find a list of "user PoL identifier history" linked to his Web3 pokemon address.

