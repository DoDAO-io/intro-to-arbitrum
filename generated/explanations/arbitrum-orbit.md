## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Arbitrum Orbit
 
 **Owning the Orbit Chain**        
## Orbit Licensing 
The licensing for Arbitrum Orbit chains is designed to provide both security and flexibility for developers using the Arbitrum Nitro codebase. When you create an Orbit chain, you receive a license that is both perpetual, meaning it cannot be revoked, and recursive, allowing your Orbit chain to host further chains under the same licensing terms. This ensures that once you've developed your Orbit chain, you retain unfettered and ongoing access to the software, and you can extend these rights to additional chains created within your Orbit chain's ecosystem.

<div align="center">
  <img style="max-height:400px;margin-bottom:30px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/arbitrum_orbit_arbitrum_university_525/1701179466748_licensing.png"/>
</div>

However, this license applies specifically to chains that settle to an Arbitrum-DAO-governed chain. If you wish to establish an independent Layer 2 chain on Ethereum that does not settle to an Arbitrum-DAO chain, you must obtain a separate license. For this, you have two avenues:

**1. Offchain Labs**: You can directly request a custom license from Offchain Labs, the original developers of the Arbitrum Nitro codebase and the primary licensor.

**2. Arbitrum DAO Proposal**: Alternatively, you can submit a proposal to the Arbitrum DAO, which has been granted co-licensor rights. The DAO will then make a democratic decision on whether to grant a license for your new L2 chain.

## How to customize your Orbit chain's deployment configuration?
To customize your Orbit chain's configuration, follow these steps when you access the Orbit chain deployment portal:

### Step1: Access the Deployment Portal
Navigate to the Orbit chain deployment portal where you'll launch your new Orbit chain. You will encounter a form with various configuration fields. This form typically comes with default values that are suitable for many cases but can be customized.

### Step 2: Update Information
For devnets, the Chain ID is automatically assigned and isn't crucial. In production, you'll choose a unique integer identifier that hasn’t been used on chain indexes like Chainlist.org. Enter a distinctive name for your Orbit chain that is easily recognizable to your users and developers.

<div align="center">
  <img style="max-height:700px;margin-bottom:50px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/arbitrum_orbit_arbitrum_university_525/1701179515385_configuration.png"/>
</div>

### Step 3: Customise Specifications
Decide on the Challenge period in blocks, balancing the time validators have to dispute states against the withdrawal delay for users. This is measured in blocks of the underlying L1 chain. Specify the token for validators to use as a stake, using the token's contract address on the L2 chain to which your Orbit chain settles, or use the address for ETH if that's the chosen stake token. Set the Base stake amount, considering that a lower stake lowers the barrier to entry but may increase vulnerability to attacks, while a higher stake deters attacks but raises the barrier to validator participation.

### Step 4: Owner
Provide the account address that will own and manage the Orbit chain's base contracts. In a production environment, this address might be governed by a DAO or a multisig, but for a devnet, it can be a standard Ethereum wallet address. Carefully review the default values and modify them based on the needs and security considerations of your project. Once you've finalized the configuration values, proceed with the deployment, ensuring that the Owner address has sufficient ETH to cover gas costs for contract deployment on L2.

By customizing these settings, you can tailor your Orbit chain to the specific requirements of your application, balancing security, participation, and administrative control according to your project's needs. 
 **How to launch an Orbit Chain?**        
## Steps to launch an Orbit Chain

### Prerequisites

- Docker

- A browser-based Ethereum wallet (like MetaMask)

- At least 1.5 testnet ETH

### Step 1: Aqcuire Arbitrum Testnet $ETH
To initiate your Orbit chain, a minimum of 1.5 testnet ETH is required to fund the deployment of the foundational contracts to the chosen base chain, which can be either Arbitrum Goerli or Sepolia. With Sepolia being the preferred choice due to the planned obsolescence of Goerli, you should secure your testnet ETH from an Ethereum Layer 1 faucet for either Goerli or Sepolia. Once obtained, you can transfer your L1 testnet ETH to the corresponding Arbitrum Layer 2 testnet through the Arbitrum bridge.

### Step 2: Choose Chain Type: Anytrust vs Roll up
Arbitrum Rollup ensures a secure, open validation process by storing data on Ethereum L1, while Arbitrum AnyTrust reduces fees through a trusted Data Availability Committee managing data off-chain. Rollup chains are recommended for highly secure applications such as DeFi platforms, while AnyTrust is better suited for transaction-intensive applications like games and social dApps that prioritize lower fees. Then Configure the orbit chain's deployment using the step by step guide available in the previous slide.

