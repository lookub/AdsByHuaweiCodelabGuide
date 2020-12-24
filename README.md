## Table of Contents


*  [Introduction](#introduction)

*  [Installation](#installation)

*  [Configuration ](#configuration )

*  [Supported Environments](#supported-environments)

*  [Sample Code](#Sample-Code)

*  [License](#license)

## Introduction

HUAWEI Ads Publisher Service utilizes Huawei's vast user base and extensive data capabilities to deliver targeted, high quality ad content to users. With this service, your app will be able to generate revenues while bringing your users content which is relevant to them.

We offer a range of ad formats so you can choose whichever that suits your app best. Currently, you can integrate banner, native, rewarded, interstitial, splash, and roll ads, and we'll be launching even more formats in the future.

Use the HUAWEI Ads SDK to quickly integrate HUAWEI Ads into your app. Once you have chosen an ad format, you are ready to start bringing in revenue using our high-quality advertising service

Please refer to this link for more information :  [Ads Kit Guide](#https://developer.huawei.com/consumer/en/doc/HMSCore-Guides-V5/publisher-service-introduction-0000001050064960-V5) 
    
Before you use this codelab, it's assumed that you already have a HUAWEI developer account and have already created an app to implement the HMS Ads Kit.

If you haven't, please refer to  [Developers Introduction](https://developer.huawei.com/consumer/en/doc/start/introduction-0000001053446472) and  [Registration](https://developer.huawei.com/consumer/en/doc/start/registration-and-verification-0000001053628148)

## Installation

Before using HMS Ads Kit Codelab code, check whether the Android Studio environment has been installed.

Download the HMS Ads Kit Codelab project by zip or clone in Github.

Wait for the gradle build in your project.

## Supported Environments

• Android Studio 3.x or later version

• Java JDK 1.8 or later version

• EMUI 5.0 or later version

• HMS Core (APK) 5.0.1.300 or later version

• Android 4.4 or later

  

## Configuration

1. Register and sign in to HUAWEI Developers.

2. Create a project and then create an app in the project, enter the project package name.

3. Download the agconnect-services.json file and place it to the app's root directory of the project.

4. Add the Maven repository address "maven {url 'https://developer.huawei.com/repo/'}" to the project-level build.gradle file.

5. Configure the dependency "com.huawei.hms:ads-lite:13.4.36.301" in the app-level buildle.gradle file.

6. Synchronize the project.

## Sample Code

HMS Ads Kit Codelab code uses the Client structure in the project.The following describes methods in the Client structure.

1) Create and initialize SplashAd
You can obtain and use the initialized SplashAd
Code location com.hms.codelab.adskit.adsbyhuawei.SplashAdActivity.kt

2) Create and initialize BannerAd
You can obtain and use the initialized SplashAd
You can edit and customize with different BannerAd slot sizes
Code location com.hms.codelab.adskit.adsbyhuawei.BannerAdActivity.kt

3) Create and initialize InterstialAd
You can obtain and use the initialized InterstialAd
You can edit and customize with different InterstialAd slot type ( image - video )
Code location com.hms.codelab.adskit.adsbyhuawei.InterstialAdActivity.kt

4) Create and initialize RewardAd
You can obtain and use the initialized RewardAd
Code location com.hms.codelab.adskit.adsbyhuawei.RewardAdActivity.kt

5) Create and initialize NativeAd
You can obtain and use the initialized NativeAd
You can edit and customize with different NativeAd slot type ( small - image - video )
Code location com.hms.codelab.adskit.adsbyhuawei.NativeAdActivity.kt

6) Create and initialize InstreamRollAd
You can obtain and use the initialized InstreamRollAd
Code location com.hms.codelab.adskit.adsbyhuawei.InstreamRollAdActivity.kt

## License

HMS Ads Kit Codelab is licensed under the [Apache License, version 2.0](http://www.apache.org/licenses/LICENSE-2.0).