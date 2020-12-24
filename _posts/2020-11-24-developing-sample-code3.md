---
title: Developing Reward Ad
description: 15
---
<center>
<img style="width: 150.00px " src="assets/reward.png" onclick="imageclick(src)">
</center>

<p><strong>1. Locate following line to create RewardAd and AdStatusListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create RewardAd
    private lateinit var rewardedAd: RewardAd
<span class="pln">
    // TODO : create adStatus listeners
    private lateinit var rewardAdListener: RewardAdStatusListener
<br></span></code></pre>

<p><strong>2. Locate following line to Initialize AdStatusListener</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : create adStatus listener
    rewardAdListener  = object : RewardAdStatusListener() {
        override fun onRewardAdFailedToShow(errorCode: Int) {
            Log.e(TAG,"RewardAdStatusListener.onRewardAdFailedToShow() with errorCode $errorCode")
        }
        override fun onRewardAdClosed() {
            Log.d(TAG,"RewardAdStatusListener.onRewardAdClosed() Ad will reCreate")

            // TODO : call initialize RewardAd
            createAndLoadRewardAd()
        }
        override fun onRewardAdOpened() {
            Log.e(TAG,"RewardAdStatusListener.onRewardAdOpened")
        }
        override fun onRewarded(reward: Reward) {
            // You are advised to grant a reward immediately and at the same time, check whether the reward
            // takes effect on the server. If no reward information is configured, grant a reward based on the
            // actual scenario.

            // You are advised to grant a reward immediately and at the same time, check whether the reward
            // takes effect on the server. If no reward information is configured, grant a reward based on the
            // actual scenario.
            val addScore = if (reward.amount == 0) defaultScore else reward.amount

            Log.d(TAG,"onRewarded() : reward.getAmount() you can use addScore : $addScore")

            // TODO : optional : call initialize RewardAd for reInitialize for after usage
            createAndLoadRewardAd()
        }
    }
<br><span class="pln">
</span></code></pre>

<p><strong>3. Locate following line to Initialize RewardAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : initialize RewardAd
    rewardedAd = RewardAd(this@RewardActivity, getString(R.string.ad_id_reward))
    val rewardAdLoadListener: RewardAdLoadListener = object : RewardAdLoadListener() {
        override fun onRewardAdFailedToLoad(errorCode: Int) {
            Log.e(TAG,"RewardAdStatusListener.onRewardAdFailedToLoad() with errorCode $errorCode")
        }
        override fun onRewardedLoaded() {
            Log.d(TAG, "rewardAdLoadListener.onRewardedLoaded.")
        }
    }
    rewardedAd.loadAd(AdParam.Builder().build(), rewardAdLoadListener)
<br><span class="pln">
</span></code></pre>

<p><strong>4. Locate following line to Display RewardAd</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    // TODO : display RewardAd
    if (rewardedAd.isLoaded) {
        rewardedAd.show(this@RewardActivity, rewardAdListener)
    }
<br><span class="pln">
</span></code></pre>

<aside class="special"><p><strong>Note: You can use testAdId for demo ad show : with video  : <string name="ad_id_reward">testx9dtjwj8hp</string> 
</strong></p></aside>

<center>
<img style="width: 300.00px " src="assets/ss_reward.png" onclick="imageclick(src)">
</center>