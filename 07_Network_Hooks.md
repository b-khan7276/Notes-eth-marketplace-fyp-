# Network Hooks

- I will use network hook to show the etherum network 
- I will be displaying actual network to the user he is connect to metamask 
- I will make new file in `providers/web3/hooks` call `useNetwork.js`

## Showing the chain of the network 
- To show the chain of the network  I made to files 
- And I write the variable network to display the newwork keys

```js 
const NETWORKS = {
  1: "Ethereum Main Network",
  3: "Ropsten Test Network",
  4: "Rinkeby Test Network",
  5: "Goerli Test Network",
  42: "Kovan Test Network",
  56: "Binance Smart Chain",
  1337: "Ganache",
}
```
- I will also set the target network
# Displaying message
- I will also set the messege if user is connected to the worng network
- And I will pass data to display on page 

# Displaying install require message
- I will display a red message of install meta mask if user do not have installed meta mask 
- I will made propertry to display install 
