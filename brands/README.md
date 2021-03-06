# Brands

After creating an account and getting access to the dashboard, the next step is to create a test **Brand** (Merchant). This lets you create locations and add them to a Program so you can start tracking transactions. 


  
The **Brand** object is used to aggregate locations and keep track of the Brand consent. To track real-time transactions at a Brand's locations, you need to obtain consent from authorised personnel (Brand Contact), and provide the Brand with access to view transactional data. You can do this when creating the Brand (see below).

Once you create a **Brand**, it cannot be deleted.

## Create Brand

![Create brand](https://raw.githubusercontent.com/FidelLimited/docs/master/assets/images/create-brand.png "Create brand")


To create a new Brand, go to the **Brands** page on the dashboard, click the **+** icon and enter a name. Optionally, you can add a link to the brand logo (Note: the logo cannot be added later).  You can also [create a Brand](https://reference.fidel.uk/reference#create-brand) with the API:
```bash
curl -X POST \
  https://api.fidel.uk/v1/brands \
  -H 'content-type: application/json' \
  -H 'fidel-key: {your Secret key}' \
  -d '{
    "name": "Brand B",
    "logoURL": "https://mycompany.com/brandlogo.png"
  }'
```

## Brand Consent

>NOTE: Brand consent is only required in the Live environment. Test Brands are automatically given Brand consent.

All brands must be approved by the authorised Brand Contact. There are two ways that brands are approved. For an external brand, you may request Brand consent either in the dashboard, or with our API. For self-funded Brands, this can be skipped by auto-approving consent.

### Requesting Brand Consent

On the dashboard, enter the name and email of the Brand Contact and Fidel will send an email inviting them to create a Brand account at [clo.fidel.uk](https://clo.fidel.uk). To request Brand Consent with the API, use the [Brand Consent Endpoint](https://reference.fidel.uk/reference#create-brand-user). After creating an account, the Brand User provides consent and will have access to transactions made by cardholders at participating locations.

<div class="info-box">
Brand Consent is only required in the Live environment. Test Brands are automatically given Brand consent.
</div>

You can monitor consent status on the dashboard and also set up a `brand.consent` webhook to be notified when the status changes.

### Auto-Approve Consent 

If you're funding your own offers, or you've received direct authorisation from a brand, you can auto-approve the brand's consent:

![Auto approve Brand](https://raw.githubusercontent.com/FidelLimited/docs/master/assets/images/autoapproveConsent.png "auto-approve brand")

Using the Brand Consent API, you can auto-approve your Brand by adding  ```skipInvite: true``` to the JSON request with the brand owner information.
