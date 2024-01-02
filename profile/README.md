# Dadaia-s-Chain-Analyser Organization

Buch of repositories related with crawling blockchains compatible with EVM (Ethereum Virtual Machine) and Ingestion Tools it to a set of tools related with Data Engineering Tasks. 
Each one of these repos were create separately because each one of them represents Docker Images and has its own deployment workflow. They had also different functionalities that can be combined to explore and analyse Blockchain Data, giving some insides about opportunities at this field and also providing data to monitor these networks. Follows a brief description about the mecioned repositories and its functionalities.

### 1 - Offchain Watchers

This repo contains an docker image that runs python code (4 jobs) with the goal of get data from Blockchains using the library Web3.py and the Blockchain Node as a Service providers Infura and Alchemy. 
The goal for this repo is work as a system that can ingest real time transactions from Blockchain networks EVM compatible, such as Ethereum, Polygon, Binance Smart Chain, Arbitrum, Avalanche, Fantom and others, minimizing the latency.
The architecture for these 4 Jobs relies on Queue Services like Apache Kafka and it's designed in order to minimize the requests to the Blockchain Nodes.

### 2 - Onchain Watchers

This repo contains an docker image that runs Solidity and Python code, using specially a framework called `Brownie` used to automate the and interaction with deployed smart contracts in Blockchain networks EVM compatible. This repo has the goal of get data from blockchains direct from it's smart contracts, differentiating it from Offchain Watchers that makes HTTP requests, acquiring the data from a centrilized source. Getting the data directly from the chain (that's why Onchain) can be conceived as a decentralized manner (since the crawler has it's own node, not trusting in a Blockchain Node as a Service provider). 
Getting the data directly from the smart contracts makes possible to  is possible to monitor important smart contracts, in this case AAVE Borrowing and Lending and UNISWAP Decentralized Exchange contracts.

### 3 - Onchain Actors

This repo contains code needed to build a docker image that runs Solitidy and Python code, using also `Brownie`. However, the services based on Onchain Actor images aims to really interact with the smart contracts, making transactions such as:
- Putting ERC20 tokens as collateral in AAVE V2 and V3 protocols.
- Borrow ERC20 tokens AAVE V2 and V3 protocols.
- Execute Flash Loans using AAVE V2 and V3 protocols.
- Swap ERC20 tokens using the UNISWAP protocols V2 and V3.
- Execute some fuctionalities in ERC20 contracts.


### 4 - Apache Airflow

This repo contains a docker image for the Apache Airflow Service. The needs for this specific image is to copy the DAG definition to the docker image during a build. Using this strategy always some change is made on the DAGs, such as new Jobs added to a specific DAG, when commited to Github there is a Github Action (CI/CD tool to automate deploys semilar to Jenkins) that builds a new docker image version and then the Cluster of Docker Swarm can update the service Airflow to put effectively the changes in "Production".

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
