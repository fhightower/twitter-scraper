Twitter Scraper
===============

Twitter's API is annoying to work with, and has lots of limitations —
luckily their frontend (JavaScript) has it's own API, which I reverse–engineered.
No API rate limits. No restrictions. Extremely fast.

You can use this library to get the text of any user's Tweets trivially.

Very useful for making markov chains.

Usage
=====

.. code-block:: pycon

    >>> from twitter_scraper import get_tweets

    >>> for tweet in get_tweets('kennethreitz', pages=1):
    >>>     print(tweet)
    P.S. your API is a user interface
    s3monkey just hit 100 github stars! Thanks, y’all!
    I’m not sure what this /dev/fd/5 business is, but it’s driving me up the wall.
    …

It appears you can ask for up to 25 pages of tweets reliably (~486 tweets).

Markov Example
==============

First, install markovify:

.. code-block:: shell

    $ pipenv install markovify

.. code-block:: pycon

    >>> import markovify
    
    >>> tweets = '\n'.join([t for t in get_tweets('kennethreitz', pages=25)])
    >>> text_model = markovify.Text(tweets)
    
    >>> print(text_model.make_short_sentence(140))
    Wtf you can’t use APFS on a prototype for “django-heroku”, which does a lot out of me.

Notes
=====

- Due to the user agent being sent, there's no way for Twitter to know that this isn't a web browser sending these requests (unless they're **extremely** clever).
- Links in tweets are currently excluded (pull requests accepted!)

Installation
============

.. code-block:: shell

    $ pipenv install twitter-scraper

Only Python 3.6 is supported.
