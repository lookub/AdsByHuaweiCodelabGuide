---
title: Integrate SDK and set up the Project
description: 5
---

<p>You can download the codelab project from: <a href="https://github.com/lookub/AdsByHuaweiCodelab.git" target="_blank">https://github.com/lookub/AdsByHuaweiCodelab.git</a></p>

<h2><strong>Creating a Project</strong></h2>
<p><strong>Step 1</strong>: Start Android Studio.</p>
<p><strong>Step 2</strong>: Choose <strong>File</strong> &gt; <strong>Open</strong>, go to the directory where the sample project is decompressed, and click <strong>OK</strong>.<br><center><img style="width: 300.00px" src="assets/package.jpg" onclick="imageclick(src)"></center></p>
<p><strong>Step 3</strong>: Configure the AppGallery Connect plug-in, Maven repository address, build dependencies, obfuscation scripts, and permissions. (These items have been configured in the sample code. If any of them does not meet your requirements, change it in your own project.)</p>
<p><strong>1. Configure the Maven repository address and AppGallery Connect plug-in in the project's build.gradle file.</strong></p>
<ul>
	<li>Go to <strong>allprojects</strong> &gt; <strong>repositories</strong> and configure the Maven repository address for the HMS Core SDK.<pre><div id="copy-button1" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">allprojects </span><span class="pun">{</span><span class="pln">
		repositories </span><span class="pun">{</span><span class="pln">
			maven </span><span class="pun">{</span><span class="pln"> url </span><span class="str">'https://developer.huawei.com/repo/'</span><span class="pln"> </span><span class="pun">}</span><span class="pln">
			</span><span class="pun">...</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
	<li>Go to <strong>buildscript</strong> &gt; <strong>repositories</strong> and configure the Maven repository address for the HMS Core SDK.<pre><div id="copy-button2" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">buildscript </span><span class="pun">{</span><span class="pln">
		repositories </span><span class="pun">{</span><span class="pln">
		   maven </span><span class="pun">{</span><span class="pln">url </span><span class="str">'https://developer.huawei.com/repo/'</span><span class="pun">}</span><span class="pln">
			</span><span class="pun">...</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
</ul>
<p><strong>2. Configure the dependency package in the app's build.gradle file.</strong></p>
<ul>
	<li>Add a dependency package to the <strong>dependencies</strong> section in the <strong>build.gradle</strong> file.<pre><div id="copy-button4" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">dependencies </span><span class="pun">{</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
    </span><span class="str">            // Ads Kit SDK</span><span class="pln">
		implementation </span><span class="str">'com.huawei.hms:ads-lite:13.4.36.301'</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
  <p>For Ads Kit SDK, please refer to <a href="https://developer.huawei.com/consumer/en/doc/HMSCore-Guides-V5/publisher-service-version-change-history-0000001050066909-V5" target="_blank">latest version</a>.</p>
	</li>
</ul>
<p><strong>3. Configure obfuscation scripts.</strong></p>
<ul>
	<li>Configure the following information in the <strong>app/proguard-rules.pro</strong> file:<pre><div id="copy-button7" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>                <span class="pun">-</span><span class="pln">ignorewarnings</span><span class="pln">
		</span><span class="pln">-keep </span><span class="kwd">class</span><span class="pln"> com.huawei.openalliance.ad.** { *; }</span><span class="pln">
		</span><span class="pun">-keep </span><span class="kwd">class</span><span class="pln"> com.huawei.hms.ads.** { *; }</span><span class="pln">
		</span></code></pre>
	</li>
</ul>
<p><strong>4. Configure permissions in the AndroidManifest.xml file.</strong></p>
<pre><div id="copy-button9" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.INTERNET"</span><span class="tag">/&gt;</span>
<span class="pln"></span>
<span class="str">// Add this congiguration to in application scope on manigers file. 
//For To allow HTTP network requests on devices with targetSdkVersion 28 or later </span><span class="pln"></span>
<span class="pln">
	<span class="kwd">android:usesCleartextTraffic="true"</span>
</span> </code></pre>
<p><strong>Step 4</strong>: In the Android Studio window, choose <strong>File</strong> &gt; <strong>Sync Project with Gradle Files</strong> to synchronize the project.</p>
<aside class="special">
<p><strong>Note: Test adSlot adID list :</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    /*
    *******************************************
    Banner Ads testID : testw6vs28auh3
    Native Ad Video testID : testy63txaom86
    Native Ads testID : testu7m3hc4gvm
    Native Ad Small testID : testb65czjivt9
    Rewarded Ads testID : testx9dtjwj8hp
    Interstitial Ads testID : testb4znbuh3n2 video
    Interstitial Ads testID : teste9ih9j0rc3 image
    Splash Ads testID : testq6zq98hecj
    *******************************************
    */
<br><span class="pln">
</span></code></pre>
</aside>