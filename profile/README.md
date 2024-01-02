## Dadaia-s-Chain-Analyser Organization

Buch of repositories related with crawling blockchains compatible with EVM (Ethereum Virtual Machine) and Ingestion Tools it to a set of tools related with Data Engineering Tasks.


### Offchain Watchers

This repo contains an docker image that runs python code with the goal of Get Data from Blockchains using its Scan services, such as Etherscan for Ethereum or Polyscan for Polygon network. The data is obtained using batch processes and making requests for the blockchain scan API services.

### Onchain Watchers

This repo contains an docker image that runs Solidity and Python code, using specially a framework called `Brownie` used to automate the and interaction with deployed smart contracts in Blockchain networks EVM compatible. This repo has the goal of get data from blockchains direct from it's smart contracts, differentiating it from Offchain Watchers that makes HTTP requests, acquiring the data from a centrilized source. Getting the data directly from the chain (that's why Onchain) can be conceived as a decentralized manner (since the crawler has it's own node, not trusting in a Blockchain Node as a Service provider). 
Getting the data directly from the smart contracts makes possible to  is possible to monitor important smart contracts, in this case AAVE Borrowing and Lending and UNISWAP Decentralized Exchange contracts.

### Onchain Actors

This repo contains code neneeded to build a docker image that runs Solitidy and Python code, using also Brownie



### Apache Airflow

This repo contains a docker image for the Apache Airflow Service. The needs for this specific image is to copy the DAG definition to the docker image during a build. Using this strategy always some change is made on the DAGs, such as new Jobs added to a specific DAG, when commited to Github there is a Github Action (CI/CD tool to automate deploys semilar to Jenkins) that builds a new docker image version and then the Cluster of Docker Swarm can update the service Airflow to put effectively the changes in "Production".

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
