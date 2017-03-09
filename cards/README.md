## Cards
The Card object holds information about the card details submitted by the user using the web or mobile SDKs. One user can link multiple cards, debit or credit under the same account.

The details required to link a card to a program are the 16-digit card number, expiry date, country code and the `programId` of the Program you want to link this card to. The card number is tokenised and transmitted directly from our secure pre-built iFrame to FIDEL API. This way, your servers are never exposed to sensitive information, removing all PCI compliance requirements from your side.

FIDEL never stores the 16-digit PAN (Primary Account Number) entered by the user. To identify the user in a transaction object you should the use the `cardId` property. After this point only the `cardId` is exchanged between your servers, the card schemes and FIDEL API.

After the card is linked successfully, we will monitor any purchase made by this card on any of the program’s physical or online locations and send the transaction object to a webhook URL specified by you.

<br/>

# Add Card

To add a new card, go to the **API Playground** on the dashboard, choose **Add Card** from the left menu endpoints. The method will be set to POST and the endpoint to **_/cards_**. An editable sample JSON object like the one displayed below will be used to create the card. In order to add a card from the Playground, you’ll need to use one of the available testing card numbers displayed below. Also, provide an expiry date in the future and the `programId` you want to link this card to.

You can use the dropdown menus to automatically set the ids in the request body or copy them to use in your application code without leaving the playground.

<h5>Create sample cards in test mode using the API Playground.</h5>

![Create card](https://docs.fidel.uk/assets/images/create-card.png "Create card")

<br/>

If the card is successfully linked, the newly created card object is returned in JSON and displayed in the response body box. You can also use the [Web SDK](/web) to create cards in the test environment using your test API key. If an error occurs on the card creation, you can verify the error message in the HTTP response body.

<h5>JSON Card object</h5>

```json
fileName:card.json
{
  "items": [
    {
      "id": "e3fff00f-ab85-4a0a-b572-08b464ebf67a",
      "accountId": "a30e933f-cde1-4ac1-9a5e-acd329497a48",
      "programId": "e3fff00f-ab85-4a0a-b572-08b464ebf67a",
      "provider": "mastercard",
      "type": "master-card",
      "lastNumbers": "3183",
      "expMonth": 1,
      "expYear": 2018,
      "expDate": "2018-01-01T00:00:00.000Z",
      "countryCode": "GBR",
      "mapped": true,
      "live": true,
      "created": "2017-02-13T17:02:12.535Z",
      "updated": "2017-02-13T17:17:02.833Z",
    }
  ],
  "resource": "/v1/cards",
  "status": 201,
  "execution": 2803.465225
}
```

<br/>

# Testing Card Numbers
Note that on the Playground you can only create cards in test mode. In live mode new cards can only be linked to programs using the SDKs. Use the following test card numbers to test card linking in test mode, either in the Playground or using the SDKs with the live API key.

<h5>Visa testing card numbers</h5>

```json
visa: [
  '4444000000004001',
  '4444000000004002',
  '4444000000004003',
  '4444000000004004',
  '4444000000004005',
  '4444000000004006',
  '4444000000004007',
  '4444000000004008',
  '4444000000004009',
  '4444000000004010'
]
```
<h5>Mastercard testing card numbers</h5>

```json
mastercard: [
  '5555000000005001',
  '5555000000005002',
  '5555000000005003',
  '5555000000005004',
  '5555000000005005',
  '5555000000005006',
  '5555000000005007',
  '5555000000005008',
  '5555000000005009',
  '5555000000005010'
]
```