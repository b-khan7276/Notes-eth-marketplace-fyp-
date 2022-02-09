# Web3 Providers

- I created new Folder in `components/providers/` and make new file `index.js`
- I write the code to change the global state of my web3 provider
```js
const {createContext, useContext} = require("react");


const Web3Context = createContext(null)

export default function Web3Provider({children}){
    return(
        <Web3Context.Provider value={{test: "Hello"}}>
            {children}
        </Web3Context.Provider>
    )
}

export function useWeb3(){
    return useContext(Web3Context)

}
```
- Then I create a new `index.js` file in `components/providers`
- And export the the web3 functions as 
```js
export {default as Web3Provider} from "./web3"
export {useWeb3} from "./web3"
```
- Then I wraped The `layout/base/index.js` files with my *Web3Provider*
- As so 
```js
import { Web3Provider,  } from "@components/providers"
import { Navbar, Footer } from "@components/ui/common"
export default function BaseLayout({children}){
    return(
<Web3Provider>
<div className="max-w-7xl mx-auto px-4">
         <Navbar/>
          <div className="fit">
        {children}
        </div>
        </div>
         <Footer/>
</Web3Provider>
    )
}
```
## Installing the packages for metamass and web3 providers
```bash
 npm i web3 @metamask/detect-provider
 ```
 - I write the code to check the metamass is installed in the browser or not
 ``` js
 const { createContext, useContext, useEffect, useState } = require("react");

import detectEthereumProvider from "@metamask/detect-provider";
import Web3 from "web3";

const Web3Context = createContext(null)

export default function Web3Provider({children}) {
  const [web3Api, setWeb3Api] = useState({
    provider: null,
    web3: null,
    contract: null,
    isLoading: true
  })

  useEffect(() => {
    const loadProvider = async () => {

      const provider = await detectEthereumProvider()
      if (provider) {
        const web3 = new Web3(provider)
        setWeb3Api({
          provider,
          web3,
          contract: null,
          isLoading: false
        })
      } else {
        setWeb3Api(api => ({...api, isLoading: false}))
        console.error("Please, install Metamask.")
      }
    }

    loadProvider()
  }, [])

  return (
    <Web3Context.Provider value={web3Api}>
      {children}
    </Web3Context.Provider>
  )
}

export function useWeb3() {
  return useContext(Web3Context)
}
```

 
