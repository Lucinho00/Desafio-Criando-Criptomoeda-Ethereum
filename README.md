# Desafio-Criando-Criptomoeda-Ethereum

Passo 1: Criar um Projeto Truffle
Inicialize o projeto:

mkdir MyToken
cd MyToken
truffle init


Instale o OpenZeppelin:

npm install @openzeppelin/contracts


Passo 3: Escrever o Contrato ERC-20 em Solidity
Crie um arquivo MyToken.sol na pasta contracts e adicione o seguinte código:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor(uint256 initialSupply) ERC20("MyToken", "MTK") {
        _mint(msg.sender, initialSupply);
    }
}


Passo 4: Configurar o Deploy do Contrato
Crie um arquivo de migração 2_deploy_contracts.js na pasta migrations e adicione o seguinte código:

const MyToken = artifacts.require("MyToken");

module.exports = function (deployer) {
    deployer.deploy(MyToken, 1000000 * 10 ** 18); // Mint 1,000,000 tokens
};


Passo 5: Configurar a Rede Blockchain (por exemplo, Ropsten)
No arquivo truffle-config.js, configure a rede Ropsten:

const HDWalletProvider = require('@truffle/hdwallet-provider');
const mnemonic = 'your mnemonic here';
const infuraKey = 'your infura key here';

module.exports = {
  networks: {
    ropsten: {
      provider: () => new HDWalletProvider(mnemonic, `https://ropsten.infura.io/v3/${infuraKey}`),
      network_id: 3,
      gas: 5500000,
      confirmations: 2,
      timeoutBlocks: 200,
      skipDryRun: true
    },
  },
  compilers: {
    solc: {
      version: "^0.8.0"
    }
  }
};


Passo 6: Migrar o Contrato
Use o Truffle para migrar o contrato para a rede Ropsten:

truffle migrate --network ropsten


Passo 7: Interagir com o Contrato
Depois de migrar o contrato, você pode usar a Metamask para interagir com ele, enviando e recebendo transações.

Passo 8: Usar o Remix IDE
Você também pode usar o Remix IDE para compilar e implementar o contrato diretamente no navegador. Siga os passos:

Copie o código do contrato e cole no Remix IDE.
Compile o contrato.
Conecte-se ao Metamask e implemente o contrato.
