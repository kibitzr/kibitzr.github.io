# Notify on Firefox Developer Edition release

Firefox offers developer edition that has all the hottest features and perfomance improvements.
However it doesn't have proper upgrade channles like ESR version.

This configuration will post a Slack message once the new version is released:

```yaml
checks:
  - name: Firefox DE
    url: https://developer.mozilla.org/en-US/Firefox/Releases
    transform:
      - css: .multiColumnList > ol > li > a
      - text
      - changes: new
    period: 1 day
    notify:
      - slack
```

The configuration assumes, slack credentials are configured in `kibitzr-creds.yml`:

```yaml
slack:
    url: https://hooks.slack.com/services/A05237ZVB/321JNKATH/1v2x3v4jtx3dfhlkjhfIKX
```

See [Kibitzr documentation](https://kibitzr.readthedocs.io/en/latest/index.html) for details.
