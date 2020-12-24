---
title: Developing InstreamRoll Ad
description: 15
---
<center>
<img src="assets/instream_roll.png" onclick="imageclick(src)">
</center>

<p><strong>1. Locate following line to add InstreamRollAd layout element InstreamView to XML layout file.</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // &lt;!-- TODO : add InstreamView XML element --&gt;
    &lt;com.huawei.hms.ads.instreamad.InstreamView
                android:id="@+id/instream_view"
                android:layout_width="match_parent"
                android:layout_height="match_parent" /&gt;
<br><span class="pln"></span></code></pre>

<p><strong>2. Locate following line to Initialize NativeView whatever type you want</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize NativeView
        smallNativeView = findViewById(R.id.native_ad_small)
        largeNativeView = findViewById(R.id.native_ad_large)
        videoNativeView = findViewById(R.id.native_ad_video)
<br><span class="pln">
</span></code></pre>

<p><strong>2. Locate following line to create InstreamView, InstreamAd List, InstreamAdLoader, and create Listeners of InstreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create InstreamView
    private lateinit var instreamView: InstreamView

    // TODO : create List< InstreamAd >
    private var instreamAds: List< InstreamAd > = ArrayList()
<br>
    // TODO : create InstreamAdLoader
    private lateinit var instreamAdLoader: InstreamAdLoader

    // TODO : create InstreamAdLoadListener
    private lateinit var instreamAdLoadListener: InstreamAdLoadListener

    // TODO : create InstreamMediaChangeListener
    private lateinit var instreamMediaChangeListener: InstreamMediaChangeListener

    // TODO : create InstreamMediaStateListener
    private lateinit var instreamMediaStateListener: InstreamMediaStateListener

    // TODO : create InstreamMediaStateListener
    private lateinit var mediaMuteListener: MediaMuteListener
<br></code></pre>

<p><strong>4. Locate following line to call AdListeners</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : call createInstreamAdLoadListener
    createInstreamAdLoadListener()

    // TODO : call createInStreamMediaChangeListener
    createInStreamMediaChangeListener()

    // TODO : call createInStreamMediaStateListener
    createInStreamMediaStateListener()

    // TODO : call createMediaMuteListener
    createMediaMuteListener()
<br><span class="pln">
</span></code></pre>

<p><strong>4.1. Locate following line to Initialize InstreamAdLoadListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize InstreamAdLoadListener
    instreamAdLoadListener = object : InstreamAdLoadListener {
        override fun onAdLoaded(ads: MutableList< InstreamAd >) {
            if (null == ads || ads.size == 0) {
                // You can playNormalVideo()
                return
            }
            val it = ads.iterator()
            while (it.hasNext()) {
                val ad = it.next()
                if (ad.isExpired) {
                    it.remove()
                }
            }
            if (ads.size == 0) {
                // You can playNormalVideo()
                return
            }
            loadButton.text = "Ad Loaded"
            instreamAds = ads
            Log.d(TAG,"onAdLoaded, ad size: " + ads.size + ", you can PlayInStreamAd.")
            )
            // TODO call display InstreamAds
            playInstreamAds(instreamAds)
        }

        override fun onAdFailed(errorCode: Int) {
            Log.e(TAG,"instreamAdLoader.onAdFailed() with errorCode $errorCode")
            loadButton.text = "Load Ad"
            // You can playNormalVideo()
        }
    }
<br><span class="pln">
</span></code></pre>

<p><strong>4.2. Locate following line to Initialize InstreamMediaChangeListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize InstreamMediaChangeListener
    instreamMediaChangeListener = InstreamMediaChangeListener { instreamAd -> // Switch       from one roll ad to another.
            Log.d(TAG,"InstreamMediaChangeListener.onSegmentMediaChange() : InstreamAd : $instreamAd" )
            whyThisAdUrl = "null"
            whyThisAdUrl = instreamAd.whyThisAd
            Log.d(TAG,"InstreamMediaChangeListener.onSegmentMediaChange() : whyThisAd : $whyThisAdUrl")
            if (!TextUtils.isEmpty(whyThisAdUrl)) {
                whyThisAd.visibility = View.VISIBLE
                whyThisAd.setOnClickListener {
                    startActivity(Intent(Intent.ACTION_VIEW, Uri.parse(whyThisAdUrl)))
                }
            } else {
                whyThisAd.visibility = View.GONE
            }
            val cta = instreamAd.callToAction
            Log.d(TAG,"InstreamMediaChangeListener.onSegmentMediaChange() : callToAction : $cta")
            if (!TextUtils.isEmpty(cta)) {
                callToAction.visibility = View.VISIBLE
                callToAction.text = cta
                instreamView.callToActionView = callToAction
            }
        }
