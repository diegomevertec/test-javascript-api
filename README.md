# ATH Móvil Payment Button - Javascript Integration and Services

## Introduction
ATH Móvil's Javascript integration provides a simple, secure and fast checkout experience to customers paying on your website. After integrating our Payment Button on your website, you will be able to receive real time payments from more than 1.5 million ATH Móvil users.

## Prerequisites
You should have the link of athmovil_base.js for you can add in your ecommerce platform with a tag <script></script>. Also, you should have your public token, for example:
```javascript
public token: a66ce73d04f2087615f6320b724defc5b4eedc55
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

![boton](boton.png)
 
After clicking you consume the first service "/payment", this service could response a success or an error status.

If you receive a success status, also you get a ecommerceId and auth_token into data response property and open a modal that show you a message for waiting.

```javascript
{
    "status": "success",
    "data": {
        "ecommerceId": "ad42df37-f989-11ed-8935-cd14e3558bc7",
        "auth_token": "eyJraWQiOiJNeUtVRXZvb2NSMWptbnZocHZXVEI0WmZvcU1wbEx6TWF5VzdjUWd1ck5FIiwidHlwIjoiSldUIiwiYWxnIjoiUlMyNTYifQ.eyJzdWIiOiI0MjdmOTZiMTExMmYyZGZlNTk4NjM0YWVkNmYyOTA4NmJmNWU5OTdlYjYyYTVjMDJlOTI0YTdmNTIzZDI3ZDliMzI2OGE1N2RmYWQ4ZWE3NGY1M2JhNWQzMjMyNTRkYTEiLCJmaUlkIjoiIiwibmJmIjoxNjg0ODYwNTIzLCJhenAiOltdLCJwZXJtaXNzaW9ucyI6WyJjdXN0b21lci5idXNpbmVzcy5lY29tbWVyY2UuYXV0aG9yaXphdGlvbjp3cml0ZSJdLCJpc3MiOiJQcm9jZXNzIFBheW1lbnQiLCJzY29wZXMiOlsiY3VzdG9tZXIuYnVzaW5lc3MuZWNvbW1lcmNlLmF1dGhvcml6YXRpb246d3JpdGUiXSwiZXhwIjoxNjg0ODYxNDIzLCJpYXQiOjE2ODQ4NjA1MjN9.HFPQncPDvIIqU4DeORiirntetxoU-KaRLWBK_bIAqJdR2cOWyhTTjVhVtbnCMN6qjsWB3knhp9N0aaVXPOi9DhYoWRlGVWLhSByp4K7c1fJwKFLhJoasQCew8SlXwQlalbYHt1F5s1hQgGmStGATIwnXRrE-4doBKpNedQn9CKo3qX08QGk78eAPnejzJKMlYOr__kFDR1c-L7P2btOvlx5vYDXhqmq_gljqp8f5a28pBFVh6DMx12IUu_FiQrI4ofinjiij3CWfXOVcqzBbE0UJudlS43Jb7JlZPflDrD6TM3PR4a8_KtM89Solm-r4__aIw02Gqf5ROsan_YT7FA"
    }
}
```
![screen_uno](screen_uno.png)

Immediately should open the phoneNumberATHM.html screen, here you have enter your phone number for update the transaction, this screen consume “/updatePhoneNumber” service and you should close phoneNumberATHM.html and open the waitingPaymentATHM.html screen and receive a push notification on your ATHMovil app too.

![screen_dos](screen_dos.png)

![screen_tres](screen_tres.png)

From your ATHMovil app you could confirm the transaction and later confirm it and consume the ”authorization” service automatically and should close waitingPaymentATHM.html  and show you a success message on main screen where you have a payment button.

![screen_cuatro](screen_cuatro.png)

### HTML