### Step 3: Configure Validators and batch Poster
In the Configure Validators section of the Orbit chain deployment, you'll specify the number of validators and their addresses for your chain. The first validator's address is auto-generated, with its private key saved in a configuration file. These validators will ensure transaction integrity and manage the state of your Orbit chain on the base chain. They will be included in an allow-list on your chain's base contract, granting them permission to stake and validate. The terms "base contracts" and "base chain" refer to the L2 contracts of your Orbit chain and the L2 network they're deployed on, respectively. After setting up validators, you'll move on to configure the batch poster. In the Configure Batch Poster section, an address for the batch poster will be auto-generated, responsible for posting transaction batches from your Orbit chain to its base chain's contracts. Its private key is also auto-generated and stored in a JSON configuration file. After configuring this address, you proceed to the next deployment phase of your Orbit chain.

<div align="center">
  <img style="max-height:700px;margin-bottom:50px" src="https://d31h13bdjwgzxs.cloudfront.net/academy/arbitrum-university/Guide/arbitrum_orbit_arbitrum_university_525/1701183863381_launching.png"/>
</div>

### Step 4: Deploye Orbit Chain
To deploy your Orbit chain's base contracts, click the Deploy button on the configuration form, which prompts a transaction submission to the Arbitrum Goerli or Sepolia testnet from your wallet, incurring a minor gas fee payable in testnet ETH. This action deploys your chain's base contracts through an Orbit factory contract on Arbitrum's L2 testnet, which sets up your chain's infrastructure for transaction processing, staking, and other critical operations. After completing this transaction, you'll either move to configure a keyset for an AnyTrust chain or proceed to download configuration files to launch your chain, depending on your chosen chain type.

### Step 5: Keysets Configuration (Anytrust Only)
The Batch Poster's functionality hinges on activating a keyset in the SequencerInbox contract, using keyset and hash binaries. For Orbit AnyTrust chains, an initial keyset is generated and linked to the SequencerInbox during deployment. Post-deployment, completing a transaction with a gas fee on the Arbitrum testnet redirects you to a download page to advance your chain's setup.

### Step 6: Set Up Orbit Chain's Local Development Environment
After deploying your Orbit chain, you'll be presented with two JSON configurations: Rollup Config and L3 Config. You should download both:

1. **Rollup Config**: Saves as `nodeConfig.json`, containing your chain's node settings and the private keys for the validator and batch poster to sign transactions.

2. **L3Config**: Saves as `orbitSetupScriptConfig.json`, holding your chain's overall settings, including those for Token Bridge contracts.

Next, to set up your local environment:

1. Clone the `orbit-setup-script` repository from GitHub.
2. Place the `nodeConfig.json` file into the `config` directory of the cloned repository.
3. Similarly, move the `orbitSetupScriptConfig.json` file into the `config` directory.
4. Install necessary dependencies by executing `yarn install` in the repository's root directory. 

### Step 7: Finish Setting up Chain
Start Docker and execute `docker-compose up -d` in the orbit-setup-script repository's root directory to initiate a Nitro node and BlockScout explorer. You can then navigate to `http://localhost:4000/` to interact with the BlockScout explorer, enabling you to inspect transactions and blocks on your chain for debugging purposes. A provided Hardhat script automates several setup tasks, including funding validator and batch-poster accounts, depositing ETH through the bridge, deploying Token Bridge contracts, and setting chain parameters. Execute this script from the orbit-setup-script repository's root, substituting `0xYourPrivateKey` with your Owner account's private key and the local RPC URL with your node's. 

- For Arbitrum Goerli, use
`PRIVATE_KEY="0xYourPrivateKey" L2_RPC_URL="https://goerli-rollup.arbitrum.io/rpc" L3_RPC_URL="http://localhost:8449" yarn run setup`. 

- For Arbitrum Sepolia, 
`PRIVATE_KEY="0xYourPrivateKey" L2_RPC_URL="https://sepolia-rollup.arbitrum.io/rpc" L3_RPC_URL="http://localhost:8449" yarn run setup`. 
 **How to Customise Orbit Chain's Behaviour **        
## How to Customise Orbit Chain's Behaviour 
Modifying your Orbit chain's State Transition Function (STF), responsible for block generation, requires updating the fraud proof system for changes like new EVM opcodes or gas rules to be recognized. Simple updates, like adding RPC methods or altering transaction order, don't impact consensus and don't need these adjustments. To be compatible with Arbitrum Nitro, STF changes must ensure determinism, preserve historical block integrity, avoid external dependencies, confine state changes to Ethereum's state trie, maintain quick processing for node synchronization, and consistently produce blocks without errors.
If you're looking to alter the State Transition Function, it's necessary to create a custom version of the Arbitrum Nitro node Docker image. The behaviour of an orbit chain can be customised by following the steps given below:

### Step 1: Download Nitro Source Code
Start by duplicating the Nitro repository:

