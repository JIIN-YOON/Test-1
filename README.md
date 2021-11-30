# IDIS GDK Programming Guide

## 1. Introduction
**What is G2Client GDK?**
  Using IDIS G2Client GDK, you can download real-time or recorded images from remote devices linked via a network and control various settings of the remote devices associated with real-time monitoring.
IDIS G2Client GDK does not include UI-related or drawing-related features. For this reason, an application program is required in order to print those images obtained from the G2Client GDK in a suitable format or to print OSD data.

  **Overview**

  This programming guide is designed for developers who embark on application development using IDIS G2Client GDK. This guide provides all the useful information for the development of a prgram that performs remote monitoring features such as displaying currently monitored or previously recorded images through the service connected to the network and controlling PTZ operations.
  
  This guide consists of the following: 
  + The Chapter "Getting started with the G2Client GDK" describing how to use the G2Client GDK.
  + The Chapter "g2admin" describing how to obtain device information through access to iNEX Admin service.
  + The Chapter "g2_live" describing how to obtain monitored images in real time by accessing the iNEX streaming service.
  + The Chapter "g2_play" describing how to obtain recorded images by accesesing the iNEX recording service.
  + The Chapter "Authority" describing how to batin authorities for each user account.
  + The Chapter "PTZ Control" describing how to control Pan, Tilt and Zoom operations of the camera connected to a remote device.
  
  When developing a program, please refer to the Tester Program distributed along with the G2Client GDK.
  
  
## 2. Getting Started with the G2Client GDK

  **Requirements**
 
  In order to use the G2Client GDK, the library files, G2ClientGDK.dll and the G2Sampler.dll are required. The files, /sampler/csharp/g2_define_* .cs and the /sampler/csharp/g2_* .cs included in the distributed G2ClientSDK Tester show one way of using the SDK in an explicit linking method as the wrapper classes of the G2Client GDK.
 
  **Listener Functions**
  
  There are two types of function provided by the G2Client GDK. One is with no response from the remote device and the other is with response from the remote device. When the function requesting the response from the remote device calls (e.g. request_ptz_menu), the function immediately returns whether or not the sending the request success. When the response arrives after the response has arrived from the remote device, G2Client GDK generates the callback. Even if the notification message or data from the remote device arrives, the callback occurs accordingly.
  For example, when an image from a remote device arrives, the GDK generates the callback *on_g2live_receive_frame_data*, and when status information of a remote device arrives, it shall generate the callback *on_g2live_receive_camera_status*. For an application program to be able to receive such callbacks, it is required to set up a receiving class to g2live_listener.  
  
  ```java
  class connective_live : g2live_listener
  {
    public connective_live()
    {
      _live = new g2live();
      _live.set_listener(this);
    }
    
    g2live _live;
  }
```

G2Sampler, which is a G2Client GDK's Wrapper class, registers DLL's callback functions automatically. Application program must be developed to perform appropriate actions, by registering listener from receiving g2live_listener class.  

**Application Initialization**

At the beginning of the application running with GDK, the initialization step should be needed for initializing GDK global variables.

```java
static void Main()
{
  g2main.app_initialize{G2LANGUAGE.ID.ENGLISH};
  
  // Application code
  
  g2main.app_finalize();
}
```


## 3. g2admin

**About g2admin**

The g2admin accesses ISS(iNEX) Admin service and obtains information of the device registered to the service.
Here, the obtained device information is used to access the remote device and to obtain its monitored or recorded images.

**Obtaining Device Information from Admin Service Using g2admin**

The following figure presents the general operation process of a program that implements the features such as Connection, Disconnection and obtaining device information.

