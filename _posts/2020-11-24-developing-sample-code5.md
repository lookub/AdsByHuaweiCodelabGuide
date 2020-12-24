---
title: Developing Banner Ad
description: 15
---

<center>
<img style="width: 150.00px " src="assets/banner.png" onclick="imageclick(src)">
</center>

<p><strong>1. Locate following line to ad BannerView and FrameLayout to XML layout file.</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // &lt;!-- TODO : add BannerView and FrameLayout XML layout --&gt;<br>
    &lt;FrameLayout
        android:id="@+id/ad_frame"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toTopOf="@id/hw_banner_view"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" /&gt;

    &lt;com.huawei.hms.ads.banner.BannerView
        android:id="@+id/hw_banner_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        hwads:adId="testw6vs28auh3"
        hwads:bannerSize="BANNER_SIZE_360_57" /&gt;
<br><span class="pln"></span></code></pre>

<aside class="special"><p><strong>Note: You can use testAdId for demo ad show : <string name="ad_id_banner">testw6vs28auh3</string> </strong></p></aside>

<p><strong>2. Locate following line to create BannerView, FrameLayout and AdListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create BannerView
    private lateinit var bannerView: BannerView<br>
    // TODO : create FrameLayout
    private lateinit var adFrameLayout: FrameLayout
<span class="pln">
    // TODO : create listeners
    private lateinit var adListener: AdListener
<br></span></code></pre>

<p><strong>3. Locate following line to Initialize BannerView, FrameLayout</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize FrameLayout
    adFrameLayout = findViewById(R.id.ad_frame)<br>
    // TODO : initialize BannerView
    bannerView = findViewById(R.id.hw_banner_view)
<br><span class="pln">
</span></code></pre>


<p><strong>4. Locate following line to Initialize AdListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize AdListener<br>
    adListener = object : AdListener() {
        override fun onAdLoaded() {
            super.onAdLoaded()
            Log.d(TAG,"adListener.onAdLoaded")
        }

        override fun onAdFailed(errorCode: Int) {
            val errorMessage = AdvancedAdUtils.getDetailsFromErrorCode(errorCode)
            Log.e(TAG,"adListener.onAdFailed() with errorMessage $errorMessage")
        }

        override fun onAdClosed() {
            super.onAdClosed()
            Log.d(TAG,"adListener.onAdClosed")
        }

        override fun onAdClicked() {
            Log.d(TAG,"adListener.onAdClicked")
            super.onAdClicked()
        }

        override fun onAdOpened() {
            Log.d(TAG,"adListener.onAdOpened")
            super.onAdOpened()
        }
    }
<br></code></pre>

<p><strong>5. Locate following line to invoke Splash Ad Listeners create methods</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : customize and load BannerAd
    if (bannerView != null) {
        adFrameLayout.removeView(bannerView)
        bannerView.destroy()
    }
    bannerView = BannerView(this)
    bannerView.adId = getString(R.string.ad_id_banner)
    bannerView.setBackgroundColor(Color.BLUE)
    bannerView.bannerAdSize = BannerAdSize.BANNER_SIZE_360_57
    bannerView.setBannerRefresh(5)
    bannerView.adListener = adListener
    bannerView.loadAd(AdParam.Builder().build())
    adFrameLayout.addView(bannerView)

    // can customize ad RequestOptions parameters
    // <a href="https://developer.huawei.com/consumer/en/doc/HMSCore-Guides-V5/publisher-service-advanced-settings-0000001050064972-V5" target="_blank">Advanced Settings</a>
<br><span class="pln"></span></code></pre>

<p><strong>4. The following table lists the standard Banner Ad Sizes : <br></strong></p>
<table style="width: 100%; table-layout: fixed; border: 1px solid black;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1" ><p><strong>Type</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Size in dp (W x H)</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Description</strong></p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>BANNER_SIZE_320_50</p>
	</td><td colspan="1" rowspan="1"><p>320 x 50</p>
	</td><td colspan="1" rowspan="1"><p>Common banner ads, applicable to phones.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>BANNER_SIZE_320_100</p>
	</td><td colspan="1" rowspan="1"><p>320 x 100</p>
	</td><td colspan="1" rowspan="1"><p>Large banner ads, applicable to phones.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>BANNER_SIZE_300_250</p>
	</td><td colspan="1" rowspan="1"><p>300 x 250</p>
	</td><td colspan="1" rowspan="1"><p>Medium rectangular banner ads, applicable to phones.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>BANNER_SIZE_360_57</p>
	</td><td colspan="1" rowspan="1"><p>360 x 57</p>
	</td><td colspan="1" rowspan="1"><p>Common banner ads, applicable to 1080 x 170 px ad assets.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>BANNER_SIZE_360_144</p>
	</td><td colspan="1" rowspan="1"><p>360 x 144</p>
	</td><td colspan="1" rowspan="1"><p>Large banner ads, applicable to 1080 x 432 px ad assets..</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>BANNER_SIZE_SMART</p>
	</td><td colspan="1" rowspan="1"><p>Screen width x 32|50|90</p>
	</td><td colspan="1" rowspan="1"><p>Adaptive banner ads (whose size is automatically adjusted based on the aspect ratios of devices), applicable to phones.</p>
	</td></tr>
</tbody></table>
<br>
<center>
<img style="width: 300.00px " src="assets/ss_banner.png" onclick="imageclick(src)">
</center>