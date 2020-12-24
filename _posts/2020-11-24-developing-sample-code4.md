---
title: Developing Interstitial Ad
description: 15
---
<center>
<img style="width: 150.00px " src="assets/interstitial.png" onclick="imageclick(src)">
</center>

<p><strong>1. Locate following line to create InterstitialAd and AdListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create listeners
    private lateinit var adListener : AdListener
<span class="pln">
    // TODO : create InterstitialAd
    private lateinit var interstitialAd: InterstitialAd
<br></span></code></pre>

<p><strong>2. Locate following line to Initialize BannerView, FrameLayout</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize FrameLayout
    adFrameLayout = findViewById(R.id.ad_frame)<br>
    // TODO : initialize BannerView
    bannerView = findViewById(R.id.hw_banner_view)
<br><span class="pln">
</span></code></pre>


<p><strong>3. Locate following line to Initialize AdListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize AdListener<br>
        adListener = object : AdListener() {
            override fun onAdLoaded() {
                super.onAdLoaded()
                Log.d(TAG, "adListener.onAdLoaded")

                // TODO : Display an interstitial ad when its loaded
                showInterstitial()
            }

            override fun onAdFailed(errorCode: Int) {
                Log.e(TAG,"adListener.onAdFailed() with errorCode $errorCode")
            }

            override fun onAdClosed() {
                super.onAdClosed()
                Log.d(TAG, "adListener.onAdClosed")
            }

            override fun onAdClicked() {
                Log.d(TAG, "adListener.onAdClicked")
                super.onAdClicked()
            }

            override fun onAdOpened() {
                Log.d(TAG, "adListener.onAdOpened")
                super.onAdOpened()
            }
        }
    }
<br></code></pre>

<p><strong>4. Locate following line to Initialize InterstitialAd</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize InterstitialAd
        interstitialAd = InterstitialAd(this)
        interstitialAd.adId = R.string.ad_id_interstitial_video
        interstitialAd.adListener = adListener
        val adParam = AdParam.Builder().build()
        interstitialAd.loadAd(adParam)
<br><span class="pln"></span></code></pre>

<p><strong>5. Locate following line to Display InterstitialAd</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Display an interstitial ad when its loaded
        if (interstitialAd != null && interstitialAd.isLoaded) {
            interstitialAd.show()
        } else {
            Log.d(TAG, "interstitialAd is NULL or did not Loaded")
        }
<br><span class="pln"></span></code></pre>

<p><strong>6. The following table lists the standard Banner Ad Sizes : <br></strong></p>
<table style="width: 100%; table-layout: fixed; border: 1px solid black;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1" ><p><strong>Display Form</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Screen Orientation</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Dimensions</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Test Ad Slot ID</strong></p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>Image</p>
	</td><td colspan="1" rowspan="1"><p>Portrait</p>
	</td><td colspan="1" rowspan="1"><p>1080 x 1620</p>
	</td><td colspan="1" rowspan="1"><p>teste9ih9j0rc3</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>Video</p>
	</td><td colspan="1" rowspan="1"><p>Portrait</p>
	</td><td colspan="1" rowspan="1"><p>720 x 1080</p>
	</td><td colspan="1" rowspan="1"><p>testb4znbuh3n2</p>
	</td></tr>
</tbody></table>

<aside class="special"><p><strong>Note: You can use testAdId for demo ad show : 
<br>
with video  : <string name="ad_id_interstitial_video">testq6zq98hecj</string> 
<br>
with image : <string name="ad_id_interstitial_image">teste9ih9j0rc3</string> 
</strong></p></aside>

<center>
<img style="width: 300.00px " src="assets/ss_interstitial.png" onclick="imageclick(src)">
</center>