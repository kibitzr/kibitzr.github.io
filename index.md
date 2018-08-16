<iframe src="https://ghbtns.com/github-btn.html?user=kibitzr&repo=kibitzr&type=star&count=true&size=large" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>

# Get notified when important things happen

Ever waited for long-running TeamCity build to finish?
Or repeatedly checked for new library bug-fix release?
Why not receive notification instead?
Configure kibitzr for polling web page and notify you in messenger or e-mail.

## Personal

* Self-hosted - trust no one with your credentials
* Runs everywhere: **Windows**, **Linux** and **Mac OS** both desktop and server.
* Can go wherever you can go (authenticate on websites, ssh, vpn)

## Web

* From raw SSH commands to complex browser scenarios - Kibitzr knows protocols
* Integrated with powerfull services, like Slack and MailGun

## Assistant

* Define recurrent tasks in human-friendly YAML format
* Sit back and relax, Kibitzr will notify you when something happens

## Explore

* Check out the [Zapier integration tutorial](zapier-how-to.html)
* [Bank balance how-to](https://peterdemin.github.io/kibitzr-banks.html)
* Success story on polling a [Russian passport readiness](russian-passport.html)
* [Deploy behind firewall](automatic-deployment.html) on git push
* [Get OPM Alerts in Telegram](opm-status-alert.html)
* [Firefox Developer Edition release notification](firefoxde.html)

## Engage!

* Read the [documentation](https://kibitzr.readthedocs.org)
* Try it with [AWS Free Tier](https://kibitzr.readthedocs.io/en/latest/aws.html) or [GCP Always Free](https://kibitzr.readthedocs.io/en/latest/gcp.html).
* Ask in [chat](https://gitter.im/kibitzr/Lobby)
* Open [issue](https://github.com/kibitzr/kibitzr/issues/)
* Fork on [GitHub](https://github.com/kibitzr/kibitzr)

## Easy to start

* install - `pip install kibitzr` (Python 2 and 3 compatible)
* configure - whole configuration in one YAML file
* run - `kibitzr`

## Powerfull

* Browser scenarios with selenium
* HTML parsing with XPath and CSS selectors
* Integrations with MailGun and Slack

## Lightweight

* Can run on tiniest VM offered by cloud providers.

## Extensible

* Use bash and python scripts
* Create plugins
* Vibrant friendly community (on gitter)

## Free forever

* Free Open Source Software
* MIT license

## Miscellaneous

* [Why Python is a perfect language for Kibitzr](why-python.html)
* [ProductHunt page](https://www.producthunt.com/posts/kibitzr)

<!-- Start of Async Drift Code -->
<script>
"use strict";

!function() {
  var t = window.driftt = window.drift = window.driftt || [];
  if (!t.init) {
    if (t.invoked) return void (window.console && console.error && console.error("Drift snippet included twice."));
    t.invoked = !0, t.methods = [ "identify", "config", "track", "reset", "debug", "show", "ping", "page", "hide", "off", "on" ], 
    t.factory = function(e) {
      return function() {
        var n = Array.prototype.slice.call(arguments);
        return n.unshift(e), t.push(n), t;
      };
    }, t.methods.forEach(function(e) {
      t[e] = t.factory(e);
    }), t.load = function(t) {
      var e = 3e5, n = Math.ceil(new Date() / e) * e, o = document.createElement("script");
      o.type = "text/javascript", o.async = !0, o.crossorigin = "anonymous", o.src = "https://js.driftt.com/include/" + n + "/" + t + ".js";
      var i = document.getElementsByTagName("script")[0];
      i.parentNode.insertBefore(o, i);
    };
  }
}();
drift.SNIPPET_VERSION = '0.3.1';
drift.load('br87dd5kh22p');
</script>
<!-- End of Async Drift Code -->
