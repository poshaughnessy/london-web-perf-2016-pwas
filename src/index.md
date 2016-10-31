title: PWAs – Service Workers and Server-free Selfies
output: public/index.html
style: styles.css
script: script.js
controls: false


--

# Progressive Web Apps

## Service Workers & Server-free Selfies

<div class="contact">
  <p>Peter O'Shaughnessy</p>
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
  <p>[@samsunginternet](https://twitter.com/samsunginternet)</p>
</div>

--

![Samsung Internet](images/samsunginternet-devrel.jpg)

--

![Snapwat](images/snapwat.png)

--

![Snapwat](images/snapwat-ldnwebperf.png)

--

## Not to be confused with...

<img src="images/snapchat.svg" alt="Snapchat" width="30%"/>
<p class="caption">Snapchat by Snap Inc.</p>

--

> PWAs combine the best of web & the best of native

--

## Best of web

* Multi-platform
* Frictionless
* Discoverable
* Accessible

--

## Best of native

* Add to Home Screen
* Offline
* Instant load
* Push notifications

--

> &ldquo;PWAs are all about removing friction&rdquo;

--

# 10 things I learned

--

## 1. Generate resources list with globs

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

## 2. But don't cache too much on install!

![Emoji SVGs](images/svgs.png)

--

![I switched SVGs for emojis as text](images/emojis.png)
<p class="caption">Emoji One SVGs (left), Unicode emojis (right)</p>

--

## 3. URLs, not files

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

## 4. Remember to check Lighthouse

![Lighthouse](images/lighthouse-report.png)

--

## 5. getUserMedia does not observe requested constraints

```javascript

```

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 6. getUserMedia prompt doesn't appear in localhost standalone

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 7. Data-uri downloads may be blocked

<img src="images/image-save-error.png" alt="Data URI image save error" width="30%">

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 8. SWs miss &lt;a download&gt; requests

[![Chromium bug](images/chromium-bug.png)](https://bugs.chromium.org/p/chromium/issues/detail?id=468227#c13)

<div class="corner-logos">![Chrome](images/chrome.png) ![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 9. 'New tab' in standalone mode kills page

<!-- TODO if there's time, make a test case and quick video of this -->

```javascript
window.open(saveCanvas.toDataURL('image/png'), '_blank');
```

<div class="corner-logos">![Chrome](images/chrome.png) ![Samsung Internet](images/sbrowser5.0.png)</div>

--

## 10. Long tap disabled in standalone mode

<!-- TODO show a video? -->

<div class="corner-logos">![Samsung Internet](images/sbrowser5.0.png)</div>

--

## Do we need a 'save image' feature?

[bit.ly/save-image-feature](https://discourse.wicg.io/t/save-image-feature-on-mobile-platforms/1676)

--

## Other tricky things

* &lt;input type=”file”&gt; photo orientation (used [JavaScript-Load-Image](https://github.com/blueimp/JavaScript-Load-Image.git))
* Calculating text bounds on canvas (I assume emojis are square)
* Text doesn't render to canvas when over about 240px? :-/

--

# Rendering

--

## Google recommend (in order)

1. SSR app shell & content for entry page. CSR takes over.
1. SSR only app shell. JS fetches content once loaded.
1. SSR full page.
1. CSR full page.

--

# Caching strategies

--

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

--

* “network only”
* “cache only”

--

# What's next?

--

## Push notifications

<div class="corner-logos">![Chrome](images/chrome.png) ![Samsung Internet](images/sbrowser5.0.png) ![Firefox](images/firefox.png) ![Opera](images/opera.png)</div>

--

## Background sync

```javascript
navigator.serviceWorker.ready.then(function(reg) {
    return reg.sync.register('syncTest');
  }).then(function() {
    log('Sync registered');
  });
```

<div class="corner-logos">![Chrome](images/chrome.png)</div>

--

<!-- ## Save-Data header -->

<!-- Not really sure how this would work for Snapwat TBH, but thought worth sharing -->

<!-- <div class="corner-logos">![Chrome](images/chrome.png) ![Opera](images/opera.png)</div> -->

## Web Share API

<div class="corner-logos">![Chrome](images/chrome.png)</div>

--

# Thanks!

<div class="contact">
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
  <p>[@samsunginternet](https://twitter.com/samsunginternet)</p>
  <p>[medium.com/samsung-internet-dev](https://medium.com/samsung-internet-dev)</p>
</div>
