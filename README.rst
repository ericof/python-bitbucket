python-bitbucket
----------------

A simple python library to access the BitBucket API.  API Coverage is not
that high at the moment as the API has not been officially released and is
still in a state of flux.  Right now only read (GET) calls are supported.

usage
=====

API Usage all stems from the ``BitBucket`` object.  You can instantiate one
easily::
    
    >>> import bitbucket
    >>> bb = bitbucket.BitBucket()
    >>> bb
    <BitBucket API>

Certain areas of bitbucket's API require authentication or promise to provide
more data if you are authenticated.  Authentication lives on the ``BitBucket``
object, so if you want to authenticate pass the username and password::

    >>> bb = bitbucket.BitBucket('jmoiron', 'mypassword')
    >>> bb
    <BitBucket API (auth: jmoiron)>

If at any time you set both the ``username`` and ``password`` attributes on the
bb object, authentication becomes active.  BitBucket's auth is HTTP Basic over
https.

getting data
============

``BitBucket`` provides an object-oriented wrapper around the API's REST
structure.  Top level API calls are available off the ``BitBucket``
object itself.  To fetch a user, and poke around at his repositories::

    >>> jmoiron = bb.user('jmoiron')
    >>> jmoiron
    <User: jmoiron>
    >>> jmoiron.repositories()
    [{'description': 'simple python bitbucket API library',
     'followers_count': 1,
     'name': 'python-bitbucket',
     'slug': 'python-bitbucket',
     'website': 'http://bitbucket.org/jmoiron/python-bitbucket/'},
    ... ]
    >>> pybb = jmoiron.repository('python-bitbucket')
    >>> pybb
    <Repository: jmoiron's python-bitbucket>
    >>> pybb.tags()
    ...
    >>> pybb.branches()
    ...

 ``python-bitbucket`` does not attempt to format or abstract the return values
 of API calls in any way.

