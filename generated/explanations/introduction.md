## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Introduction
 
 **Arbiturm - Optimistic Rollup**        
## Roll Ups
Rollups are a type of Layer 2 scaling solution that execute transactions outside the main Ethereum chain (off-chain) but record transaction data on the main chain (on-chain). The core idea is to "roll up" or batch many transactions into a single one, which is then posted to the main chain. This reduces the amount of data that needs to be stored and processed on the main chain, significantly increasing throughput and reducing transaction fees.

### Types of Roll ups
There are two main types of rollups, each with its own approach to validating the batched transactions:

#### Optimistic Rollups
These operate on the principle that all transactions are assumed to be valid by default. They only execute transaction computations on-chain in the event of a challenge. This means that instead of performing computation to prove the correctness of transactions upfront, Optimistic Rollups post the transactions along with a bond. After a challenge period, if no one disputes the transaction batch with a "fraud proof" showing that something was wrong, the transactions are considered valid. This method allows for significant scaling benefits, but the challenge period can introduce a delay in finalizing transactions.

<div align="center">
  <img style="max-height:600px;margin-bottom:40px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/introduction_to_arbitrum_arbitrum_university_794/1700677076473_types_of%20rollups.png"/>
</div>

#### Zero-Knowledge Rollups (ZK-Rollups)
ZK-Rollups bundle transactions and generate a cryptographic proof, known as a zero-knowledge proof (specifically, a zk-SNARK or zk-STARK), attesting to their validity. This proof is then posted to the main chain, where it can be quickly verified. Because the validity of the entire batch can be confirmed without executing the transactions individually, ZK-Rollups can finalize transactions much more quickly than Optimistic Rollups. Additionally, ZK-Rollups enhance privacy since the actual transaction data can be kept off-chain.

## Optimistic Rollup; How it works?
Optimistic Rollups operates on the assumption that all transactions are honest and valid unless proven otherwise. Here's how they work:

#### Step 1: Execution and Aggregation
In optimistic rollups, operators, or validators, process transactions by aggregating and compressing them before submitting them to Ethereum's blockchain. Any user can act as a validator by providing a bond, similar to proof-of-stake systems, and risks penalties for any invalid submissions. Validators also maintain their version of the rollup's state and can issue fraud proofs if discrepancies arise. Some rollups use a 'sequencer' instead of multiple validators, which centralizes transaction processing and submission but provides greater control over transaction order and immediate access to the rollup chain.

#### Step 2: Sending Roll up Blocks to Ethereum
Operators consolidate multiple off-chain transactions into a single batch and compress the transaction data to minimize storage costs on Ethereum. This batch is then submitted to Ethereum as 'calldata' — a temporary and immutable form of data used by smart contracts to execute functions. While 'calldata' remains in the blockchain's history, it does not become part of the Ethereum state, thereby conserving space and reducing costs. The 'calldata' keyword in Solidity is instrumental in calling smart contract functions and organizing inputs, playing a critical role in the efficient operation of optimistic rollups. 

#### Step 3: State Commitments
State commitments play a crucial role in maintaining the integrity of the system. The state is structured as a Merkle tree, also known as the state tree, which contains all the information about the current state of the rollup. Operators compute new state roots reflecting the latest state changes and submit these roots to the rollup contract on Ethereum. By committing to the old and new state roots when posting transaction batches, and including the Merkle root for transactions, operators provide a verifiable record of the rollup's state changes on the Layer 1 blockchain. This mechanism ensures that the state of the rollup can be trusted and verified.

<div align="center">
  <img style="max-height:600px;margin-bottom:40px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/introduction_to_arbitrum_arbitrum_university_794/1700677113051_working_of%20rollup.png"/>
</div>

#### Step 4: Fraud Proof 
The essence of optimistic rollups lies in their fraud-proof mechanism. They allow blocks to be published without immediate validity checks. If discrepancies are suspected, users can challenge transitions within a set timeframe. Challenges trigger fraud-proof calculations, where disputed transactions are replayed on Ethereum's main network through a verifier contract. If fraud is confirmed, the responsible validator is penalized. To support this, rollups must make detailed state commitments and transaction data public on-chain, which incurs gas fees. Multi-round interactive proofs can enhance this process's efficiency by reducing the data and computation required for each verification step.

#### Step 5: Multiround Interactive Proving
Multi-round interactive proving is a critical component of optimistic rollups. It involves a dialogue between a challenger and the block's producer (asserter/operator), overseen by a Layer 1 verifier contract. If a block is challenged, the operator splits the disputed assertion for the rollup block into two, with each part undergoing repeated division through a bisection protocol until the specific point of contention is isolated. The verifier contract then adjudicates the dispute and identifies any fraudulent activity. This process ensures that only valid transactions are finalized, with the capability to penalize malicious actors, thereby maintaining the integrity of the rollup.   
 **Arbitrum Chains**        
Arbitrum ecosystem consists of various chains with distinct features that utilise unique technologies that enable ethereum scalability. The major arbitrum chains include.

### Arbitrum One
Arbitrum One is a Layer 2 optimistic rollup solution that enhances Ethereum blockchain. It doesn't require any additional trust beyond that which is inherent to Ethereum's Layer 1. Enabled by the Nitro technology stack, Arbitrum One features efficient data handling and execution, improved transaction compression, and compatibility with Ethereum's gas system, streamlining the process while keeping security tight.

