+++
date = '2025-05-24T11:56:55+03:00'
draft = false
title = 'The brief history of crypto interop'
+++

The blockchain ecosystem began with a singular, isolated network—Bitcoin. As more chains emerged, the need for interoperability—the ability for different blockchains to communicate and exchange value—became evident. This post takes you through the pivotal moments in the history of crypto interoperability.

This post is going to be technical diving deeper in each solution that emerged during this time and also will give you a glimpse of how future technologies look like. It's not just a fact/research post, its the history with filled with my own experiences and opinions about interop and crypto overall.

### Bitcoin

Lets step back and remember when it started and how we created this problem? It all started with Bitcoin. Once Bitcoin was live, for a first time in the history of humanity we had a digital non-replicable peace of information. I like to phrase in this way, because we had a digital money for a long time before Bitcoin. We have it now as well, in online banking systems, in fact most of the money is anyway digital. The innovation of Bitcoin was, that now you have a piece of information, bunch of 1s and 0s, that are not simply copy-pastable. Because before it, you (or someone else) could just replicate all the 1s and 0s and result in a same original data, without any difference between the original and new one. And here it comes, Bitcoin was born, as an implementation of digital currency. 

Anyway this is not a post about Bitcoin, fast-forward to 2011 October, Bitcoin saw a thromondoues growth. At june 2011 it reached $200M market cap (then quickly droped to $30M, just a reminder what this space looked like). The block producing become way expensive that it started. In 2010 just 2 leading 0's very necsseary for mining. A quick recamp, the mining is the process for miners, where they combine the block and calculate a HASH function on top of that information. Minining difiiculity was determined by how many 0s should be included in the thash that can be accepted. For this Miners have 'Nonce' filed that they could manipulte with original block data to result in hash that have 0. It's almost impossible to guess, so miners do a bruteforcing, how many more 0s are requirend in hash, that makes the mining exponentatially (or different function, idk) difficutl.  So back to 2011 mining complexity increased rom 1-2 to, 5-6 zeros. For curious minds, now its 20. This was a huge spike.

### Litecoin

Growth of Bitcoin hinted multiple scalability issues that could happen if Bitcoin grows more. So couple of projects emerged. Welcome on stage the Litcoin. Litecoin was developed in October 2011 by Charlie Lee, a former Google engineer, as a “lite” version of Bitcoin. The main promise of the Litecoin was that it can be faster, it can be cheaper to do mining. 
I remember back at that time my friend has few GPUs doing a Bitcoin mining and he was complaining that it's already non-profitable and when Litecoin was announced, he was super excited and just jumped right away to it. At that time I was like this guy is crazy wierdo.

Charlie Lee explicitly stated Litecoin wasn’t meant to compete with or replace Bitcoin, but rather to act as “silver to Bitcoin’s gold.” It aimed to serve as a testing ground for innovations that could later be adopted by Bitcoin (e.g., SegWit, Lightning Network).

In short Litecoin was created, to scale the crypto ecosystem. Enough of the history here, this was written 1000s time, even more, if you just ask ChatGPT, it will generate this same blog post (except the non-important parts where I told that my friend was doing mining). So what the crypto space looked like at that time. You had BTC asset in Bitcoin network and you hat LTC asset in Litecoin network. Those networks very sovereign networks, separate from each other, non of them know that there is other asset somewhere else. And a simple question arises from this situation, if I have a BTC, how do I get a LTC? BIG QUESTION. No answer until 2013. But what would people do? They would just use CEXes (at that time for example Mx. Gox). You could deposit BTC, sell it to USD, and then buy LTC and withdraw to LTC. Nice! Would you be surprised that people now in 2025 use this exact flow when they need to do this kind of operation. Something is definitely off, but would get do that along the post. Now lets get back to first technical solution that was proposed for this problem.

### Atomic Swaps

Year 2013, May 02, 10:35 AM, guy named Tier Nolan, hit the submit button in BitcoinTalks form. Alt chains and atomic transfers. This was the first time that a trustless secure way was proposed for swapping Litcoin with Bitcoin. This solution takes advange of Bitcoin P2SH (Pay to Script Hash) addresses. Bitcoin uses a simple scriptiong language, that allows you to do some basic scripting, like arhimetics and  basic cryptographic. 

There is also a movement for supporting OP_CAT in Bitcoin scripting that can allow zk proof verifications thats Starkware is pionering. But back to bitcoin scripting and Atomic Swaps, this is how the porcess looks like.

Let's say Bob has 1 BTC and Alice has 10 LTC they want to exchange the assets.

Bob generates some random data - secret and calculates HASH(S) which is used in step 2, Then creates a Bitcoin P2SH transaction with a script, that allow spending that UTXO if the secret is provided (it compares with the hash, as Bitcoin scripting gives you ability to calculate the hash), or if specified timelock is expired Bob can spend this UTXO to get funds back.
Alice sees this transaction in Bitcoin that Bob is willing to do an exchange with her. So she copies HAHS(S) from Bob's step 2 transaction and creates a transaction in Litecoin network under the same condition, except now if the secret is provided funds will go to Bob.
Once Bob observes this, now Bob reveleas the secret by doing public transaction to spend that UTXO in Litecoin.
As the secret become public Alice uses this secret and spends the UTXO in Bitcoin network.  
As the Litecoin supports almost the same Bitcoin scripting with all neccessar components like comparing and calculating hash, this worked. This scripts are also colled HTLC - Hash-Time Locked Contracts. The timelock component of this exchange is essential, as it gives appropriate time for each party to act and if they don't act timely parties can refunds their assets. This clever idea first time for the human history allowed cross-chain swaps between sovereign chains in a trustless manner. Parties don't have to trust each other as well as trust any other 3rd party.
TODO: do a BTC transaction with HTLC

