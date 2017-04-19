# How to hook Kibitzr notification to Zapier trigger

[Kibitzr](https://kibitzr.github.io/) is perfect for scrapping deep web,
and it is even better when combined with integration solutions for public web.
One of the most popular interations platform is [Zapier](https://zapier.com/).
It has a free plan, that should cover personal needs.

If you don't have Kibitzr installed, it's a good time to get one with [AWS Free Tier](https://kibitzr.readthedocs.io/en/latest/aws.html) or [GCP Always Free](https://kibitzr.readthedocs.io/en/latest/gcp.html) instance.

This tutorial will guide through creation of basic Kibitzr check wired to Zapier trigger.

Create new zap - click **MAKE A ZAP!** button on [Zapier dashboard](https://zapier.com/app/dashboard).

For a trigger app choose **Webhooks** > **Catch Hook**.

Leave *Child Key* empty.

Copy hook URL.

Add a check to `kibitzr.yml`:
```
checks:
  - name: Kibitzr release
    url: https://pypi.python.org/pypi/kibitzr/json
    transform:
      - jq: .info | .version
      - changes: verbose
    notify:
      - zapier: https://hooks.zapier.com/hooks/catch/1628105/1kan4u/
```
(Replace with you zapier URL).

Launch kibitzr:
```
kibitzr
```

Make sure Trigger test passes.

Add Zapier action. Let's pick something fancy, SMS.

In template choose **Step 1 | Text** from drop-down list.

You're all set! Get notified on new version of Kibitzr through SMS.
