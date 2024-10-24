Ivan Wagner

Projeto: Criando seu Primeiro Token do Zero nos Padrões Web3

Introdução

Neste projeto, vamos criar um token personalizado do zero na blockchain Ethereum, seguindo os padrões Web3. O token será um token ERC-20, que é um padrão amplamente adotado para tokens fungíveis na blockchain Ethereum.

Pré-requisitos

Conhecimento básico de Solidity
Conhecimento básico de desenvolvimento Web3
Uma carteira Ethereum (por exemplo, MetaMask)
Um editor de código (por exemplo, Visual Studio Code)
Etapas

1. Criar um Contrato Inteligente

Crie um novo arquivo Solidity chamado MyToken.sol e adicione o seguinte código:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor(string memory name, string memory symbol) ERC20(name, symbol) {}

    function mint(address to, uint256 amount) public {
        _mint(to, amount);
    }

    function burn(address from, uint256 amount) public {
        _burn(from, amount);
    }
}
2. Compilar o Contrato Inteligente

Use um compilador Solidity para compilar o contrato inteligente. Você pode usar o compilador online da Remix IDE ou uma ferramenta de linha de comando como o solc.

3. Implantar o Contrato Inteligente

Depois de compilar o contrato inteligente, você precisa implantá-lo na blockchain Ethereum. Você pode usar uma carteira Ethereum como o MetaMask para implantar o contrato.

4. Criar uma Interface da Web

Crie uma interface da web simples para interagir com o token. Você pode usar uma estrutura como o React ou o Vue.js para criar a interface.

5. Integrar o Contrato Inteligente com a Interface da Web

Use a biblioteca Web3.js para integrar o contrato inteligente com a interface da web. Isso permitirá que os usuários interajam com o token por meio da interface.

6. Testar o Token

Após integrar o contrato inteligente com a interface da web, teste o token para garantir que ele esteja funcionando conforme o esperado. Você pode usar uma conta de teste para enviar e receber tokens.

Conclusão

Neste projeto, criamos um token personalizado do zero na blockchain Ethereum, seguindo os padrões Web3. O token pode ser usado para criar aplicativos descentralizados e outros casos de uso da Web3.

Códigos Adicionais

Interface da Web (usando React):

import React, { useState } from "react";
import Web3 from "web3";

const App = () => {
  const [web3, setWeb3] = useState(null);
  const [tokenContract, setTokenContract] = useState(null);
  const [account, setAccount] = useState(null);

  useEffect(() => {
    const initWeb3 = async () => {
      const web3 = new Web3(window.ethereum);
      setWeb3(web3);

      const accounts = await web3.eth.getAccounts();
      setAccount(accounts[0]);

      const tokenContract = new web3.eth.Contract(abi, contractAddress);
      setTokenContract(tokenContract);
    };

    initWeb3();
  }, []);

  const mintTokens = async (amount) => {
    await tokenContract.methods.mint(account, amount).send({ from: account });
  };

  const burnTokens = async (amount) => {
    await tokenContract.methods.burn(account, amount).send({ from: account });
  };

  return (
    <div>
      <h1>My Token</h1>
      <p>Account: {account}</p>
      <button onClick={() => mintTokens(100)}>Mint 100 Tokens</button>
      <button onClick={() => burnTokens(50)}>Burn 50 Tokens</button>
    </div>
  );
};

export default App;
