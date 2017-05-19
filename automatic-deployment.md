# Deploy behind firewall on git push

There are a number of services, that allow deploying application after a push to a git repository.
Good examples are [Travis CI](https://travis-ci.org/) and [Deploy HQ](https://www.deployhq.com/).
They are triggered by a webhook from GitHub after a push event.
Then they build a package and deploy it to your server.

However, these solutions can't get behind firewall or NAT in a case of a home system.
As usual for systems inaccessible from a public network, the workflow has to be inverted.
Deployment service has to be deployed in the local network and monitor external resource (such as git repo) for changes.
Once change detected, it should run the same steps as public deployment service would.

[Kibitzr](http://kibitzr.github.io) is a good fit for the task.
Here is an example `kibitzr.yml` for a real system:

```yaml
  - name: Release
    script: git pull
    transform:
      - python: |
          if content.strip() == 'Already up-to-date.':
              content = ''
    notify:
      - bash: |
          pip install -e .
          supervisorctl -c supervisor.cfg restart app
```

It periodically runs `git pull`, if it's stdout is different from `Already up-to-date.`, it will execute bash script:

```bash
pip install -e .
supervisorctl -c supervisor.cfg restart app
```

The first line installs a new version of a Python package, that was just pulled from the external git repository.
Second restarts application using freshly installed version.

Such lightweight deployment automation system is useful for Raspberry PI projects, where computational resources are tightly limited.
