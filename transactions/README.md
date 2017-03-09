## Transactions
The transaction object is the central piece of data of your card-linked application. When a user makes a purchase with a linked card in any of the linked program's locations, FIDEL API spots the transaction and sends it to your server as a webhook event.

There are two types of transactions depending on the time of processing and clearing state: authorization transactions and cleared transactions. Authorization transactions are processed in real-time, when the user pays in-store (only available on MasterCard. Please email [developer@fidel.uk](mailto:developer@fidel.uk) for VISA availability). You can use the `transaction.auth` webhook event to notify or reward the user in your application in real-time.

All transactions are cleared usually 24-48 hours after the purchase by Visa and Mastercard and for consistency, FIDEL API processes cleared transactions and triggers the `transaction.clearing` webhook events daily at 12:00 UTC.

For Mastercard linked cards you will receive both `transaction.auth` events in real-time and `transaction.clearing` events. We suggest that you use the auth event to notify the user that you registered the transaction and will fulfill the reward when the transaction clears, since the clearing is the confirmation that the transaction was successfully completed.

After you received a Mastercard authorisation transaction in real-time, you will also receive the cleared transaction in the next 24-48 hours. At 12:00 UTC daily when we process the clearing transactions, we match every cleared transaction and if an authorization transaction exists we update the `cleared` property from `false` to `true`.

<br/>

# Create Transaction

For testing purposes, you can use the **API Playground** to create transactions and test your application logic.

To create a transaction you will need a test program, at least one location and a webhook event to receive the transaction object. Also, you will need a test card linked to your test program.

On the dashboard, go to **API Playground** and click on **Create transaction** from the endpoints menu. The method will be set to POST and the endpoint to **_/transactions/test_**. An editable sample JSON object like the following one will be use to create the transaction.

To create a test transaction you only need to submit three properties, the `cardId`, `locationId` and the `amount` of the transaction you want to create. You can use the dropdown menus to set these properties. If the transaction is created successfully you will see the transaction object in the response body box.

<br/>

<h5>Create sample transactions in test mode using the API Playground.</h5>

![Create transaction](https://docs.fidel.uk/assets/images/create-transaction.png "Create transaction")

<br/>

Click **Send** and a test transaction will be created and sent to the webhook URL created for this program with the event property set to `transaction.auth`. An example of the returned transaction object is displayed below.

<br/>

<h5>JSON transaction object</h5>

```json
fileName:transaction.json
{
  "items": [
    {
      "id": "7fdfd5d8-9589-402f-8477-4a727ad239a2",
      "accountId": "4ed4b62b-aa4c-43a1-8064-da6d1368e17a",
      "programId": "6e38aa0c-b7ef-46bd-b1bd-c07c648d9cba",
      "locationId": "7a916fbd-70a0-462f-8dbc-bd7dbfbea160",
      "cardId": "bc538b71-31c5-4699-840a-6d4a08693314",
      "mapId": "82c5a9ed-5301-46ab-8599-6bcb0d017cc5",
      "amount": 100,
      "currency": "GBP",
      "countryCode": "GBR",
      "scheme": "visa",
      "lastNumbers": "4001",
      "address": "2 Soho Square",
      "postcode": "W1D3PX",
      "city": "London",
      "merchantId": "12345",
      "live": false,
      "cleared": false,
      "time": "2017-03-02T19:12:01.743Z",
      "date": "2017-03-02T19:12:01.743Z",
      "created": "2017-03-02T19:12:01.744Z",
      "updated": "2017-03-02T19:12:01.744Z"
    }
  ],
  "resource": "/v1/transactions/test",
  "status": 201,
  "execution": 180.642048
}
```