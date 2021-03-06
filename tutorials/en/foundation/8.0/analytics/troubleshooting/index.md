---
layout: tutorial
title: Troubleshooting Analytics
breadcrumb_title: Troubleshooting
show_disqus: true
print_pdf: true
relevantTo: [ios,android,javascript]
weight: 7
---
### Why is there no data?
Check the following possibilities.

* Verify that your apps are set to point to the MobileFirst Server, which forwards the logs to the MobileFirst Analytics Server. Ensure that the following values are set in the mfpclient.plist (iOS), mfpclient.properties (Android), or config.xml (Cordova) files.

    ```xml
    protocol = http or https
    host = the IP address of your MobileFirst Server
    port = the HTTP port that is set in the server.xml file for reporting analytics
    wlServerContext = by default "/mfp/"
    ```

* Ensure that your MobileFirst Server is pointing to your MobileFirst Analytics Server.

    ```xml
    /analytics-service
    /analytics
    ```
    
* Check that you are calling the send method.
    * iOS: `[[WLAnalytics sharedInstance] send];`
    * Android: `WLAnalytics.send();`
    * Cordova: `WL.Analytics.send();`

### Why is there crash data in the Crash Overview table, but nothing in the Crash Summary table?
Verify that your apps are sending logs after a crash. To be safe, send logs on app start-up to ensure that any previously unsent information is reported.

### Why is there no data in the Server Usage Flow graph or the Network Request graph?
Configure your apps to collect analytics on the Network device event.

* For cross-platform apps that use Cordova, follow the iOS or Android guides, as the configurations are the same as for native apps.
* To enable the capture of network analytic data in iOS, add the following code in your Application Delegate `application:didFinishLaunchingWithOptions` method.

    ```objc
    WLAnalytics *analytics = [WLAnalytics sharedInstance];
    [analytics addDeviceEventListener:NETWORK];
    ```
  
* To enable the capture of network analytic data in Android, add the following code in your Application subclass `onCreate` method.

    ```java
    WLAnalytics.init(this);
    WLAnalytics.addDeviceEventListener(DeviceEvent.NETWORK);
    ```
    
### Why is there no data for app sessions?
Configure your apps to collect analytics on the Lifecycle device event.

* For cross-platform apps that use Cordova, follow the iOS or Android guides, as the configurations are the same as for native apps.
* To enable the capture of network analytic data in iOS, add the following code in your Application Delegate `application:didFinishLaunchingWithOptions` method.
    
    ```objc
    WLAnalytics *analytics = [WLAnalytics sharedInstance];
    [analytics addDeviceEventListener:LIFECYCLE];
    ```
    
* To enable the capture of network analytic data in Android, add the following code in your Application subclass `onCreate` method.
    
    ```java
    WLAnalytics.init(this);
    WLAnalytics.addDeviceEventListener(DeviceEvent.LIFECYCLE);
    ```
    