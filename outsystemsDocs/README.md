# OutSystems Mobile Plugin
The mobile plugin is largely built on top of the open source [phonegap-plugin-push plugin](https://www.google.com/url?q=https://github.com/Chuckytuh/phonegap-plugin-push/&sa=D&ust=1509368386691000&usg=AFQjCNGZ0-jauolhcodBq94sXkTsBPN79w). This plugin enables your mobile application to receive push notifications that are visible on the operating system notification center and also receive the notification data inside your OutSystems Mobile app.
## Application Behaviour
### Receiving a Push Message
The following flowchart explains how the application behaves when a push notification is received, depending on the application state.<details><summary>Open Image</summary><img src="imgs/image25.png"/></details><br>

### Push message arrives with app in foreground
The plugin receives the data from FCM service and triggers the OnNotification event on the instance of FCMCentralDispatcher WebBlock if the plugin has been successfully initialized. Additionally, no notification is shown on the notification center of the operating system since it isn’t the expected behaviour on both Android and iOS.
<br>
<br>
### Push message arrives with app in background
The plugin receives the data from FCM service and checks for the existence of a title or message in the received message payload. If it exists, the message is displayed on the notification center of the OS. 

## Setup
In order to enable push notifications on an OutSystems mobile application, some requirements must be met, specifically:
* Firebase account
* And for iOS you need:
  * A valid Apple developer account
  * Access to osx to create certificates
### [iOS Setup](iosConf.md)

### [Android Setup](androidConf.md)

## Plugin Configurations and Usage
### Plugin Initialization
FirebaseCloudMessagePlugin should be initialized as early as possible on the application life cycle. The recommended place to execute the plugin initialization process is on “OnApplicationReady” event handler.<details><summary>Open Image</summary><img src="imgs/image23.png"/></details><br>


Place a InitPushNotifications client action inside “On Application Ready” event handler. This action registers the device with Firebase Cloud Message service and initializes the plugin enabling the reception of push notifications on the device and within the application.<details><summary>Open Image</summary><img src="imgs/image22.png"/></details><br>

### Receiving Push Notifications
In order to receive push notifications on your application make use of the FCMCentralDispatcher WebBlock.

This block is responsible for dispatching OnNotification events upon push notification reception. For each received notification the following information is available:

* **Title** - the title of the notification, if available.
* **Message** - the message/body of the notification, if available.
* **Count** - the badge number sent on the notification.
* **AdditionalData** - a JSON formatted string containing any additional data sent on the notification that isn’t predefined for all push notifications. This field allows you to send custom data on the notification payload and receive that custom data inside your application.
* **Coldstart** - If the application was launched by tapping the notification.
* **Foreground** - If the application was in foreground at the moment of the notification reception.

Place this block on all pages of your application or on the layout, hook the OnNotification event and you’re all set.<details><summary>Open Image</summary><img src="imgs/image22.png"/></details><br>

### Device registration and management
Once the plugin successfully initializes, it is possible for the device to subscribe topics or to be associated with a user.

#### Topics
Topics allow an easy way of grouping many devices and to broadcast messages to that group.

The following client actions are present to deal with topics:

* **SubscribeTopic** - Subscribes to a topic by topic name. Note that if the topic was never created before or no other device has subscribed to that topic before, it might take up to 24 hours for the topic to be available.
* **UnsubscribeTopic** - Unsubscribes a topic by its name and ceases the receive any messages sent to that topic.
* **UnsubscribeTopics** - Unsubscribes to all the provided topics.

#### Users
By default, a devices is registered anonymously but it is possible to associate one or more devices with one user.

The following client actions are available to deal with device registration with a user:

* **RegisterDeviceForUser** - Registers the device with the provided user. Once a device is associated with a user, it is possible to send notifications to one or more devices associated with that user.
* **UnregisterDeviceForUser** - Unregisters the device from the currently associated user. This should be used upon user log out.

### Google-service.json /  GoogleService-Info.plist files
In order for your OutSystems Mobile application to register with FCM, these files must provided.

**Note**: Only use the file for the supported platforms or, if supporting both Android and iOS, use both google-service.json and GoogleService-Info.plist files.

On your **mobile application**, Import google-service.json and/or GoogleService-Info.plist files and make sure to:

* Set “Deploy Action” to “Deploy to Target Directory”
* Set the “Target Directory” to “google-services”. **This is very important!**<details><summary>Open Image</summary><img src="imgs/image22.png"/></details><br>

## Firebase Cloud Message Middleware
Server side application responsible for managing device registrations with users and to provide a way to push notifications to devices.

### Available server actions to send notifications:

SendNotificationToTopic - Allows to broadcast a message to a topic.
SendNotificationToUser -  Allows to send a message to all devices associated with a user.
SendNotificationToUsers - Allows to send a message to a group of users.

### [Android Features](androidFeatures.md)
