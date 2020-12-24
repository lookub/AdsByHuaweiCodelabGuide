---
title: Developing Native Ad
description: 15
---
<center>
<img style="width: 150.00px " src="assets/native.png" onclick="imageclick(src)">
</center>

<p><strong>0. Locate following line to ad Native Ad template layouts  layout include element to XML layout file.</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // &lt;!-- add native_video_template layout include element --&gt;
    &lt;include
           android:id="@+id/native_ad_video"
           layout="@layout/native_video_template"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:layout_marginBottom="40dp" /&gt;
    <br>
    // &lt;!-- add native_small_template layout include element --&gt;
    &lt;include
            android:id="@+id/native_ad_small"
            layout="@layout/native_small_template"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="40dp" /&gt;
    <br>
    // &lt;!-- add native_large_template layout include element --&gt;
    &lt;include
            android:id="@+id/native_ad_large"
            layout="@layout/native_large_template"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_marginBottom="40dp" /&gt;
    <br>
<br><span class="pln"></span></code></pre>

<p><strong>1. Locate following line to find these layout xml files.( 
will also be in project layout files</strong></p><ul>
<li><a href="https://github.com/lookub/AdsByHuaweiCodelab/blob/master/app/src/main/res/layout/native_small_template.xml" target="_blank">native_small_template.xml</a></li>
<li><a href="https://github.com/lookub/AdsByHuaweiCodelab/blob/master/app/src/main/res/layout/native_large_template.xml" target="_blank">native_large_template.xml</a></li>
<li><a href="https://github.com/lookub/AdsByHuaweiCodelab/blob/master/app/src/main/res/layout/native_small_template.xml" target="_blank">native_small_template.xml</a></li>
</ul>

<p><strong>2. Locate following line to create NativeView whatever type you want, and create VideoLifecycleListener for videoNativeView</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create NativeView for smallNativeView
    private lateinit var smallNativeView: NativeView
<br>
    // TODO : create NativeView for largeNativeView
    private lateinit var largeNativeView: NativeView
<br>
    // TODO : create NativeView for videoNativeView
    private lateinit var videoNativeView: NativeView

    // TODO : create VideoLifecycleListener for videoNativeView
    private lateinit var videoLifecycleListener: VideoLifecycleListener

    // TODO : create AdListener
    private lateinit var adListener: AdListener
<br><span class="pln">
</span></code></pre>

<p><strong>3. Locate following line to Initialize NativeView whatever type you want</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize NativeView
        smallNativeView = findViewById(R.id.native_ad_small)
        largeNativeView = findViewById(R.id.native_ad_large)
        videoNativeView = findViewById(R.id.native_ad_video)
<br><span class="pln">
</span></code></pre>

<p><strong>4. Locate following line to call AdListeners</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize AdListener
    createNativeAdListener()
    // TODO : call createVideoLifecycleListener
    createVideoLifecycleListener()
<br><span class="pln">
</span></code></pre>

<p><strong>4.1. Locate following line to Initialize AdListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize createAdListener
    adListener = object : AdListener() {
        override fun onAdLoaded() {
            super.onAdLoaded()
            Log.d(TAG,"adListener.onAdLoaded")
        }

        override fun onAdFailed(errorCode: Int) {
            Log.e(TAG,"NativeAd.onAdFailed() with errorCode $errorCode")
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
<br><span class="pln">
</span></code></pre>

<p><strong>4.2. Locate following line to Initialize VideoLifecycleListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize VideoLifecycleListener
    videoLifecycleListener = object : VideoLifecycleListener() {
        override fun onVideoStart() {
            Log.d(TAG,"videoOperator.onVideoStart() : Video playback state: starting to be played "
            )
        }

        override fun onVideoPlay() {
            Log.d(TAG,"videoOperator.onVideoStart() : Video playback state: being played ")
        }

        override fun onVideoEnd() {
            Log.d(TAG,"videoOperator.onVideoStart() : Video playback state: playback completed.")
            // If there is a video, load a new native ad only after video playback is complete.
        }
    }
<br><span class="pln">
</span></code></pre>

<p><strong>5. Locate following line to call load ads whatever type you want with ad id </strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : call load ads with ad id
        loadAd(getString(R.string.ad_id_native_video), videoNativeView)

        loadAd(getString(R.string.ad_id_native_small), smallNativeView)

        loadAd(getString(R.string.ad_id_native), largeNativeView)
<br><span class="pln">
</span></code></pre>

<aside class="special"><p><strong>Note: You can use testAdId for demo ad show : 
<br>
with large : <string name="ad_id_native">testu7m3hc4gvm</string> 
<br>
with small : <string name="ad_id_native_small">testb65czjivt9</string> 
<br>
with video : <string name="ad_id_native_video">testy63txaom86</string> 
</strong></p></aside>


<p><strong>6. Locate following line to initialize NativeAdLoader and nativeAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize NativeAdLoader and nativeAd<br>    // demo method can use with these params : (adId: String, nativeView: NativeView)<br>
    val builder = NativeAdLoader.Builder(this, adId)
    builder.setNativeAdLoadedListener { nativeAd ->
        Log.d(TAG,"onNativeAdLoaded : Ad Loaded successfully.")
        // Display native ad.
        showNativeAd(nativeAd, nativeView)

        nativeAd.setDislikeAdListener {
            Log.d(TAG, "setDislikeAdListener : Ad is closed!")
        }
    }.setAdListener(adListener)
    val adConfiguration = NativeAdConfiguration.Builder()
        .setChoicesPosition(NativeAdConfiguration.ChoicesPosition.TOP_RIGHT) // Set custom attributes.
        .build()
    val nativeAdLoader = builder.setNativeAdOptions(adConfiguration)build()
    Log.d(TAG,"loadAd() : nativeAdLoader.loadAd() ")
    nativeAdLoader.loadAd(AdParam.Builder().build())
<br><span class="pln">
</span></code></pre>


<p><strong>7. Locate following line to  create and display NativeAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create and display NativeAd<br>    // demo method can use with these params : (nativeAd: NativeAd, nativeView: NativeView)<br>
    // Register a native ad material view.
    nativeView.titleView = nativeView.findViewById(R.id.ad_title)
    nativeView.mediaView = nativeView.findViewById< View >(R.id.ad_media) as MediaView
    nativeView.adSourceView = nativeView.findViewById(R.id.ad_source)
    nativeView.callToActionView = nativeView.findViewById(R.id. ad_call_to_action)

    // Populate a native ad material view.
    (nativeView.titleView as TextView).text = nativeAd.title
    nativeView.mediaView.setMediaContent(nativeAd.mediaContent)
    if (null != nativeAd.adSource) {
        (nativeView.adSourceView as TextView).text = nativeAd.adSource
    }
    nativeView.adSourceView.visibility =
        if (null != nativeAd.adSource) View.VISIBLE else View.INVISIBLE
    if (null != nativeAd.callToAction) {
        (nativeView.callToActionView as Button).text = nativeAd.callToAction
    }
    nativeView.callToActionView.visibility =
        if (null != nativeAd.callToAction) View.VISIBLE else View.INVISIBLE

    // Obtain a video controller.
    val videoOperator = nativeAd.videoOperator

    // Check whether a native ad contains video materials.
    if (videoOperator.hasVideo()) {
        Log.d(TAG,"initNativeAdView() : videoOperator.hasVideo ")
        // Add a video lifecycle event listener.
        videoOperator.videoLifecycleListener = videoLifecycleListener
    }

    // Register a native ad object.
    nativeView.setNativeAd(nativeAd)
<br><span class="pln">
</span></code></pre>

<p><strong>6. The following table lists the standard Native Ad Sizes : <br></strong></p>
<table style="width: 100%; table-layout: fixed; border: 1px solid black;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1" ><p><strong>Display Form</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Dimensions</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Aspect Ratio</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Test Ad Slot ID</strong></p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>Large image with text</p>
	</td><td colspan="1" rowspan="1"><p>1080 x 607</p>
	</td><td colspan="1" rowspan="1"><p>16:9</p>
	</td><td colspan="1" rowspan="1"><p>testu7m3hc4gvm</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>Small image with tex</p>
	</td><td colspan="1" rowspan="1"><p>225 x 150</p>
	</td><td colspan="1" rowspan="1"><p>3:2</p>
	</td><td colspan="1" rowspan="1"><p>testb65czjivt9</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>Video with text</p>
	</td><td colspan="1" rowspan="1"><p>640 x 360</p>
	</td><td colspan="1" rowspan="1"><p>16:9</p>
	</td><td colspan="1" rowspan="1"><p>testy63txaom86</p>
	</td></tr>
</tbody></table>
<br>
<center>
<img style="width: 300.00px " src="assets/ss_native.png" onclick="imageclick(src)">
</center>
