# How to hook Kibitzr notification to Zapier trigger

[Kibitzr](https://kibitzr.github.io/) is perfect for scrapping deep web,
and it is even better when combined with integration solutions for public web.
One of the most popular interations platform is [Zapier](https://zapier.com/).
It has a free plan, that should cover personal needs.

This tutorial will guide through creation of basic Kibitzr check wired to Zapier trigger.

1. Create new zap - click **MAKE A ZAP!** button on [Zapier dashboard](https://zapier.com/app/dashboard).
2. For a trigger app choose **Webhooks** > **Catch Hook**.
3. Leave *Child Key* empty
4. Copy hook URL
5. Add a check to `kibitzr.yml`:
   ```yaml
   checks:
     - name: Kibitzr release
       url: https://pypi.python.org/pypi/kibitzr/json
       transform:
         - jq: .info | .version
         - changes: verbose
       notify:
         - zapier: https://hooks.zapier.com/hooks/catch/1628105/1kan4u/
   ```
   (Replace with you zapier URL)
6. Run kibitzr once to check integration:
   ```
   kibitzr --once
   ```
7. Add Zapier action. Let's pick something fancy, SMS.
8. In template choose **Step 1 | Text** from drop-down list.

You're all set! Get notified on new version of Kibitzr through SMS.
