# IDIS GDK Programming Guide

1. Introduction
* What is G2Client GDK?
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
  
  
2. Getting Started with the G2Client GDK

  **Requirements**
 
  In order to use the G2Client GDK, the library files, G2ClientGDK.dll and the G2Sampler.dll are required. The files, /sampler/csharp/g2_define_* .cs and the /sampler/csharp/g2_* .cs included in the distributed G2ClientSDK Tester show one way of using the SDK in an explicit linking method as the wrapper classes of the G2Client GDK.
 
  **Listener Functions**
  
  There are two types of function provided by the G2Client GDK. 
