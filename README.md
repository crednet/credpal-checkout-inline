# CredPal Checkout Inline

Quickly embed CredPal Checkout in your website using our Inline JavaScript integration flow

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
If you specified a onSuccess function in your request, we will send you a response like the one below. when the transaction is successfully completed:

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
        phone_no: '+234810383....',
    },
    created_at: '2021-11-28 14:43:20',
}
```

`onError` response
If you specified a onError function in your request, we will send you a response like the one below. when the transaction failed:

```javascript
{
    success: false,
    message: 'Error Message',
}
```
