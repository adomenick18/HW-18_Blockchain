# HW-18_Blockchain

## Steps to set up and use ADOMNET:

1. Navigate to https://download.mycrypto.com/ and download the MyCrypto App.
2. Navigate to https://geth.ethereum.org/downloads/, scroll down to "Stable Releases" and install the 64-bit "Geth & Tools 1.9.7".
3. Update your conda and create a new environment (if you have not done so already) called "adomnet".  I've called mine "ethereum", but that's the blockchain of the past. 
    - In this environment, pip install web3 and bit packages.
    - You will then have to install Microsoft Visual C++ Build Tools in Windows (our company only uses windows computers).

    You now have your ADOMNET environment set up.

4.  This is a "Proof of Authority" blockchain, which means the consensus mechanism is done through the identity of approved addresses.  POA is easier to implement in private blockchains and delivers generally faster transactions than other consensus mechanisms.
5. From terminal, navigate to your blockchain tools folder and create two new nodes for adomnet.
    - ./geth --datadir adomnetnode1 account new
    - ./geth --datadir adomnetnode2 account new
6. Run ./puppeth and type adomnet.
    - puppeth is an Ethereum private network manager that allows you to create and manage new networks.
    - We are configuring a new genesis block and choosing Proof of Authority as the consensus algorithm
    - Add the two node addresses from the nodes you created to be prefunded.  Proof of Authority chains do not mine block rewards so the nodes need ot be pre-funded.
7. From the puppeth main menu, go to manage existing connections and export your genesis configuration.  
    - This will create a adomnet.json file that contains the node addresses as well as your randomly generated chain ID.
8. Initialize each node.
    - ./geth --datadir adomnetnode1 init adomnet.json
    - ./geth --datadir adomnetnode2 init adomnet.json
9. We will now Run the nodes in separate terminal windows with the following commands.
    - ./geth --datadir node1 --unlock "a8ced6e6d0d922c9565708fb7f2aafe56584dd42" --mine --rpc --allow-insecure-unlock
        - this command is unlocking the first node and telling it to mine.  We allow the insecure unlock so it doesn't get stuck in firewalls.  RPC = remote procedure call.
    - ./geth --datadir adomnetnode2 --unlock "73988eef3dea1334b8e86891b2b36cb619d757b8" --mine --port 30304 --bootnodes "enode://3f2639dcb3ca6b84eb4b31db77fc079434079ad099e4de70e246f6ff20fa13386350ea54e71b43d3c9bf2d09dc619bd7f6a0a7bc629737ce383467add672fc68@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
        - Similarly to node1, this command is unlocking the second node for mining (in a different port, 30304).  The bootnodes command is used to connect the peer node1 and ipcdisable has to be used for windows or else this won't work.

    NOW WE ARE MINING!

10. Go into your MyCrypto app and change the network to the custom adomnet.
    - The chain ID from the adomnet.json file is needed here.
11. Access the node1 wallet by searching for the keystore file in the adomnetnode1 folder.  This is done from the mycrypto app.
12. Retrieve the address for node2 and send money to it!
13. When the transaction is complete you can view the transaction using the hash. 



