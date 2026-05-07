# 🚗 Car Auction Network using Hyperledger Fabric Node SDK and IBM Blockchain Starter Plan

## 📌 Aim

To create a Car Auction Network using Hyperledger Fabric Node SDK and IBM Blockchain Starter Plan, invoke chaincode transactions, and store auction data securely in the blockchain network.

---

# 🎯 Objective

* Set up IBM Blockchain Starter Plan
* Create a Hyperledger Fabric network
* Deploy chaincode for car auction
* Use Node SDK to connect blockchain application
* Invoke and query chaincode transactions
* Store auction data securely in blockchain ledger

---

# 🛠 Requirements

## Software Requirements

* Ubuntu / WSL Ubuntu
* Docker
* Docker Compose
* Node.js and npm
* Git
* Hyperledger Fabric binaries
* IBM Blockchain Starter Plan
* Visual Studio Code

---

# ⚙️ Algorithm

1. Install Hyperledger Fabric prerequisites.
2. Create IBM Blockchain Starter Plan account.
3. Download Hyperledger Fabric samples and binaries.
4. Start Hyperledger Fabric test network.
5. Create and initialize channel.
6. Deploy chaincode into blockchain network.
7. Configure Hyperledger Fabric Node SDK.
8. Write Node.js application for invoke and query.
9. Execute transactions.
10. Verify blockchain ledger output.

---

# 📂 Project Structure

```bash
car-auction-network/
│
├── app.js
├── package.json
├── wallet/
├── connection-org1.json
└── README.md
```

---

# 🚀 Installation Steps

## Step 1 — Update Ubuntu Packages

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 2 — Install Required Packages

```bash
sudo apt install git curl docker.io docker-compose nodejs npm -y
```

---

## Step 3 — Enable Docker

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Check Docker Version:

```bash
docker --version
```

---

## Step 4 — Download Hyperledger Fabric Samples

```bash
curl -sSL https://bit.ly/2ysbOFE | bash -s
```

This downloads:

* Fabric samples
* Docker images
* Fabric binaries

---

## Step 5 — Navigate to Test Network

```bash
cd fabric-samples/test-network
```

---

## Step 6 — Start Blockchain Network

```bash
./network.sh up
```

---

## Step 7 — Create Channel

```bash
./network.sh createChannel
```

Example Channel Name:

```bash
mychannel
```

---

## Step 8 — Deploy Chaincode

```bash
./network.sh deployCC -ccn auction -ccp ../asset-transfer-basic/chaincode-javascript -ccl javascript
```

### Parameters

| Parameter | Description        |
| --------- | ------------------ |
| ccn       | Chaincode name     |
| ccp       | Chaincode path     |
| ccl       | Chaincode language |

---

# 💻 Node SDK Code

## File: `app.js`

```javascript
const { Gateway, Wallets } = require('fabric-network');
const fs = require('fs');
const path = require('path');

async function main() {

    try {

        const ccpPath = path.resolve(__dirname,
        'connection-org1.json');

        const ccp = JSON.parse(fs.readFileSync(ccpPath, 'utf8'));

        const walletPath = path.join(process.cwd(), 'wallet');

        const wallet = await Wallets.newFileSystemWallet(walletPath);

        const gateway = new Gateway();

        await gateway.connect(ccp, {
            wallet,
            identity: 'appUser',
            discovery: { enabled: true, asLocalhost: true }
        });

        const network = await gateway.getNetwork('mychannel');

        const contract = network.getContract('auction');

        // Invoke Transaction
        await contract.submitTransaction(
            'CreateCar',
            'CAR001',
            'BMW',
            'Black',
            'Darane',
            '500000'
        );

        console.log('Car Auction Transaction Submitted');

        // Query Transaction
        const result = await contract.evaluateTransaction(
            'ReadCar',
            'CAR001'
        );

        console.log('Query Result:');
        console.log(result.toString());

        gateway.disconnect();

    } catch (error) {

        console.error(`Failed: ${error}`);
        process.exit(1);
    }
}

main();
```

---

# 📦 Install Dependencies

```bash
npm install fabric-network
```

---

# ▶️ Run Application

```bash
node app.js
```

---

# 📤 Expected Output

```bash
Car Auction Transaction Submitted

Query Result:
{
  "ID":"CAR001",
  "Company":"BMW",
  "Color":"Black",
  "Owner":"Darane",
  "Price":"500000"
}
```

---

# 🔍 Explanation

## Invoke Transaction

```javascript
submitTransaction()
```

Used to:

* Store auction data
* Create blockchain transaction
* Update ledger records

Example:

```javascript
CreateCar
```

---

## Query Transaction

```javascript
evaluateTransaction()
```

Used to:

* Retrieve stored blockchain data
* Verify auction records

Example:

```javascript
ReadCar
```

---

# ✅ Result

Thus, the Car Auction Network was successfully implemented using Hyperledger Fabric Node SDK and IBM Blockchain Starter Plan. Chaincode transactions were invoked successfully, and auction data was stored and retrieved securely from the blockchain ledger.

---

# 🔥 Features

* Secure blockchain transactions
* Immutable ledger records
* Distributed auction system
* Smart contract integration
* Node SDK based blockchain interaction

---

# 📚 Technologies Used

* Hyperledger Fabric
* Node.js
* Docker
* IBM Blockchain Platform
* JavaScript

---

# 👨‍💻 Author

**Darane**

Cyber Security Student 🚀
