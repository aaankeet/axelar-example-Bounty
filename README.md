# Axelar Network - Bounty

Contract Address Deployed @: https://testnet.axelarscan.io/gmp/0x19f74a888b8a2e364e9e162e510f9421f58551117b2a5a177d78a11690734bae

Explanation What I did:

1. Modified call-contract-with-token's index.js with custom gasLimit and added value:(6e17) param so that the contract can receive enough gas to initiate, Like this : 

    const sendTx = await source.contract.sendToMany(destination.name, destination.distributionExecutable, accounts, 'aUSDC', amount, {
            value: BigInt(6e17),
            gasLimit: 3e5,
        });


2. Edited .env file with my Private Key.

3. Added testnets (Networks) into my metamask to track currencies (native tokens) and for verification purposes.
4. Transferd some test Native tokens (to pay the gas Fees) for each of the network axelar network mentioned in the testnet.json file & aUSDC    from the axelar discord server.
5. Deployed call-contract-with-token on testnet. using command - node scripts/deploy examples/call-contract-with-token testnet
6. ran test.js script on testnet and transferred some aUSD to two different addresses from Moonbeam to Avalanche. 
   using command - node scripts/test examples/call-contract-with-token testnet "Moonbeam" "Avalanche" {amount} {address1} {address2}
 
 How it Works -
 
 1. We call the callContractWithToken function with appropriate payload on the Axelar Gateway Contract to initiate the call.
 2. Once the call is initiated the user pays the gas fees on the source chain to axelar's gas service contract (Axelar gas services             contract is deployed for every chain eg: fantom, polygon, avalanche and others). 
 3. Then the call reaches Axelar's Gateway through that it goes to the Axelar's Network where Validators confirms the callContractWithToken     call and converts the paid gas fees from source chains's native token to destinatio Chain's native token & then Axelar Validators           prepare a signed command for the destination Chain gateway.
 4. Then the Call's gets Approved from the Axelar's Gateway.
 5. After Getting Approved Axelar services executes the dApp with the payload on the Destination chain.
 6. Thus Making the results visible on the Destination Chain.
