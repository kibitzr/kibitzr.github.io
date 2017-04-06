# Why Python is a perfect language for Kibitzr

Kibitzr is a command line utility, that (depending on configuration)
polls web pages and notifies on changes through different channels.
Kibitzr is written in Python and first version was built within an hour.
This speed of development is achieved by Python nature itself and it's ecosystem.

Python being interpretted language is known for being not the most perfomant choice.
On the other hand, most of it's internals (and some of third-party libraries)
are written in pure C.

Kibitzr uses Python to glue these highly optimized pieces together,
achieving both runtime speed and development agility.


## Configuration

Kibitzr' configuration file has to be expressive and human-editable.
That's why it uses [YAML](http://yaml.org/)
with awesome [PyYAML](https://pypi.python.org/pypi/PyYAML) Python package.

While current version is more complex, and has some post-processing, the first one
was just:

```python
import yaml 
with open("kibitzr.yml") as fp:
    conf = yaml.load(fp)
```

## Command line interface

Writing argument parser from scratch can be tough.
That's why Python has two built-in implementations of it: argparse and optparse.
But Kibitzr uses [Click](http://click.pocoo.org/) instead.
So whole argument parsing magic is wrapped inside a stack of decorators:

```python
import click

@click.command()
@click.option("--once", is_flag=True,
              help="Run checks once and exit")
@click.option("-l", "--log-level", default="info",
              type=click.Choice(LOG_LEVEL_CODES.keys()),
              help="Logging level")
@click.argument('name', nargs=-1)
def entry(once, log_level, name):
    ...
```

To make kibitzr an executable, Python's built-in
[entry points](http://python-packaging.readthedocs.io/en/latest/command-line-scripts.html)
are used:

```python
setup(
    ...
    entry_points={
        'console_scripts': [
            'kibitzr=kibitzr.cli:entry'
        ]
    },
    ...
)
'''

## Schedule

Kibitzr checks are recurrent. An excellent
[schedule](https://schedule.readthedocs.io/en/stable/)
allows building schedule with

```python
schedule.every(period).seconds.do(checker.check)
```

And execute them with 

```python
schedule.run_pending()
```

## HTTP

While it's an ubiqutous task, making HTTP request can be cumbersome.
Just think about handling redirects, handling different network failures, content encoding...
Thanks to [requests](http://docs.python-requests.org/en/master/) it's all done in one line:

```python
response = requests.get(self.url)
```

## JavaScript

Having raw HTML contents is good enough some times. But not always for sure.
Modern web sites might not even open without some JavaScript.
That's why kibitzr comes with powerfull browser automation library -
[Selenium](http://www.seleniumhq.org/)
which launches [headless](https://pypi.python.org/pypi/xvfbwrapper) Firefox:

```python
with firefox(headless) as driver:
    driver.get(url)
    if scenario:
        run_scenario(driver, scenario)
    if delay:
        time.sleep(delay)
```

One can do all kind of browser interactions, like authenticating,
filling forms and clicking buttons.

## HTML processing

Of course operating with full HTML page is uncomfortable.
Often required information is hidden inside one small tag.
Kibitzr leverages powerfull [lxml](https://pypi.python.org/pypi/lxml/3.4.4)
and handy [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/)
for cropping contents to just one
[CSS Selector](https://www.w3schools.com/cssref/css_selectors.asp),
[XPath](https://www.w3schools.com/xml/xpath_intro.asp),
or tag.
Than kibitzr strips all HTML markup out leaving only plain text.

## JSON

In the golden age of APIs kibitzr would be incomplete without
sophisticated JSON processing support, provided by [jq](https://stedolan.github.io/jq/).

Parsing latest release version and title from [GitHub API](https://api.github.com/repos/kibitzr/kibitzr/releases/latest) is done by succint transform:

```yaml
  - jq: .tag_name + " " + .name
```

## Notifications

Python comes with
[SMTP](https://docs.python.org/2/library/smtplib.html)
support out of the box.
Whereas all modern instant messangers (like Slack and Gitter) have API web hooks,
accessible through the very same requests library.

But providing all possible integrations is not a viable option these days,
that's why kibitzr allows building custom notifiers right inside
the configuration file with plain bash of Python snippets. 

## Storing Changes History

There are many possible ways of persisting changes history.
Following UNIX philosophy, kibitzr uses [git](https://git-scm.com/)
with cozy wrapper - [sh](https://amoffat.github.io/sh/):

```python
sh.git.add('-A', '.')
sh.git.commit('-m', self.commit_msg)
```
