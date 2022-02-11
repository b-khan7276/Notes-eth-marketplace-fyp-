# Order
## Card Button 
- Displaying purchse button on with every item
- I added a button the card of course so that user can use that button to purchase
## Integrating model component
- In a marketplace I will add a tag of modal 
- And I will display a warring message to the user
- I will pass props and show that in marketplace

```js 

export default function Modal({isOpen}) {

  return (
    <section>
      <div className={`${!isOpen && "hidden"} fixed z-10 inset-0 overflow-y-auto"`} aria-labelledby="modal-title" role="dialog" aria-modal="true">
        <div className="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
          { isOpen &&
            <div className="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" ariaHidden="true"></div>
          }
```

- Calling props in marketpace 
```js 
      </CourseList>
      <Modal isOpen={false} />
    </>
```

## Settinup the modal 
- Now I will show the modal to the user 
- where a user can put his information to buy a course 

## Showing eth price to the user
- I will make new file in hooks by the name   `useEthPrice.js`
-  Getting data 
```js
import useSWR from "swr"

const URL = "https://api.coingecko.com/api/v3/coins/ethereum?localization=false&tickers=false&community_data=false&developer_data=false&sparkline=false"

const fetcher = async url => {
  const res = await fetch(url)
  const json = await res.json()
  return json.market_data.current_price.usd ?? null
}

export const useEthPrice = () => {
  const swrRes = useSWR(
    URL,
    fetcher,
    { refreshInterval: 1000 }
  )

  return { eth: {...swrRes}}
}
```
- Calling it in marketplace
```js 
import { useEthPrice } from "@components/hooks/useEthPrice"
```
## Adding eth image 
- Now I will add eth image along side with price of eth 
