# Rave's Android Drop In UI

Rave's Android Drop-In is a readymade UI that allows you to accept card and bank payments in your Android app.

<img alt="Screenshot of Drop-In" src="https://firebasestorage.googleapis.com/v0/b/saveup-9e594.appspot.com/o/Group.png?alt=media&token=e0c89192-b2a4-47e0-a883-3a78005acd2a" width="600"/>

## Before you begin
- [Create your Rave staging keys from the sandbox environment](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-staging-keys-from-the-rave-sandbox-environment)
- [Create your Rave live keys from the Rave Dashboard](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-live-keys-from-the-rave-dashboard)

## Requirements


The minimum supported SDK version is 15

## Adding it to your project


**Step 1.** Add it in your root build.gradle at the end of repositories:

    allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}

**Step 2.** Add the dependency

    dependencies {
	     implementation 'com.github.Flutterwave:rave-android:1.0.40'
	}

**Step 3.** Add the required permission

Add the `READ_PHONE_PERMISSION` and `INTERNET` permissions to your android manifest

     <uses-permission android:name="android.permission.READ_PHONE_STATE" />
     <uses-permission android:name="android.permission.INTERNET" />

> **REQUIRED PERMISSION**
> This library requires the **READ_PHONE_PERMISSION** to get the build number for fraud detection and flagging as recommended here https://developer.android.com/training/articles/user-data-ids.html#i_abuse_detection_detecting_high_value_stolen_credentials

## Usage

###  1. Create a `RavePayManager` instance
Set the public key, encryption key and other required parameters. The `RavePayManager` accepts a mandatory instance of  the calling `Activity`

        new RavePayManager(activity).setAmount(amount)
                        .setCountry(country)
                        .setCurrency(currency)
                        .setEmail(email)
                        .setfName(fName)
                        .setlName(lName)
                        .setNarration(narration)
                        .setPublicKey(publicKey)
                        .setEncryptionKey(encryptionKey)
                        .setTxRef(txRef)
                        .acceptAccountPayments(boolean)
                        .acceptCardPayments(boolean)
                        .acceptMpesaPayments(boolean)
                        .acceptAchPayments(boolean)
                        .acceptGHMobileMoneyPayments(boolean)
                        .acceptUgMobileMoneyPayments(boolean)
                        .acceptZmMobileMoneyPayments(boolean)
                        .acceptRwfMobileMoneyPayments(boolean)
                        .acceptUkPayments(boolean)
                        .acceptBankTransferPayments(boolean)
                        .acceptUssdPayments(boolean)
                        .onStagingEnv(boolean)
                        .setMeta(List<Meta>)
                        .withTheme(styleId)
                        .isPreAuth(boolean)
                        .setSubAccounts(List<SubAccount>)
                        .shouldDisplayFee(boolean)
                        .showStagingLabel(boolean)
                        .initialize();

