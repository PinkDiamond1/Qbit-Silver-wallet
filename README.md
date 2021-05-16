![Optional Text](../main/feature-image.png)

# Qbit-Silver-wallet

Initial Setup
cd Qbit-Silver-wallet
yarn install
Running
node --max-old-space-size=8192 node_modules/react-native/local-cli/cli.js start (Just need to run this once to start the server, leave it running)
react-native run-android
Logging
react-native log-android

Creating a release
You need to bump the version number in:

src/Config.js - appVersion
android/app/build.gradle - versionCode and versionName
package.json - version - Not strictly required
Update user agent in android/app/src/main/java/com/Qbit-Silver-wallet/MainApplication.java and android/app/src/main/java/com/Qbit-Silver-wallet/TurtleCoinModule.java
Then either run yarn deploy-android, or:

cd android

Create an AAB
./gradlew bundleRelease

Create an APK
./gradlew assembleRelease

Deploy to device
./gradlew installRelease

Integrating QR Codes or URIs
Qbit-Silver-wallet supports two kinds of QR codes.

Standard addresses / integrated addresses - This is simply the address encoded as a QR code.

Qbit:// URI encoded as a QR code.

Your uri must begin with Qbit:// followed by the address to send to, for example, Qbit://QBC9FvxSfrfN1M8h1MmjKpYuqHTHQarhAh7y3JRkuV3ZeiAcUfe29BdKt2dvLxdAsrjK5zafRApFrKA8hFDptpR261Z6dpRsdi

There are a few optional parameters.

name - This is used to add you to the users address book, and identify you on the 'Confirm' screen. A name can contain spaces, and should be URI encoded.
amount - This is the amount to send you. This should be specified in atomic units.
paymentid - If not using integrated address, you can specify a payment ID. Specifying an integrated address and a payment ID is illegal.
An example of a URI containing all of the above parameters:

Qbit://QBC9FvxSfrfN1M8h1MmjKpYuqHTHQarhAh7y3JRkuV3ZeiAcUfe29BdKt2dvLxdAsrjK5zafRApFrKA8hFDptpR261Z6dpRsdi
amount=10000&name=McDonald's Quarter Pounder with Cheese%20Banana Milkshake&paymentid=f13adc8ac78eb22ffcee3f82e0e9ffb251dc7dc0600ef599087a89b623ca1402
This would send 20.91 QBC (2000.91 in bits) to the address QBC9FvxSfrfN1M8h1MmjKpYuqHTHQarhAh7y3JRkuV3ZeiAcUfe29BdKt2dvLxdAsrjK5zafRApFrKA8hFDptpR261Z6dpRsdi, using the name McDonald'sQuarter Pounder with Cheese Banana Milkshake(Note the URI encoding), and using a payment ID of f13adc8ac78eb22ffcee3f82e0e9ffb251dc7dc0600ef599087a89b623ca1402

You can also just display the URI as a hyperlink. If a user clicks the link, it will open the app, and jump to the confirm screen, just as a QR code would function. (Provided all the fields are given)

Developing
Trigger a background sync to fire: adb shell cmd jobscheduler run -f com.Qbit-Silver-wallet 999
