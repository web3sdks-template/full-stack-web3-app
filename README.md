<!-- Banner Image -->

![web3sdks solidity hardhat get started hero image](hero.png)

<h1 align='center'>Build an Application with Solidity, web3sdks & React</h1>

<p align='center'>This template extends from the <a href='https://replit.com/@web3sdks/Get-Started-with-Solidity-using-Hardhat-and-web3sdks-deploy'>Greeter contract template</a> by building an application on top of the smart contract.</p>

<br />

<b>Tools used in this template: </b>

- web3sdks [Typescript](https://docs.web3sdks.com/typescript) and [React](https://docs.web3sdks.com/react) SDKs to interact with our smart contract

- [Solidity](https://docs.soliditylang.org/en/v0.8.14/), [Hardhat](https://hardhat.org/), and [web3sdks deploy](https://docs.web3sdks.com/web3sdks-deploy) to develop, test, and deploy our smart contract.

_To learn more about the contract, check out [this template](https://replit.com/@web3sdks/Get-Started-with-Solidity-using-Hardhat-and-web3sdks-deploy)_.

<br />

<b>Run the Application:</b>

To run the web application, change directories into `application`:

```bash
cd application
```

Then, run the development server:

```bash
npm install # Install dependencies first

npm run dev
```

Visit the application at [http://localhost:3000/](http://localhost:3000/).

<br />

<h2 align='center'>How to use this template</h2>

This template has two components:

1. The smart contract development in the [contract folder](./contract).
2. The web application in the [application folder](./application).

<h3>Deploying the contract</h3>

To deploy the `Greeter` contract, change directories into the `contract` folder:

```bash
cd contract
```

Use [web3sdks deploy](https://docs.web3sdks.com/web3sdks-deploy) to deploy the contract:

```bash
npm install # Install dependencies first
npx web3sdks deploy
```

Complete the deployment flow by clicking the generated link and using the web3sdks dashboard to choose your network and configuration.

<h3>Using Your Contract</h3>

Inside the [home page](./application/pages/index.js) of the web application, connect to your smart contract inside the [`useContract`](https://docs.web3sdks.com/react/react.usecontract#usecontract-function) hook:

```jsx
// Get the smart contract by it's address
const { contract } = useContract("0x..."); // Your contract address here (from the web3sdks dashboard)
```

We configure the desired blockchain/network in the [`_app.js`](./application/pages/_app.js) file; be sure to change this to the network you deployed your contract to.

```jsx
// This is the chainId your dApp will work on.
const activeChainId = ChainId.Goerli;
```

Now we can easily call the functions of our [`Greeter`](./contract/Greeter.sol) contract, such as the `greet` and `setGreeting` contract by using the [useContractData](https://docs.web3sdks.com/react/react.usecontractdata) hook to read, and the [useContractCall](https://docs.web3sdks.com/react/react.usecontractcall) hook to write data.

```jsx
// Read the current greeting
const { data: currentGreeting, isLoading } = useContractData(contract, "greet");

// Write a new greeting
const { mutate: writeGreeting, isLoading: isWriting } = useContractCall(
  contract,
  "setGreeting"
);
```

### Connecting to user wallets

To perform a "write" operation (a transaction on the blockchain), we need to have a connected wallet, so we can use their **signer** to sign the transaction.

To connect a user's wallet, we use one of web3sdks's [wallet connection hooks](https://docs.web3sdks.com/react/category/wallet-connection). The SDK automatically detects the connected wallet and uses it to sign transactions. This works because our application is wrapped in the [`Web3sdksProvider`](https://docs.web3sdks.com/react/react.web3sdksprovider), as seen in the [`_app.js`](./application/pages/_app.js) file.

## What's next?

Learn how to use web3sdks's [Contract Extensions](https://docs.web3sdks.com/web3sdks-deploy/contract-extensions) to create your own NFT Collection smart contract + application in our [next template](https://replit.com/@web3sdks/Create-an-NFT-collection-with-Solidity-web3sdks#.replit).
