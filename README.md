
# react-native-custom-billing

## Getting started

`$ npm install react-native-custom-billing --save`

### Mostly automatic installation

`$ react-native link react-native-custom-billing`

### Manual installation


#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
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


## Usage
```javascript
import RNCustomBilling from 'react-native-custom-billing';

// TODO: What to do with the module?
RNCustomBilling;
```
  