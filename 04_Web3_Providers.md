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
## Connecting to metaMask 
- I write this function inside the web3 provider

```js
  const _web3Api = useMemo(() => {
    return {
      ...web3Api,
      connect: web3Api.provider ?
        async () => {
          try {
            await web3Api.provider.request({method: "eth_requestAccounts"})
          } catch {
            location.reload()
          }
        } :
        () => console.error("Cannot connect to Metamask, try to reload your browser please.")
    }
  }, [web3Api])
  ```
  ## Is web3 Loaded 
  - To show the user if the meta mask is loaded or not I will show the button referening wethere it's working or not
  ```js 
    <span
                onClick={connect}
                className="px-8 py-3 border rounded-md text-base font-medium text-white bg-indigo-600 hover:bg-indigo-700">
                </Button> :
                <Button
                  onClick={connect}>
                  Install Metamask
              </span>
                </Button>
                
```
## Disable button 
- I will show to the user now if the metamask is not install the button will be diable 
- And the user will be linked to the page of metamask to install metamask 
```js 




import { useWeb3 } from "@components/providers"
import Link from "next/link"
import { Button } from "@components/ui/common"

export default function Footer() {
  const { connect, isLoading, isWeb3Loaded } = useWeb3()

  return (
    <section>
      <div className="relative pt-6 px-4 sm:px-6 lg:px-8">
        <nav className="relative" aria-label="Global">
          <div className="flex justify-between items-center">
            <div>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Home
                </a>
              </Link>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Marketplace
                </a>
              </Link>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Blogs
                </a>
              </Link>
            </div>
            <div>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Wishlist
                </a>
              </Link>
              { isLoading ?
                <Button
                  disabled={true}
                  onClick={connect}>
                    Loading...
                </Button> :
                isWeb3Loaded ?
                <Button
                  onClick={connect}>
                    Connect
                </Button> :
                <Button
                  onClick={() => window.open("https://metamask.io/download.html", "_blank")}>
                  Install Metamask
                </Button>
              }
            </div>
          </div>
        </nav>
      </div>
    </section>
  )
}
```
## using hooks 
- I use hooks in button to connect to meta mask easily 
 

 