### Lightning Network

After this idea, the real world implementations emerged. One of the greatest and successful use cases of the atomic swaps was the Lightning Network in 2015. With current terms first and longest running L2 on Bitcoin. 
The Lightning Network is an off-chain payment protocol that allows users to, sned/recieve Bitcoin instantly, with low fees and with highly scalable architecture.
It achieves this by creating payment channels — temporary smart contracts between two users that let them send funds back and forth without touching the blockchain for every transaction. Only the opening and closing of the channel are on-chain. Everything else happens off-chain. These opening and closing channel contracts are created with HTLC contracts.
Ethereum
So far so good, we scratched the surface of the interoperability space and now as we move forward everything becomes way more complicated, so lets dive in.
Lets fast forward one year to 2016, when great and almighty V and crew invented Ethereum. The foundation of creating Ethereum was the same idea, if we can have now non-replicable, verifiable peace of information, it means that this information was somehow created, in Bitcoin that information was limited, like UTXOs and some basic scripting, what if instead of that basic scripting we could of fully functional programming language. Solidity and Ethereum were born. With this innovation Ethereum created a situation where new tokens could be created in Ethereum itself (ERC20s). Interop and Atomic Swaps were pushed back and it was not an important solution, as you could create as many tokens as possible in EThereum - in the same chain, and then you would have protocols like Uniswap for changing them inside Ethereum without any interopability mambo jumbo stuff.
Additionally CEXes very rising, so if someone needed to exchange BTC to ETH, they could still do it with CEXes. In a same way, deposit BTC to CEX, trade it to USDT then to ETH and withdraw it back.
After few years of tromodeus sucess with Ethereum, it become evident that Ethereum needs to be scaled again. One-chain was not enough, during peak times blockchain was getting congested and fees were skyrocketing. For few folks in the space including co-founder of Ethereum (Gary Wood) it become evident that one-chain to rule them all is not going to work. So 2 independent projects were built around same time Polkadot and Cosmos, both had a vision to enable launching new chains - presumable each chain would be specialized for specific application or usecase. 

### Cosomos

Cosmos - introduces an idea of Hub and Zones. You will have a single blockchain HUB, that will connect all Zones, Zones are separate application-usecase-specific blockchains. They lanuched an Cosmos SDK, which allows to launch your own network, with your own validators, tokens, customization and etc. On top of this they introduced one of the greatest interop solutions IBC. The core idea is that you can have a soverign chains, but thease chains have a built in interop solution (IBC). With IBC, it requires for each chain to run a light client for other chains, the ones that the chain wants to be connected. Running a Light Client is required so you could verify that something really happened on that other chain. Alternativly you can be connected to Hub itself and only run a Light Client for Hub, with this design all chains can validate the Hub and route messages trough Hub. This simplifies topology from O(n²) (direct links between all Zones) to O(n) (Zones only connect to Hubs). The later is core design decision built-in in Polkadot.
In IBC (Inter-Blockchain Communication), you do not directly specify the destination chain by name in the message like you would with an HTTP endpoint. Instead, the destination chain is implicitly defined by the channel and port you're using. You can find a channel that you want to use from block explorers like mapofzones.

### Polkadot

Polkadot - introduced an idea of Relay Chains and Parachains. It looks similar at first to Cosmos, but its fundamentally diffrenet. Relay Chain is a single settlement layer. Relay Chain Validators, also validate all Parachains as well. Parachains dont have the same freedom has Cosmos chains have, in terms of their own architecture, Parachains should have and fit in the same architecutre. As Relay Chain validators have to validate that parachain. So with this design you have a unified security infrastructure, where all chains have same security and all cross-chain messages are validated by Relay Chain Validator. With Polkadot, you don't think about this when you launch a parachain, everything is handled by Relay Chain Validators, they validate all the messages in the 'core chain' and send/read messages through a same settlement layer.
Ethereum Layer 2
After this few years went by without any new innovation around interopability. Ethereum and Solana doesn't need one, Polkadot and Coosmos introduced interop inside their soveregnities, you could trade your ETH to SOL, or to BTC in CEXes. All was good until Ethereum L2s very introduced and go adoption, it was 2019 Loopring, 2021 Arbitrum and Optimism. Since then dozen of interop protocol emerged, we will walk trough each of them, what was their ideology, how they aproach the problem and ofcourse will test and run them.
The catalyst of the interop solutions was driver by design of Arbitrum and Optimism network. First they seen a trmanadeous growth, but they design introduced a big limitaiton (incconvience) - you could send your funds to Arbitrum trustleslly in few minutes, but you had no ability to withdraw them instantly, you would send a withdrawal transaction, lock your funds for 7 days and after that time you could only claim your fund back in Ethereum. This was a massive problem and huge opportunity for the ones, who could deeploy big liqudity freeze the assets for 7 days, but give users funds instantly but a same time charge them a fee. This had a big economic incentive for creating an interop protocol and the first ones started emerging.

