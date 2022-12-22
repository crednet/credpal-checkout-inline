# CredPal Inline Checkout

Quickly embed CredPal Checkout in your website using our Inline JavaScript integration flow



Below is a basic example of how to embed our plugin in your website.

add our minified js script to your head file in your website
```html
<head>
 <script
  type="text/javascript"
  src="https://corporate-loans.s3.amazonaws.com/minifiedJS/index.js"
 ></script>
</head>
```

Initialize our checkout using details of your payment, this includes the amount of the transaction, a discription of the product, your Merchant key gotten from your Credpal Dashboard, then callback functions to check the status if your transaction.

```javascript
 const checkout = new Checkout({
   key: 'Your Key', // Your Key
   amount: 50000,
   product: 'Macbook Pro',
   onClose: () => console.log('Widget closed'),
   onLoad: () => console.log('Widget loaded successfully'),
   onError: (error) => console.log(error)
   onSuccess: (data) => {
    success(data);
    checkout.close();
   },
  });
 checkout.setup();
  ```

Call the open method to open CredPal's popup.
```javascript
checkout.open();
```


Below is a full example, you can try it out using the following link


```html
<head>
 <script
  type="text/javascript"
  src="https://corporate-loans.s3.amazonaws.com/minifiedJS/index.js"
 ></script>
</head>

<button onclick="payWithCredPal()" type="button">Pay With CredPal</button>

<script>
 const payWithCredPal = () => {
  const checkout = new Checkout({
   key: 'Your Key', // Your Key
   amount: 50000,
   product: 'Macbook Pro',
   onClose: () => console.log('Widget closed'),
   onLoad: () => console.log('Widget loaded successfully'),
   onError: (error) => console.log(error)
   onSuccess: (data) => {
    success(data);
    checkout.close();
   },
  });
  checkout.setup();

  return checkout.open();
 };

 const success = (data) => console.log(data); // callback function
</script>
```

`onSuccess` response
If you specified a `onSuccess` function in your request, we will send you a response like the one below. when the transaction is successfully completed:

```javascript
{
    order_no: 'ORD_619E5B5C1F672',
    item: 'Iphone X',
    amount: 600000,
    status: 'success', // status can also be pending
    channel: 'checkout',
    customer: {
        full_name: 'John Doe',
        email: 'johndoe@gmail.com',
        phone_no: '+234810383....'
    },
    created_at: '2021-11-28 14:43:20'
}
```

`onError` response
If you specified a `onError` function in your request, we will send you a response like the one below. when the transaction failed:

```javascript
{
    success: false,
    message: 'Error Message'
}
```