| function        | parameter           | type | required  |
| ------------- |:-------------:| -----:| -----:|
| setAmount(amount)      |  This is the amount to be charged from card/account | `double` | Required
| setCountry(country)     | This is the route country for the transaction with respect to the currency. You can find a list of supported countries and currencies [here](https://flutterwavedevelopers.readme.io/docs/multicurrency-payments) | `String` | Required
| setCurrency(currency) | This is the specified currency to charge the card in | `String` | Required
| setfName(fName) | This is the first name of the card holder or the customer  | `String` | Required
| setlName(lName) | This is the last name of the card holder or the customer | `String` | Required
| setEmail(email) | This is the email address of the customer | `String` | Required
| setNarration(narration) | This is a custom description added by the merchant. For `Bank Transfer` payments, this becomes the account name of the account to be paid into. See more details [here](https://developer.flutterwave.com/v2.0/reference#pay-with-bank-transfer-nigeria). | `String` | Not Required
| setPublicKey(publicKey) | Merchant's public key. Get your merchant keys here for [ staging](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-staging-keys-from-the-rave-sandbox-environment) and [live](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-live-keys-from-the-rave-dashboard)| `String` | Required
| setEncryptionKey(encryptionKey) | Merchant's encryption key. Get your merchant keys here for [ staging](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-staging-keys-from-the-rave-sandbox-environment) and [live](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-live-keys-from-the-rave-dashboard) | `String` | Required
| setTxRef(txRef) | This is the unique reference, unique to the particular transaction being carried out. It is generated by the merchant for every transaction | `String` | Required
| acceptAccountPayments(boolean) | Set to `true` if you want to accept payments via bank accounts, else set to `false`. | `boolean` | Not Required
| acceptCardPayments(boolean) | Set to `true` if you want to accept payments via cards, else set to `false` | `boolean` | Not Required |
| acceptMpesaPayments(boolean) | Set to `true` if you want to accept Mpesa payments, else set to `false` . For this option to work, you should set your country to `KE` and your currency to `KES` | `boolean` | Not Required |
| acceptGHMobileMoneyPayments(boolean) | Set to `true` if you want to accept Ghana mobile money payments, else set to `false` . For this option to work, you should set your country to `GH` and your currency to `GHS`| `boolean` | Not Required |
| acceptUgMobileMoneyPayments(boolean) | Set to `true` if you want to accept Uganda mobile money payments, else set to `false` . For this option to work, you should set your country to `UG` and your currency to `UGX`| `boolean` | Not Required |
| acceptZmMobileMoneyPayments(boolean) | Set to `true` if you want to accept Zambia mobile money payments, else set to `false` . For this option to work, you should set your country to `NG` and your currency to `ZMW`. `MTN` is the only available network at the moment, see more details in the [API documentation](https://developer.flutterwave.com/reference#zambia-mobile-money).| `boolean` | Not Required |
| acceptRwfMobileMoneyPayments(boolean) | Set to `true` if you want to accept Rwanda mobile money payments, else set to `false` . For this option to work, you should set your country to `NG` and your currency to `RWF`. See more details in the [API documentation](https://developer.flutterwave.com/reference#rwanda-mobile-money).| `boolean` | Not Required |
| acceptUkPayments(boolean) | Set to `true` if you want to accept UK Bank Account payments, else set to `false` . For this option to work, you should set your country to `NG`, set currency to `GBP`, set accountbank `String`, set accountname `String`, set accountnumber `String`, set is_uk_bank_charge2 `true`, set payment_type `account`. `Please use your live credentials for this` | `boolean` | Not Required |
| acceptAchPayments(boolean) | Set to `true` if you want to accept US ACH charges from your customers, else set to `false` . For this option to work, you should set your country to `US` and your currency to `USD`. You also have to set `acceptAccountPayments(true)`| `boolean` | Not Required |
| acceptBankTransferPayments(boolean) | Set to `true` if you want to accept payments via bank transfer from your customers, else set to `false`. This option is currently only available for Nigerian Naira. <br/><br/><strong>Note:</strong> By default, the account numbers generated are dynamic. This method has been overloaded for more options as shown below:<br><ul><li>To generate static (permanent) accounts instead, pass in `true` as a second parameter. E.g. <br/>```acceptBankTransferPayments(true, true)```</li><li>To generate accounts that expire at a certain date, or after a certain number of payments, pass in integer values for `duration` and `frequency` as such: <br/>```acceptBankTransferPayments(true, duration, frequency)``` </li></ul>You can get more details in the [API documentation](https://developer.flutterwave.com/v2.0/reference#pay-with-bank-transfer-nigeria).| `boolean`<br/><br/>Optional overloads:<br/>`boolean`, `boolean`<br/>`boolean`, `int`, `int` | Not Required |
| acceptUssdPayments(boolean) | Set to `true` if you want to accept payments via USSD transfer from your customers, else set to `false` . This option is currently only available for the Nigerian Naira.| `boolean` | Not Required |
| onStagingEnv(boolean) | Set to `true` if you want your transactions to run in the staging environment otherwise set to `false`. Defaults to false  | `boolean` | Not Required
| setMeta(`List<Meta>`) | Pass in any other custom data you wish to pass. It takes in a `List` of `Meta` objects | List<Meta> | Not Required
| setSubAccounts(`List<SubAccount>`) | Pass in a `List` of `SubAccount`,if you want to split transaction fee with other people. Subaccounts are your vendors' accounts that you want to settle per transaction. To initialize a `SubAccount` class, do `SubAccount(String subAccountId,String transactionSplitRatio)` or `SubAccount(String subAccountId,String transactionSplitRatio,String transactionChargeType, String transactionCharge)` to also charge the subaccount a fee. [Learn more about split payments and subaccounts](https://developer.flutterwave.com/docs/split-payment).| `List<SubAccount>`| Not Required
| setIsPreAuth(boolean) | Set to `true` to preauthorise the transaction amount. [Learn more about preauthourization](https://developer.flutterwave.com/v2.0/reference#introduction-1). | `int` | Not Required
| withTheme(styleId) | Sets the theme of the UI. | `int` | Not Required
| setPaymentPlan(payment_plan) | If you want to do recurrent payment, this is the payment plan ID to use for the recurring payment, you can see how to create payment plans [here](https://flutterwavedevelopers.readme.io/v2.0/reference#create-payment-plan) and [here](https://flutterwavedevelopers.readme.io/docs/recurring-billing). This is only available for card payments | `String` | Not Required
| shouldDisplayFee(boolean) | Set to `false` to not display a dialog for confirming total amount(including charge fee) that Rave will charge. By default this is set to `true` | `boolean` | Not Required
| showStagingLabel(boolean) | Set to `false` to not display a staging label when in staging environment. By default this is set to `true` | `boolean` | Not Required
| initialize() | Launch the Rave Payment UI  |  N/A | Required

###  2. Handle the response
In the calling activity, override the `onActivityResult` method to receive the payment response as shown below

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        /*
         *  We advise you to do a further verification of transaction's details on your server to be
         *  sure everything checks out before providing service or goods.
        */
        if (requestCode == RaveConstants.RAVE_REQUEST_CODE && data != null) {
            String message = data.getStringExtra("response");
            if (resultCode == RavePayActivity.RESULT_SUCCESS) {
                Toast.makeText(this, "SUCCESS " + message, Toast.LENGTH_SHORT).show();
            }
            else if (resultCode == RavePayActivity.RESULT_ERROR) {
                Toast.makeText(this, "ERROR " + message, Toast.LENGTH_SHORT).show();
            }
            else if (resultCode == RavePayActivity.RESULT_CANCELLED) {
                Toast.makeText(this, "CANCELLED " + message, Toast.LENGTH_SHORT).show();
            }
        }
        else {
            super.onActivityResult(requestCode, resultCode, data);
        }
    }
The intent's `message` object contains the raw JSON response from the Rave API. This can be parsed to retrieve any additional payment information needed. Typical success response can be found [here](https://gist.github.com/bolaware/305ef5a6df7744694d9c35787580a2d2) and failed response [here](https://gist.github.com/bolaware/afa972cbca782bbb942984ddec9f5262).

> **PLEASE NOTE**
>  We advise you to do a further verification of transaction's details on your server to be
 sure everything checks out before providing service or goods.

###  3. Customize the look
You can apply a new look by changing the color of certain parts of the UI to highlight your brand colors

        <style name="DefaultTheme" parent="AppTheme.NoActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <item name="OTPButtonStyle">@style/otpBtnStyle</item>
        <item name="PayButtonStyle">@style/payBtnStyle</item>
        <item name="PinButtonStyle">@style/pinButtonStyle</item>
        <item name="OTPHeaderStyle">@style/otpHeaderStyle</item>
        <item name="TabLayoutStyle">@style/tabLayoutStyle</item>
        <item name="PinHeaderStyle">@style/pinHeaderStyle</item>
        <item name="SavedCardButtonStyle">@style/svdCardsBtnStyle</item>
    </style>
## Configuring Proguard
To configure Proguard, add the following lines to your proguard configuration file. These will keep files related to this sdk
```
keepclasseswithmembers public class com.flutterwave.raveandroid.** { *; }
dontwarn com.flutterwave.raveandroid.card.CardFragment
```


##  Help
* Have issues integrating? Join our [Slack community](https://join.slack.com/t/flutterwavedevelopers/shared_invite/enQtMjU2MjkyNDM5MTcxLWFlOWNlYmE5MTIxNjAwYzc5MDVjZjNhYTJjNTA0ZTQyNDJlMDhhZjJkN2QwZGJmNWMyODhlYjMwNGUyZDQxNTE) for support
* Find a bug? [Open an issue](https://github.com/Flutterwave/rave-android/issues)
* Want to contribute? [Check out contributing guidelines]() and [submit a pull request](https://help.github.com/articles/creating-a-pull-request).

## Want to contribute?

Feel free to create issues and pull requests. The more concise the pull requests the better :)


## License

```
Rave's Android DropIn UI
MIT License

Copyright (c) 2017

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
