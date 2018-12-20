# Mobrand android monetization SDK

## Context
 * This documentation is intended to help you integrate Mobrand's android monetization SDK.

## Getting started
 * Before starting to monetize with mobrand you will need a publisher account. You can [login] or [register] on our site.
 * create or get the id of the [apps] your wish to monetize, the id will be required later on.

[login]: https://www.mobrand.com/console/login
[register]: https://www.mobrand.com/welcome/register.html
[apps]: https://www.mobrand.com/console/monetize/apps/

## Android Native
If you want to use the Mobrand monetization SDK natively on your android app this guide is for you.

 Add the Mobrand monetization SDK on your gradle dependencies :

    implementation 'com.mobrand:android-sdk:1.0.6'

### Banner Ads

Add AdView to the layout

    <com.mobrand.sdk.MobrandBanner
        android:id="@+id/mobrand_ad"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center">
    </com.mobrand.sdk.MobrandBanner>

Banner sizes
 * You can pick any of the 3 banner sizes provided by mobrand.

| Banner Type         | Size in dp (WxH)	         |
| ------------- |-------------|
| MobrandBanner        | 320x50  |
| MobrandLargeBanner       | 320x100      |
| MobrandFullBanner | 468x60     |

* Changing the banner type will change the size of the banner, custom banner size are not yet available.

Load an ad

* call fetchAd() and pass in your appid , remember you can get the id [here]

[here]: https://www.mobrand.com/console/monetize/apps/

        MobrandBanner banner = findViewById(R.id.mobrand_ad);
        banner.fetchAd("431tXmgwTyK8OBCGbpys8Q");

Your app is now ready to display the Mobrand banner ads.

### Interstitial Ads

Update your AndroidManifest.xml

    <activity android:name="com.mobrand.sdk.intersitial.InterstitialActivity" />

Create the interstitial and call fetchAd() and pass in your appid , remember you can get the id [here]

[here]: https://www.mobrand.com/console/monetize/apps/

    mInterstitial = new InterstitialAd(this);
    mInterstitial
        .setCountDown(2)  // our default is 4
        .fetchAd("431tXmgwTyK8OBCGbpys8Q");

###### You can change the number of seconds the user needs to wait before closing the interstitial by setting the countdown

To show an interstitial, use the isLoaded() method to verify that it's done loading, then call show()

        if (mInterstitial.isLoaded()) {
            mInterstitial.show();
        } else {
            Log.d("TAG", "The interstitial wasn't loaded yet.");
        }

If you want to show the add as soon as it loads, add setShowOnload()

        mInterstitial = new InterstitialAd(this);
        mInterstitial
            .setShowOnload()    // this will open the interstitial as soon as it is loaded
            .fetchAd("431tXmgwTyK8OBCGbpys8Q");


## Admob Mediation
If you want to use the Mobrand monetization SDK using Admob mediaion on your android app this guide is for you.
This guide assumes you are already integrated and working with admob, if not, please do so [here].

[here]: https://developers.google.com/admob/android/quick-start

 Add the Mobrand Admob Mediation SDK on your gradle dependencies :

    implementation 'com.mobrand:android-admob-mediation:1.0.8'

 No further code changes are required, now all we need to do is create a [mediation group] on admob.


 Go to admob [mediation group] , and click "Create Mediation Group".

 ![Create_Mediation](http://static.mobrand.net/img/sdk//Create_Mediation.png)

 Select ad format (Banner) & platform. Rewarded formats are not available yet.
 
  ![Select_ad](http://static.mobrand.net/img/sdk//Select_ad.png)

 Configure the mediation group. Click "ADD AD UNITS" and select the ad unit that you wish to mediate.
 
  ![Add_ad_units](http://static.mobrand.net/img/sdk//Add_ad_units.png)

 On Ad Sources, click "ADD CUSTOM EVENT"
 
 ![Ad_Sources](http://static.mobrand.net/img/sdk//Ad_Sources.png) 
 
 Give it a name and the wanted eCPM.
 
 ![Add_Custom_Event](http://static.mobrand.net/img/sdk//Add_Custom_Event.png)

 Set the Class Name as "com.mobrand.mobrand.admob.mediation.MobrandEventBanner" and the Parameter with your App Id.

 ![Configure_Ads](http://static.mobrand.net/img/sdk//Configure_Ads.png)

 Click Save to save the mobrand mediation group

 [mediation group]: https://apps.admob.com/v2/mediation/groups/list?pli=1

