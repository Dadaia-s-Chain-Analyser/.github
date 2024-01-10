# Organização Dadaia-s-Chain-Analyzer

- **Autor**: Marco Aurelio Reis Lima Menezes
- **Posição**: Engenheiro de Dados Pleno
- **Badge**: Data Engineer Advanced
- **Empresa**: F1rst Digital Service

## 1 - Introdução 

A organização `Dadaia-s-Chain-Analyzer` é um conjunto de repositórios criados com intuito de conceber um sistema para extrair e ingestar dados públicos de blockchains compatíveis com Ethereum Virtual Machine (EVM) em recursos nos quais seja possível processar esses dados, gerando assim insides para algumas oportunidades que a arquitetura blockchain e aplicações Web3 oferecem.

As aplicações na Web3, compostas de contratos inteligentes deployados em blockchains P2P têm crescido consideravelmente nos últimos anos, principalmente no universo DeFi. Em [Illama DeFi](https://defillama.com/) é possível analisar quantidade de recursos presos nessas plataformas DeFi. Porém antes de explorar algumas aplicações interessantes de finanças decentralizadas e suas possibilidades, exploremos alguns conceitos de Blockchain.

## 2 - Conceitos importantes e referências

### 2.1 - Blockchain

Blockchain é uma Rede P2P onde participantes da rede podem realizar basicamente 2 tipos de ação:
- Minerar novos blocos da rede caso resolvam um desafio proposto e os outros nós da rede entrem em consenso sobre esse fato.
- Submeter transações que serão posteriormente mineradas nos novos blocos por nós mineradores.

Cada bloco contém transações, que foram submetidas por algum outro nó, além de outros metadados como o número do bloco e o hash do bloco atual e o hash do bloco anterior. A presença dos hashes do bloco atual e do bloco anterior, desde o bloco genesis, gera um efeito de consistência em relação aos dados que compõem essa cadeia de blocos. É possível simular esse comportamento usando o [Super Data Science Tools Aba Blockchain](https://tools.superdatascience.com/blockchain/blockchain). Os protocolos de consenso para mineração de novos blocos de cada blockchain também garantem a consistência e segurança da rede P2P.

Cada nó da rede possui uma cópia de todos os blocos da rede e suas respectivas transações. Assim podem validar a cadeia de blocos e verificar sua consistência. O que torna os dados de todas as transações do blockchain visíveis a todos os outros nós participantes da rede.

### 2.2 - Blockchain Pública

Existem 2 tipos de blockchain. Pública e privada. O que diferencia uma da outra é a existência de uma regra para que 1 nó ingresse na rede P2P. Em blockchain públicas, tais como Bitcoin ou Ethereum, qualquer nó pode ingressar na rede. A rede P2P por si só, devido a fatores explicados brevemente no tópico anterior, garante sua segurança, desde que determinadas condições sejam satisfeitas.

### 2.3 - Contratos Inteligentes

A 1º rede P2P blockchain criada foi o Bitcoin. Nessa rede tokens são gerados na mineração de novos blocos e esses tokens podem ser trocados entre os integrantes dessa rede. Em 2015 surgiu um novo tipo de protocolo blockchain idealizado na criação da rede Ethereum. Nesse tipo de protocolo, além de transações de tokens minerados, foi criado o conceito de contrato inteligente. Este consiste de uma aplicação que é deployada em um bloco do blockchain e nós da rede podem efetuar requisições e submeter transações a esses contratos inteligentes.

Um exemplo de contrato inteligente bem comum são os do tipo `ERC20`. Todo token fungível dentro da rede Ethereum por exemplo segue esse padrão. tais como:

- Stable Coin [DAI na rede Ethereum](https://etherscan.io/token/0x6b175474e89094c44da98b954eedeac495271d0f)
- Stable Coin [USDC na rede Ethereum](https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
- Wrapped Ether [WETH na rede Ethereum](https://etherscan.io/token/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2)
- Wrapped Bitcoin [WBTC na rede Ethereum](https://etherscan.io/token/0x2260fac5e5542a773aa44fbcfedf7c193bc2c599)

**Curiosidade**

De onde vem o valor para esses tokens?

- **Wrapped tokens**: Cada rede blockchain possui seu proprio token, que é o prêmio para mineração de novos blocos. Esses tokens podem ser trocados e também são usados ao se efetuar transações que alteram o estado da blockchain, consumindo esses tokens na forma de `gas` ou taxas. Isso da valor ao token, de forma bem grosseira similar ao valor que tem um crédito na AWS para usar recursos computacionais de uma EC2 e a rede da AWS. Contudo, tokens ERC20 são gerados a partir de contratos inteligentes deployados dentro de uma rede blockchain específica. Como poderia existir um token de Bitcoin, que tem sua propria rede, dentro da rede Ethereum? São criados então os `Wrapped Tokens`, a partir de contratos inteligentes que por algum mecanismo decentralizado paream o valor do token dentro da rede com o valor do token original.

- **Stablecoins Tokens**: Cada token de uma stable coin é pareado com o valor de uma moeda tal como o dólar. Os contratos implementam diferentes mecanismos para manter o valor do token pareado. Esse tipo de token tem bastante utilidade, desde que lastreia no mundo real o valor de um token na blockchain.

- **Tokens de utilidade**: Uma das possibilidades seria alguém hipoteticamente criar um emprendimento futuro de um clube vender cotas. Para isso ele cria um contrato inteligente ERC20 que emite em sua criação 100 tokens chamados COTA. Assim ele tem 100 tokens COTA que pode vender no mercado descentralizado, cada token valendo uma cota no clube futuro.

Além dos tokens ERC20, existem também contratos inteligentes que são aplicações descentralizadas para diversas finalidades, como troca de tokens ERC20, empréstimo de tokens, mercados futuros, stake e muitos outros.  Aqui serão explorados 2 contratos:

- Troca de tokens ERC20, como a [Exchange Descentralizada UNISWAP](https://app.uniswap.org/swap?chain=mainnet)
- Borrowing and Lending com o protocolo de [empréstimo de tokens ERC20 com Aave](https://app.aave.com/). 

### 2.4 - Contrato inteligente Uniswap

Nesse contrato inteligente é possível trocar tokens ERC20 de forma descentralizada. As bases para esse tipo de contrato são:

- É possível `um usuário criar uma piscina de liquidez` e depositar quantidades de de 2 tokens, como por exemplo [uma pools dos tokens WETH - DAI](https://etherscan.io/address/0xA478c2975Ab1Ea89e8196811F51A7B7Ade33eB11#readContract).

- Outros usuários podem também depositar o par desses tokens na proporção de valor correspondente. Assim se tem uma piscina de liquidez onde é possível trocar esses 2 tokens um pelo outro. Usuários que fornecem liquidez para as piscinas recebem retornos relacionados com as taxas cobradas por quem efetua troca de tokens.

- O valor de troca desses 2 tokens é calculado a partir de um mecanismo bem inteligente chamado [Automated Market Makers](https://chain.link/education-hub/what-is-an-automated-market-maker-amm). Um mecanismo simples que pode ser usado é o de produto constante. ele implementa que o produto das quantidades de tokens na piscina deve ser constante. Vejamos um exemplo:

**Exemplo de Piscina de Liquidez com AMM do tipo produto Constante**

- Uma piscina de liquidez é criada com 2 tokens, por exemplo 1000 WETH e 100 COTA (token hipotetico de utilidade).
- O produto dessa piscina de liquidez é de 100000 WETH x COTA. Ele permanece constante, cravado no contrato da piscina.
- Se 1 ETH na cotação hipotética vale 3000 USD, cada COTA vale 3000 USD.
- 1 usuário tem WETH e quer comprar uma cota no clube, então ele troca WETH por 1 COTA. Mas quantos WETH ele deve pagar?
- Para manter o produto constante ele deixará na piscina somente a quantidade de 99 COTA. Então X * 99 deve ser igual a 100000 WETH x COTA.
- Logo a piscina precisará de 1010,1010... WETH para manter o produto constante.
- Em conclusão para comprar 1 COTA se precisará de 10.1010... WETH.

Esse mecanismo decentralizado abre a possibilidade para **troca de tokens ERC20** e possibilita a **execução de arbitragem**, pois por exemplo se muitos tokens são comprados em uma piscina de liquidez seu valor varia pra cima. Então pode-se comprar o token em outro lugar por um valor menor e vende-lo na piscina até que o preço estabilize em um valor. Como esses smart contracts são públicos é possivel identificar flutuações em preços de tokens a partir do monitoramento de estados desses contratos e executar as operações de arbitragem.

**Conclusão**: Com uma análise em tempo real das piscinas de liquidez  é possível identificar oportunidades para executar operações de arbitragem e obter retornos.

### 2.5 - Contrato inteligente Aave

Nesse contrato inteligente é possível emprestar e pegar tokens ERC20 emprestados. Segue abaixo uma descrição desse funcionamento.

- **Emprestar tokens para o protocolo**: É depositar determinados tokens para esse protocolo e ganhar retornos sobre esse valor depositado. Esses tokens depositados servem como garantia caso se deseje pegar outros tokens emprestados.

- **Pegar tokens emprestados na Aave de forma convencional**: É possível pegar tokens emprestados através de empréstimos convencionais. Para esse tipo de empréstimo é necessário ter uma garantia depositada em tokens de 150% do valor a ser pego emprestado. Por exemplo, caso um usuário deposite 15 ETH valendo 15000 USD, então poderá pegar 10000 USD em tokens emprestados, pagando é claro juros.

- **Liquidar posições de empréstimo convencionais**: Dadas as 2 funcionidades citadas acima é possivel que o valor do token depositado como garantia flutue para baixo em relação ao token pego de empréstimo, ficando assim essa posição de empréstimo sem garantia necessária. É preciso algum mecanismo de segurança para liquidar essas posições, ou seja, vender no mercado os tokens de garantia em exchanges decentralizadas como a UNISWAP e pagar o débito do empréstimo. Quem efetua essa ação são os **Keepers**, mantendo o protocolo seguro e tendo certo retorno sobre essas operações.

- **Pegar tokens emprestados na Aave na forma de Flash Loans**: Para efetuar esse tipo especial de empréstimo na Aave não precisa ter tokens de garantia depositados. Porém o empréstimo deve ser iniciado e finalizado no mesmo bloco. Esse mecanismo se basea na arquitetura da rede blockchain onde é possivel efetuar inúmeras transações de maneira atômica num mesmo bloco. Assim é possível um usuário pegar 1 milhão de dólares em WETH emprestados no protocolo, realizar qualquer outra transação (como por exemplo troca do token pego emprestado na Uniswap por outro token) e ao final devolver a Aave os 1 milhão em WETH mais taxas de gás da transação. Caso o pagamento falhe, toda transação atômica falha. Qualquer usuário pode realizar um flash loan.

**Conclusão**: Com uma análise em tempo real de posições de usuários da Aave é possível identificar oportunidades para executar liquidações e obter retornos. Também é possível realizar Flash Loans com operações de arbitragem entre a transação que adquire os tokens e a transação que os devolve.

Essas são algumas das oportunidades que um sistema extraia, ingeste e processe dados de blockchains públicas e contratos inteligentes específicos podem criar. Mas como materializar o sistema proposto? O conjunto de repositórios dessa organização fornecem uma implementação para esse sistema.

## 3 - Estrutura de repositórios da organização

A decisão para segmentar o sistema nos repositórios listados abaixo foi motivada pelo fato de que cada os 4 primeiros são imagens docker e cada uma utiliza diferentes tipos de tecnologia, alterando o peso de cada imagem e também pela finalidade de cada uma. Já o último repositório contém os arquivos de definição yml usados para orquestar containers docker que compõem o sistema Chain-Analyzer.

Cada um desses repositórios tem funcionalidades específicas que serão detalhadas a seguir.

- **Offchain Watchers**: Conjunto de aplicações python que usam a biblioteca Web.py para fazer requisições a nós membros de determinado protocolo Blockchain EVM e obter informações como metadados de blocos minerados e dados de suas respectivas transações em tempo real. Os scripts desse repositório funcionam como producers e consumers de um Cluster Kafka para criar um streaming de dados eficiente e viável, dadas algumas restrições que serão exploradas mais detalhadamente a seguir.

- **Onchain Watchers**: Conjunto de aplicações python que usam a biblioteca Web3.py e a framework brownie para `interagir diretamente com contratos inteligentes e obter dados` a partir de chamada de métodos desses contratos. Os scripts desse repositório interagem com 3 tipos de contratos relacionados com o universo DeFi.

- **Onchain Actors**: Conjunto de aplicações python que usam a biblioteca Web3.py e a framework brownie para `interagir diretamente com contratos inteligentes e submeter transações` a partir da chamada de métodos desses contratos. Os scripts desse repositório interagem com 3 tipos de contratos relacionados com o universo DeFi.

- **Apache Airflow**: Esse repositório é composto por uma imagem docker do serviço apache Airflow. Ele contém definições de DAGs de pipelines para executar rotinas na camada Batch. Esses Jobs possuem acesso a recurso de um Cluster Hadoop e também recursos da Azure.

- **chain-analyzer-services**: Repositório com definições de para orquestração de containers que juntos compõe o sistema Chain-Analyser.
