## W3 Target:

Target:

1. How to pervent Pokemon Go (web2) unable to cheat (using web3)
2. Go to conference using NFC to tap tell to prove I'm really here



## 03_How does Pokemon Go Pervent GPS Spoofing

Pokemon Go cheating software, also known as "spoofing" or "teleporting" software, allows players to fake their GPS location and move around the map in the game without physically moving. This allows players to catch Pokemon, visit **PokeStops**, and participate in **Gyms** from anywhere, without actually being there.

#### Cheating Methods:

##### Third-Party Apps / Rooted Device

- Change the output of the GPS hardware
- Change the read value of Pokemon Go
- Pretend to be a new GPS hardware. 

##### iOS

- Xcode in development mode
- download modified version of Pokemon Go from TestFlight
- similuator on PC

##### Hardware

> https://hackaday.com/2016/07/26/we-declare-the-grandmaster-of-pokemon-go-gps-cheats/
>
> It broadcasts fake GPS signals to your phone allowing the player to “walk around” the real world using a gaming joystick.

#### Pervent Methods:

> "*We have detected* ***activity on your account that indicates you are using modified*** *client software or unauthorized third-party software in violation of our Terms of Service.*" 

##### Software / Guess

- Mainly accelerometer data doesn’t match up to the amount of GPS movement going on.
- Pokemon Go uses a combination of methods to prevent location cheating, including GPS spoofing detection, IP address tracking, and device fingerprinting. The game also uses a system of soft and hard bans to penalize players who are caught cheating. In addition, Niantic, the developer of Pokemon Go, encourages players to report any suspicious behavior they see in the game.



## 04_FOAM Whitepaper (Largest PoL)

> New applications driven by smart contracts will need consensus-driven geospatial data that can be verified and trusted
>
> FOAM provides the tools to enable a **crowdsourced map** and **decentralized location services**.
>
> - Users can controlling **when** and with **whom** they choose to share their location
> - Efficiently slove the infrastructure development problem

#### Recall from Last Week:

##### Decentralized and infrastructure-independent proof-of-location scheme:

> The paper from last week introcuced a infrastructure independent PoL scheme (i.e every nodes are cell phone with bluetooth connection)

- The FOAM is infrastructure dependent PoL scheme
- This difference brings a challenge that FOAM have to slove -> hard to setup

##### Oracle Problem:

> One of definition of Oracle Problem: regarding crowdfunding or gambling, verifying the reliability of extrinsic information **without altering the consensus mechanism** was indeed a problem: “I think of it as ‘The Oracle Problem’”. 

- FOAM is not nesessarly sloves the oracle problem, one conter example is it still doesn't sloves "a mango sitting on a store shelf", but it reduce the problem a little bit, Example: Uber could use it to get more accurate distance, Underground location tracking, Pokemon Go, Transportation services...
- FOAM is helping with Oracle Problem by **altering the consensus mechanism** and act as an Oracle

#### Crypto-Spatial Coordinates(CSC):

> Crypto-Spatial Coordinates are Ethereum smart contract addresses with corresponding addresses positioned in physical space that are verifiable both on- and off-chain.

- This allows for physical addresses in the built environment to have a corresponding smart contract address that is accessible for decentralized applications. (the CSC can be hash back to geohash + ETH address)
- CSC example: 5AH71r9wTRp9eHsqR (a hash with inputs consisting of)
  - A geohash (example: dr5ru7k)
  - A corresponding ETH address
- Resolution of a CSC is round 1 m^2^ 

##### Geohash Standard

- Geohash is a de facto standard to enconde LatLong in only one (base32) number, example: dr5ru7k

- Geohash is used by **OpenStreetMap(OSM)**
  - OpenStreetMap is a free, open geographic database updated and maintained by a community of volunteers via open collaboration, users can definine variety of objects including Roads, Buildngs, Points of Interest, Natural features...
  - Note that Pokemon Go switched base map from Google Maps to OSM data in December 2017. Because the crowdsourced and open map gets better and better.

#### Spatial Index and Visualizer(SIV):

> a frontend map for users and interface for smart contract to access the FOAM services.

Whitepaper provides the full architecture we can use as example if we are planning to build a blockchain that requires onchain map preview in the future.

#### Static Proof of Location:

##### Biggest Challenge of Proof of Location

> Consensus: difficle to implements
>
> FOAM: Previous attempts to create an open source map that is legible to humans, verifiable, and readable by machines, have been crippled due to a lack of funding for open source projects

##### Token Curated Registries(TCR)

> Different with the list/registry that owned/maintained by a central party, TCR create trusted lists that are maintained by very people that use it (to decide which item should stay in the list)

Consumers: want to utilize the list

Candidates: want to be on the list

Cartographers: Token holders

If Candidates want to add a CSC as **Point of Interest(POI)** to the registry, Candidates need to deposit token into TCR contract, registraction period will start

- if Cartographers(token holders) have no objection during registraction period, POI will be added into the TCR list
- if Cartographers(community) dont agree to add POI into the list, then challenge period will start
  - all Cartographers have option to vote yes or no, at end of period, POI will be either removed or add into the list and
    - if removed: the token desposited by Candidates will distrubute to the Cartographers(voters) reach a no consensus
    - if added: Cartographers who vote no will lose part of tokens to yes-Cartographers
  - Soso: this period works similar decentralized prediction markets I mentioned last week

##### Signal Function:

> Cartographer stakes FOAM Tokens to a Signaling smart contract by reference to a particular area. These staked tokens serve as indicators of demand. (the earlier/less well-served area the better) which is indicators to determine the mining rewards.

#### Dynamic Proof of Location:

> Zone Anchors synchorze the clock with each other using Fault Tolerant Clock Synchronization (need 4 Anchors work together), after reaching consense on time, a Zone is created.
>
> When User request a Presence Claim (prove his/her location) to network, nearest Zone Anchors will form 1 or more tranglelation and check the time of transmission of information from User to get the distance and location
>
> Then the local consensus will be upload to Verifiers, verifiers checks the data recored with in other zone, after verified, a block generated and upload to block chain, after this step, the dApps can view user's location(with time) from the public blockchain.

A **Zone Anchor** (Pokestops) is a device with a radio transmitter, a local clock, and a public key. A node is capable of engaging in a clock-synchronization protocol, requires a connection to a gateway

- cost can be as low as $10 since they are using "Low Power Wide Area Networks(LPWAN)" instead of define a new protocol
- need to provide accurate time synchronization for a set period of time in order to not be seen as faulty. A distributed system is Byzantine fault tolerant when the coordination of untrustworthy participants will always convey honest information, given more than 2/3 act honestly.

A **Zone Authority** (Gyms) is a distinguished gateway gnode with internet access and “sucient” computational power to maintain a shared State Machine. It has the ability to determine if a the state machine is in sync

- Zone Authority is responsible for maintaining and verifying the accuracy of location data within a zone, while Zone Anchor is responsible for providing location data.

A **Zone** is the quorum that maintains clock sync for a given region. Anchor in the Zone are rewared with Zone token.

A **Presence Claim** (PC) is a set of counter-signed Requests with the same Nonce, which is intended to provide enough data to constitute an exact localization. Issued by Zone participants to BPK for a fee. The presence claim is subject to fraud proof computation before being authenticated as a proof.

The **Verifiers** are computational engines that incentivized to check the time logs of Zones for fraud and finalize Proofs of Location. The verifiers need to have at least the same computational power as that of an Authority inside a zone. Because Verifiers compute locations from the time stamped data they can be said to be mining triangulations.















