# ATH Móvil Payment Button - Javascript Integration and Services

## Introduction
ATH Móvil's Javascript integration provides a simple, secure and fast checkout experience to customers paying on your website. After integrating our Payment Button on your website, you will be able to receive real time payments from more than 1.5 million ATH Móvil users.

## Prerequisites
You should have the link of athmovil_base.js for you can add in your ecommerce platform with a tag <script></script>. Also, you should have your public token, for example:
public token: a66ce73d04f2087615f6320b724defc5b4eedc55
```javascript
<script src="js/athmovil_base.js"></script>
```

## Support
If you need help signing up, adding a card or have any other question please refer to https://athmovilbusiness.com/preguntas or contact our support team at (787) 773-5466. For technical support please complete the following form:  https://forms.gle/ZSeL8DtxVNP2K2iDA.

## Installation
From your ecommerce platform you should identify whose page show the payment button, for example: "my_cart.html".
The next step is add in your tag <body></body> two scripts using <script></scrip> tag. 
The first script should have with the link of athmovil_base.js in src property, for example:  
```javascript
<script src="js/athmovil_base.js"></script>
```
The second script should have an JSON object called "ATHM_Checkout" where you should put your public token as value for the property publicToken from ATHM_Checkout object.
Also, this second script should have three callback functions:
•	authorizationATHM()
•	cancelATHM()
•	expiredATHM()

Finally, you should add in your body html a <div></div> tag with value "ATHMovil_Checkout_Button_payment" in id property.

*Example:*
```html
<body>
<div id="ATHMovil_Checkout_Button_payment"></div>
<script src="js/athmovil_base.js"></script>
<script type="text/javascript">
          const ATHM_Checkout = {
              env: 'dev',
              publicToken: 'a66ce73d04f2087615f6320b724defc5b4eedc55',
              timeout: 600,
              orderType: '',
              theme: 'btn',
              lang: 'en',
              total: 1,
              subtotal: 1,
              tax: 1,
              metadata1: 'Prueba1.1',
              metadata2: 'Prueba2.2',
              items: [
                  {
                      "name":"Nombre de arreglo",
                      "description":"Prueba de items",
                      "quantity":"3",
                      "price":"2",
                      "tax":"1",
                      "metadata":"prueba metadata"
                  }
            ],
            phoneNumber: ""
          }
          async function authorizationATHM(){
            const responseAuth = await authorization();
            console.log(responseAuth);
          }
          async function cancelATHM(){
            const responseCancel = await findPaymentATHM();
            console.log(responseCancel);
          }
          async function expiredATHM(){
            const responseExpired = await findPaymentATHM();
            console.log(responseExpired);
          }
    </script>
</body>
```

## Usage
The correct implementation of div and scripts, should show the payment button like this example:

![alt text](https://image.ibb.co/e7883o/Default.png)
 
After clicking you consume the first service "/payment", this service could response a success or an error status.

If you receive a success status, also you get a ecommerceId and auth_token into data response property and open a modal that show you a message for waiting.

### HTML