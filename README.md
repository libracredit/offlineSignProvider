# offlineSignProvider
This is a customized Ethereum web3-provider to facilitate separation of business layer and wallet layer
## Install

    $ npm install libra-offlinesign-provider
    
## General Usage
You can use this provider wherever a Web3 provider is needed.

    const config = require('../config');
    var Web3 = require('web3');
    var nodeUrl = 'http://127.0.0.1:8545';
    
    var web3 = new Web3(new Web3.providers.HttpProvider(nodeUrl));
    
    var abi = require("./contract.json");
    var TruffleContract = require("truffle-contract");
    
    var signServiceUrl = 'http://127.0.0.1:8080/api/pearl/v1/eth/sign_transaction';
    
    var providerNew = new OfflineSignProvider(nodeUrl, signServiceUrl, [account1,account2,...], config.aesKey, false);
    
    var contractAddress = "0xafc60ddf39e7a953c4d341f2f4a80accf3432b76";
    var myContract = TruffleContract({ abi: abi });
    myContract.setProvider(providerNew);
    myContract.defaults({ from: "0xd7358e66c2ec3e398b39567b0c9f53a8e8c6000f" });
    var web3 = new Web3(providerNew);
    
    myContract.at(contractAddress).then(function (instance) {
                    console.log(instance)
                }).catch(e => {
                    reject(e);
                });
                
Parameters:

    var providerNew = new OfflineSignProvider(nodeUrl, signServiceUrl, [account1,account2,...], config.aesKey);
    
param1: The eth network node url.
param2: The signature service url.
param3: Array format account address, that sign service will use one of them to signature the transaction data .
param4: AES key defined with the signature service.
param5: Use 0Ex or not.