# Chainlink Data Streams - Streams Trade

This project uses the Streams Trade implementation of Chainlink Data Streams. This implementation uses Chainlink Automation Log Trigger to monitor for an event emission, signaling that data needs to be fetched off-chain.
How does the Streams Trade implementation work?

   An event is emitted from an emitter smart contract, which we will write and name LogEmitter.

  We will tell Automation to call a second contract when this even is emitted. When Automation detects the event has been emitted, it runs the checkLog function implemented on the second smart contract which we will write and name StreamsUpkeep. checkLog and will return a StreamsLookup custom error. Don't worry too much about this right now, we will go through this again as we write the code.

   Chainlink Automation uses the StreamsLookup custom error to retrieve a signed report from the Data Streams Aggregation Network and return the data in a callback to the performUpkeep function.

  The performUpkeep function verifies the data by calling the verify function on the Chainlink Verifier contract.
    <img width="928" height="265" alt="image" src="https://github.com/user-attachments/assets/2a44de2d-0839-4b97-b803-e1952dbeebf3" />

# We are going to write two smart contracts:

   A LogEmitter contract. This is a simple, smart contract with a single function that emits an event. Automation will pick up this Event to trigger the retrieval of the off-chain data. This function is a simple example in place of an action that a user would perform, such as minting, staking, borrowing, etc.
    A StreamsUpkeep contract. This contract will contain the Automation logic, including:

  Callback for data processing.
  Callback for error processing.
  performUpkeep function for Automation to return the data.
  We will request the ETH/USD price stream.



