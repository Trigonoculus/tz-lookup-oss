tz-lookup
=========

### Notice:
**This is a fork of https://github.com/darkskyapp/tz-lookup-oss / https://www.npmjs.com/package/tz-lookup**

I have attempted to regenerate the database to 2020d, instead of 2019b in the no-longer-maintained original repository. There are no guarantee that it will work perfectly; use at your own discretion.

---

This is a little Javascript library that allows you to look up the time zone of
a location given its latitude and longitude. It works in both the browser and
in Node.JS, and is very fast and lightweight (~71KB) given what it does. We
use it in production for [The Dark Sky API][1].

[1]: https://darksky.net/dev/

Usage
-----
To install:

    npm install tz-lookup-oss

Node.JS usage:

```javascript
var tzlookup = require("tz-lookup-oss");
console.log(tzlookup(42.7235, -73.6931)); // prints "America/New_York"
```

Browser usage:

```html
<script src="tz.js"></script>
<script>
alert(tzlookup(42.7235, -73.6931)); // alerts "America/New_York"
</script>
```

**Please take note of the following:**

*   The exported function call will throw an error if the latitude or longitude
    provided are NaN or out of bounds. Otherwise, it will never throw an error
    and will always return an IANA timezone database string. (Barring bugs.)

*   The timezones returned by this module are approximate: since the timezone
    database is so large, lossy compression is necessary for a small footprint
    and fast lookups. Expect errors near timezone borders far away from
    populated areas. However, for most use-cases, this module's accuracy should
    be adequate.
    
    If you find a real-world case where this module's accuracy is inadequate,
    please open an issue (or, better yet, submit a pull request with a failing
    test) and I'll see what I can do to increase the accuracy for you.

Sources
-------
Timezone data is sourced from Evan Siroky's [timezone-boundary-builder][tbb].
The database was last updated on 6 Jan 2019.

To regenerate the library's database yourself, you will need to install GDAL:

```
$ brew install gdal # on Mac OS X
$ sudo apt install gdal-bin # on Ubuntu
```

Then, simply execute `rebuild.sh`. Expect it to take 10-30 minutes, depending
on your network connection and CPU.

The script may throw an error after downloading the files. If that's the case,
execute these commands (after the files have been downloaded):

```bash
mkdir dist
cp combined.json dist
```

Then, reexecute the script. You do not have to override the files.

[tbb]: https://github.com/evansiroky/timezone-boundary-builder/

License
-------
To the extent possible by law, The Dark Sky Company, LLC has [waived all
copyright and related or neighboring rights][cc0] to this library.

[cc0]: http://creativecommons.org/publicdomain/zero/1.0/
