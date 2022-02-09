# Hooks:
## To show the account number on screen I use hooks in `useAccount`
```js
import { useEffect, useState } from "react"

export const handler = web3 => () => {
  const [account, setAccount] = useState(null)

  useEffect(() => {
    const getAccount = async () => {
      const accounts = await web3.eth.getAccounts()
      setAccount(accounts[0])
    }

    web3 && getAccount()
  }, [web3])

  return { account }
}
```
## Styling account  number
- I will now move account number left corner to right 
- Below the connect button 
- I will add some pading to it 
```js
  <div className="flex justify-end pt-1 sm:px-6 lg:px-8">
          <div className="text-white bg-indigo-600 rounded-md p-2">
            {account}
          </div>
        </div>
```

## Fetching data using SWR:
- To install swr
```bash
npm i swr
```
- To fetch the accounts I will use 
```js


  const { mutate, ...rest } = useSWR(() =>
    web3 ? "web3/accounts" : null,
    async () => {
      const accounts = await web3.eth.getAccounts()
      return accounts[0]
    }
  )
```
# is Admin ?
- To login in as admin I will use 
```js 
const adminAddresses = {
  "0x2Dbcb4894067D97fa9B83ED51F42Efc4f0917DE0": true
}
```
- And this function in `useAccount.js`
```js
 return {
    account: {
      data,
      isAdmin: (data && adminAddresses[data]) ?? false,
      mutate,
      ...rest
    }
  }
  ```
  
# Adding a layer of protection 
- I will  use hash keccak-256
- I will first convert my account number into hash 
```js
const adminAddresses = {
  "0x118ea763d63a0277f4e4231d487677499c7d2f33bd1c7b1ca34a5456f1687307": true
}
```

- Then I will convert the hash into the account number 
```js
  return {
    account: {
      data,
      isAdmin: (
        data &&
        adminAddresses[web3.utils.keccak256(data)]) ?? false,
      mutate,
      ...rest
    }
  }
 ```
 
