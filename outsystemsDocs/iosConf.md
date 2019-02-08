### iOS Setup
When targeting the iOS platform, in order to enable push notifications the mobile application has to be signed with push notification capabilities.

Access the Apple Developer Console and create a new App Id. Make sure to check “Push Notifications” under App Services.<details><summary>Open Image</summary><img src="imgs/image24.png"/></details><br>

Edit the created App Id and, under Push Notifications, create a new Push Notification certificate and save both the private and public certificate. In order to get a .p12 file, access your keychain and export both the public and private key.<details><summary>Open Image</summary><img src="imgs/image1.png"/></details><br>

You can now configure an application on Firebase. Access the [Firebase console](https://www.google.com/url?q=https://console.firebase.google.com/&sa=D&ust=1509368386696000&usg=AFQjCNHjP_YfTLYJdd75fHnpc5n0caW3CQ) and create a new application.<details><summary>Open Image</summary><img src="imgs/image9.png"/></details><br>

Click on “Add Firebase to your iOS app”. 

Insert the same bundle id/ app id created before on the Apple Developer Console and hit “REGISTER APP”<details><summary>Open Image</summary><img src="imgs/image20.png"/></details><br>

Download “GoogleService-Info.plist” to your machine and you can ignore the following steps. 

This file is used to configure the FirebaseCloudMessagePlugin in your application. See detailed information under “FirebaseCloudMessagePlugin Configurations” section.<details><summary>Open Image</summary><img src="imgs/image18.png"/></details><br>

Under project overview, access the application Settings<details><summary>Open Image</summary><img src="imgs/image10.png"/></details><br>

Under “CLOUD MESSAGING” tab, scroll down to APNs Authentication Key and upload the APNs certificate generated earlier.<details><summary>Open Image</summary><img src="imgs/image13.png"/></details><br>

For more detailed information see: [https://firebase.google.com/docs/cloud-messaging/ios/certs](https://firebase.google.com/docs/cloud-messaging/ios/certs)
