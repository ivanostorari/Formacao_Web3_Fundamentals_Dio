### Submissão de Proposta na DAO (JavaScript)

```
const Web3 = require('web3');
const DAOContract = require('./contracts/DAO.json'); // Abstração do contrato DAO

const web3 = new Web3('http://localhost:8545'); // Conexão local ao nó Ethereum
const daoAddress = '0x123...'; // Endereço do contrato DAO
const daoContract = new web3.eth.Contract(DAOContract.abi, daoAddress);

const submitProposal = async (title, description, amount) => {
  const accounts = await web3.eth.getAccounts();
  const sender = accounts[0];

  try {
    const result = await daoContract.methods.submitProposal(title, description, web3.utils.toWei(amount, 'ether')).send({ from: sender });
    console.log('Proposal submitted:', result);
  } catch (error) {
    console.error('Error submitting proposal:', error);
  }
}

// Exemplo de uso:
submitProposal('New Project Proposal', 'Detailed description of the project...', '10');
```