<br><span class="pln">
</span></code></pre>


<p><strong>4.3. Locate following line to Initialize InstreamMediaStateListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize InstreamMediaStateListener
    instreamMediaStateListener = object : InstreamMediaStateListener {
        override fun onMediaProgress(percent: Int, playTime:        Int) {
            // Playback process.
            //Log.d(TAG, "InstreamMediaStateListener.onMediaProgress() : percent : " + percent + " - playTime : " + playTime);
            updateCountDown(playTime.toLong())
        }

        override fun onMediaStart(playTime: Int) {
            Log.d(TAG,"InstreamMediaStateListener.onMediaStart() : playTime : $playTime")
            updateCountDown(playTime.toLong())
            // You can re show create/play Ad Buttons this state
        }

        override fun onMediaPause(playTime: Int) {
            Log.d(TAG,"InstreamMediaStateListener.onMediaPause() : playTime : $playTime")
            updateCountDown(playTime.toLong())
        }

        override fun onMediaStop(playTime: Int) {
            // Stop playback.
            Log.d(TAG,"InstreamMediaStateListener.onMediaStop() : playTime : $playTime")
            updateCountDown(playTime.toLong())
            // You can hide create/play Ad Buttons this state
        }

        override fun onMediaCompletion(playTime: Int) {
            // Playback is complete.
            Log.d(TAG,"InstreamMediaStateListener.onMediaCompletion() : playTime : $playTime")
            updateCountDown(playTime.toLong())
            // You can playNormalVideo()
            // You can hide create/play Ad Buttons this state
        }

        override fun onMediaError(playTime: Int, errorCode: Int,        extra: Int) {
            Log.d(TAG,"InstreamMediaStateListener.onMediaCompletion() : playTime : $playTime")
            updateCountDown(playTime.toLong())
        }
    }
<br><span class="pln">
</span></code></pre>

<p><strong>4.4. Locate following line to Initialize InstreamMediaMuteListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize InstreamMediaMuteListener
    mediaMuteListener = object : MediaMuteListener {
            override fun onMute() {
                Log.d(TAG, "MediaMuteListener.onMute()")
                isMuted = true
            }

            override fun onUnmute() {
                Log.d(TAG, "MediaMuteListener.onUnmute()")
                isMuted = false
            }
        }
<br><span class="pln">
</span></code></pre>

<p><strong>5. Locate following line to call initialize InStreamAdLoader, InstreamAdView and Load InStreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : call createInStreamAdLoader
    createInStreamAdLoader()

    // TODO : call initializeInstreamAdView
    initializeInstreamAdView()

    // TODO : call loadInStreamAd
    loadInStreamAd()
<br><span class="pln">
</span></code></pre>

<p><strong>5.1. Locate following line to Initialize InstreamAdLoader</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize InstreamAdLoader
    /**
    * if the maximum total duration is 60 seconds and the maximum number of roll ads is eight,
    * at most four 15-second roll ads or two 30-second roll ads will be returned.
    * If the maximum total duration is 120 seconds and the maximum number of roll ads is four,
    * no more roll ads will be returned after whichever is reached.
    */
    val totalDuration = 60
    val maxCountRoll = 4
    // "testy3cglm3pj0" is a dedicated test ad slot ID. Before releasing your app, replace the test ad slot ID with the formal one.
    val builder =  InstreamAdLoader.Builder(applicationContext, getString(R.string.ad_id_roll))
        // Before reusing InstreamAdLoader to load ads, ensure that the previous request is complete.
    // Set the maximum total duration and number of roll ads that can be loaded.
    instreamAdLoader = builder
        .setTotalDuration(totalDuration)
        .setMaxCount(maxCountRoll)
        .setInstreamAdLoadListener(instreamAdLoadListener)
        .build()