### What is the CORE Problem of Interop?

As you can see from Bitcoin and Litecoin example as well ass Cosmos and Polkadot designs, the core driver for interop solutions is solving the scalability issue and the core problem with that solutions is, who verifies what. To just get to the bottom of interop its as simple as sending assets from one wallet to another wallet. But in different networks. So what is the question you ask about blockchain, when you are considering holding/buying/using their infra, what is the consensus of that that blockchain, how many validators, how many miners and etc. Once you are confident you use the wallet and you do the transfers. With cross-chain transfers, now you have 2 same questions. You are operating in 2 different security zones, for example for Bitcoin and Ethereum those zones are similar but for long-tail chain or app chain versus Bitcoin the security zones are different. So this is the thing you should consider. And in top of that you should ask the question, about actual transportation layer, what handles that cross-chain transfer, what is the consensus. Let's say for Bitcoin to Ethereum transfers, the security of that transfer should at least be in a same security level as Bitcoin and Ethereum transfers right? Apparently thats not true. And there is a lot there, it means that in order to do Bitcoin to Ethereum tranfer, you are passing through a 3rd zone, which has its own security attributes. Who are verifing the transactions, who are signign the transactions, what happens if.... Thats why its a way complicated topic, there are way too much solutions trying to solve this exact problem, what is the exact transportation mechanism? Who is goverining this process? Because of the single chain we have the answers, we know miners, we know validators how they workd and etc, but the same question should be asked for an interop solution as they effectivly act cross-chain ledger kind of. Who is governing the cross-chain transaction process? The question that raised billions of dollars, and sparked dozens of solutions. This post will explore the majority of them and will try to answer the same exact question from different solutions perspective. Current interop protocol do more volume than some of the actual chains. Yet the security of these protocols are underexplored. Will explore the all details end to end now.

We will start exploring each solutions I recall in short time scale which project was announced first, but at that time emerged multiple solution and you could put them in to 2 categories, ones that were trying to solve the problem in a decentralized way, and ones that were solving it in a centralized way but were communicating that they are decentralized.
Decentralized protocols, actually good ones and my faviroties were Connext and Hop. Centralized one, that was missleding users that they are decentralized was Orbiter. After few month Layerswap was introduced, it was centralized one, but had no communication around that question (not claiming that centralized nor claming that decentralized). Btw I am founder of Layerswap, so will tell you some more details around our deceision making at that time. So lets go step by step and explore each of these solution.

We will be exploring each interop protocol through 4 lenses:

- **Participants** - Who are the participants for the single bridging transaction from one chain to another? What parties are involved for finalization of the transaction?
- **User Flow** - How it looks like end-to-end, from user submitting a transaction to receiving funds in destination chain.
- **Security** - How the settlement is done between chains? Who and what verifies what happened in source and destination chains.
- **Extendability** - How extendable is the protocol? Can new networks be added? How easy it easy? Are participant permmissionless?

Alongside with it, will try to share my experience and some notes. As the problem intensified with L2s, one of the first solutions that arised was the HOP Protocol. Specifically designed for Ethereum L2s.
I will present a flow chart to capture the basic idea of the protocol and will not with colors action done by specific participant or component.

![colors](/img/interop/colors.jpg)

- **User** - Person doing the cross-chain transaction
- **Solver/Pool** - Solver or Liqudity Pool or any participant who is frontrunning the liquidity
- **Native** - Any Native Component, Like L1->L2 bridge
- **External** - External component, decentralizde file storage, separate network with validators, Oracles and etc

The core design idea of flowschars were inspired from Acrross Prime Blogpost. Will talk about it Across and Across Prime later in the post.

#### Full list of the protocols covered in this post

