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

<blockquote><p>PWAs combine the best of web & the best of native</p></blockquote>

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

# Lessons learned

--

## 1. Caching on install

```javascript
const RESOURCES = [
  '/',
  '/css/styles.css',
  '/build/bundle.js',
  '/images/emojione/1f354.svg',
  '/images/emojione/1f369.svg',
  ...
];
...
cache.addAll( RESOURCES );
```

--

# Thanks!

<div class="contact">
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
  <p>[@samsunginternet](https://twitter.com/samsunginternet)</p>
  <p>[medium.com/samsung-internet-dev](https://medium.com/samsung-internet-dev)</p>
</div>
