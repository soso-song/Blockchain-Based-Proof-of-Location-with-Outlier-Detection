# W4 Target:

1. Read 05_ProvingYourLocationWithoutGivingupYourPrivacy.pdf 
   - Read Apple Location Services Privacy WhitePaper (Apple, 2019)
1. Read 06_HeliumWP.pdf and can they do PoL



## 05_Proving Your Location Without Giving up Your Privacy

#### Paper Summary:

> 2010, Cited by 86
>
> Notice this is an "old" paper from 2010. They claimed it's first paper that provide the location proof architecture that is **flexible** enough to support all envisioned use case (truly useful)
>
> To allow this flexibility, the last half of the paper need spend time to talk about user privacy.

#### Location Proof

An electronic form of document that certiﬁes someone’s presence at a certain location at some point in time

Attribute:

- Flexibility: this paper reach high flexibility by choosing proactive gathering of Location Proofs, User passively update their locaiton to the chain, But it might violate user's location privacy
- Granularity of the location: the lower the safer (they defined)

Motivation:

- Location-based access control (doctor access info inside hospital, conference)
- Location-based social networking (local group chat, pokemon go)

##### Location Proof Architecture

A mechanism  

- with which **mobile** users can obtain location proofs from proof issuers **APs**
- with which **applications** can verify the validity of these proofs



#### Flexible Location Proof Architecture:

> Components: User Anonymity and Location Privacy
>
> Useful <=> Flexible => Proactive Gathering(this paper) => Must be done Carefully

##### Six essectial design goals

#1 Scalability

- Central entity issue location proofs does not scale and makes deployment difficult (consider infrastructure dependent scheme from last week)
- Use individual APs or cell towers issue location proofs.
  - issue: performance will decline as the number of users increase
  - avoid using mobile devices, use desktop which has more processing power and not using battery power.

#2 Application-Agnostic Location Proofs

- location proofs should be produces in an application-agnosic manner, to reduce the workload and battery power consumption.

#3 Proactive Location Proofs

- previous assumes that there are three parties involved in a location proof architecture:
  - User intedns to prove their location (User from FOAM)
  - Location proof issuer gives out location proof (Zone Anchor/Authority from FOAM)
  - Verifier (application) that prossess a valid location proof(applications on chain)
- A retroactive location proof: collect location proofs when aksed (user check-in at the conference)
- A proactive location proof: collect location proofs continuously (notify user conference nearby)
- this design goal propose proactive location proof can is more useful, and it's also sloves design goal #2

#4 User Anonymity

- to be widely adopted (helps user education, speakers Mike Rabinovici mentiond in D71)
- Some previous work use broadcast-based approach, anyone holds the token broadcast by an AP can use the token as location proof, but the issue is tokens can be redistributed.
- its hard because the location prover needs to know who it is vouching for

#5 Location Privacy

- Ability to control how much location information to disclose in response to the location requirements of diﬀerent applications and services

- Retroactive vs Proactive location proof: Granularity

  > For retroactive location proofs, a user can inform the proof issuer of the required granularity for the location information contained in the proof.

  > For proactive location proofs, this is not possible since the user does not yet know about the granularity required by an application.

- Even if a proof contains only coarse-grained(low granularity) location information, it might still be possible to learn a user’s ﬁne-grained(high granularity) location simply by looking up the location of the AP issuing the proof on the Internet

#6 No Dedicated Hardware

- A location proof architecture should not rely on any dedicated hardware
- Precision and Negligible processing delay.



#### Relizes the Design Goals:

> shows how cryptography can improve user privacy and system security

##### Generation of Location Proof:

1. user sends a locaiton proof reuqest with **granularity level** to the AP
2. AP generates a **nonce~ap~** and sends it to the user
3. user send **H = hash[sign~user~(nonce~user~ || nonce~ap~) || nonce~user~]** to AP
   - **sign~user~(nonce~user~ || nonce~ap~**) act as a commitment by the user
   - **nonce~user~** is for AP to notice user's identity
4. AP generates a **proof = group signature = sign~ap~(H, location~ap~, time, nonce~ap~)**
   - H is identity check between user and ap
   - location~ap~ is location of user with granularity 
     - this is the part that we interest in blockchain but they didnt give much about concenses (its 1vs1 not Many vs Many)
   - time
   - nonce~ap~ are used only once and only to pervent replay attack

##### Veriﬁcation of Location Proof:

1. user send to app

   - **signature = S~user~(n~user~ || n~ap~)** 
   - **n~user~**
   - **P~user~**
   - **proof = group signature = sign~ap~(H, location~ap~, time, nonce~ap~)**

2. app check the user has **private key** corresponding to P~user~

   > this step checks the user's identity is the one inside proof

   - step1: compute hash(signature || n~user~) = H', then check if H == H'

     - this step validate the nonce~user~ and nonce~ap~ app received is same pair in the proof

     > If H ′ equals hash value H contained in the location proof

     - not sure how does app get H from proof that signed by ap

   - step2: check signature = S~user~(n~user~ || n~ap~) using P~user~ and n~ap~

     - detail not provided, but I think its using symmetric-key encryption
     - use public key to unzip the signature signed by secret key
     - then check if n~ap~ is inside that message
     - this valides the user with P~user~ is the same guy was who signed in the proof, becuase the P~user~ and S~user~ are mathematic related and unique

3. checks the **proof = group signature = sign~group~(H, location~ap~, time, nonce~ap~)**

   - assume app knows the **P~group~** of organisations that are trusted by the app to issue location proof
   - now they can check group signature S~group~ by using P~group~ which is same above

