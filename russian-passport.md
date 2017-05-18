# Monitor Passport Readiness on Russian Embassy site

If you ever tried to get a Russian international passport in United States,
you know that embassy has a funny procedure of notifying about passport readiness.
They publish a list of all people who can come and grab their new passport
on a single HTML page (with broken layout).

Yes, that stupid. Here is this page: [Ready Passports](http://www.russianembassy.org/ru/page/информация-о-готовности-паспортов).
It's all in Russian language, but you can get the idea.

There is no SMS or e-mail notifications, everyone just has to open this page from time to time
and search for his name in this list.
It's not that bad, if you have [Kibitzr](https://kibitzr.github.io) running.
I have mine running on my desktop, added to AutoStart.

Here is the check I use to get e-mail once my Passport will be ready:

```yaml
checks:
  - name: Passport
    url: http://www.russianembassy.org/ru/page/информация-о-готовности-паспортов
    transform:
      - text
      - bash: grep -i -e 'Демин' -e 'Дёмин'
      - changes: verbose
    notify:
      - mailgun
    period: 8 hours
    error: ignore
```

Let's break it down.
First item - name - is used in logging and e-mail subject.
Then URL, nothing special.
Then list of transforms.
First transform, `text`, takes HTML and stripes all tags out leaving me with clear text.
Second, `bash`, calls bash command on results of `text`.
It executes `grep` with two alternatives of my last name, since I'm not sure how it will appear.
Third transform, `changes`, saves results in git repository and passes verbose git log forward only if something have changed.
Then goes the list of notifications. I have only one - mailgun.
I registered a free account with them, and authorized my e-mail address.
Here is my mailgun configuration in `kibitzr-creds.yml`:

```yaml
mailgun:
    key: key-b31874e8c06bd9e21080d1d667e3a280
    domain: sandbox9ad289034b0fbcaaa11b575a97805a89.mailgun.org
    to: Peter Demin <peterdemin@gmail.com>
```

I configured polling period for 8 hours, there is no rush to take the passport, but I want to check more often than once a day.
The last line defines what to do in case of error.
As you can expect from guys, who build notification services as a public list of names, their site is... Flaky, so to say.
I don't want to know how low their uptime is, so I ignore all errors.
Without this line I would receive error report for every failure.
