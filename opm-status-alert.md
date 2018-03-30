# OPM Status Alerts in Telegram

For those who work for the US government, it's sometimes surprising when federal agencies get closed due to inclined weather.

There is a [page dedicated to current working status](https://www.opm.gov/policy-data-oversight/snow-dismissal-procedures/current-status/) of federal agencies:

Usually, it states "STATUS: OPEN" but if it snows a little,
the status can become CLOSED, or something else.

OPM even made mobile apps for notifying about status change.

But who wants to install an app just for receiving notification, right?

So here is a [Kibitzr](https://kibitzr.github.io) solution that will send a notification to Telegram chat (or Slack or Discord with some tweaking)

Put this check config into your kibitzr.yml:

```yaml
checks:
  - name: OPM
    url: https://www.opm.gov/policy-data-oversight/snow-dismissal-procedures/current-status/
    transform:
      - css: .Status > h3
      - text
      - changes: new
    notify:
      - telegram: 337821181
    period: 1 hour
```

And configure telegram authentication in kibitzr-creds.yml:

```yaml
telegram:
    token: 241553491:ABHCRz_snz15548kSlIS1txnNXWT7p8M800
```

See [Telegram Notifier](https://kibitzr.readthedocs.io/en/latest/telegram.html#telegram)
documentation for instructions on how to get the token and chat identifier.

That's it! I run my kibitzr inside docker container on
[GCP free tier](https://cloud.google.com/free/) instance.

Here is how I set it up:

```shell
$ docker create -v $PWD:/root/ --name kibitzr peterdemin/kibitzr run
$ docker start kibitzr
```
