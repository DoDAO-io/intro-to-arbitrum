## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

---

## Arbitrum Nova
 
## What is Arbitrum Nova?
Arbitrum Nova is a variant within the Arbitrum ecosystem that provides a high-performance blockchain solution. Arbitrum Nova operates on the AnyTrust protocol, which is mostly trustless but introduces a new element of trust. The core of this additional trust assumption is the Data Availability Committee (DAC), which has the task of efficiently handling Layer 2 transaction data—storing it, batching it, and then posting it to Ethereum's Layer 1. The presence of the DAC in the AnyTrust protocol is what allows Arbitrum Nova to offer enhanced performance and cost-effectiveness, making it suitable for use cases where these attributes are prioritized. 

<div align="center">
  <img style="max-height:600px;margin-bottom:40px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/arbitrum_nova_arbitrum_university_144/1701175411237_anytrust_intro.png"/>
</div>

## What is Anytrust Protocol 
The AnyTrust protocol is a variation of the Arbitrum Nitro technology designed to reduce costs by incorporating a slight trust assumption. Instead of requiring every node within the Arbitrum network to have access to all Layer 2 transaction data—typically ensured by posting this data on Ethereum's Layer 1, AnyTrust delegates this responsibility to a Data Availability Committee. This committee, comprising multiple members, operates under the assumption that at least two members are honest. Consequently, even if the majority collude, the integrity of data availability is maintained, allowing the rollup protocol to function correctly and reducing the reliance on Ethereum's more costly data posting process.

### Benefits of AnyTrust
The benefits of AnyTrust are extensive including:

<div align="center">
  <img style="max-height:400px;margin-bottom:30px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/arbitrum_nova_arbitrum_university_144/1701175449131_faide_anytrust.png"/>
</div>

#### 1. Cost Reduction 
The AnyTrust protocol reduces costs on the Arbitrum system by entrusting a Committee with data storage and distribution, thus minimizing the data posted to Ethereum's mainnet. Through a managed system of public keys and signatures called Keysets, it ensures data integrity while lessening the gas fees typically incurred for data posting.

#### 2. Operational Efficiency 
The KeysetManager contract on L1 manages Keysets to facilitate secure and flexible operation of the Committee, allowing for easy updates to membership and keys. This ensures data availability and supports a trust-minimized, efficient blockchain ecosystem.

## Links