`git clone --branch v2.1.1 https://github.com/OffchainLabs/nitro.git
cd nitro
git submodule update --init --recursive --force
`

Proceed to apply your modifications to the State Transition Function.

### Step 2: Run Node Without Fraud Proof
For building the custom Arbitrum Nitro node Docker image, ensure Docker is installed by checking with docker version in the terminal. If it's not installed, refer to Docker's official guide or install it using your Linux distribution's package manager and enable the Docker service. With Docker ready, navigate to the Nitro directory and build your custom node using the command `docker build . --tag custom-nitro-node`. After constructing your Nitro node image, edit your node's `nodeConfig.json` file, typically in the `config` directory, to include the `--node.staker.dangerous.without-block-validator` parameter under the staker configuration to bypass fraud proof checks.
Here's an example snippet for the nodeConfig.json:
`...
"staker": {
  ...
  "dangerous": {
    "without-block-validator": true
  }
  ...
},
...
`
You can launch your node in two ways:

1. Via docker-compose: Update the docker-compose.yml file to use custom-nitro-node for the Nitro service, then execute docker compose up to start all services.
`...
nitro:
  image: custom-nitro-node
  ports:
...
`
2. Directly with docker run: To run just the Nitro node, use:
`docker run --rm -it -v /path/to/your/node/dir:/home/user/.arbitrum -p 0.0.0.0:8449:8449 custom-nitro-node --conf.file /home/user/.arbitrum/nodeConfig.json`

### Step 3: Enable Fraud Proof
To enable fraud proofs, you'll need to build the "replay binary", which defines the State Transition Function for the fraud prover. The replay binary (sometimes called the machine) re-executes the State Transition Function against input messages to determine the correct output block. It has three forms:

The replay.wasm binary is the Go replay binary compiled to WASM. It's used by the JIT validator to verify blocks against the fraud prover.
The machine.wavm.br binary is a compressed binary containing the Go replay binary and all its dependencies, compiled to WASM, then translated to the Arbitrum fraud proving variant WAVM. It's used by Arbitrator when actually entering a challenge and performing the fraud proofs, and has identical behavior to replay.wasm.
The WASM module root (stored in module-root.txt) is a 32 byte hash usually expressed in hexadecimal which is a merkelization of machine.wavm.br. The replay binary is much too large to post on-chain, so this hash is set in the L1 rollup contract to determine the correct replay binary during fraud proofs.
To run a validator node with fraud proofs enabled, the validator node's Docker image will need to contain all three of these versions of the replay binary.

#### Build a dev image
The simplest way to build a Docker image with the new replay binary is to build a dev image. These images contain a freshly built replay binary, but note that the replay binary and corresponding WASM module root will generally change when the code is updated, even if the State Transition Function has equivalent behavior. It's important that the validator's WASM module root matches the on-chain WASM module root, which is why this approach is harder to maintain. Over the longer term, you'll want to maintain a separate build of the replay binary that matches the one currently on-chain, usable by any node image.

To build the dev node image and get the WASM module root, run:

`docker build . --target nitro-node-dev --tag custom-nitro-node-dev
docker run --rm --entrypoint cat custom-nitro-node-dev target/machines/latest/module-root.txt`

Once you have the WASM module root, you can put it on-chain by calling `setWasmModuleRoot(newWasmModuleRoot)` on the rollup contract as the owner. The rollup contract address can be found in the chain deployment info JSON. You can confirm that the WASM module root was updated by calling `wasmModuleRoot()` on the rollup contract.

Once you have set the new WASM module root on-chain, you can re-enable fraud proofs and run your node.

To re-enable fraud proofs, open your `nodeConfig.json` file again, and remove the "dangerous" section (containing the `without-block-validator` property) that you previously added.

After that, you'll have, again, two ways of running your node.

1. Using the docker-compose file

As mentioned before, this is the recommended way if you're running your Orbit chain locally through the provided docker-compose file. In `docker-compose.yml`, modify the Docker image used for the Nitro container. Notice that we'll now use the `custom-nitro-node-dev` you just created:

`...
nitro:
  image: custom-nitro-node-dev
  ports:
...`

And run docker compose up to run all of your containers.

2. Use docker run to run your Nitro node only

