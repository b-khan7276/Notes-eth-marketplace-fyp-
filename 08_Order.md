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

