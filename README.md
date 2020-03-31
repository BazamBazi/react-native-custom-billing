InApp Billing for CafeBazaar/Myket/IranApps/Google (Android)
=============
**React Native Custom Billing** is built to provide an easy interface to InApp Billing for **CafeBazaar/Myket/IranApps/Google (Android)**,


## Getting started

`$ npm install react-native-custom-billing --save`

### Mostly automatic installation (for React Native <= 0.59 only, React Native >= 0.60 skip this as auto-linking should work)

`$ react-native link react-native-custom-billing`

### Manual installation (Skip step 1,2,3 for React Native >= 0.60)


#### Android

1. Open up `android/app/src/main/java/[...]/MainApplication.java`
  - Add `import com.customBilling.reactnative.RNCustomBillingPackage;` to the imports at the top of the file
  - Add `new RNCustomBillingPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-custom-billing'
  	project(':react-native-custom-billing').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-custom-billing/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-custom-billing')
    ```
4. Add your Vendor Name (CafeBazaar/Myket/IranApps/Google) as a line to your `android/app/src/main/res/values/strings.xml` with the name `RNCB_VENDOR_NAME`. For example:
```xml
<string name="RNCB_VENDOR_NAME">bazaar</string>
or
<string name="RNCB_VENDOR_NAME">myket</string>
or
<string name="RNCB_VENDOR_NAME">google</string>
or
<string name="RNCB_VENDOR_NAME">iranapps</string>
```
5. Add your Vendor Public key as a line to your `android/app/src/main/res/values/strings.xml` with the name `RNCB_VENDOR_PUBLIC_KEY`. For example:
```xml
<string name="RNCB_VENDOR_PUBLIC_KEY">YOUR_CAFE_BAZAAR_PUBLIC_KEY</string>
or
<string name="RNCB_VENDOR_PUBLIC_KEY">YOUR_MYKET_PUBLIC_KEY</string>
or
<string name="RNCB_VENDOR_PUBLIC_KEY">YOUR_IRAN_APPS_PUBLIC_KEY</string>
or
<string name="RNCB_VENDOR_PUBLIC_KEY">YOUR_GOOGLE_PUBLIC_KEY</string>
```
6. Add the billing permission as follows to AndroidManifest.xml file based on your Vendor (CafeBazaar/Myket/Google):
```xml
Cafe Bazaar: <uses-permission android:name="com.farsitel.bazaar.permission.PAY_THROUGH_BAZAAR"></uses-permission>
or
Myket: <uses-permission android:name="ir.mservices.market.BILLING"></uses-permission>
or
Iran Apps: <uses-permission android:name="ir.tgbs.iranapps.permission.BILLING"/>
or
Google: <uses-permission android:name="com.android.vending.BILLING"></uses-permission>
```

## Javascript API
Most of methods returns a `Promise`.

### open()

**Important:** Opens the service channel to RNCustomBilling. Must be called (once!) before any other billing methods can be called.

```javascript
import RNCustomBilling from 'react-native-custom-billing'

...

RNCustomBilling.open()
.then(() => RNCustomBilling.purchase('YOUR_SKU','DEVELOPER_PAYLOAD',RC_REQUEST))
.catch(err => console.log('Vendor err:', err))
```

### close()
**Important:** Must be called to close the service channel to RNCustomBilling, when you are done doing billing related work. Failure to close the service channel may degrade the performance of your app.
```javascript
RNCustomBilling.open()
.then(() => RNCustomBilling.purchase('YOUR_SKU','DEVELOPER_PAYLOAD',RC_REQUEST))
.then((details) => {
  console.log(details)
  return RNCustomBilling.close()
})
.catch(err => console.log('Vendor err:', err))
```

### purchase('YOUR_SKU','DEVELOPER_PAYLOAD',RC_REQUEST)
##### Parameter(s)
* **productSKU (required):** String
* **developerPayload:** String
* **rcRequest:** Integer

##### Returns:
* **Details:** JSONObject:
  * **mDeveloperPayload:**
  * **mItemType:**
  * **mOrderId:**
  * **mOriginalJson:**
  * **mPackageName:**
  * **mPurchaseState:**
  * **mPurchaseTime:**
  * **mSignature:**
  * **mSku:**
  * **mToken:**

```javascript
RNCustomBilling.purchase('YOUR_SKU','DEVELOPER_PAYLOAD',RC_REQUEST)
.then((details) => {
  console.log(details)
})
.catch(err => console.log('RNCustomBilling err:', err))
```

### consume('YOUR_SKU')
##### Parameter(s)
* **productSKU (required):** String

##### Returns:
* **Details:** JSONObject:
  * **mDeveloperPayload:**
  * **mItemType:**
  * **mOrderId:**
  * **mOriginalJson:**
  * **mPackageName:**
  * **mPurchaseState:**
  * **mPurchaseTime:**
  * **mSignature:**
  * **mSku:**
  * **mToken:**

```javascript
RNCustomBilling.consume('YOUR_SKU')
.then(...)
.catch(err => console.log('Vendor err:', err))
```

### loadOwnedItems()

##### Returns:
* **items:** JSONArray:


```javascript
RNCustomBilling.loadOwnedItems()
.then((details) => {
  console.log(details)
})
.catch(err => console.log('Vendor err:', err))
```

### loadInventory([item1_SKU,item2_SKU,...])
##### Parameter(s)
* **productSKUs (required):** Array<String>

##### Returns:
* **mPurchaseMap:** JSONObject
* **mSkuMap:** JSONObject

```javascript
RNCustomBilling.loadInventory([])
.then(...)
.catch(err => console.log('Vendor err:', err))
```

## Use event listener
Below function dispatch **Event** instead of **Promise** and return value is same.

### purchaseWithEvent('YOUR_SKU','DEVELOPER_PAYLOAD',RC_REQUEST)
### consumeWithEvent('YOUR_SKU')
### loadOwnedItemsWithEvent()


```javascript
import {DeviceEventEmitter} from 'react-native';
...
  componentDidMount(){
    DeviceEventEmitter.addListener('Vendor', function(e: Event) {
      // handle event.
      console.log(e);
    });
  }
```