##### Security Analysis:

- User is anonymous when generating the locaiton proof because they only send out the signature instead of their public key.
- Malicious application unable to re-using the valid proof because they unable to find signature/nonce to generate same hash
- ##### ?Since each n~ap~ is used only once, dishonest user is unable to do replay attack to prove the location user is no longer located?

##### Group Signature Schemes:

> Allows a member of a group to sign a message on behalf of the group while staying anonymous.
>
> A proof issued by any member of the group will be veriﬁable by the application, but the application has no way of knowing which issuer created the proof.
>
> In practice, proof issuers belonging to a certain corporation or geographical region would form a group

- Anyone can verify the validity of the signature without learning who signed it.
- Group manager can learn the signer’s identity

##### Modification for Proactive Location Proofs:

> add granularity level = *
>
> issuer encrypts the ﬁve granularity representations of the location with ﬁve diﬀerent symmetric keys, and includes the ﬁve ciphertexts in the location proof.

- When the user ﬁnally wants to present the proof to an application, she reveals the appropriate key to the application, which can decrypt location information of a speciﬁc granularity level, as required by the application.

##### Interesting Facts (impressive):

> We have implemented our architecture and are deploying it in a WiFi testbed [1]. The testbed covers two ﬂoors of the Davis Centre at the University of Waterloo. It consists of 38 APs that are connected to a central controller, which also issues location proofs in our implementation



#### My Comments after Reading:

##### Good points from this paper:  

- Proactive Location Proofs enables Application-Agnostic Location Proofs

  - Collect location proofs continuously (Design goal #3 )
    - very "flexible" and "useful" (but not good for battery)
  - Apps share the same location that the user "uploaded" (Design goal #2)
    - Save the battery

- Problem: 

  > For proactive location proofs, this(granularity) is not possible since the user does not yet know about the granularity required by an application.
  >
  > Solution is mentioned, add * as new granularity value, which upload multiple location repersentation with 5 levels of granularity 

##### Good tech from today:

>Notice this paper is from 2010 (people still using iPhone4). With knowledge of the **smart contract** and as a 2023 iOS (**operation system**) user, I have some ideas...
>
>Resource Used: Apple Location Services Privacy WhitePaper (Apple, 2019)
>
>- https://www.apple.com/privacy/docs/Location_Services_White_Paper_Nov_2019.pdf

- Apple use "Location Services" as gatekeeper between a user's location data and apps

  - User have option to turn on/off Location Service for some apps
  - User have option to set the granularity for some apps (Precise Location on/off)
  - User have option to set allow apps to access location in the background or while using

- Some apps may have tried to circumvent(bypass) the controls on location access that users have set up in Location Services by scanning for Bluetooth or Wi-Fi signals to infer the user’s location. (because nearby wifi list are public)

- Beacons and iBeacon(Apple 2013) may also by pass the "location service":

  > https://developer.apple.com/ibeacon/Getting-Started-with-iBeacon.pdf
  >
  > Beacons are devices that emit a Bluetooth Low Energy signal and are installed in a physical location. For example, after beacons are set up in a store, an app could notify the user about a promotion related to the product that the user is walking by.
  >
  > Probobaly the current hackable solution of problem you mentioned: "use NFC at conference to prove location"

  - Bluetooth one way communication: Bluetooth Advertising
    - iBeacon: Bluetooth Broadcaster
  - Bluetooth two way communication: Bluetooth Connection
  - Bluetooth Low Energy signal powerconsumption is extermely low

##### Comments:

- even Apple using the **Retroactive location proof** which is "not Flexible <=> not Useful", but operation system could make it behave like **Proactive location proofs** by activally request "presenced claim"

  - this achieves Design goal #3
  - gives user option to set granularity for different apps

- the OS could also work as gatekeeper to achieve Design goal #2, which makes the "Presence Claim(PC)"(from last week) avaliable to selected apps, request new PC only if it's outdated or granularity is not enough.

- Summary: the design shouldn't limited on

  > User does not know about the application that a location proof will be used for, she also does not know about the location granularity that will be required by the application

  > For proactive location proofs, this is not possible since the user does not yet know about the granularity required by an application.

  because I understand OS as a part of user, user should always know/schedule on what/when/where who/how about the futrute location proving (they allowed to OS)

- The final step to prove my point is to find what blockchain component acts as OS I mentioned 

- this shows the above comments not only applies to centrolized location provider, it's also works on chain(public)



#### Small Summary:

This paper: 

- Proactive location proof = flexible

- Let centralized AP only show 1/5 of granularity to Apps

Web2 Apps:

- Retroactive location proof but can be flexible:
  - using OS to manage memory of last locaiton proof, and granularity

Web3 Apps:

- Retroactive location proof but can be flexible:

  - apps wants to save gas fee, they will read last avaliable location on chain

- ##### problem: there is no different granularity for different apps 





#### Extra Note:

##### Threat Model

Dishonest users: get fake location proof from Malicious intruder's help

Malicious intruders: help Dishonest users get location proofs on their behalf

Curious APs and applications: learn more location information from a location proof than it really needs

Malicious applications: obtains location proofs from its users and then tries to take advantage of these proofs to get unauthorised access to other applications.

Active and passive eavesdroppers: records and maybe modiﬁes communication between users, proof issuers, or applications.

Do not Consider:

- Wormhole attacks and Weak identities
- no easily deployable solutions against either of them











