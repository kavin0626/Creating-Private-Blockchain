# CREATING PRIVATE BLOCKCHAIN

## NAME:KAVIN RAJ S

## REGISTER NUMBER:212223100019

## AIM
To create a private Ethereum blockchain, configure and connect two nodes, create Ethereum accounts, allocate Ether, and deploy and execute a smart contract using Geth and Remix IDE.

## TECHNOLOGIES USED
- Geth (Go Ethereum)
- Ethereum Blockchain
- Solidity
- Remix IDE
- Visual Studio Code
- Windows Command Prompt / PowerShell

## ALGORITHM

1. Download and install Geth with the development tools.
2. Verify the installation using the `geth` command.
3. Create a main directory named `go-ethereum`.
4. Create two node directories named `node1` and `node2`.
5. Generate Ethereum accounts for both nodes.
6. Create a genesis file named `genesis.json` with the chain ID, consensus configuration, and initial account balances.
7. Initialize both nodes using the genesis file.
8. Create a bootnode and generate its enode address.
9. Start Node 1 and Node 2 using the configured network parameters.
10. Connect Remix IDE to the private blockchain using the external HTTP provider.
11. Create and compile a Solidity smart contract.
12. Deploy the smart contract and execute its functions.
13. Verify the contract execution on the private blockchain.

## 1. INSTALLATION AND SETUP

Download Geth from:

https://geth.ethereum.org/

Verify the installation:

```bash
geth version
```

Create the project directories:

```bash
mkdir go-ethereum
cd go-ethereum

mkdir node1
mkdir node2
```

## 2. CREATE ETHEREUM ACCOUNTS

### Node 1

```bash
cd node1
geth --datadir "./data" account new
```

### Node 2

```bash
cd ../node2
geth --datadir "./data" account new
```

Save both account addresses and passwords securely.

## 3. CREATE THE GENESIS FILE

Create a file named `genesis.json` inside the main `go-ethereum` directory.

The genesis file defines the private blockchain configuration and initial account balances.

Example configuration:

```json
{
  "config": {
    "chainId": 12345678,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "istanbulBlock": 0,
    "berlinBlock": 0,
    "clique": {
      "period": 5,
      "epoch": 30000
    }
  },
  "difficulty": "1",
  "gasLimit": "8000000",
  "extradata": "0x00000000000000000000000000000000000000000000000000000000000000006b149fd7e14f04f955036b3bdf04a2c802aa74e20000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "alloc": {
    "6b149Fd7e14f04f955036b3BDf04a2c802aA74E2": {
      "balance": "3000000000000000000"
    },
    "a230DA3a4D59B70A41EACdEB586AE9aBE970fE82": {
      "balance": "3000000000000000000"
    }
  }
}
```

Replace the placeholder addresses with your actual account addresses. For Clique consensus, `extradata` must contain the properly encoded signer address.

## 4. INITIALIZE BOTH NODES

Initialize Node 1:

```bash
cd node1
geth --datadir ./data init ../genesis.json
```

Initialize Node 2:

```bash
cd ../node2
geth --datadir ./data init ../genesis.json
```

## 5. CREATE THE BOOTNODE

Generate a bootnode key:

```bash
bootnode -genkey boot.key
```

Start the bootnode:

```bash
bootnode -nodekey boot.key -verbosity 7 -addr "127.0.0.1:8545"
```

Save the generated enode information for node configuration.

## 6. CREATE PASSWORD FILES

Create a `password.txt` file inside both node directories.

Enter the corresponding account password in each file. Do not upload password files or private keys to GitHub.

## 7. START NODE 1

Open a terminal in the Node 1 directory and execute:

```bash
geth --datadir "./data" --port 30304 --bootnodes "YOUR_BOOTNODE_ENODE" --authrpc.port 8547 --ipcdisable --allow-insecure-unlock --http --http.addr 127.0.0.1 --http.port 8545 --http.corsdomain "https://app.remix.live,https://remix.ethereum.org" --http.api web3,eth,debug,personal,net,admin --networkid 12345678 --unlock YOUR_NODE1_ADDRESS --password password.txt --mine --miner.etherbase=YOUR_NODE1_ADDRESS
```

## 8. START NODE 2

Open another terminal in the Node 2 directory:

```bash
geth --datadir "./data" --port 30306 --bootnodes "YOUR_BOOTNODE_ENODE" --authrpc.port 8546 --networkid 12345678 --unlock YOUR_NODE2_ADDRESS --password password.txt
```

Replace the placeholders with your actual bootnode enode and account addresses.

## 9. CONNECT REMIX IDE

Open Remix IDE:

https://app.remix.live/

1. Select **Deploy & Run Transactions**.
2. Choose **Custom - External HTTP Provider**.
3. Enter the RPC URL:

```text
http://127.0.0.1:8545
```

4. Connect to the private Ethereum blockchain.
5. Create a new Solidity file named `New.sol`.

## 10. SMART CONTRACT PROGRAM

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

contract New {
    string name;

    function setName(string memory _name) public {
        name = _name;
    }

    function getName() public view returns (string memory) {
        return name;
    }
}
```

## 11. COMPILE AND DEPLOY THE CONTRACT

1. Open the Solidity Compiler in Remix.
2. Select compiler version `0.8.19` or a compatible version.
3. Compile `New.sol`.
4. Open the Deploy & Run Transactions tab.
5. Select the compiled `New` contract.
6. Click **Deploy**.
7. Confirm that the contract is deployed successfully.

## 12. EXECUTE AND VERIFY

### Set Name

Call the `setName()` function and enter:

```text
Kavin
```

Submit the transaction and wait for it to be mined.

### Get Name

Call the `getName()` function.

Expected output:

```text
Kavin
```

## OUTPUT

## Bootnode Execution
  <img width="1337" height="913" alt="image" src="https://github.com/user-attachments/assets/61cb1944-b7ae-404a-8bde-1d0e4a355018" />
## Remix IDE Connection
<img width="1590" height="1007" alt="image" src="https://github.com/user-attachments/assets/a253728d-07ba-4482-83c6-eef992960b60" />
## Smart Contract Deployment
 <img width="1507" height="845" alt="image" src="https://github.com/user-attachments/assets/3f8392fd-30e1-4360-aff0-9f119cfeef2d" />
 ## . Contract Execution
<img width="1816" height="926" alt="image" src="https://github.com/user-attachments/assets/49f81980-b3c9-4baf-b557-6300da04164b" />





## RESULT

Thus, a private Ethereum blockchain was successfully created using Geth. Two nodes were configured and connected, Ethereum accounts were created, and a Solidity smart contract was successfully deployed and executed using Remix IDE.
