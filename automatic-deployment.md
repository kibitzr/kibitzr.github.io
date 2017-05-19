# Deploy behind firewall on git push

There are a number of services, that allow to deploy application after a push to git repository.
Good examples are [Travis CI](https://travis-ci.org/) and [Deploy HQ](https://www.deployhq.com/).
They are triggered by a webhook from GitHub after a push event.
Then they build package and deploy it to your server.

However these solutions can't get behind firewall or NAT in case of home system.
As usual for systems inaccessible from public network, workflow has to be inverted.
Deployment service has to be deployed in local network and monitor external resource (such as git repo) for changes.
Once change detected, it should run the same steps as public deployment service would.

[Kibitzr](http://kibitzr.github.io) is a good fit for the task.
