p2pool-ui-static
==================

Another alternative p2pool UI.
Makes use of Bootstrap, jQuery and Highcharts.

Features:
- Important information at the top of the page
- Mobile friendly
- Each user can highlight their own miners through configuration stored on the local client
- Change themes with the click of a button (themes provided by: [Bootswatch.com](http://bootswatch.com))
- Chart indicates when blocks are found (merged from https://github.com/roy7/p2pool-node-status)

See Screenshots:

#### Main UI with Stock p2pool
![Main UI - Stock p2pool](/img/screenshot_stock_p2pool.png?raw=true "Main UI - Stock p2pool")

#### Main UI with Extended p2pool
![Main UI - Extended p2pool](/img/screenshot_extended_p2pool.png?raw=true "Main UI - Extended p2pool")

#### Main UI sporting graph modal
![with Graph](/img/screenshot-graph.png?raw=true "with Graph")

## Installation

### Parallel to the default web-static

To run this UI in parallel to your current p2pool web interface, do in your web-static directory:

``` Bash
git clone https://github.com/criptolot/p2pool-ui-Static.git
```

### As web-static replacement

To replace your current web-static, in the top directory of your p2pool installation:

``` Bash
mv web-static web-static-original
git clone https://github.com/criptolot/p2pool-ui-Static.git
ln -s p2pool-ui-Static web-static
```

## Setup

Once you have the UI installed, you'll need to create a configuration file.
You can find the file in the `/js/` directory.
Copy the example config `config.example.js` to `config.js` and modify to fit your needs.
See the `Configuration` section below for option descriptions.

Once this is setup, you'll be able to access the UI either by:
`http://<url-to-your-p2pool>:<port>/static/p2pool-ui-Static/` if you chose to do a parallel installation
or
`http://<url-to-your-p2pool>:<port>/static` is you chose to do a replacement installation

## Configuration

The `config.js` is found in `js` directory.

### Highlight the pool owners addresses.

If you want your server miner addresses highlighted, adjust `myself` variable accordingly. E.g.

``` JavaScript
var config = {
    myself: [
        "195ufic8mfNrDqxgFCfmw5mQYwdu2im9G5",
        "1MzFr1eKzLEC1tuoZ7URMB7WWBMgHKimKe"
    ],
    host: "",
    reload_interval: 30,
    reload_chart_interval: 600,
    header_content_url: ""
}
```

### Point the UI to a different p2pool server

You need to configure the host and port of your p2pool server in the `host` variable like

``` JavaScript
var config = {
    myself: [],
    host: "http://p2pool.org:9332",
    reload_interval: 30,
    reload_chart_interval: 600,
    header_content_url: ""
}
```

**NOTE** Loading content is subject to [Same-Origin Policy](http://en.wikipedia.org/wiki/Same_origin_policy)

### Load additional content onto the page

``` JavaScript
var config = {
    myself: [],
    host: "",
    reload_interval: 30,
    reload_chart_interval: 600,
    header_content_url: "cool_content.html"
}
```

**NOTE** Loading content is subject to [Same-Origin Policy](http://en.wikipedia.org/wiki/Same_origin_policy)

### Change the default theme
In the config hash, simply add a new key called `theme` and set it's value to the name of the theme you'd like to
be the default.

``` JavaScript
var config = {
    theme: 'cyborg'
}
```

### Add new themes
In the config hash, simply add a new array key called `available_themes` and add the theme name.

When adding custom themes, add the `.min.css` file to the `css` directory in the format:

```
./css/bootstrap-<THEME NAME>.min.css
```

```javascript
var config = {
  available_themes: [
    'cool-theme'
  ]
}
```

### Adjust the reload interval

Per default the UI updates the miner list and server stats every 30 seconds.  You can adjust the `reload_interval` variable like

``` JavaScript
var config = {
    myself: [],
    host: "",
    reload_interval: 20,
    reload_chart_interval: 1200,
    header_content_url: ""
}
```

to set it to 20 seconds for example.

`reload_chart_interval` sets the amount of seconds until the hashrate graph is reloaded.  In above example, it's configured to 1200 seconds (20 minutes).

**Beware** that each API query puts network and CPU load on your p2pool installation.  Avoid decreasing this value too much.  In my tests, 20 to 30 seconds seem to be fair enough.

## Roadmap

- Replace HighCharts with another graph lib which can still be used on nodes having a fee (nodes considered as commercial)

- Add section for recent shares and share tree in network

- More graphs for the p2pool node

- Individual address page with individual stats (more like tradition central pools, MPOS dashboard view)

## Deprecated
- jsonp.php - this was deprecated and should not be used, it was a huge security risk. Instead use standard remote host config. If that doesn't work because of cross-origin restrictions, check your p2pool HTTP config to allow it.

- config.json - this was incorrectly designated as JSON when in fact it was really just plain javascript. Simply renaming it from `config.json` -> `config.js` will fix it.

### Donations

If you like this UI, find it useful, or like that people out there are writing free software for everybody to use or contribute, please donate some coins:

```
Bitcoin: 195ufic8mfNrDqxgFCfmw5mQYwdu2im9G5
Ethereum: dee42d6b58e5d5d9f6f4c4783bea4fff34369c64
Dashpay: XerSXuygP6PeUoqVRyC2BFFHpUXXkFU8UP
```

### License

```
The MIT License (MIT)

Copyright (c) 2014-2018 Justin La Sotten justin.otten@gmail.com
Copyright (c) 2013-2014 Alexander Zschach alex@zschach.net

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
