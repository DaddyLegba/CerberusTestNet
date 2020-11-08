# Cerberus Test Net

Cerberus Test Net is a dev-friendly testing ground used for applications being built on top of and within Cerberus net [a next-generation blockchain that leverages the in-game digital asset Embyr (EXC) and our bridge token Embyr-X (EXT) which is used for settlement when executing smart contracts]. We invite vendors and innovators to test projects designed to increase not only liquidity within the Cerberus universe, but also create new and unique use cases for EXC and EXT within and outside of the Cerberus ecosystem.

## Features

- A testing ground for developers who want to utilize tEXC with Flare's tFXRP, and $gZil to run applications before risking actual value.

- A network where creators test applications that directly connect within the ecosystem of "Project: Embyr". Further details can be found via the command lines: 

###     Embyr:
```
https://github.com/Embyr/Embyr.git 
```

ref: https://github.com/Embyr/Embyr.git

## Get Started with XRP and ZIL on Cerberus Test Net

This repo can be downloaded via the commandline:
```
https://github.com/Embyr/CerberusTestNet.git
```
You can navigate to the `CerberusTestNet` repo using:
```
cd CerberusTestNet
```

Cerberus Net leverages Node.js for its faucet and also for Web3 applications such as Truffle. Install Node.js v8 or higher (Node.js v10.19.0 LTS is recommended) using a package manager [here](https://nodejs.org/en/download/package-manager/). After installing Node.js, check the version of the node binary from the terminal command line using: `node --version` or `node -v`. On some platforms, the binary is named nodejs instead: `nodejs --version` or `nodejs -v`.

Coston uses Yarn to manage dependencies; Yarn v1.13.0 is recommended and can be installed [here](https://classic.yarnpkg.com/en/docs/install#debian-stable). After you have installed Yarn, you can check the version of the yarn binary from a command line: `yarn --version` or `yarn -v`.

Use Yarn to install Cerberus Net dependencies:
```
yarn
```


### Use the Cerberus Faucet

To get test-XRP onto Cerberus Net, you'll first have to generate XRPL Testnet credentials [here](https://xrpl.org/xrp-testnet-faucet.html). After you've generated the credentials, you can run the faucet system which transfers 500 test-XRP to Cerberus Net:
```
node faucet.js
```

This program will ask for the XRPL Testnet credentials that you generated in the previous step, use these credentials to transfer value to the Coston network, and then save your Coston network credentials in a file called: `CerberusNetAccount.json`. 

### ZIL on [Zillet]

[Zillet] is an in-browser wallet & gateway to blockchain apps. [Zillet] can be downloaded [here](https://zillet.io/). Once you've completed storing your JSON private key in a [*secure location*](https:cerberusnet.zil/opsec-tips), you'll be ready to connect your test wallet with the Cerberus test net.

### Connecting

Click the network drop-down button located at the top right corner of the test app. Select the 'Custom RPC' option and entering the following fields:

- Network Name: `Cerberus Test Network`
- New RPC URL: `http://coston.flare.network:9650/ext/bc/C/rpc`
- Symbol: `tEXC`

After you have created and toggled to the test network, you can now load in your Coston network credentials to MetaMask that were saved in the previous step to `costonAccount.json`. In MetaMask, click the 'My Accounts' button in the top-right corner of the app, navigate to 'Import Account' and then paste in your Coston network private key. After your account has loaded, you can refresh MetaMask by selecting the Coston Test Network RPC endpoint again in the network drop-down menu. Your balance of tokens on the Coston network should then appear as:

![XRP on MetaMask](https://github.com/flare-eng/coston/blob/master/costonMetaMask.png)

### Smart Contracts with XRP

Coston is compatible with the latest Ethereum Virtual Machine functionality, including the complete [Web3](https://web3js.readthedocs.io/en/v1.2.7/) suite of tools such as [Truffle](https://www.trufflesuite.com/truffle). Truffle was automatically installed earlier as a dependency using Yarn. To get started testing out a Truffle smart contract project on Coston, you can download this example project called MetaCoin:

```
git clone https://github.com/truffle-box/metacoin-box.git
```
After the project has been downloaded, its deployment configuration can be updated for Coston using:
```
cd metacoin-box
cp ../truffle-config.js truffle-config.js
```
Deploy the smart contract project to Coston using:
```
truffle migrate --network coston --reset
```
After the deployment is complete, you can interact with the Truffle development console using:
```
truffle console --network coston
```
After opening the Truffle development console, you can interact with the MetaCoin smart contract project using the following commands. Begin by establishing both the deployed MetaCoin contract instance and the Coston account that you sent XRP to in an earlier step:
```
truffle(coston)> let instance = await MetaCoin.deployed()
truffle(coston)> let accounts = await web3.eth.getAccounts()
```
Generate a new account:
```
truffle(coston)> let newAccount = web3.eth.accounts.create()
truffle(coston)> accounts[1] = newAccount.address
```
Check the metacoin balance of the account that deployed the contract:
```
truffle(coston)> let balance = await instance.getBalance(accounts[0])
truffle(coston)> balance.toNumber()
```
See how much FXRP that balance is worth (and note that the contract defines a metacoin to be worth 2 FXRP):
```
truffle(coston)> let fxrp = await instance.getBalanceInEth(accounts[0])
truffle(coston)> fxrp.toNumber()
```
Transfer some metacoin from one account to another:
```
truffle(coston)> instance.sendCoin(accounts[1], 500)
```
Check the balance of the account that received the metacoin:
```
truffle(coston)> let received = await instance.getBalance(accounts[1])
truffle(coston)> received.toNumber()
```
Check the balance of the account that sent the metacoin:
```
truffle(coston)> let newBalance = await instance.getBalance(accounts[0])
truffle(coston)> newBalance.toNumber()
```

### Continue learning
This quickstart showed you the basics of the Truffle project lifecycle, but there is much more to learn. Please continue on with the rest of Truffle's [documentation](https://www.trufflesuite.com/docs) and especially the [tutorials](https://www.trufflesuite.com/tutorials) to learn more.