<br><span class="pln">
</span></code></pre>

<aside class="special"><p><strong>Note: You can use testAdId for demo ad show : <string name="ad_id_roll">testy3cglm3pj0</string> </strong></p></aside>

<p><strong>5.2. Locate following line to Initialize InstreamAdView</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : Initialize InstreamAdView
    instreamView = findViewById(R.id.instream_view)
    instreamView.setInstreamMediaChangeListener (instreamMediaChangeListener)
    instreamView.setInstreamMediaStateListener  (instreamMediaStateListener)
    instreamView.setMediaMuteListener(mediaMuteListener)
    instreamView.setOnInstreamAdClickListener {
        Log.d(TAG,"setOnInstreamAdClickListener")
    }
<br><span class="pln">
</span></code></pre>

<p><strong>5.3. Locate following line to load InStreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : load InStreamAd
     if (null != instreamAdLoader) {
        loadButton.text = "Loading"
        instreamContainer.visibility = View.VISIBLE
        // you can customize ad RequestOptions parameters
        instreamAdLoader.loadAd(AdParam.Builder().build())
    } else {
        Log.d(TAG,"instreamAdLoader id NULL. You must create Ad before loading Ad")
    }
<br><span class="pln">
</span></code></pre>

<p><strong>6. Locate following line to display InStreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : display InStreamAd
    maxAdDuration = getMaxInstreamDuration(ads)
        instreamContainer.visibility = View.VISIBLE
        loadButton.text = "Load Ad"
        instreamView.setInstreamAds(ads)
        // You can re show create/play Ad Buttons this state
<br><span class="pln">
</span></code></pre>

<p><strong>7. Locate following line to play or pause InStreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : play or pause InStreamAd
    if (instreamView.isPlaying) {
        instreamView.pause()
        pauseButton.text = "Play"
    } else {
        instreamView.play()
        pauseButton.text = "Pause"
    }
<br>    // You can use in onResume, onPause methods <span class="pln">
</span></code></pre>

<p><strong>7. Locate following line to mute or unMute InStreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : play or pause InStreamAd
    // isMuted veriable is updating in mediaMuteListener onMute/onUnmute methods
    if (isMuted) {
        instreamView.unmute()
        muteButton.text = "Mute"
    } else {
        instreamView.mute()
        muteButton.text = "UnMute"
    }
<br><span class="pln">
</span></code></pre>

<p><strong>8. Locate following line to skipAd InStreamAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : skipAd InStreamAd
    skipAd.setOnClickListener {
        if (null != instreamView) {
            instreamView.onClose();
            instreamView.destroy();
            instreamContainer.removeView(instreamView);
            instreamContainer.setVisibility(View.GONE);
            instreamAds.clear();
            //Log.d(TAG, "skipped Ad, and you need new Ad load by start first process.");
        }
    }
<br><span class="pln">
</span></code></pre>

<p><strong>6. The following table lists the standard InstreamRoll Ad Sizes : <br></strong></p>
<table style="width: 100%; table-layout: fixed; border: 1px solid black;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1" ><p><strong>Display Form</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Dimensions</strong></p>
	</td><td colspan="1" rowspan="1"><p><strong>Test Ad Slot ID</strong></p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>Image or video</p>
	</td><td colspan="1" rowspan="1"><p>640 x 360</p>
	</td><td colspan="1" rowspan="1"><p>testy3cglm3pj0</p>
	</td></tr>
</tbody></table>
<br>


<center>
<img style="width: 300.00px " src="assets/ss_instream_roll.png" onclick="imageclick(src)">
</center>

<aside class="special">
<p><strong>Note: When the display of a roll ad ends, you should destroy the roll ad view : eg :</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : destroy instreamView when onDestroy
    override fun onDestroy() {
        super.onDestroy()
        if (instreamView != null) {
            instreamView.removeInstreamMediaStateListener()
            instreamView.removeInstreamMediaChangeListener()
            instreamView.removeMediaMuteListener()
            instreamView.destroy()
        }
    }
<br><span class="pln">
</span></code></pre>
</aside>