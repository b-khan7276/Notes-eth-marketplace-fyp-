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