### Arbitrum Nova
Arbitrum Nova is a Layer 2 scaling solution designed for high performance and cost efficiency. It operates on the AnyTrust protocol, which is a slightly less trustless system compared to Arbitrum One's Rollup protocol. The primary distinction lies in the AnyTrust protocol's reliance on a Data Availability Committee (DAC) to manage transaction data. This committee ensures the speedy and efficient handling of Level 2 transaction data before it is finalized on Ethereum's main chain. Arbitrum Nova is tailored for applications where high throughput and affordability are prioritized.

<div align="center">
  <img style="max-height:600px;margin-bottom:40px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/introduction_to_arbitrum_arbitrum_university_794/1700677166386_chains.png"/>
</div>

### Arbitrum Orbit
Arbitrum Orbit allows the creation of personalized chains that settle transactions to Arbitrum's Layer 2 chains, such as Arbitrum One or Arbitrum Nova. You have full control over your Orbit chain, with the ability to tailor its privacy settings, permissions, governance structure, and fee token according to your specific requirements. Orbit chains can be as open or restricted as you prefer, offering a customizable path to decentralization and the option to integrate ongoing enhancements from the Arbitrum Nitro technology stack

## How is arbiturm diferent from other Optimistic L2 Rollups?
Arbitrum's approach prioritizes a balance of speed, cost, security, and developer accessibility, underpinning its leading market position. Some of the major differences include:

### Fraud Proofs
Arbitrum sets itself apart from other Optimistic L2 Rollups primarily through its multi-round fraud proof system, which contrasts with single-round fraud proofs used by platforms like Optimism. This system verifies only challenged transactions, which may result in lower fees due to decreased reliance on Layer 1 computations.

<div align="center">
  <img style="max-height:600px;margin-bottom:40px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/introduction_to_arbitrum_arbitrum_university_794/1700677202817_difference.png"/>
</div>

### Virtual Machine Compatibility
The Arbitrum Virtual Machine (AVM) is more closely optimized for EVM coding languages, making it developer-friendly as applications don't need to be rewritten to transition from the EVM to the AVM. This contrasts with Optimism's Virtual Machine (OVM), which has faced some compatibility issues with the EVM.

### Transaction Finality and Fees
Due to the multi-round fraud proof mechanism, transaction finality on Arbitrum can be slower compared to some other rollups, but this trade-off allows for lower fees because of reduced Layer 1 computation reliance​. 
 **Arbitrum Ecosystem**        
The Arbitrum ecosystem boasts a vibrant network of decentralized applications, offering users enhanced transaction speed and reduced costs. With its robust compatibility with Ethereum's tools and smart contracts, it simplifies the developer experience for deploying dApps. 

## Stylus
Stylus is an innovative platform that extends smart contract development on the Ethereum blockchain to languages like Rust, C, and C++, diversifying beyond the conventional Solidity-centric approach. Integrated with Arbitrum Nitro's enhanced tech stack, Stylus employs the WebAssembly (WASM) virtual machine in tandem with the Ethereum Virtual Machine (EVM), enabling the execution of smart contracts authored in WASM-compatible languages on the Arbitrum network.

Stylus enhances the Arbitrum ecosystem by allowing developers to write smart contracts in Rust, C, and C++ and introducing significant performance enhancements for decentralized applications. It also adds the ability to create custom precompiles for advanced cryptographic functions, which, along with WASM support, enables high-speed execution and broader innovation, all while maintaining compatibility with the Ethereum ecosystem through its EVM+ integration.

## Ecosystem Support
Arbitrum offers a robust support ecosystem for its users, emphasizing accessibility and community engagement. The cornerstone of this support is detailed documentation and academy site that provides a wealth of information on platform functionalities and integration processes. For interactive assistance and community-driven support, Arbitrum hosts channels like Discord, where users can seek advice, troubleshoot in real-time, and engage with both peers and the Arbitrum team. Additionally, a bug bounty program encourages the community to contribute to the platform's security, rewarding those who identify and report vulnerabilities. Users are also empowered through the Arbitrum DAO to participate in governance, offering a platform to propose and vote on changes, ensuring that the community's voice is integral to the network's evolution. For direct inquiries, a dedicated support team is likely available to handle specific issues, providing personalized help.

Arbitrum's comprehensive support fosters community, loyalty, and platform security, as users contribute to identifying issues via the bug bounty program. Educational resources and tutorials empower users, while governance participation ensures a democratic, community-aligned platform. This support system is vital for user operations and the network's ongoing enhancement and resilience.

<div align="center">
  <img style="max-height:600px;margin-bottom:40px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/introduction_to_arbitrum_arbitrum_university_794/1700677255572_ecosystem.png"/>
</div>


## Decentralize governance
Arbitrum's decentralized governance is orchestrated through the Arbitrum DAO, which allows stakeholders to vote on key decisions affecting both the Arbitrum One and Arbitrum Nova chains. The governance structure includes a Security Council that can make urgent or minor changes, as well as a set of allow-listed validators who confirm the chains' states. For Arbitrum Nova, there's also a Data Availability Committee tasked with data storage and availability. The governance system has the power to modify validators and Sequencers, who are responsible for transaction ordering, thereby maintaining a balance between central oversight and progressive decentralization. This governance framework is designed to evolve, with the potential for changes based on community feedback, reflecting the adaptive nature of the protocol's management.

Progressive decentralization is a strategic approach to building trust and stability within a blockchain ecosystem. It starts with a centralized authority, such as the core development team, who can quickly respond to issues and update the system efficiently. Over time, control is handed over to a broader set of stakeholders, which enhances security by reducing central points of failure. It also deepens community involvement, as more participants are empowered to govern the network, which in turn fosters a more resilient and democratic infrastructure. This gradual transition allows the network to maintain continuity and stability while progressively mitigating risks and adapting to a decentralized governance structure. 
 
