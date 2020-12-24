---
title: Developing Splash Ad
description: 15
---

<center>
<img style="width: 150.00px " src="assets/splash.png" onclick="imageclick(src)">
</center>

<p><strong>0. Locate following line to create Initialize the HUAWEI Ads SDK! in onCreate()</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize the HUAWEI Ads SDK.
        HwAds.init(this)
<br></code></pre>

<p><strong>1. Locate following line to create SplashView, SplashAdDisplayListener and SplashAdLoadListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create splashView
    private lateinit var splashView: SplashView<br>
<span class="pln">    // TODO : create listeners
    private lateinit var adDisplayListener: SplashAdDisplayListener
    private lateinit var splashAdLoadListener: SplashAdLoadListener
<br></span></code></pre>

<p><strong>2. Locate following line to invoke Splash Ad Listeners create methods</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create Listeners
        createAdLoadListener()
        createAdDisplayListener()
<span class="pln"></span></code></pre>

<p><strong>2.1. Locate following line to create SplashAdLoadListener</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create createAdLoadListener<br>
    private fun createAdLoadListener() {
        splashAdLoadListener = object : SplashAdLoadListener() {
            override fun onAdLoaded() {
                Log.i(TAG, "SplashAdLoadListener onAdLoaded.")
            }
            override fun onAdFailedToLoad(errorCode: Int) {
                val errorMessage = AdvancedAdUtils.getDetailsFromErrorCode(errorCode)

                Log.e(TAG, "SplashAdLoadListener.onAdFailedToLoad() with errorMessage $errorMessage" )
                // jump from splahScreen to MainActivity ( call startActivity ) 
                jump()
            }
            override fun onAdDismissed() {
                Log.i(TAG, "SplashAdLoadListener onAdDismissed.")
                // jump from splahScreen to MainActivity ( call startActivity ) 
                jump() 
            }
        }
    }
<br><span class="pln"></span></code></pre>

<p><strong>2.2. Locate following line to create SplashAdDisplayListener</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create createAdDisplayListener<br>
    private fun createAdDisplayListener() {
        adDisplayListener = object : SplashAdDisplayListener() {
            override fun onAdClick() {
                Log.i(TAG, "SplashAdDisplayListener onAdShowed.");
            }
            override fun onAdShowed() {
                Log.i(TAG, "SplashAdDisplayListener onAdClick.")
            }
        }
    }
<br><span class="pln"></span></code></pre>

<p><strong>3. Locate following line to Initialize SplashView and load Ad</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : load Ad<br>
    private fun loadAd() {
        val adParam = AdParam.Builder().build()
        // Obtain SplashView.
        splashView = findViewById(R.id.splash_ad_view)
        splashView.setAdDisplayListener(adDisplayListener)

        // Set a logo image.
        splashView.setLogoResId(R.drawable.icon_ads)
        // Set logo description.
        splashView.setMediaNameResId(R.string.app_name)
        // Set the audio focus type for a video splash ad.
        splashView.setAudioFocusType(AudioFocusType.NOT_GAIN_AUDIO_FOCUS_WHEN_MUTE)
        // Load the ad. AD_ID indicates the ad slot ID.
        splashView.load(
            getString(R.string.ad_id_splash),
            ActivityInfo.SCREEN_ORIENTATION_PORTRAIT,
            adParam,
            splashAdLoadListener
        )
    }
<br><span class="pln"></span></code></pre>

<p><strong>4. Locate following line to add SplashView to XML layout file.</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // &lt;!-- TODO : add SplashView XML layout --&gt;<br>
    &lt;com.huawei.hms.ads.splash.SplashView
        android:id="@+id/splash_ad_view"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" /&gt;
<br><span class="pln"></span></code></pre>

<aside class="special"><p><strong>Note: You can use testAdId for demo ad show : <string name="ad_id_splash">testq6zq98hecj</string> </strong></p></aside>

<center>
<img style="width: 300.00px " src="assets/ss_splash.gif" onclick="imageclick(src)">
</center>