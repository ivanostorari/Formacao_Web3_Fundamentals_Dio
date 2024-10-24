### Interface de Usuário para DAO (React.js)

import React, { useState, useEffect } from 'react';
import { ethers } from 'ethers';
import VotingContract from './contracts/Voting.json'; // Abstração do contrato Voting

const App = () => {
  const [contract, setContract] = useState(null);
  const [account, setAccount] = useState(null);
  const [candidate, setCandidate] = useState('');
  const [loading, setLoading] = useState(false);
  const [message, setMessage] = useState('');

  useEffect(() => {
    init();
  }, []);

  async function init() {
    try {
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const signer = provider.getSigner();
      const network = await provider.getNetwork();
      const contractAddress = VotingContract.networks[network.chainId].address;
      const votingContract = new ethers.Contract(contractAddress, VotingContract.abi, signer);
      setContract(votingContract);

      const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
      setAccount(accounts[0]);
    
    } catch (error) {
      console.error('Error initializing app:', error);
    }
  }

  async function handleVote() {
    setLoading(true);
    try {
      await contract.vote(ethers.utils.formatBytes32String(candidate));
      setMessage('Voted successfully!');
    } catch (error) {
      console.error('Error voting:', error);
      setMessage('Error voting. Check console for details.');
    }
    setLoading(false);
  }

  return (
    <div>
      <h1>Decentralized Voting App</h1>
      {account && <p>Connected account: {account}</p>}
      <input type="text" value={candidate} onChange={(e) => setCandidate(e.target.value)} placeholder="Enter candidate name" />
      <button onClick={handleVote} disabled={loading || !candidate}>Vote</button>
      {message && <p>{message}</p>}
    </div>
  );
}

export default App;

