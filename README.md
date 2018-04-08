# google-play-purchase-validator #



### How to use? ###

````
var Verifier = require('google-play-purchase-validator');
var options = {
  email: 'gmailservice@accountemail',
  key: '-----BEGIN PRIVATE KEY-----your private key-----END PRIVATE KEY-----',
  keyFile: 'alternatively path to key file'
};
var verifier = new Verifier(options);
var receipt = {
  packageName: "de.example.com",
  productId: "subscription",
  purchaseToken: "PURCHASE_TOKEN_RECEIVED_BY_THE_USERS_DEVICE_AFTER_PURCHASE"
};
verifier.verify(receipt, function cb(err, response) {
  if (err) {
    console.log("there was an error validating the receipt");
    console.log(err);
  }
  console.log("sucessfully validated the receipt");
  /* response looks like this
  {
  "kind": "androidpublisher#subscriptionPurchase",
  "startTimeMillis": "long",
  "expiryTimeMillis": "long",
  "autoRenewing": boolean
  }*/
  console.log(response);
});
````

### How to get the credentials I need? ###
We do JWT singning for our requests send to Google. To be able to query this successfully please follow the following steps.

1. Start off by going into the google play developer console as the main Administrator of the account (this role is the only one who is allowed to perform the following steps).
1. Go to "Settings->API Access" to link a Google Developer project to this account.
1. If you are new here choose "create new project".
1. You will now have more options. Choose "Create Service Account".
1. Follow the link to the Google Developer Console and your project
1. Click "Create new client id" to create a new client ID
1. Ignore the .p12 file that will be downloaded to your machine and instead click "generate new JSON key".
1. This will download a JSON file to your machine. We will get back to that file in a second.
1. Now go back to the play store publisher account and click "done". Your new generate user will appear here.
1. Click "grant access" and grant the user rights to read your project.
1. Now setup your Node.JS project with this module and provide the email-address and the private key found in the json file as options to this module.

### I don't understand a thing. ###

Don't hesitate to contact me if this is all to brief for you. I admit I was in a hurry writing this.