- [Multichain](#multichain)
- [Wormhole](#wormhole)
- [Axelar](#axelar)
- [HOP](#hop)
- [Connext V2 Protocol](#connext-v2)
- [Across](#across)
- [deBridge](#debridgede)
- [ChainFlip](#chainflip)
- [Stargate](#stargate)
- [Everclear](#everclear)
- [Meson](#meson)
- [Centralized Bridges: Layerswap, Relay, Orbiter](#centralized)
- [TRAIN Protocol](#train)
- [LayerZero](#layerzero)
- [Hyperlane](#hyperlane)
- [Synapse](#synapse)
- [THORChain](#thorchain)
- [CCIP](#ccip)
- [1inch Fusion+](#1inch-fusion)
- [Hyperbridge](#hyperbridge)
- [Garden Finance](#garden-finance)

### [Multichain](#multichain)

![Multichain protocol overview](/img/interop/multichain.jpg)

| Aspect        | Description |
|---------------|-------------|
| **Participants** | User, network of SMPC nodes that control the Decentralized Management Account (vault) |
| **User flow** | User deposits the native asset into the SMPC vault on the origin chain → SMPC nodes detect the event and mint 1:1 wrapped tokens to the user on the destination chain (or burn/mint in reverse). When the user later sends wrapped tokens back, the contract burns them and SMPC nodes release the originals from the vault. |
| **Security**  | Assets are at risk only if a ≥ threshold subset of SMPC nodes colludes; keys are never reconstructed and signatures require TSS (t,n) e.g., (15, 21). Finality on each chain is respected before mint/release. |
| **Extendability** | Adding a chain means deploying the bridge contract + letting SMPC nodes run a light node for that chain; the same node set can serve EVM and non-EVM networks, so coverage scales easily. |

On the paper Multichain was fairly decentralized, even more decentralized that all current interop protocols. Oh I forgot to mention that Multichain is not in operational state right now, apparently CEO was arrested and the whole protocol operations were stop. Not that MULTI sig apparently. We at Layerswap also lost around 40 ETH in Multichain, we used them for few routes for liqudity rebalancing and their operations were stopped, but their website was running so we just did the transaction and it is stuck forever. The Multichain case is a good reminder that any design that relay on closed set of few actors is inherently critical.

### [Wormhole](#wormhole)

![Wormhole protocol overview](/img/interop/wormhole.jpg)

| Aspect            | Description |
|-------------------|-------------|
| **Participants**  | User, Guardian Network - independent validator nodes that sign messages (VAAs*), Relayer carry a VAA to target chain. |
| **User flow**     | User emits a message (or token deposit) via the core contract on the source chain → Guardians observe and produce a VAA → Relayer submits the VAA to the destination contract, which verifies signatures and mints/unlocks the asset or executes the payload for the user. |
| **Security**      | Message executes only if the destination contract sees a valid threshold Guardian multisig; an attacker must corrupt strong majority Guardians. |
| **Extendability** | To support a new chain, deploy the core contracts and have Guardians run a light node there; Any chain type (EVM, Solana, etc.) can be onboarded. |

*Verified Action Approvals (VAAs) are Wormhole's core messaging primitive. They are packets of cross-chain data emitted whenever a cross-chain application contract interacts with the Core Contract.

### [Axelar](#axelar)

![Axelar protocol overview](/img/interop/axelar.jpg)

| Aspect        | Description |
|---------------|-------------|
| **Participants** | User, proof-of-stake validators that run the Cosmos-based Axelar network |
| **User Flow** | User calls the Gateway on the source chain (token transfer or General-Message-Passing call) → Validators observe the event, reach BFT consensus and co-sign an approval → an executor submits the approval to the Gateway on the destination chain → Gateway mints/unlocks tokens or executes the target contract, delivering assets/data to the user. |
| **Security**  | Cross-chain actions require a threshold of staked validators; mis-signing is punished by slashing. Because the same validator set runs its own consensus, Axelar inherits PoS security similar to other Cosmos chains. |
| **Extendability** | Any chain that can host a Gateway contract (EVM, Cosmos SDK, etc.) can join; validators just add the new light client module. Once integrated, it gains immediate connectivity to all other Axelar-linked networks through the same validator set and message format. |

With this design,  as with Wormhole, adding a new chain is a big problem, because all of your existing validators should run a light client for the new chain, so with each chain added to Axlear, every Axlear node operator become way harder and resounrce expensive to run. Axelar actually addresses this problem with Axelar Amplifier network. Where you can add a network that core validators don't need to verify, you add a network with its own verifiers. But I am not quite sure how the security of the messages coming from verifiers is adapted and matched with message that is verified with 'core' validators.

### [HOP](#hop)

![HOP protocol overview](/img/interop/hop.jpg)

| Aspect         | Description |
|----------------|-------------|
| **Participants** | User, Bonders front liquidity, AMM LPs (hToken to Native) |
| **User Flow**    | Deposit canonical token → mint/burn hToken → bonder sends hToken on destination → auto-swap to native asset → L1 settlement reimburses bonder. |
| **Security**     | Users can’t lose funds—if no bonder steps in, the deposit still moves the slow way. Bonders risk their own capital and only get paid when an on-chain proof of your source-chain deposit is accepted on L1, so they can’t cheat. The system adds no extra validators; it leans on the security of the underlying chains. |
| **Extendability**| Easy to add L2 within Ethereum ecosystem only. But not permissionless. Team has to do integration themselves. |

### [Connext V2](#connext-v2)

![Connext V2 protocol overview](/img/interop/connext.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → permissionless Routers (LPs) → optional Relayers pay gas. |
| **User Flow**    | xcall locks funds on source → router locks own liquidity on destination → user signs fulfillment → relayer submits proof → funds released on destination, router reimbursed on source. |
| **Security**     | Two-phase hashed-timelock; both chains escrow until matching proof is seen. No third-party consensus—safety equals source & destination chain security; timeout refunds if flow fails. |
| **Extendability**| Works on any EVM (and portable to others); anyone can deploy contracts and become a router, so new chains/assets just need liquidity. |

### [Across](#across)

![Across protocol overview](/img/interop/across.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → open set of Solver → UMA Optimistic Oracle (voters) → mainnet Hub-Pool LPs. |
| **User Flow**    | User deposits to Spoke-Pool on source → fastest solver instantly sends funds on destination → solver submits claim to Oracle → after challenge window, relayer reimbursed from Ethereum Hub-Pool; slow canonical bridge later refills pool. |
| **Security**     | Optimistic oracle; any claim can be disputed and bond slashed. Users already have funds; worst case is oracle dispute—no user loss. |
| **Extendability**| Has a dependency to an UMA protocol/Oracle System, theoretically can support all chains that have UMA protocol, currently only support EVM networks. Not permissionless - team has to do integration themselves. |

### [deBridge](#debridge)

![deBridge protocol overview](/img/interop/across.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → on-chain deBridgeGate contracts → staked Validator network (≥⅔ signs) → anyone can be Claimer who submits signatures. |
| **User Flow**    | User send() emits submission → validators sign & upload to Arweave → claimer fetches signatures and calls claim() on destination → funds released / calldata executed. |
| **Security**     | Destination contract verifies threshold validator signatures; mis-signing slashed. Users can recall funds if never claimed; gas only paid by claimer. |
| **Extendability**| Chain-agnostic; deploy Gate and add chain to validator nodes. Claiming is permissionless; validator seats governed by staking. |

### [ChainFlip](#chainflip)

![deBridge protocol overview](/img/interop/chainflip.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → chain-specific Vault → 100-of-150 FLIP-staked Validators run Substrate State-Chain & JIT-AMM → LPs provide liquidity. |
| **User Flow**    | User deposits native asset to Vault with swap details → validators witness deposit, record on State-Chain → AMM prices swap → validators TSS-sign native txn from destination-chain Vault → user receives asset. |
| **Security**     | Funds in Vaults controlled by FROST threshold; compromising requires super-majority of validators who face heavy slashing. Witnessing waits source-chain finality. No external oracles. |
| **Extendability**| Supports EVM and non-EVM (BTC, SOL, DOT) by adding Vault adapters; validator seats permissionless auctions, LPs open; new assets need only AMM pool entry. |

### [Stargate](#stargate)

![Stargate protocol overview](/img/interop/stargate.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → Stargate Router & Pools → LayerZero Relayer + DVNs verify cross-chain proofs → LPs provide unified liquidity. |
| **User Flow**    | User swap() on source → Lo Relayer & DVNs deliver header & proof to destination endpoint → Router debits its pool, credits user with native asset. |
| **Security**     | Dual attestation: message executes only if Relayer and DVNs match; collusion required to forge. Users receive native assets, not wrappers. |
| **Extendability**| Deploy Endpoint, Router & Pools on any chain whose headers can be read; unified pools share depth across networks. Liquidity, assets, and DVN slots are permissionless. |

Stargate has one of the deepest liqudities in the interop space. Works really neat and stable. They use 2 configured DVNs basically just 2 entity multisig, which I am not fun of and the technicall challange here is if they ramp up the security, lets say increase it to 4-8-12 DVNs the costs of the transaction would be skyrocketing and they will not be competetive in the market, considering that solutions like Layerswap and Relay, with a centralized (non-security) aproach are just attracting users - until something bad happens.

### [Everclear](#everclear)

![Everclear protocol overview](/img/interop/everclear.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User (targeted as Solver) creates an Intent; open, competitive Solvers pre-deposit liquidity and compete to fill it; on every chain a Spoke contract escrows user funds / solver balances, while a single Hub on the clearing chain nets and settles; off-chain Relayers & Cartographer bots batch the queues and relay messages over Hyperlane. |
| **User Flow**    | newIntent debits the user and queues an Intent on the source Spoke → off-chain agent dispatches it to the Hub → any Solver with balance on the destination Spoke calls fillIntent, paying the user instantly → a Fill message is sent to the Hub → when both messages are present the Hub “nets” them, issues a Settlement to whichever Spoke has liquidity, and the Solver’s on-chain balance is credited (withdrawable or reusable). |
| **Security**     | All assets stay inside audited Spoke/Hub contracts; Solvers can only spend what they’ve pre-deposited, and settlements are pure internal accounting, so no third-party custody risk. Messages move via Hyperlane, and intents are settled only when both intent + fill hashes match on the Hub, preventing mismatched or forged fills. |
| **Extendability**| Adding a chain is just deploying a Spoke and Hyperlane connector—Everclear advertises permissionless chain expansion—and all roles (Solver, Relayer, Router) are open, letting liquidity and clearing depth grow wherever it’s profitable. |

### [Meson](#meson)

![Meson protocol overview](/img/interop/meson.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → competitive Liquidity Providers (LPs) bond swaps and supply liquidity on every chain; a p2p / optional c-Relayer network just broadcasts messages (never holds funds); optional Trusted Verifiers can co-sign for absent users |
| **User Flow**    | User signs an off-chain swap request; relayers gossip it → first LP to win bonds the order on the source chain, escrowing the user’s tokens → the same LP instantly locks its own liquidity on the destination chain → user (or trusted verifier) signs one release signature; anyone calls release so the user receives funds on the destination chain → LP reuses that same signature to unlock the escrow + fee on the source chain |
| **Security**     | Classic HTLC atomic swap—either both locks release with the same signature or both expire and refund, so neither party can steal funds. No external validators or wrapped assets. |
| **Extendability**| Deploying Meson contracts on a new chain automatically enables swaps with all existing chains, so work grows linearly not quadratically; supports EVM and non-EVM networks. All roles (LP, relayer, verifier) are permissionless, letting liquidity scale wherever profitable. |

I user this bridge really rarely, but I thought its good to mention them as they use Atomic Swap workflow as well. They aproach with Trusted verifier is default in their dApp so basically you trust someone to not steal your funds (if they collide with LP they can steal) which I am not fun of and it completly demolishes the buity of Atomic Swaps. Again this is decision to stay competetive in the market, because as you could see with pure atomic swaps User's has to do 2 steps which noeone is fun of. As everythong things that the all problems with crypto is UX.

### [Centralized Bridges: Layerswap, Relay, Orbiter](#centralized-bridges)

![Centralized bridges overview](/img/interop/layerswap.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User → Centralized Solver |
| **User Flow**    | User requests a quote → accepts → sends the asset straight to the solver → relayer instantly transfers the requested token on the destination chain from its own balances → relayer later rebalances and keeps the fee |
| **Security**     | No Security Mechanism. |
| **Extendability**| Works on any chain—no contracts or liquidity pools needed there—as long as solver wants to integrate the network. |

Oh boooy. These players are kind of distruptive in this space. As with a centralized design you can is WAY easier to operate solver, way easeir 

### [TRAIN](#train)

![TRAIN protocol overview](/img/interop/train.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User with an Intent → competitive Solvers (liquidity providers) listed in the on-chain Discovery registry → an off-chain Auction picks the best Solver → swap is executed by minimal PreHTLC contracts on each chain. |
| **User Flow**    | User commits funds on the source chain (commit) → PreHTLC escrow starts → Solver locks equivalent funds on the destination chain (lock) → User (or wallet) forwards the hashlock back with addLock on the source → Solver reveals the secret (redeem): user gets funds instantly on the destination, Solver claims the source escrow. |
| **Security**     | Pure atomic-swap (PreHTLC/HTLC) logic—either both chains unlock with the same secret or both refunds occur, so user funds cannot be stolen. Solvers post an extra reward that is slashed on failure, and there are no pooled vaults or upgradeable contracts, limiting attack surface. |
| **Extendability**| Deploying the standard contracts on a new chain (EVM or non-EVM) automatically links it to all existing networks; Solvers self-register via Discovery, so the system scales completely permissionlessly to any chain. |

I am co-founder of this protocol. Take this with bunch of salt.

### [LayerZero](#layerzero)

![LayerZero protocol overview](/img/interop/layerzero.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User / OApp → immutable Endpoint contracts → configurable set of DVNs (Decentralized Verifier Networks) that attest each payloadHash → off-chain Executor that pays gas and calls the destination contract |
| **User Flow**    | App calls lzSend() on the source Endpoint → Each chosen DVN independently delivers an attestation of the message hash to the destination chain → When the channel’s X-of-Y-of-N DVN threshold is met, any Executor commits the message to the destination Endpoint and triggers lzReceive() in the target contract—completing the cross-chain action. |
| **Security**     | Message executes only if the configured DVN quorum matches on the same hash; no single party can forge data. Apps can mix first-party DVNs, third-party services, or their own adapters, and can lock configs so they can’t be changed later. All core contracts are non-upgradeable. |
| **Extendability**| To add a chain you merely deploy the Endpoint; any group can run DVNs/Executors for it. Because security is app-level-configurable, new networks join without diluting existing guarantees. |

### [Hyperlane](#hyperlane)

![Hyperlane protocol overview](/img/interop/hyperlane.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User / Mailbox contract → off-chain Relayers carry messages → application-chosen Interchain Security Module (ISM) verifies them. Default Multisig-ISM is secured by staked Validators using HYPER via Symbiotic restaking; apps can swap or compose ISMs at will. |
| **User Flow**    | dispatch() writes the message to the source Mailbox → Validators (if required by the ISM) sign the Merkle checkpoint → A Relayer submits deliver() on the destination chain, packaging the signatures / proof that the chosen ISM expects → The ISM’s verify() passes → Mailbox calls the destination app. |
| **Security**     | Completely modular: every app selects or builds an ISM (Multisig, Aggregation, ZK-proof, etc.). Slashing applies when a staking-based ISM (e.g., Symbiotic vault) is used, giving economic finality; if verification fails, the message is simply never executed. |
| **Extendability**| Deploy Mailbox + any ISM on a new chain and point Relayers at it—no permission needed. Because security is pluggable, chains with different trust models can interoperate while apps still pick the guarantees they want. |

### [Synapse](synapse)

![Hyperlane protocol overview](/img/interop/synapse.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User / Bridge contract → off-chain Relayers that front gas & deliver messages → Guard entities that watch every relay during an optimistic dispute window → LPs in Synapse pools supply cross-chain liquidity. |
| **User Flow**    | ① User submits a bridge tx via Synapse Router. ② A Relayer executes the matching transaction on the destination chain, giving the user their funds immediately. ③ Relayer posts a prove tx on the origin chain; Guards monitor the relay and can dispute during the set window. ④ If undisputed, the Relayer claims reimbursement from the escrowed funds; if disputed, their bond is slashed and the user’s transfer falls back to the slow path. |
| **Security**     | SIN is optimistic: only a single honest Guard needs to challenge a bad relay. Relayers post collateral and are paid only after the dispute period ends, creating strong economic guarantees without a standing validator multisig. |
| **Extendability**| Bridge, Router, and SIN contracts are live on 20+ EVM & non-EVM chains; adding another network just means deploying the standard contracts and pointing Relayers/Guards at it—all roles (Relayer, Guard, LP) are permissionless. |

### [THORChain](#thorchain)

![THOR protocol overview](/img/interop/thor.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | Swapper (user) → chain-specific inbound address → ~100 Validator Nodes running a Cosmos-SDK chain; they collectively control Asgard TSS vaults and lightweight Yggdrasil vaults → external Liquidity Providers fund RUNE-paired pools. |
| **User Flow**    | ① User sends native L1 asset with a swap memo to an inbound address. ② Nodes observe the deposit; once a super-majority see it, the swap is priced via THORChain’s RUNE-centric AMM. ③ Nodes co-sign an outbound TSS transaction from the Asgard vault on the destination chain; one node broadcasts it. ④ User receives the target asset natively—no wrappers or waiting periods. |
| **Security**     | All vault keys are split with GG20 threshold signatures; stealing funds requires ≥ ⅔ of bonded nodes, who would lose their RUNE bond and future rewards. Nodes run full-nodes for each connected chain, verifying finality before signing. |
| **Extendability**| Governance can add any L1 chain by having validators run its full-node and integrating a Bifrost module; vault sharding lets the network scale beyond 40 nodes, and liquidity pools are permissionless so assets and chains can be added as demand grows. |

### [CCIP](#ccip)

![THOR protocol overview](/img/interop/ccip.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User, staked Committing DON (Chainlink oracle nodes that sign every cross-chain message), independent Risk-Management DON that re-verifies each commit → any Executor submits the attested payload and pays gas on the destination chain. |
| **User Flow**    | ① User calls ccipSend() (message or “Programmable Token Transfer”). ② Committing DON observes the event, reaches BFT consensus, and writes an attestation for the payload to the destination chain. ③ Risk-Management DON simultaneously monitors every transfer and can halt any that breach pre-set limits. ④ Once the required signatures are final, any Executor triggers ccipReceive(), which unlocks / mints tokens or hands data to the target contract—all in a single on-chain tx for the user. |
| **Security**     | “Level-5” defense-in-depth: a forged message would require collusion of both DONs and the Executor; the Risk-Management DON is written in a different language and runs on separate infra to reduce correlated risk. Nodes are economically bonded and slashable; Routers are immutable and can enforce per-token rate limits. |
| **Extendability**| Any chain that can host the Router contracts can integrate; Chainlink nodes just add a light-client module, so new L1s/L2s join without changes to existing networks. The v1.5 CCT (Cross-Chain Token) standard and Token Manager let issuers plug tokens into CCIP with minimal code, while dApps choose their own Executors/DON sets. |

### [1inch Fusion+](#1inch-fusion)

![1inch Fusion+ protocol overview](/img/interop/ccip.jpg)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | Maker (user) signs an intent with a minimum-return; competing Resolvers (KYC’d market-makers that pre-fund liquidity and stake 1INCH for “Unicorn Power”) race to fill it; a lightweight 1inch Relayer/Auction engine broadcasts orders and later reveals the secret; anyone may be the on-chain Executor that posts the final tx and receives a small tip. |
| **User Flow**    | Maker’s signed order enters a Dutch auction; resolvers bid off-chain. 2⃣ Winning resolver escrows Maker’s tokens on source chain and its own payout on destination, both in identical HTLC escrows (same hashlock + timelocks). 3⃣ Relayer reveals the secret ➜ resolver unlocks its refund on source, then uses the same secret to release Maker’s tokens on destination. 4⃣ If no one acts before timeout, any resolver can cancel both escrows and return funds (safety-deposit tip incentives this). |
| **Security**     | Pure hash-timelock atomicity – either both escrows unlock with the revealed secret or both refund, so funds can’t be stolen. Resolvers post an extra safety-deposit and risk lost auction costs, aligning incentives. |
| **Extendability**| To support a new L1/L2, deploy the standard 1inch Escrow contract; Fusion+ instantly links it to all other chains because swaps are peer-to-peer between resolvers and makers. Resolver and executor roles are open (after compliance onboarding), so liquidity scales wherever profits exist. |

### [Hyperbridge](#hyperbridge)

| Aspect           | Description |
|------------------|-------------|
| **Participants** | User / App on any connected chain → on-chain Dispatcher / ISMP Host contract → Hyperbridge parachain (runs as a Polkadot parachain and aggregates proofs) → fully permissionless Relayers (“Tesseract”) that move messages and pay gas; no validator multisig or whitelists. |
| **User Flow**    | 1⃣ User calls send() on the source contract with payload + fee (example in docs). 2⃣ Dispatcher posts a commitment that the Hyperbridge parachain picks up and includes in its block. 3⃣ Any relayer fetches the cross-chain proof from the parachain and submits it to the destination chain’s ISMP Host. 4⃣ Host verifies the aggregated proof root; if valid, it calls the destination app (handle()), delivering tokens / data in one tx. |
| **Security**     | Hyperbridge verifies full consensus & state proofs (GRANDPA, Sync-Committee, etc.) inside its parachain, then emits an aggregated root; destination chains check this cryptographic proof, so no extra trust is added. Relayers are permissionless couriers— they can’t forge messages and are paid only after proof acceptance. |
| **Extendability**| Chain-agnostic: add a network by implementing its consensus + state client in the ISMP library and deploying the Host contract—no multisig or liquidity pools needed. Relayer and node roles are open, SDKs exist for Solidity & Polkadot, so coverage scales as soon as someone spins up a node and liquidity isn’t required. |

### [Garden Finance](garden-finance)

#### Resource Locks

#### Shared Bridges

#### Aggregators

https://www.bungee.exchange/litepaper.pdf
Intents vs Messaging
This is a bullshit question, and bullshit debate. There was never this question, it was just made a mainstream by few influental founders to keep people busy. This has not technological explanation, like almost any Intent based bridge in some ways uses a cross-chain messaging. It's not a debate at all. I think the better question to explore is Intents VS Pools, a more better way to say is Active LPs VS Passive LPs. Probably will have some follow up posts about this later.
Hyperlane vs LayerZero
New Ideas, Initiatives
I tried to introduce all the possible solutions that are there now, including the ones that are already winded down, but I bealvie this gives a glimpse was this space looks like and how important is interop solutions. In this section I will go over briefly with new ideas and initiatives that are emerging now and are worth exploring. 
Open Intents Protocol
The Open Intents Framework is a modular, open-source framework for building and deploying intent product experiences. Instead of building intents infrastructure from scratch, developers can leverage a suite of modular abstractions - including a solver and composable smart contracts - to customize and deploy intent-based protocols with ease.
This is an initiative coming from a motivatiation and premis to modualizrie intent protocol componetns. Like messaging, running Solver and etc. I actually respect this initative, but Stundartigizing Solver looks like a non-standartzible thing. Solvers are fundamentally different, they have bunch of integrations with CEXes, other bridges, swap protocols, they have bunch of admin panels, tools for monitoring and etc, becasue of unstable cross-chain infrasturcture including RPC outages, architectural differences beetwin blockchains and etc, they have sophisticated transaction processing systems. All of this way complicated, way custom, that this is really hard to standartize. The solver that uses an atomic swap protocol, works different that one uses x-chain messaging, and that one is different from Solvers like in deBridge protocol. There are too many differences to get an usefull standard. Existing solvers will need some kind of incentive to move to this standard, this standard should generate a bigger orderflow somehow (lets say if this got implemented with wallets), or the standart should solve a good problem for them. I don't see either of these happing soon.
Across Prime

### Li.Fi x Catalyst

Li.Fi acquiring Catalyst - basically as far as I can tell asquhiring - is the most badass move I seen in this space. Why is that? So listen, the big portion of the cross-chain volume is already going through Jumper. They managed to both attract users as well as wallets (in startup terms B2C and B2B). Now they have the biggest order-flow for cross-chain in single place. And what is the next trhing to do? They route all this orderflow to different solvers and protocols and those capture the value from those transactions. Now Li.Fi wants to capture that value for themselves. If they add their own solver/protocol system, they can eventually route all the order flow to their solver and capture that value instead of leaving it underlying solver/protocols. Smartass, badass move. I am not sure how this will play out. I have few ideas that would want to share here for them, is that I think the aggregator type of integration for example in wallet, when the integrated bridges has a very wide range of security details, being from centralized to semi-decentralized or ones that fake decentralized, this should be probably an option for integrators (I dont know if they have or not have this feature) so they can select a security level. The other option that I would really like to see in Li.Fi which is super difficult to implement technically, to have a permissionless integraiton of the bridges. Additionally its very easy to 'trick' the aggregator, I can just add a centralized bridge to it and majority of alll the order flow will go trhough it, and users has no assurance from security persepective or any other information shown in UI, its only the fee and speed. Paying with VISA is faster than any blockchain, cheaper than any blockahin, why we are building crypto?

### TRAIN x Aztec

With public announcement of the first Privacy-preserving L2 Aztec, the cross-chain ecosystem becomes much more interesting. If you can build a cross-chain bridge - a private one, from any N chain to Aztec, and from Aztec to any M chain, it will mean that you can basically have a private cross-chain bridging from N to M chains. Pretty exciting. And the TRAIN's design perfectly fits this idea. Combaning the Atomic Swaps with Multi-hop Transaction, TRAIN can enable this seemslesly fomr a single UI/UX.
Let's explore it a bit more. So TRAIN protocol allows two parties (user, solver) to trustless exchange assets in 2 chains. Also this can be chained together, to go to chains that do not have direct connection (e.g. single solver). TRAIN now is being built to support Aztec. To basically do a private cross-chain bridge to Aztec. So you can privately bridge to Aztec from Arbitrum, or from Solana. Thats already interesting, but if you have 2 solvers supporting Aztec, this can also allow you to do a cross-chain bridge from Arbitrum to Solana, in the middle using Aztec, so first solver will solve Arbitrum to Aztec, second solver will solve Aztec to Solana. There is a bit still technical challange because TRAIN for multihop transactions uses the same HASHLOCK so ARbitrum and Solana locks will share that and it will be easly linked and we are trying to solve it.