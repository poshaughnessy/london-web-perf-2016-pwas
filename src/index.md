title: PWAs – Service Workers and Server-free Selfies
output: public/index.html
style: styles.css
script: script.js
controls: false


--

# Progressive Web Apps

## Service Workers & Server-free Selfies 📷

<div class="contact">
  <p>Peter O'Shaughnessy</p>
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
  <p>[@samsunginternet](https://twitter.com/samsunginternet)</p>
</div>

--

![Samsung Internet icon on homescreen](images/samsung-internet-home.png)

--

![Samsung Internet colleagues](images/samsunginternet-devrel.jpg)

--

![Snapwat](images/snapwat.png)

--

![Snapwat](images/snapwat-ldnwebperf.png)

--

## Not to be confused with... 👻

<img src="images/snapchat.svg" alt="Snapchat" width="30%"/>
<p class="caption">Snapchat by Snap Inc.</p>

--

> &ldquo;PWAs combine the best of web & the best of native&rdquo; 💯

--

## Best of web 🌎

* Multi-platform
* Frictionless
* Discoverable
* Accessible

--

## Best of native  📱

* Add to Home Screen
* Offline
* Instant load
* Push notifications

--

> &ldquo;PWAs are all about removing friction&rdquo; 🏎

--

# 🔟 things I learned

--

## 1⃣️ Automate precache resource list 📝 

```javascript
gulp.task('generate-service-worker', function(callback) {

  swPrecache.write(path.join(rootDir, 'service-worker.js'), {
    staticFileGlobs: [rootDir + '/**/*.{js,html,css,svg}'],
    stripPrefix: rootDir
  }, callback);

});
```

[github.com/GoogleChrome/sw-precache](https://github.com/GoogleChrome/sw-precache)

--

```javascript
// sw.js
import resources from '\0initial-resources';
...
cache.addAll( resources );
```

[gitlab.com/Rich-Harris/rollup-cache-manifest-example](gitlab.com/Rich-Harris/rollup-cache-manifest-example)

--

## 2⃣️ Don't cache too much on install! ⚖

![Emoji SVGs](images/svgs.png)

--

![I switched SVGs for emojis as text](images/emojis.png)
<p class="caption">Emoji One SVGs (left), Unicode emojis (right)</p>

--

## 3⃣️ URLs, not files 🗂

```javascript
const RESOURCES = [
  '/',
  '/index.html',
  ...
];
...
cache.addAll( RESOURCES );
```

--

## 4⃣️ Remember to check Lighthouse 🔦🏠

![Lighthouse](images/lighthouse-report.png)

--

## 5⃣️ Don't rely on getUserMedia constraints 🙈

```javascript
const constraints = {
   width: {ideal: width, max: width},
   height: {ideal: height, max: height}
  };

navigator.mediaDevices.getUserMedia({video: constraints})
...
```

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 6⃣️ Test standalone mode at non-localhost URL 🙊

<img src="images/localhost-bug.png" alt="Localhost bug" width="25%"/>

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 7⃣️ Data-uri downloads currently blocked ⛔️

<img src="images/image-save-error.png" alt="Data URI image save error" width="25%"/>

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 8⃣️ SWs miss &lt;a download&gt; requests 🙉

<a href="https://bugs.chromium.org/p/chromium/issues/detail?id=468227#c13"><img src="images/chromium-bug.png" alt="Chromium bug" width="75%"/></a>

<div class="corner-logos">![Chrome](images/chrome.png) ![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 9⃣️ 'New tab' in standalone mode kills page 💀

<!-- TODO if there's time, make a test case and quick video of this -->

```javascript
window.open(canvas.toDataURL('image/png'), '_blank');
```

<div class="corner-logos">![Chrome](images/chrome.png) ![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 🔟 No long tap menu in standalone mode 🚫

<img src="images/no-long-tap.png" alt="No long tap menu" width="25%"/>

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## Do we need a 'save image' feature? 💾

[bit.ly/save-image-feature](https://discourse.wicg.io/t/save-image-feature-on-mobile-platforms/1676)

--

## Other tricky things 🤔

* &lt;input type=”file”&gt; orientation (used [JavaScript-Load-Image](https://github.com/blueimp/JavaScript-Load-Image.git))
* Calculating canvas text bounds
* Text doesn't render when over ~240px?

--

# Performance 🏃

--

## Rendering recommendations (in order) 👇

1. SSR app shell & content for entry page. CSR takes over.
1. SSR only app shell. JS fetches content once loaded.
1. SSR full page.
1. CSR full page.

--

## Caching strategies 🏁

* “cache first”, then fallback to network

```javascript
toolbox.router.get(‘/images’, toolbox.cacheFirst);
```

--

* “network first”, then fallback to cache

```javascript
toolbox.router.get(‘/api’, toolbox.networkFirst);
```

--

* “fastest” — serve whichever comes back first

```javascript
toolbox.router.get(‘/profile’, toolbox.fastest);
```
<div></div>
* “network only”
* “cache only”

--

## Save-Data header 🗜

```javascript
self.addEventListener('fetch', function(event) {
  if (event.request.headers.get('save-data')) {
    ...  
```

[bit.ly/save-data-header](http://bit.ly/save-data-header)

<div class="corner-logos">![Chrome](images/chrome.png) ![Opera](images/opera.png)</div>

--

# Next for PWAs? 🆕

--

## Background sync ⛰

```javascript
navigator.serviceWorker.ready.then(function(reg) {
    return reg.sync.register('syncTest');
  }).then(function() {
    log('Sync registered');
  });
```

<div class="corner-logos">![Chrome](images/chrome.png)</div>

--

## Foreign fetch ✈️

```
Link: </service-worker.js>; rel="serviceworker"
Origin-Trial: token_obtained_from_signup
```

[bit.ly/foreign-fetch](http://bit.ly/foreign-fetch)

--

## Multiple service workers for parallelisation? 👯

[jakearchibald.com/2016/service-worker-meeting-notes/](https://jakearchibald.com/2016/service-worker-meeting-notes/)

--

# 🔜

* Service worker "v2"
* Cache API "v2"

--

# Next for Snapwat? ⏩

--

## Push notifications 🙌

<img src="images/podle-push-notification.png" alt="Podle push notification" width="25%"/>

<!-- [bit.ly/web-fundamentals-push-notifications](http://bit.ly/web-fundamentals-push-notifications) -->

<div class="corner-logos">![Chrome](images/chrome.png) ![Samsung Internet](images/sbrowser5.0.png) ![Firefox](images/firefox.png) ![Opera](images/opera.png)</div>

--

## Web Share API 🗯

<div class="corner-logos">![Chrome](images/chrome.png)</div>

--

## Head tracking 👀

<img src="images/head-tracking.png" alt="Head tracking example" width="25%"/>

--

* Brushes 🖌
* Undo/Redo ↩️↪️
* Local storage? 📥
* Any suggestions...? 😃

--

# 🔗 [snapw.at](https://snapw.at)

## 📃  [github.com/SamsungInternet/snapwat](https://github.com/SamsungInternet/snapwat)

--

# Thanks! 🙏

<div class="contact">
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
  <p>[@samsunginternet](https://twitter.com/samsunginternet)</p>
  <br/>
  <p>[github.com/samsunginternet](https://github.com/samsunginternet)</p>
  <p>[medium.com/samsung-internet-dev](https://medium.com/samsung-internet-dev)</p>
</div>