This method will only run the customized Nitro node (i.e., it will not run Blockscout, or the DA server if you're using an AnyTrust chain). Use the following command:

`docker run --rm -it -v /path/to/your/node/dir:/home/user/.arbitrum -p 0.0.0.0:8449:8449 custom-nitro-node-dev --conf.file /home/user/.arbitrum/nodeConfig.json`


####  Preserving the replay binary
The primary issue with simply using a nitro-node-dev build is that, whenever the code changes at all, the replay binary will also change.

If the node is missing the replay binary corresponding to the on-chain WASM module root, it will be unable to act as a validator. Therefore, when releasing new node Docker images it's important to include the currently on-chain WASM module root.

To do that, you'll need to first extract the replay binary from the nitro-node-dev Docker image built earlier:

`docker run --rm --name replay-binary-extractor --entrypoint sleep custom-nitro-node-dev infinity
docker cp replay-binary-extractor:/home/user/target/machines/latest extracted-replay-binary
docker stop replay-binary-extractor
cat extracted-replay-binary/module.root
mv extracted-replay-binary "target/machines/$(cat extracted-replay-binary/module.root)"`

These commands will output the new WASM module root, and create the directory `target/machines/<wasm module root>.` There you'll find the three versions of the replay binary mentioned earlier: `replay.wasm`, `machine.wavm.br`, and `module-root.txt`, along with some other optional files. Now that you've extracted the replay binary, there are two ways to add it to future Docker images, including non-dev image builds. You can either keep it locally and copy it in, or host it on the web.

Option 1: Store the extracted replay binary locally
Now that we've extracted the replay binary, we can modify the `Dockerfile` to copy it into new Docker builds. Edit the Dockerfile file in the root of the nitro folder, and after all the `RUN ./download-machines.sh ...` lines, add:

`COPY target/machines/<wasm module root> <wasm module root>
RUN ln -sfT <wasm module root> latest`

Replace each `<wasm module root>` with the WASM module root you got earlier.

Option 2: Host the replay binary on the web
To support building the Docker image on other computers without this local machine directory, you'll need to either commit the machine to git, or preferably, host the replay binary on the web.

To host the replay binary on the web, you'll need to host the `replay.wasm` and `machine.wavm.br` files somewhere. One good option is GitHub releases, but any hosting service works.

Once you have those two files hosted, instead of the `COPY` and `RUN` command mentioned in option 1, you'll need to add these new lines to the Dockerfile file in the root of the nitro folder, after all the `RUN ./download-machines.sh ...` lines:

`RUN wasm_module_root="<wasm module root>" && \
    mkdir "$wasm_module_root" && \
    wget <url of replay.wasm> -O "$wasm_module_root/replay.wasm" && \
    wget <url of machine.wavm.br> -O "$wasm_module_root/machine.wavm.br" && \
    echo "$wasm_module_root" > "$wasm_module_root/module-root.txt" && \
    ln -sfT "$wasm_module_root" latest`

Replace the `<wasm module root>` with the WASM module root you got earlier, the `<url of replay.wasm>` with the direct link to the `replay.wasm` file (it must be a direct link to the file and not just a download site), and the `<url of machine.wavm.br>` with the direct link to the `machine.wavm.br` file.

### Step 4: Verify Fraud Proofs
With your Docker images ready, test your blockchain by making transactions and monitoring for "validation succeeded" in the logs, indicating the State Transition Function is working. If you encounter "Error during validation," check that your replay binary is updated with your latest changes and the WASM module root in the rollup contract is correctly set to match your binary.

## Chain Parameters
Chain parameters define the essential rules and configurations for a blockchain network, such as block size, block time, consensus rules, and network IDs, ensuring that all nodes on the network are in sync and follow the same protocol for validating and adding transactions. They are critical for maintaining the blockchain's integrity and security.

| Param                | Description                                                                                               | Arbitrum One               | Nova                      | Arb Goerli                | Arb Sepolia               |
|----------------------|-----------------------------------------------------------------------------------------------------------|----------------------------|---------------------------|---------------------------|---------------------------|
| Dispute window       | Time for assertions to get confirmed during which validaors can issue a challenge                         | 45818 blocks (~ 6.4 days ) | 45818 blocks (~ 6.4 days) | 20 blocks (~ 4.0 minutes) | 20 blocks (~ 4.0 minutes) |
| Base stake           | Amount of stake required for a validator to make an assertion                                             | 1 ETH                      | 1 ETH                     | 1 Goerli ETH              | 1 Sepolia ETH             |
| Force-include period | Period after which a delayed message can be included into the inbox without any action from the Sequencer | 5760 blocks / 24 hours     | 5760 blocks / 24 hours    | 5760 blocks / 24 hours    | 5760 blocks / 24 hours    |
| Gas speed limit      | Target gas/sec, over which the congestion mechanism activates                                             | 7,000,000 gas/sec          | 7,000,000 gas/sec         | 3,000,000 gas/sec         | 7,000,000 gas/sec         |
| Gas price floor      | Minimum gas price                                                                                         | 0.1 gwei                   | 0.01 gwei                 | 0.1 gwei                  | 0.1 gwei                  |
| Block gas limit      | Maximum amount of gas that all the transactions inside a block are allowed to consume                     | 32,000,000                 | 32,000,000                | 20,000,000                | 32,000,000                |
 
 
