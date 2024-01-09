# Organização Dadaia-s-Chain-Analyzer

- Autor: Marco Aurelio Reis Lima Menezes
- Posição: Engenheiro de Dados Pleno
- Badge: Data Engineer Advanced
- Empresa: F1rst Digital Service

## 1 - Introdução 

A organização `Dadaia-s-Chain-Analyzer` é um conjunto de repositórios criados com intuito de conceber um sistema para extrair e ingestar dados públicos de blockchains compatíveis com Ethereum Virtual Machine (EVM) em recursos nos quais seja possível processar esses dados e fornecer informações para aplicações voltadas ao mundo Blockchain, gerando assim insides para algumas oportunidades que esse tipo de arquitetura disponibiliza.

A decisão para segmentar o sistema nos repositórios listados abaixo foi motivada pelo fato de que cada os 4 primeiros são imagens docker e cada uma utiliza diferentes tipos de tecnologia, alterando o peso de cada imagem e também pela finalidade de cada uma. Já o último repositório contém os arquivos de definição yml usados para orquestar containers docker que compõem o sistema Chain-Analyzer.

Cada um desses repositórios tem funcionalidades específicas que serão detalhadas a seguir.

- **Offchain Watchers**: Conjunto de aplicações python que usam a biblioteca Web.py para fazer requisições a nós membros de determinado protocolo Blockchain EVM e obter informações como metadados de blocos minerados e dados de suas respectivas transações em tempo real. Os scripts desse repositório funcionam como producers e consumers de um Cluster Kafka para criar um streaming de dados eficiente e viável, dadas algumas restrições que serão exploradas mais detalhadamente a seguir.

- **Onchain Watchers**: Conjunto de aplicações python que usam a biblioteca Web3.py e a framework brownie para `interagir diretamente com contratos inteligentes e obter dados` a partir de chamada de métodos desses contratos. Os scripts desse repositório interagem com 3 tipos de contratos relacionados com o universo DeFi.

- **Onchain Actors**: Conjunto de aplicações python que usam a biblioteca Web3.py e a framework brownie para `interagir diretamente com contratos inteligentes e submeter transações` a partir da chamada de métodos desses contratos. Os scripts desse repositório interagem com 3 tipos de contratos relacionados com o universo DeFi.

- **Apache Airflow**: Esse repositório é composto por uma imagem docker do serviço apache Airflow. Ele contém definições de DAGs de pipelines para executar rotinas na camada Batch. Esses Jobs possuem acesso a recurso de um Cluster Hadoop e também recursos da Azure.

- **chain-analyzer-services**: Repositório com definições de para orquestração de containers que juntos compõe o sistema Chain-Analyser.